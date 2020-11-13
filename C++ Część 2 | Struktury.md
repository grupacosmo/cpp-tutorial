##### Wiktor Więcław 
# C++ Część 2 | Struktury

## Typy prymitywne (Primitive types)
Typy domyślnie zdefiniowane języku C++, takie jak ```int```, ```float```, ```double```, ```char```, ```bool``` nazywamy typami prymitywnymi.

## Struktura (Struct)
W C++, podobnie jak w C, można tworzyć swoje własne typy zmiennych za pomocą struktur. Syntax tworzenia struktury w C++ różni się tym, że nie trzeba używać ```typedef``` przed jej deklaracją.
 
```c++
struct Rectangle
{
  double a;
  double b;
};
```
 
Instancję takiej struktury nazywamy obiektem (object). W celu skorzystania ze zmiennych zadeklarowanych wewnątrz struktury, należy użyć z operatora kropki.

```c++
int main()
{
  Rectangle rect; // obiekt
  rect.a = 2.0;
  rect.b = 2.0;
}
```

Zwróć uwagę, że nazwy zdefiniowanych przez nas typów piszemy z dużej litery, a nazwy obiektów piszemy z małej litery. Ta konwencja nazewnictwa pomaga rozróżnić struktury od obiektów.

C++ znacząco rozszerza możliwości struktur. Na przykład, mogą one posiadać również funkcje. Funkcje zadekarowane wewnątrz struktur nazywamy metodami i posiadają one bezpośredni dostęp do zmiennych zadeklarowanych wewnątrz struktury. Do wywołania metody również korzystamy z operatora kropki.

```c++
struct Rectangle // struktura
{
   double a;
   double b;
    
   double area()
   {
      return a * b;
   }
};

int main()
{
   Rectangle rect; // obiekt
   rect.a = 2.0;
   rect.b = 2.0;
   double area = rect.area();
}
```

## Konstruktor (Constructor)
Konstruktor jest specjalną metodą, która jest automatycznie wywoływana podczas tworzenia obiektu. Konstruktor nie ma typu zwracanego i jego nazwa jest taka sama jak nazwa struktury. Jeżeli sami nie zadeklarujemy konstruktora to automatycznie tworzony zostaje konstruktor domyślny;

```c++
struct Rectangle
{
    double a;
    double b;
    
    Rectangle() = default; // jawna deklaracja domyślnego konstruktora.
    
    double area()
    {
       return a * b;
    }
};
```

W konstruktorze możemy zdefiniować proces tworzenia obiektu. Możemy też tworzyć konstruktory, które przyjmują różne parametry. Powinniśmy korzystać z nich do inicjalizacji obiektów.

```c++
struct Rectangle
{
    double a;
    double b;
    
    Rectangle(double sideA, double sideB) // konstruktor
    {
       a = sideA;
       b = sideB;
    }
    
    double area()
    {
       return a * b;
    }
};

int main()
{
    Rectangle rect{2.0, 2.0}; // stworzenie i inicjalizacja obiektu
    double area = rect.area();
}
```

## Lista inicjalizacyjna składowych (Member initializer list)
Dobrą praktyką jest inicjalizowanie składowych struktury za pomocą listy inicjalizacyjnej składowych, jest to specjalny syntax dostępny wyłącznie w konstruktorze.

```c++
struct Rectangle
{
   double a;
   double b;

   Rectangle(double sideA, double sideB) : a(sideA), b(sideB)
   {

   }
};
```

## Destruktor (Destructor)
Destruktor wywoływany jest na samym końcu życia obiektu. W odróżnieniu od konstruktora, nie może przyjmować żadnych argumentów. Destruktor odpowiedzialny jest za usuwanie obiektów.

```c++
struct Rectangle
{
   double a;
   double b;
    
   Rectangle(double sideA, double sideB) : a(sideA), b(sideB)
   {

   }
    
   ~Rectangle() = default // jawna deklaracja destruktora domyślnego
    
   double area()
   {
       return a * b;
   }
};
```

Możemy wykorzystać destruktor np. do automatycznego zwalniania dynamicznie zaalokowanej pamięci.

```c++
#include <cstring>

struct String
{
   char* text;
   // typ size_t jest aliasem do unsigned int
   size_t size;

   String(char* t, size_t s) : size(s)
   {
      text = new char[size];
      strcpy(text, t);
   }

   ~String()
   {
      delete[] text;
   }
};
```

## Podsumowanie
* Wyróżniamy typy prymitywne oraz typy zdefiniowane przez użytkowników.
* Struktury pozwalają na tworzenie własnych typów.
* Konstruktor pozwala na inicjalizację obiektu.
* Lista inicjalizacyjna składowych powinna być używana w konstruktorze do inicjalizacji składowych struktury.
* Destruktor umożliwia automatyczne niszczenie obiektów posiadających składowe, które są dynamicznie alokowane w pamięci.
