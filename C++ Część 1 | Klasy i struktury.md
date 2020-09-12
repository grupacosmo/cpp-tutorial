##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 1

## Wstęp
Niniejszy poradnik zakłada, że czytelnik zna język C na poziomie podstawowym. C++ został domyślnie stworzony jako rozszerzenie języka C, zatem wspiera jego biblioteki. Można np. dodać do programu bibliotekę ```<stdio.h>``` i wypisać zmienną na ekran za pomocą funkcji ```printf```. Należy mieć na uwadze, że C++ posiada swoje własne biblioteki, których powinno się korzystać, ale powiemy o nich w poźniejszych częściach poradnika.

## Typy prymitywne (Primitive types)
Typy takie jak ```int```, ```double```, ```char```, ```bool``` nazywamy typami prymitywnymi.


## Struktury (Structs)
 W języku C++ można tworzyć swoje własne typy zmiennych za pomocą struktur oraz klas:
```c++
struct MyStruct
{
    int a;
    double b;
}

int main()
{
    MyStruct my_object;
}
```
Instancję takiej struktury nazywamy obiektem (object). Struktura jest jedynie przepisem na stworzenie obiektu. Obiekty są bardzo ważną częścią C++, mówimy że wspiera on paradygmat programowania obiektowego.

Stworzyliśmy nową strukturę i z jej pomocą zadeklarowaliśmy nowy obiekt. Na typ ```MyStruct``` składają się dwie zmienne o prymitywnych typach: ```int a``` oraz ```double b```. Aby dostać się do zmiennych ```a``` oraz ```b``` możemy skorzystać z operatora kropki.
```c++
int main()
{
    MyStruct my_object;
    my_object.a = 1;
    my_object.b = 2.3;
}
```
#### Metody (Methods)
Istnieje o wiele lepszy sposób na inicjalizację struktury. Otóż, struktury mogą zawierać również funkcje, które mają bezpośredni dostęp do zmiennych zawartych w strukturze. Specjalnym rodzajem takiej funkcji jest tak zwany konstruktor (constructor):
```c++
struct MyStruct
{
    int a;
    double b;
    
    MyStruct(int arg_a, double arg_b)
    {
        a = arg_a;
        b = arg_b;
    }
};
```
Konstruktor musi mieć taką samą nazwę jak struktura, oraz musi nie posiadać typu zwracanego. Teraz, aby stworzyć nasz obiekt, wystarczy napisać:
```c++
int main()
{
    MyStruct my_object(1, 2.3);
}
```


Funkcje zdefiniowane wewnątrz struktury nazywamy metodami. Stwórzmy jeszcze jedną metodę:
```c++
struct MyStruct
{
    int a;
    double b;
    
    MyStruct(int arg_a, double arg_b)
    {
        a = arg_a;
        b = arg_b;
    }
    
    double get_sum()
    {
        return a + b;
    }
};
```
A teraz wywołajmy ją w funkcji main():

```c++
int main()
{
    MyStruct my_object(1, 2.3);
    double sum_result = my_object.get_sum();
}
```
## Klasy (Classes)
Z technicznego punktu widzenia, klasa w C++ różni się od struktury tylko jedną własnością. Kiedy już stworzymy obiekt klasy, domyślnie nie mamy dostępu do jego zawartości za pomocą operatora kropki. Klas używamy wtedy kiedy z założenia chcemy ukryć pewne zmienne oraz funkcje przed programistami używającymi naszych klas. Zakładamy, że pewne rzeczy powinny dziać się w tle kiedy używamy dostępnych funkcji, tak aby programiści nie musieli tracić czasu na szczegóły. Aby umożliwić korzystanie z naszych funkcji musimy wykorzystać słowo kluczowe ```public```. Stwórzmy przykładową klasę, podobną do naszej poprzedniej struktury:
```c++
class MyClass
{
    int a;
    double b;

public:
    MyClass(int arg_a, double arg_b)
    {
        a = arg_a;
        b = arg_b;
    }
    
    double get_sum()
    {
        return a + b;
    }
};
```
Mówimy, że nasze zmienne ```a``` i ```b``` są prywatne, dla przejrzystości możemy użyć słowa ```private```:

```c++
class MyClass
{
private:
    int a;
    double b;

public:
    MyClass(int arg_a, double arg_b)
    {
        a = arg_a;
        b = arg_b;
    }
    
    double get_sum()
    {
        return a + b;
    }
};
```
Słów ```private``` oraz ```public``` możemy używać również w strukturach. Jedyną różnicą jest to, że jeśli jawnie nie oznaczymy członków struktury to będą one domyślnie publiczne, a w przypadku klasy będą one prywatne.

Klasy powinniśmy używać w przypadku, gdy nasz obiekt stanowi pewną integralną całość. Na przykład jakbyśmy chcieli za pomocą obiektów zareprezentować samochód użylibyśmy klasy, a gdybyśmy chcieli stworzyć "luźny" zbiór np. bukiet kwiatów, to użylibyśmy struktury.
