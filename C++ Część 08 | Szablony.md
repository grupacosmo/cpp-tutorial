##### Wiktor Więcław 
# C++ Część 08 | Szablony

## Szablony funkcji (Function templates)
Załóżmy że chcemy stworzyć funkcję ```max```, która porównuje dwie liczby i zwraca większą z nich. Gdybyśmy chcieli aby nasza funkcja przyjmowała różne typy, np. ```int```, ```double```, ```short``` to korzystając z przeciążania funcji musielibyśmy zaimplementować trzy niemal identyczne funkcje.

Z pomocą przychodzą szablony funkcji:

```c++
namespace tut {
// T jest to dowolny typ.
// T Może być też obiektem,
// dlatego parametry przekazujemy przez const referencje
template<typename T>
const T& max(const T& param1, const T& param2)
{
    if(param1 >= param2)
        return param1;
    else
        return param2;
}

}

int main()
{
    int i = tut::max<int>(5, 4);
    // i = 5
    
    double d = tut::max<double>(3.5, 4.4);
    // d = 4.4;
}
```

Aby ten szablon funkcji mógł zadziałać ze zdefiniowan przez nas klasą, należy przeciążyć w niej operator ```>=``` , w przeciwnym razie program nam się nie skompiluje.

Szablony są jedynie przepisem, według którego kompilator generuje odpowiednie funkcje.

## Parametry szablonu które nie są typem

Poza typami, szablony funkcji mogą przyjmować również zmienne jako parametry szablonu. Przekazywane są one podczas kompilacji. Załóżmy że chcemy napisać funkcję, która przyjmuje tablicę 2D nieznanego typu o nieznanych rozmiarach. Możemy wtedy napisać:

```c++
namespace tut {

template<typename Type, size_t rows, size_t columns>
void func(Type array[rows][columns]);

}

int main()
{
    int array2D[5][4];
    tut::func<int, 5, 4>(array2D);
}
```

W języku C musielibyśmy dokonać konwersji tablicy na podwójny wskaźnik, co w niektórych przypadkach może być nieporządane, ponieważ tracimy wtedy informacje o rozmiarze, która jest zawarta w typie zmiennej. Dodatkowym atutem użycia szablonów funkcji w tym wypadku jest to, że nasz kod jest bardziej ekspresywny, na pierwszy rzut oka widać, że do tej funkcji przekazywana jest tablica.

Więcej informacji o zjawisku konwersji tablicy na wskaźnik można znaleźć tutaj: https://stackoverflow.com/questions/1461432/what-is-array-to-pointer-decay

## Szablony klas i struktur
Szablony możemy również wykorzystywać do tworzenia klas oraz struktur. Załóżmy że chcielibyśmy napisać naszą własną strukturę danych, która może przechowywać elementy o różnych typach.

```c++
namespace tut {

template<typename Type, size_t size>
class MyDataStructure
{
    Type array[size];
    // ...
};

}

int main()
{
    tut::MyDataStructure<int, 5> mds;
}
```

## Specjalizacja szablonów (Template specialization)
Za pomocą specjalizacji szablonów możemy określić odmienne działanie funkcji dla konkretnego typu.

```c++
namespace tut {
    
template<typename Type>
void func(const Type& arg);

template<>
void func<char>(const char& arg); // musimy użyć const referencji

}

int main()
{
    tut::func<int>(5);
    tut::func<double>(5.5);
    // zostaną wywołane funkcje wygenerowane przez główny szablon

    tut::func<char>('a');
    // zostanie wywolana nasza specjalizacja szablonu funkcji
}
```

## Dedukcja typów
Nie musimy za każdym razem określać typu przekazywanej zmiennej. W większości przypadków typ zostanie automatycznie wydedukowany.

```c++
namespace tut {
    
template<typename Type>
void func(const Type& arg);

template<>
void func<char>(const char& arg);
}

int main()
{
    tut::func(5); // ok
    tut::func(5.5); // ok
    tut::func('a'); // ok
    // w każdym przypadku zostanie wywołana odpowiednia funkcja
}
```

## Szablony wariadyczne (Variadic templates)
Z wykorzystaniem szablonów wariadycznych, możemy tworzyć funkcje, które przyjmują zmienną ilość argumentów o różnych typach. Napiszmy funkcję, która dodaje wszystkie przekazane elementy.

```c++
namespace tut
{

// trzy kropki oznaczają parameter pack
// auto pozwala kompilatorowi wydedukować typ zwracany
// więcej o dowiesz się z filmów z playlisty na youtube
template<typename ... T>
auto accumulate(T ... param)
{
    // poniższy syntax jest to fold expression
    // pozwala wykonywać różne operacje na wszystkich parametrach
    return (param + ...);
}

}
int main()
{
    // przekazane zostaje double, double, int, char
    // konwersja jest dopiero dokonywna podczas dodawania
    double x = tut::accumulate(1.0, 1.0, 1, 'a');
}

```

## Podsumowanie
* Jeżeli chcemy, żeby nasza funkcja mogła przyjmować parametry o różnych typach, możemy skorzystać z szablonów funkcji.
* Szablony są jedynie przepisem, według którego kompilator generuje odpowiednie funkcje.
* Możliwe jest przekazywanie zmiennych podczas kompilacji, poprzez parametry szablonu.
* Jeżeli chcemy, aby nasza szablon funkcji działał inaczej dla konkretnego typu, możemy skorzystać ze specjalizacji szablonów
* Szablony funkcji mogą przymować zmienną liczbę argumentów z wykorzystaniem operatora trzech kropek ```...```. Takie szablony nazywamy wariadycznymi.