##### Wiktor Więcław 
# C++ Część 3 | Klasy

## Klasa (Class)
Klasy, podobnie jak struktury, pozwalają nam tworzenie nowych typów.

Z technicznego punktu widzenia klasa niewiele różni się od struktury. Najważniejszą różnicą jest to, że domyślnie wszystkie jej składowe są prywatne, co oznacza, że nie mamy do nich dostępu poza ciałem klasy.

```c++
class Rectangle
{
    double a;
    double b;
};

int main()
{
    Rectangle rect;
    rect.a = 5; // błąd kompilacji
}
```

## Specyfikatory ostępu (Access specifiers)
Wyróżniamy 3 modyfikatory dostępu: ```public```, ```private``` oraz ```protected```.

Aby umożliwić dostęp do składowy klasy musimy skorzystać ze specyfikatora dostępu ```public```.

```c++
class Rectangle
{
private:
    double a;
    double b;
public:
    Rectangle(double sideA, double sideB) : a(sideA), b(sideB) { }
    double area() { return a * b; }
};

int main()
{
    Rectangle rect{2.0, 2.0}; // ok
    double area = rect.area() // ok
    rect.a = 5; // błąd kompilacji
}
```

Specyfikatorów dostępu możemy także używać w strukturach, jednakże jest to rzadko spotykane.

O modyfikatorze ```protected``` powiemy sobie pod koniec tej części poradnika.

## Kiedy używać klasy, a kiedy struktury
Przyjęto, że klas używamy kiedy chcemy żeby nasz typ opisywał spójną całość np. samochód. 

Struktury powinny opisywać "luźny" zbiór składowych np. kosz z owocami.

## Hermetyzacja (Encapsulation)
Podstatowa zasada paradygmatu obiektowego. Polega ona na ukrywaniu implementacji. Zapewnia, że obiekt nie może zmieniać stanu wewnętrznego innych obiektów w nieoczekiwany sposób.

Według tej zasady, każda zmienna lub obiekt wewnątrz klasy powinna być zadeklarowana jako prywatna.

Pamiętaj, że ta zasada nie powinna być stosowana w przypadku struktur.

## Wskaźnik this
Wewnątrz zasięgu klasy możemy korzystać ze wskaźnika ```this```, który wskazuje na obiekt klasy, który wykonuje daną metodę.

```c++
void func(Widget& w); // deklaracja funkcji

class Widget
{
    int a;
public:
    void method()
    {
        a = 5; // ok
        // pozwala na sprecyzowanie, że zmienna a jest składową klasy
        this->a = 5; // ok

        // umożliwia też przekazanie obiektu do funkcji
        func(*this);
    }
};
```

## Gettery i Settery
Jeżeli musimy zapewnić dostęp do składowych zmiennych klasy, powinniśmy użyc tzw. getterów oraz setterów.

```c++
class Rectangle
{
public:
    Rectangle(double sideA, double sideB) : a(sideA), b(sideB) { }
    double area() { return a * b; }
    double getA() { return a; }
    double getB() { return b; }
    void setA(double a) { this->a = a; }
    void setB(double b) { this->b = b; }
// często składowe prywatne umieszczamy poniżej publicznych
private: 
    double a;
    double b;
};

int main()
{
    Rectangle rect{2.0, 2.0};
    rect.setA(4.0);
    std::cout << rect.getA() << std::endl;
}
```

## Dziedziczenie
Dziedziczenie daje nam możliwość definiowania nowych klas w oparciu o stare klasy. 

```c++
class Vehicle
{
    double maxVelocity;

protected: // pozwala klasom dziedziczącym na dostęp do zmiennej
    double maxAcceleration;

public:
    Vehicle(double maxVelocity) : maxVelocity(maxVelocity) { } 
};

/* public oznacza ze wszystkie składowe publiczne klasy
 Vehicle będą też publiczne w klasie Car */
class Car : public Vehicle // relacja - samochód jest pojazdem
{
public:
    Car(double maxVelocity) : Vehicle(maxVelocity) { }
    double getMaxAcceleration() { return maxAcceleration; } // ok
    double getMaxVelocity() { return maxVelocity; } // błąd kompilacji
};

```
Dziedziczenie jest bardzo obszernym tematem. Na ten moment zakończymy jego omawianie i wrócimy do niego w przygotowanej przez nas playliście na youtube.

## Podsumowanie
* Klasa od struktury różni się głównie tym, że wszystkie składowe klasy są domyślnie prywane, a w strukturze publiczne.
* Wyróżniamy 3 specyfikatory dostępu ```public```, ```private``` i ```protected```.
* Nie mamy dostępu do składowych prywatnych poza zasięgiem klasy.
* Klas używamy gdy modelujemy coś co jest spójną całością, a struktur, gdy mamy do czynienia z luźnym zbiorem danych.
* Hermetyzacja polega na ukrywaniu szczegółów implementacji. Nie dotyczy struktur.
* Jeżeli dostęp do zmiennych i obiektów składowych w klasie jest wymagany, możemy skorzystać z getterów i setterów.
* Dziedziczenie daje nam możliwość definiowania nowych klas w oparciu o stare klasy.