##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 4

## Przestrzenie nazw (Namespaces)
Możemy wykorzystać przestrzenie nazw do unikania konfliktów nazw oraz do grupowania zmiennych globalnych, struktur oraz funkcji. Aby dostać się do zawartości przestrzeni nazw należy skorzystać z operatora ```::```.  
```c++
namespace my_nmspc
{
    int global = 5;
    
    class Class
    {
    public:
        Class();
    };

    void func(Class arg_1, int arg_2);
}

int main()
{
    my_nmspc::Class example_class;
    
    my_nmspc::func(example_class, my_nmspc::global);
}
```

## Przestrzenie nazw klas oraz struktur
Klasy oraz struktury mają swoją własną przestrzeń nazw. Jeżeli stworzymy statyczną metodę wewnątrz klasy, czyli metodę którą można używać bez tworzenia obiektu, to aby ją wywołać musimy skorzystać z przestrzeni nazw. Więcej o słowie kluczowym ```static``` powiemy w późniejszych częsciach poradnika.
```c++
class MyClass
{
public:
    MyClass();
    static void static_func();
};

int main()
{
    MyClass::static_func();
}
```
