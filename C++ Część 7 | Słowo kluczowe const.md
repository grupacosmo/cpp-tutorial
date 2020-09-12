##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 7

## Słowo kluczowe const (const keyword)
Bardzo ważne w programowaniu w języku C++ jest używanie ```const``` wszędzie gdzie jest to możliwe. Pozwala to na określenie,
które obiekty mają pozostać w swoim pierwotnym stanie oraz umożliwia kompilatorowi na znaczną optymalizacje naszego kodu.

C++ pozwala na użycie słowa ```const``` na końcu deklaracji metody:
```c++
void example_func() const;
```
Co oznacza, że ta metoda nie zmienia żadnej zmiennej zadeklarowanej wewnątrz klasy.

## Przykład
Napiszmy sobie przykładowy program, w którym pokażemy jak korzystać ze słówka ```const```. 
Zacznijmy od małego szablonu struktury pary dwóch zmiennych tego samego typu.
```c++
template<typename Type>
struct Pair
{
    Type first;
    Type second;

    Pair(const Type &arg_first, const Type &arg_second) 
    {
        first = arg_first;
        second = arg_second;
    }
};
```
Zwróć uwagę, że nie zmieniamy wartości zmiennych ```arg_first``` oraz ```arg_second``` wewnątrz konstruktora, więc powinniśmy je przekazywać przez const referencje.


Wykorzystajmy nasz szablon struktury w nowej klasie, która będzie reprezentować wektor matematyczny.

Pierw, żeby nie powtarzać ciągle argumentu szablonu, stwórzmy sobie alias dla ```Pair<double>```. W tym celu wprowadzimy nowe słowo kluczowe: ```using```. 
```c++
using Point Pair<double>;
```
Załóżmy, że chcemy aby nie dało się zmienić punktu zaczepienia naszego wektora, czyli żeby pierwszy punkt, który opisuje wektor, był stały. 
Należy więc zadeklarować ten punkt ze słówkiem const.


Stałe można zainicjalizować wyłącznie podczas ich deklaracji, to znaczy:
```c++
const int CONSTANT_1 = 5; // dobrze

const int CONSTANT_2;
CONSTANT_2 = 5; // zle
```

Natomiast my chcemy aby nasza stała została zainicjalizowana podczas tworzenia obiektu. 
Nie możemy dokonac operacji przypisania wartości ```point_1 = arg_1``` w konstruktorze, musimy zatem wprowadzić pojęcie listy inicjalizacyjnej.
```c++
class Vector
{
private:
    const Point point_1;
    Point point_2;

public:
                                                  // lista inicjalizacyjna
    Vector(const Point &arg_1, const Point &arg_2) : point_1(arg_1), point_2(arg_2) {}
};
```
Lista inicjalizacyjna pozwala na inicjalizacje stałych członków klasy w konstruktorze, ale można też za jej pomocą inicjalizować zmienne.
Jest ona preferowanym sposobem na inicjalizacje zmiennych.


Podsumujmy napisany do tej pory kod:
```c++
template<typename Type>
struct Pair
{
    Type first;
    Type second;

    Pair(const Type &arg_first, const Type &arg_second) 
    {
        first = arg_first;
        second = arg_second;
    }
};

using Point Pair<double>;

class Vector
{
private:
    const Point point_1;
    Point point_2;

public:
                                                  // lista inicjalizacyjna
    Vector(const Point &arg_1, const Point &arg_2) : point_1(arg_1), point_2(arg_2) {}
};
```

Stwórzmy teraz metodę zwracającą długość wektora. Metoda ta nie będzie zmieniać naszej jedynej zmiennej ```point_2```, więc powinniśmy zadeklarować ją ze słówkiem ```const``` na końcu.
```c++
double get_length() const
{
  // wykorzystany tutaj został wzór na długość wektora
  double a = (point_2.first - point_1.first);
  double b = (point_2.second - point_1.second);
  return sqrt(a*a - b*b);
}
```

Na zakończenie możemy napisać metodę, która umożliwi dodawanie dwóch wektorów. Nie możemy napisać ```const``` na końcu jej deklaracji, ponieważ zmieniamy ```point_2```.
```c++
void add_vector(const Vector &vec)
{
  const double x_diff = point_2.first - vec.point_1.first;
  const double y_diff = point_2.second - vec.point_1.second; 
  point_2 = Point{vec.point_2.first + x_diff, vec.point_2.second + y_diff};
}
```

Poniżej znajduje się cały kod wraz z przykładem wykorzystania. Przyjrzyj się każdemu użyciu słowa ```const```.
```c++
template<typename Type>
struct Pair
{
    Type first;
    Type second;

    Pair(const Type &arg_first, const Type &arg_second) 
    {
        first = arg_first;
        second = arg_second;
    }
};

using Point Pair<double>;

class Vector
{
private:
    const Point point_1;
    Point point_2;

public:
                                                  // lista inicjalizacyjna
    Vector(const Point &arg_1, const Point &arg_2) : point_1(arg_1), point_2(arg_2) {}
    
    double get_length() const
    {
      // wykorzystany tutaj został wzór na długość wektora
      const double a = (point_2.first - point_1.first);
      const double b = (point_2.second - point_1.second);
      return sqrt(a*a - b*b);
    }

    void add_vector(const Vector &vec)
    {
      const double x_diff = point_2.first - vec.point_1.first;
      const double y_diff = point_2.second - vec.point_1.second; 
      point_2 = Point{vec.point_2.first + x_diff, vec.point_2.second + y_diff};
    }
};

int main()
{
    const std::array<Point, 4> points = {
        Point{1.1, 2.2},
        Point{5.6, 7.5},
        Point{3.2, 5.4},
        Point{3.2, 7.4},
    };

    Vector vec_1(points[0], points[1]);
    const Vector vec_2(points[2], points[3]);

    vec_1.add_vector(vec_2);
}
```



