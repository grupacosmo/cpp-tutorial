##### Wiktor Więcław 
# C++ Część 07 | Przeciążanie

## Przeciążanie funkcji (Function overloading)
Przeciążanie funkcji jest to tworzenie conajmniej 2 funkcji o takiej samej nazwie. Funkcje muszą różnić się typami przyjmowanych argumentów lub ich liczbą.

```c++
namespace tut {

void func(int arg);
void func(double arg);
void func(int arg1, int arg2);

}
```

Funkcje mogą różnić się typem zwracanym, natomiast jeśli funkcje przyjmują takie same typy argumentów to typ wartości zwracanej nie jest wystarczającym warunkiem na przeciążenie funkcji.

```c++
namespace tut {

// dobrze
int func(int arg);
double func(double arg);

// źle
int func(int arg);
double func(int arg);

}
```

## Przeciążanie metod w klasie
Wszystkie metody z wyjątkiem destruktora, możemy przeciążać.

```c++
namespace tut {

class Rectangle
{
    double a, b;
public:
    Rectangle() = default; // przeciążanie konstruktorów
    Rectangle(double a, double b) : a(a), b(b) { }
};

}
```

Dodatkowym warunkiem na przeciążenie metod jest modyfikator ```const```. Załóżmy, że chcemy napisać klasę, która rozszerza możliwości tablicy trzech ```int```ów.

```c++
#include <cstddef> // zawiera size_t

namespace tut {

class IntContainer 
{
    int array[3];
public:
    IntContainer() : array{} {}
    IntContainer(int a, int b, int c) : array{a, b, c} { }
    int operator[](size_t index) const { return array[index]; }
    int& operator[](size_t index) {return array[index]; }
};

}

int main()
{
    tut::IntContainer container;
    // gdybysmy mieli tylko const operator[], przypisanie wartości nie byłoby możliwe
    container[0] = 5;
    
    const tut::IntContainer constContainer{1, 2, 3};
    // gdybyśmy nie przeciążyli operatora[], nie moglibyśmy go użyć do odczytu zawartości
    int x = constContainer[2];
    constContainer[0] = 5 // błąd kompilacji
}
```

## Przeciążanie operatorów (Operator overloading)
W języku C++ mamy możliwość przeciążenia operatorów takich jak np. ```+```, ```-```, ```=```, ```==```, itd. Większość podstawowych operatorów w C++ może zostać przeciążona, z wyjatkiem: ```.```,   ```::```,  ```?:```,  ```sizeof```.

Przeciążmy operator ```+``` w klasie ```Rectangle```.

```c++
namespace tut {

class Rectangle
{
    double a, b;
public:
    Rectangle() = default;
    Rectangle(double a, double b) : a(a), b(b) { }

    /* Mamy dostep do zmiennych rect.a i rect.b dlatego,
     że jesteśmy wewnątrz klasy Rectangle */
    Rectangle operator+(const Rectangle& rect) const
    {
        /* Typ zwracany metody zawarty jest w jej deklaracji, możemy zatem wywołać kontsruktor pomijając nazwę Klasy */
        return { a + rect.a, b + rect.b };
    }
};

}

int main()
{
    tut::Rectangle r1{1.0, 1.0};
    const tut::Rectangle r2{2.0, 2.0};
    tut::Rectangle r3 = r1 + r2;
}
```

## Podsumowanie
* Możemy przeciążać funkcje, pod warunkiem, że będą przyjmować różne argumenty.
* Możemy przeciążać metody w klasach i strukturach. Istnieje wtedy też dodatkowy warunek przeciążenia - ```const```.
* Możemy przeciążyć większość operatorów.