##### Wiktor Więcław 
# C++ Część 1 | Początek

## Cel
Poradnik ten powstał w celu wprowadzenia nowych członków koła COSMO PK do programowania w języku C++. Składa się on z 12 części tekstowych oraz  [playlisty](https://www.youtube.com/playlist?list=PLODTTsk7ci-DdMLwsjcGSGTyoK4-0X17X) na platformie youtube.

Części tekstowe obejmują podstawy języka, natomiast playlista odnosi się do jego bardziej zaawansowanych funkcjonalności.

## Założenia
Odbiorca zna język C na poziomie podstawowym.

## Wersja C++
Poradnik został napisany w oparciu o wersję C++17.

## Clang-Tidy
Ważne jest, abyś używał/a narzędzia Clang-Tidy w swoim zintegrowanym środowisku programistycznym (IDE). Narzędzie to pomoże ci wykryć wiele błędów logicznych i pomoże ci utrzymać odpowiedni styl kodu. 

## Ostrzeżenia (Warnings)
Kolejnym bardzo ważnym krokiem w przygotowaniu środowiska do nauki jest włączenie ostrzeżeń w kompilatorze za pomocą flag
``` -Wall``` i ```-Wextra```.  Sprawdż jak dodawać flagi w twoim IDE.

## Optymalizacja
Dzisiejsze kompilatory bardzo dobrze potrafią optymalizować napisany przez nas kod. Usuwają niepotrzebne zmienne oraz funkcje, przenoszą zawartość niektórych funkcji bezpośrednio do miejsc ich wywołania (tzw. inlining) i minimalizują koszty abstrakcji, często nawet do zera.

To dzięki potężnym kompilatorom, jesteśmy w stanie pisać wysokopoziomowy kod w C++, który może być tak samo wydajny jak kod napisany w języku C. Nie oznacza to, że każda nowa funkcjonalność języka C++ jest tak samo szybka jak jej odpowiednik w języku C. 

Więcej informacji o tym jak kompilator optymalizuje nasz kod możesz znaleźć tutaj:
https://pl.wikipedia.org/wiki/Optymalizacja_kodu_wynikowego

## Poziomy optymalizacji
Użytkowncy kompilatora gcc mają do swojej dyspozycji kilka poziomów optymalizacji:
* -O1 - Najniższy poziom optymalizacji.
* -O2 - Średni poziom optymalizacji.
* -O3 - Wysoki poziom optymalizacji (Może powodować problemy w złożonych aplikacjach)
* -Os - Poziom optymalizacji minimalizujący rozmiar pliku wykonywalnego.
* -Og - Poziom optymalizacji, który nie utrudnia debugowania.

Aby włączyć optymalizacje, należy użyć odpowiedniej flagi podczas kompilacji. Koniecznie sprawdź jak włączyć optymalizacje w twoim IDE.

## Compiler Explorer
Zanim kod napisany w językach C i C++ będzie zdatny do wykonania przez nasz procesor, musi zostać pierw przetłumaczony na niskopoziomowy język assembly. Wgląd do kodu przetłumaczonego na assembly może pomóc w sprawdzaniu wydajności rozwiązań, co do których nie jesteśmy pewni. Zasada jest prosta, im mniej linijek kodu assembly tym lepiej.

Warto skorzystać z internetowego narzędzia Compiler Explorer, które potrafi na bieżąco tłumaczyć pisany przez nas kod na język assembly. Pamiętaj o włączeniu optymalizacji, pole do wpisywania flag znajduje się w prawym górnym rogu.

Compiler Explorer:
https://godbolt.org/

## Kompatybilność z C
C++ nie jest całkowicie kompatybilny z językiem C. Istnieją pewne różnice między tymi językami, przez które kod napisany w C może prowadzić do odmiennych rezultatów w języku C++ lub do błędów kompilacji.

## Wypisywanie danych na ekran
W celu wypisania pewnych wartości na ekran możemy posłużyć się funkcją ```printf``` znaną z C. Język C++  swój własny sposób na wyprowadzanie danych - ```std::cout```. W tej części poradnika nie będę omawiał dokładnego działania tej metody, przedstawię jedynie jak z niej korzystać.

```c++
#include <iostream> // dołączamy bibliotekę

int main()
{
    int a = 5;
    int b = 3;
    std::cout << "Hello World!" << std::endl;
    std::cout << "Suma a + b: " << a + b << std::endl;
}
```

##  bool
Typ ```bool``` może przyjmować tylko dwie wartości: ```true``` lub ```false```. Wykorzystywany jest do określania stanów logicznych.

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

## Parametry domyślne (default parameters)
W języku C++ parametry funkcji mogą przyjmować wartości domyślne. Parametr domyślny nie może znajdować się po lewej stronie zwykłego parametru. Spójrzmy na poniższy przykład:
```c++
void func1(int x, int y, int z = 0);     // ok
void func2(int x, int y = 0, int z = 1)  // ok
void func3(int x = 0, int y = 0, int z = 0); // ok

void func4(int x, int y = 0, int z);   // błąd kompilacji
void func5(int x = 0 , int y, int z);  // błąd kompilacji
void func6(int x = 0, int y, int z = 0); // błąd kompilacji

int main()
{
   func1(4, 3, 3); // ok
   func1(4, 3);    // ok, parametr z przyjmuje wartość 0
   func2(2);   // ok, parametry y przyjmuje wartość 0, a z przyjmują wartość 1
   func3();    // ok, parametry przyjmują wartość 0
}
```

## Operator new
C++ posiada własne operatory do zarządzania dynamicznie alokowaną pamięcią - ```new``` i ```delete```. Są one alternatywą dla funkcji ```malloc``` i ```free``` z języka C.

```c++
int main()
{
    int *x = new int(5);
    std::cout << *x << std::endl;// output: 5
    delete x;
    
    int *arr = new int[5]{1, 2, 3, 4, 5};
    for(unsigned int i = 0; i < 5; i++)
        std::cout << arr[i] << std::endl; // output: 1 2 3 4 5
    delete[] arr; // do usuwania tablic potrzebne są nawiasy []
}
```

Pamiętaj, w C++ musisz manualnie zwalniać tylko tę pamięć, która zostanie zaalokowana z użyciem operatora ```new```. 

## Podsumowanie
* Pamiętaj o zainstalowaniu narzędzia Clang-Tidy oraz włączeniu warningów w kompilatorze.
* Kompilatory potrafią znacząco zoptymalizować napisany przez nas kod.
* Kompilator gcc posiada 5 poziomów optymalizacji: ```-O1```, ```-O2```, ```-O3```, ```-Os``` i ```-Og```.
* Compiler explorer ułatwia porównywanie wydajności różnych rozwiązań.
* Język C++ nie jest w pełni kompatybilny z językiem C.
* Do wyprowadzania danych na ekran możemy skorzystac z ```std::cout```.
* Typ ```bool``` jest wykorzystywany do reprezentowania stanów logicznych.
* W C++ możemy deklarować funkcje, które posiadają parametry domyślne.
* Do zarządzania dynamicznie alokowaną pamiecią używamy operatorów ```new``` i ```delete```.