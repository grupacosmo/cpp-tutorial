##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 2

## Przeciążanie funkcji (Function overloading)
Przeciążanie funkcji jest to stworzenie nowej funkcji o takiej samej nazwie. Funkcje muszą różnić się typem lub liczbą przyjmowanych argumentów.

```c++
void my_function(int arg);
void my_function(double arg);
void my_function(int arg1, int arg2);
```

Funkcje mogą różnić się typem zwracanym, natomiast jeśli funkcje przyjmują takie same typy argumentów to typ wartości zwracanej nie jest wystarczającym warunkiem na przeciążenie funkcji.

```c++
// DOBRZE
int my_function(int arg);
double my_function(double arg);

// ZLE
int my_function(int arg);
double my_function(int arg);
```

Przedstawmy przykładowe zastosowanie:
```c++
struct IntPair
{
public:
    int a, b;
    
    IntPair(int arg_a, int arg_b) // constructor
    { 
        a = arg_a;
        b = arg_b; 
    }
};

int sum(int a, int b)
{
    return a + b;
}

IntPair sum(IntPair pair_1, IntPair pair_2)
{
    IntPair result(pair_1.a + pair_2.a, pair_1.b + pair_2.b);
    return result;
}
```

## Przeciążanie operatorów (Operator overloading)
W języku C++ mamy możliwość przeciążenia operatorów takich jak np. ```+```, ```-```, ```=```, ```==```, itd. Większość podstawowych operatorów w C++ może zostać przeciążona, z wyjatkiem: ```.```,   ```::```,  ```?:```,  ```sizeof```.

Zamieńmy funkcję sum z poprzedniego przykładu na przeciążenie operatora ```+```.

```c++
struct IntPair
{
public:
	int a, b;

	IntPair(int arg_a, int arg_b) // constructor
	{
		a = arg_a;
		b = arg_b;
	}
};

IntPair operator+(IntPair pair_1, IntPair pair_2)
{
	IntPair result(pair_1.a + pair_2.a, pair_1.b + pair_2.b);
	return result;
}

int main()
{
	IntPair a(1, 2);
	IntPair b(3, 4);

	IntPair c = a + b;
}
```

Jeżeli nasza struktura ```IntPair``` byłaby klasą, nasza funkcja przeciażająca operator ```+``` doprowadziłaby do błędu kompilacji, dlatego że nie miałaby dostępu do zmiennych ```a``` oraz ```b```. Możemy zatem dokonać przeciążenia operatora wewnątrz klasy (moglibyśmy również zrobić to w przypadku struktury, chociażby dla przejrzystości):
```c++
class IntPair
{
private:
	int a, b;

public:
	IntPair(int arg_a, int arg_b) // constructor
	{
		a = arg_a;
		b = arg_b;
	}

    // zwroc uwage ze tym razem podajemy tylko jeden argument
    // wyobraz sobie wywolanie tej metody jako int_pair_1.sum(int_pair_2)
    // mimo ze bedzie wygladalo ono tak: int_pair_1 + int_pair_2
    // jest to metoda klasy, wiec ma od razu dostep do pierwszego obiektu wywolujacego
	IntPair operator+(IntPair pair) 
	{
		IntPair result(a + pair.a, b + pair.b);
		return result;
	}
};

int main()
{
	IntPair a(1, 2);
	IntPair b(3, 4);

	IntPair c = a + b;
}
```

# Szablony funkcji (Function templates)
Załóżmy że chcemy stworzyć funkcję ```max```, która porównuje dwie liczby lub obiekty i zwraca większy z nich. Gdybyśmy chcieli skorzystać wyłącznie z przeciążania funkcji to musielibyśmy zaimplementować oddzielne przeciążenie dla każdego typu.

Z pomocą przychodzą szablony funkcji:
```c++
template<typename ArgType>
ArgType max(ArgType arg_1, ArgType arg_2)
{
    if(arg_1 >= arg_2)
    {
        return arg_1;
    }
    else
    {
        return arg_2;
    }
}

int main()
{
    int result_int = max<int>(5, 4);
    // result_int = 5
    
    double result_double = max<double>(3.5, 4.4);
    // result_double = 4.4;
}
```
Aby ten szablon funkcji mógł zadziałać ze zdefiniowaną przez nas klasą, należy przeciążyć operator ```>=``` w tej klasie.

Szablony funkcji mogą również przyjmować prymitywne wartości oraz obiekty. Załóżmy że mamy jakąś funkcje która przyjmuje tablicę 2D nieznanego typu o nieznanych rozmiarach. Możemy wtedy napisac:
```c++
template<typename Type, unsigned int rows, unsigned int columns>
void my_function(Type my_array[rows][columns]);

int main()
{
    int array[5][4];
    my_function<int, 5, 4>(array);
}
```
W języku C musielibyśmy dokonać konwersji tablicy na podwójny wskaźnik, co w niektórych przypadkach może być nieporządane, ponieważ tracimy informacje o rozmiarze, która jest zawarta w tablicy. Dodatkowo nasz kod jest bardziej ekspresywny, na pierwszy rzut oka widać, że mamy doczynienia z tablicą.

Więcej informacji można znaleźć tutaj: https://stackoverflow.com/questions/1461432/what-is-array-to-pointer-decay

