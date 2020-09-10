##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 3 wersja BETA
# 
# 
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

Szablony funkcji mogą również przyjmować prymitywne wartości oraz obiekty. Załóżmy że chcemy mieć funkcję, która przyjmuje tablicę 2D nieznanego typu o nieznanych rozmiarach. Możemy wtedy napisać:
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

Więcej informacji zjawisku konwersji tablicy na wskaźnik można znaleźć tutaj: https://stackoverflow.com/questions/1461432/what-is-array-to-pointer-decay

# TO BE CONTINUED
template function specialization
