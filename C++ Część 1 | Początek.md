##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 1

## Wstęp
Niniejszy poradnik zakłada, że czytelnik zna język C na poziomie podstawowym.

## Kompatybilność z C
C++ nie jest całkowicie kompatybilny z językiem C. Istnieją pewne różnice między tymi językami, przez które kod napisany w C może prowadzić do odmiennych rezultatów w języku C++ lub do błędu kompilacji.

## Wypisywanie na ekran
W celu wypisania pewnych wartości na ekran możemy posłużyć się funkcją printf znaną z języka C. C++ ma też swój własny sposób - std::cout. W tej części 
nie będę omawiał dokładnego działania tej metody, przedstawię jedynie jak z niej korzystać.
```c++
#include <iostream> // dołączamy bibliotekę

int main()
{
    int a = 5;
    int b = 3;
    std::cout << "Suma a + b: " << a + b << "\n"; 
    // "Suma a + b: 8"
}
```

## Typ bool
Typ ```bool``` może przyjmować tylko dwie wartości: ```true``` lub ```false```. Służy do określania stanów logicznych.

```c++
bool isEqual(int a, int b)
{
   return a == b;
}

int main()
{
   bool b1 = true;
   bool b2 = 5 > 4 // true;
   bool b3 = isEqual(5, 4); // false
}
```

## Referencje
Wskaźnik jest to liczba reprezentująca adres pamięci, a referencja jest to bezpośrednie wiązanie do tej pamięci. W odróżnieniu od wskaźnika, nie możemy zmienić miejsca w
pamięci, z którym związana jest referencja.

```c++
#include <iostream>

void incrementByCopy(int param) // funkcja przyjmuje kopie
{
    ++param;
}

void incrementByPointer(int* param) // funkcja przyjmuje wskaźnik
{
    ++(*param); // wyłuskanie wskaźnika
}

void incrementByReference(int& param) // funkcja przyjmuje referencje
{
    ++param;
}

int main()
{
    int i = 5;
    
    int& ref = i; // znak '&' podczas deklaracji zmiennej oznacza referencje
    ++ref;
    std::cout << i << "\n"; // output: 6
    
    incrementByCopy(i);
    std::cout << i << "\n"; // output: 6, zmienna i pozostała bez zmian
    
    incrementByPointer(&i); // znak '&' po deklaracji oznacza adres
    std::cout << i << "\n"; // output: 7
    
    incrementByReference(i);
    std::cout << i << "\n"; // output: 8
    
    int k = 2; 
    ref = k; // ref to jest alias do zmiennej i. Nie mozna juz "przepiąć" referencji na inną zmienną.
    std::cout << i << "\n"; // output: 2
    ++i;
    std::cout << ref << "\n"; // output: 3
    std::cout << k << "\n"; // output: 2
}
```
W sytuacji, w której chcemy, żeby funkcja mogła zmienić przekazywaną do niej zmienną, powinniśmy przekazać ją przez referencje, 
a nie przez wskaźnik, ponieważ nie musimy wtedy korzystać z operatorów ```&``` oraz ```*```.
