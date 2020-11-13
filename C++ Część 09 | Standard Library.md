##### Wiktor Więcław 
# C++ Część 09 | Standard Library

## Wstęp
W tej części poradnika przyjrzymy się niektórym elementom wchodzącym w skład biblioteki standardowej i zobaczymy jak wykorzystują one funkcjonalności języka C++, o których mówiliśmy w poprzednich częściach.

## Przestrzeń nazw std
Wszystkie elementy wchodzące w skład biblioteki standardowej należą do przestrzeni nazw ```std```.

## std::cout
W celu wypisania wartości na ekran możemy skorzystać z globalnie zadeklarowanego obiektu ```std::cout```, który znajduje się w headerze ```<iostream>```. Obiekt ten przeciąża operator przesunięcia bitowego ```<<``` do wyprowadzania danych na strumień wyjścia. Obiekt ```std::endl``` funkcjonuje jako znak nowej linii ```'\n'```, z tym że dodatkowo "flushuje" bufor.

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
Alternatywą do korzystania z tablicy ```char[]``` do przechowywania ciągów znaków, możemy użyć klasy ```std::string```. Znajdziemy ją w headerze ```<string>```. Przeciąża ona operator dodawania ```+``` oraz ```+=```, dzięki któremu możemy łączyć stringi.

```c++
#include <string>

int main()
{
  std::string s = "Moj string";
  int stringSize = s.size(); // długość stringa
  
  s += " mozemy powiekszac";
}
```

Miej na uwadze, że ```std::string``` jest znacznie wolniejszy niż klasyczna tablica ```char[]```, ale wygodniej się z niego korzysta i jest znacznie bardziej odporny na błędy popełniane przez programistów.

## Biblioteka iomanip
Do formatowania wyświetlanego textu przez ```std::cout``` możemy skorzystać ze standardowej bilbioterki ```<iomanip>```. Jest to bardzo mała biblioteka, w kilka minut można zapoznać się z jej zawartością.
http://www.cplusplus.com/reference/iomanip/

```c++
#include <iomanip>
#include <iostream>

int main ()
{
    // setw ustawia szerokość printowanego tekstu
    // setfill wypełnia puste miejsca znakami 'x'
    std::cout << std::setfill ('x') << std::setw(8) << "cpp" << std::endl;
    // output: xxxxxcpp

    // ustawia precyzje
    std::cout << std::setprecision(3) << 1.111111 << std::endl;
    //output: 1.11
}
```

## Podsumowanie
* ```std::cout``` jest to obiekt globalnie zadeklarowany w przestrzeni nazw ```std```.
* ```std::cin``` pozwala na wczytanie stanych z klawiatury
* ```std::string``` jest bezpieczniejszą alternatywą dla tablic ```char[]```
* Biblioteka ```<iomanip>``` posiada wiele funkcji pozwalających na formatowanie textu.