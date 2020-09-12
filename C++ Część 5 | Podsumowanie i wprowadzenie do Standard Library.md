##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 5

## Wstęp
W tej części poradnika przyjrzymy się niektórym elementom wchodzącym w skład biblioteki standardowej i zobaczymy jak wykorzystują funkcjonalności języka C++, o których mówiliśmy w poprzednich częściach.

## Przestrzeń nazw std
Wszystkie elementy wchodzące w skład biblioteki standardowej należą do przestrzeni nazw ```std```.

## std::cout
W celu wypisania wartości na ekran możemy skorzystać z obiektu ```std::cout```, który znajduje się w headerze ```<iostream>```. Obiekt ten przeciąża operator przesunięcia bitowego ```<<``` do wprowadzania danych na strumień wyjścia. Obiekt ```std::endl``` funkcjonuje jako znak nowej linii ```'\n'```, z tym że dodatkowo "flushuje" bufor.
```c++
#include <iostream>

int main()
{
  std::cout << "Hello World!" << std::endl;
}
```
```std::cout``` ma też wiele innych metod, które wywołać można za pomocą operatora kropki.

## std::cin
Do wprowadzania wartości z klawiatury używamy obiektu ```std::cin```. Używa się go podobnie do ```std::cout```, z tym, że przeciążony został operator skierowany w przeciwną stronę ```>>```.
```c++
#include <iostream>

int main()
{
  int zmienna;
  std::cin >> zmienna;
}
```
## std::string
Zamiast korzystać z tablicy ```char[]``` do przechowywania ciągów znaków, możemy użyć klasy ```std::string```. Znajdziemy go w headerze ```<string>```. Przeciąża ona operator dodawania ```+``` oraz ```+=```, dzięki któremu możemy łączyć stringi.
```c++
#include <string>

int main()
{
  std::string s = "Moj string";
  int string_size = s.size(); // dlugosc stringa
  
  s += " mozna powiekszac";
}
```
## std::array
W headerze <array> znajdziemy szablon klasy ```std::array```, która służy jako zamiennik dla tablic, które znamy z języka C. Przyjmuje dwa parametry szablonu: typ oraz rozmiar tablicy. Powinniśmy go stosować, dlatego że rozwiązuje on pewne problemy z przekazywaniem tablic oraz oferuje nowe funkcjonalności takie jak np. metoda ```size()``` zwracająca rozmiar tablicy, posiadając przy tym takie samo zużycie zasobów jak zwykła tablica.
```c++
int main()
{
  std::array<int, 5> my_array = {1, 2, 3, 4, 5};
  my_array.size();
}
```

Jak widać, wszystkie mechanizmy, o których mówiliśmy do tej pory, są wykorzystywane w najbardziej podstawowych elementach standardowej bilbioteki języka C++.
