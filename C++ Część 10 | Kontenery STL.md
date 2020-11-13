##### Wiktor Więcław 
# C++ Część 10 | Kontenery STL

## STL (Standard Template Library)
STL jest częścią biblioteki standardowej i zawiera wiele struktur danych i algorytmów, powszechnie używanych przez programistów języka C++.

## Kontenery (Containers)

### std::array
W headerze ```<array>``` znajdziemy szablon klasy ```std::array```, która służy jako zamiennik dla tablic, które znamy z języka C. Przyjmuje dwa parametry szablonu: typ oraz rozmiar tablicy. Powinniśmy go stosować, dlatego że rozwiązuje on pewne problemy z przekazywaniem i zwracaniem tablic oraz oferuje nowe funkcjonalności takie jak np. metoda ```size()``` zwracająca rozmiar tablicy, posiadając przy tym takie samo zużycie zasobów jak zwykła tablica (możesz to sprawdzić używając compiler explorera).

```c++
#include <array>

namespace tut {

void cStyleFunction(int* array, int size);

template<size_t size>
void cppStyleFunction(std::array<int, size> array);

}

int main()
{
  std::array<int, 5> array = {1, 2, 3, 4, 5};
  std::array array2 = {1, 2, 3, 4, 5} // dedukcja typu i rozmiaru
  
  int i = array1[0]; // przeciąża operator[]

  tut::cStyleFunction(array1.data(), array1.size());
  tut::cppStyleFunction(array1); // dedukcja parametru szablonu funkcji
}
```

### std::vector
Jeżeli chcemy stworzyć tablicę, która ma dynamicznie zaalokowane elementy, możemy skorzystać z klasy ```std::vector```, zdefiniowanej wewnątrz bilbioteki ```<vector>```. Destruktor ```std::vector```a odpowiedzialny jest za zwalnianie zaalokowanej pamięci, nie musimy robić tego manualnie. 

```std::vector``` ma zmienny rozmiar poczas wykonywania programu. Kiedy tworzony jest obiekt klasy  ```std::vector```, alokuje on pewną ilość pamięci. Jeżeli dodamy do niego więcej elementów niż zaalokowana pamięć na to pozwala, to zaalokuje dwa razy większy obszar pamięci, przekopiuje tam całą swoją zawartość, a następnie zwolni uprzednio zaalokowaną pamięć.

```c++
#include <vector>

int main()
{
  std::vector<double> vec1 {1.0, 2.0, 3.0}; 
  vec1.push_back(5.0); // dodaje wartość na koniec wektora

  // możemy ustawić początkowy rozmiar pamięci wektora 
  std::vector<double> vec2(5); // alokuje pamiec na 5 elementów
  vec2.reserve(10); // alokuje pamięć na 10 elementów
}
```

Klasa ```std::vector``` implementuje wiele metod, z którymi warto się zapoznać.

### Pozostałe kontenery
W bibliotece STL istnieje wiele więcej kontenerów. Są one bardzo przydatne, dlatego zachęcam do poczytania na ich temat:

http://www.cplusplus.com/reference/stl/

## Iterator 
Kontenery z biblioteki STL implementują swóje własne iteratory.

Iterator jest to klasa, która umożliwia iterowanie po pewnym obszarze kontenera. Przeciąża ona operator ```*``` dzięki czemu możemy korzystać z niego tak jak ze wskaźnika.

```c++
#include <vector>

int main()
{
  std::vector<double> vec {1.0, 2.0, 3.0, 4.0, 5.0};

  // iterator na pierwszy element wektora
  std::vector<double>::iterator it = vec.begin();
  
  it += 2 // iterator wskazuje na 3 element

  // end() zwraca iterator wskazujący na pamięć PO ostatnim elemencie
  while(it != vec.end())
  {
    *it = 1.0;
    ++it;
  }
}
```
W przypadku klas ```std::array``` i ```std::vector``` moglibyśmy również skorzystać ze zwykłej pętli ```for```. Jednakże nie wszystkie kontenery STL przeciążają operator ```[]```.

Praktyczne zastosowanie iteratorów omówimy w następnej części poradnika.

## Range-Based For Loop
Jest to bardziej czytelna alternatywa dla zwykłej pętli ```for```. Obsługiwana jest przez wszystkie iterowalne kontenery STL.

```c++
#include <vector>

int main()
{
  std::vector<double> vec {1.0, 2.0, 3.0};

  for(double& element : vec)
  {
    element = 1.0;
  }
}
```

## std::pair
Jest to prosta struktura reprezentująca parę dwóch elementów o dowolnych typach.

```c++
#include <utility>

int main()
{
  std::pair<char, size_t> pair1 {'a', 5};
  std::pair pair2 {1.0, 1}; // dedukcja typów

  char c = pair1.first;
  pair1.second = 8;
}
```

## Podsumowanie
* Należy korzystać z klasy ```std::array``` zamiast klasycznych tablic, które są statycznie alokowane.
* Jeżeli rozmiar tablicy nie jest znany podczas kompilacji, powinniśmy korzystać z klasy ```std::vector```.
* Iterator pozwala na iterowanie po pewnym obszarze kontenera.
* Range-Based For Loops są bardziej czytelną alternatywą dla zwykłego ```for```a.
* Struktura ```std::pair``` pozwala na tworzenie pary dwóch zmiennych o dowolnych typach.

