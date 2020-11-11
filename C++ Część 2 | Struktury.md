##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 1

## Wstęp
Niniejszy poradnik zakłada, że czytelnik zna język C na poziomie podstawowym.

## Kompatybilność z C
C++ nie jest całkowicie kompatybilny z językiem C. Istnieją pewne różnice między tymi językami, przez które kod napisany w C może prowadzić do odmiennych rezultatów w języku C++ lub do błędu kompilacji.

## Typy prymitywne (Primitive types)
Typy takie jak ```int```, ```float```, ```double```, ```char```, ```bool``` nazywamy typami prymitywnymi.

## Struktura (Struct)
 W języku C++, podobnie jak w C, można tworzyć swoje własne typy zmiennych za pomocą struktur. Syntax tworzenia struktury w C++ różni się tym, że nie trzeba używać ```typedef``` przed jej deklaracją.
 
 ```c++
 struct Square
 {
    double a;
    double b;
 }
 ```
 
Instancję takiej struktury nazywamy obiektem (object). W celu skorzystania ze zmiennych zadeklarowanych wewnątrz struktury, należy skorzystać z operatora kropki.
Zwróć uwagę, że nazwy zdefiniowanych przez nas typów piszemy z dużej litery, a nazwy ich instancji piszemy z małej litery. Ta konwencja nazewnictwa pomaga rozróżnić struktury od obiektów.

 ```c++
 int main()
 {
    Square square; // obiekt
    square.a = 2.0;
    square.b = 2.0;
 }
 ```
 
C++ znacząco rozszerza możliwości struktur. Na przykład, mogą one posiadać również funkcje. Funkcje zadekarowane wewnątrz struktur nazywamy metodami i posiadają one bezpośredni dostęp do zmiennych zadeklarowanych wewnątrz struktury. Do wywołania metody również korzystamy z operatora kropki.

```c++
struct Square
{
    double a;
    double b;
    
    double area()
    {
       return a * b;
    }
}

int main()
{
    Square square; // obiekt
    square.a = 2.0;
    square.b = 2.0;
    double area = square.area();
}
```

### Konstruktor (Constructor)
Konstruktor jest specjalną metodą, która jest automatycznie wywoływana podczas tworzenia obiektu. Konstruktor nie ma typu zwracanego i jego nazwa jest taka sama jak nazwa struktury. Jeżeli sami nie zadeklarujemy konstruktora to automatycznie tworzony zostaje konstruktor domyślny;

```c++
struct Square
{
    double a;
    double b;
    
    Square() = default; // jawna deklaracja domyślnego konstruktora.
    
    double area()
    {
       return a * b;
    }
}
```

W konstruktorze możemy zmieniać proces tworzenia obiektu. Możemy też tworzyć konstruktory, które przyjmują różne parametry. Powinniśmy korzystać z nich do inicjalizacji obiektów.

```c++
struct Square
{
    double a;
    double b;
    
    Square(double sideA, double sideB) // konstruktor
    {
       a = sideA;
       b = sideB;
    }
    
    double area()
    {
       return a * b;
    }
}

int main()
{
    Square square(2.0, 2.0); // stworzenie i inicjalizacja obiektu
    double area = square.area();
}
```
### Destruktor (Destructor)
Destruktor działa bardzo podobnie jak konstruktor, tylko wywoływany jest na sam koniec życia obiektu i nie może przymować żadnych argumentów. Destruktor odpowiedzialny jest za usuwanie obiektów.

```c++
struct Square
{
    double a;
    double b;
    
    Square(double sideA, double sideB) // konstruktor
    {
       a = sideA;
       b = sideB;
    }
    
    ~Square() = default // jawnie zadeklarowany destruktor domyślny
    
    double area()
    {
       return a * b;
    }
}
```

### Podsumowanie
* Język c++ nie jest w pełni kompatybilny z językiem C.
* Wyróżniamy typy prymitywne oraz stworzone przez programistów.
* Struktury pozwalają na tworzenie własnych typów.
* Konstruktor pozwala na inicjalizację obiektu.
* Destruktor umożliwia automatyczne niszczenie obiektu.
