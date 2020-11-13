##### Wiktor Więcław 
# C++ Część 11 | Algorytmy STL

## Algorytmy STL
STL implementuje ponad 100 różnych algorytmów. Znajomość ich pozwala zaoszczędzić czas i uczynić nasz kod bardziej ekspresywnym. Zacznijmy od kilku prostych algorytmów. Wszystkie algorytmy znajdują się w bibliotece ```<algorithm>```.

### std::max
Przyjmuje dwa argumenty dowolnego typu i zwraca większy z nich
```c++
#include <algorithm>
int main()
{
    int x = std::max(5, 4);
}
```

### std::max_element
Przyjmuje iterator początkowy i iterator końcowy. Zwraca iterator na największy element.
```c++
#include <algorithm>
int main()
{
    std::array arr{1, 2, 3, 4, 5};
    int x = *std::max_element(arr.begin(), arr.begin() + 2);
    // x = 3;
}
```

### std::accumulate
Służy do sumowania elementów kontenera. Przyjmuje iterator początkowy, iterator końcowy, i wartość, do której elementy mają być dodawane. Zwraca sumę elementów z obszaru wyznaczonego przez iteratory.
```c++
#include <algorithm>
int main()
{
    std::vector<double> vec{1, 2, 3, 4, 5};
    int sum = std::accumulate(vec.begin(), vec.end(), 0);
}
```

### std::find
Szuka elementu w kontenerze. Zwraca iterator wskazujący na znaleziony element. Jeżeli go nie znajdzie zwraca iterator końcowy.

```c++
#include <algorithm>
int main()
{
    std::array<int, 5> arr{1, 2, 3, 4, 5};
    std::array<int, 5>::iterator it = std::find(arr.begin(), arr.end(), 0);
    int x = -1;
    if(it != arr.end()) x = *it;
}
```

### std::sort
Sortuje kontener.

```c++
#include <algorithm>
int main()
{
    std::array<int, 5> arr{5, 1, 3, 2, 5};
    std::sort(arr.begin(), arr.end());
}
```

Spora część z tych algorytmów to po prostu kod który piszemy na co dzień, opakowany w wygodne funkcje. Dlatego też zachęcam do zapoznania się z pozostałymi algorytmami.
https://en.cppreference.com/w/cpp/header/algorithm

## Podsumowanie
* STL implementuje ponad 100 różnych algorytmów.
* Pomagają uprościć kod który piszemy na co dzień.

## Zakończenie
Dotarliśmy do końca tego poradnika. Możesz teraz przejść do oglądania [playlisty](https://www.youtube.com/playlist?list=PLODTTsk7ci-DdMLwsjcGSGTyoK4-0X17X).