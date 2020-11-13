##### Wiktor Więcław 
# C++ Część 05 | Modyfikator const

## Modyfikator const
Bardzo ważne w programowaniu w języku C++ jest używanie ```const``` wszędzie gdzie jest to możliwe.

Pozwala to na określenie,
które obiekty mają pozostać w swoim pierwotnym stanie oraz umożliwia kompilatorowi na znaczną optymalizacje naszego kodu. 

Możesz to sprawdzić korzystając z compiler explorera. Porównaj długości wygenerowanego kodu assembly: https://godbolt.org/z/hrf3EE

## Stałe

```c++
int main()
{
    const int size = 5;
    size = 4; // błąd kompilacji
}
```

## Przekazywanie obiektów do odczytu

Jeżeli chcemy przekazać obiekt wyłącznie do oczytu, powinniśmy skorzystać z const referencji. Przekazanie referencji do obiektu jest znacznie szybsze niż przekazywanie jego kopii. W tej sytuacji ```const``` gwarantuje, że obiekt nie zostanie zmieniony.

```c++
void func(const Rectangle& rect);
```

Powyższa zasada nie powinna być stosowana podczas przekazywania typów prymitywnych. Przekazywanie np. ```int```a poprzez kopię jest szybsze.

## Metody
C++ pozwala na użycie słowa ```const``` na końcu deklaracji metody. W tej sytuacji ```const``` oznacza, że metoda nie może zmieniać zmiennych składowych klasy.

```c++
class Widget
{
public:
    void func() const;
};
```

Przeanalizujmy bardziej praktyczny przykład:

```c++
struct Point
{
    double x, y;
    Point(double x, double y) : x(x), y(y) { }
};
class Vector
{
    Point a;
    Point b;
public:
    Vector(const Point& a, const Point& b) : a(a), b(b) { }
    const Point& getA() const { return a; }
    const Point& getB() const { return b; }
    void setA(const Point& point) { a = point; }
    void setB(const Point& point) { b = point; }
};
```

Gettery powinny być oznaczone słówkiem ```const```, ponieważ nie zmieniają zmiennych składowych. Zwróć uwagę, że getter zwraca ```const``` referencje, aby nie tworzyć niepotrzebnie kopii obiektu klasy ```Point```.

Trzeba pamiętać o deklarowaniu metod z użyciem ```const```, ponieważ tylko wtedy możemy z nich korzystać gdy sam obiekt, z którego korzystamy, jest stały.
```c++
int main()
{
    const Vector vector{Point{5.0, 4.0}, Point{1.0, 1.0}};
    double x = vector.getA().x; // ok
    vector.setA(Point{1.0}); // błąd kompilacji
}
```

Zauważ, że konstruktor jak i settery przyjmują jako swoje argumenty ```const``` referencje.

## Wskaźniki

```const``` po lewej stronie operatora ```*``` w deklaracji wskaznika oznacza, że zmienna na którą wskazuje jest stałą. Użycie ```const``` po prawej stronie ```*``` oznacza, że wskaźnik jest stały i jego adres nie może być zmieniony.

```c++
int main()
{
    const int four = 4;
    const int five = 5;

    int* const pFour = &four; // const wskaźnik na zwykłą zmienną

    const int* pFive = &five; // wskaźnik na const zmienną

    const int* const pFive = &five; // const wskaźnik na const zmienną
}
```

## Podsumowanie
* Używanie ```const``` wszędzie gdzie się da ułatwia kompilatorowi optymalizacje kodu.
* Powinniśmy przekazywać obiekty przez ```const``` referencje, aby uniknąć tworzenia niepotrzebnych kopii.
* Metody, które nie zmieniają składowych klasy, powinny być oznaczane modyfikatorem ```const```.
* Adres wskaźnika może być stały, pod warunkiem, że podczas jego deklaracji użyjemy ```const``` po prawej stronie operatora ```*```.