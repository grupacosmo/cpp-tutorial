##### Wiktor Więcław 
# C++ Część 6 | Przestrzenie nazw

## Przestrzenie nazw (Namespaces)
Możemy wykorzystywać przestrzenie nazw do unikania konfliktów nazw oraz do grupowania zmiennych globalnych, klas oraz funkcji. 

Aby dostać się do zawartości przestrzeni nazw należy skorzystać z operatora ```::```.  

```c++
namespace tut { // skrót od tutorial

const int global = 5;
    
class Class
{
public:
    Class() = default;
};

void func(const Class& param1, int param2);

}

int main()
{
    tut::Class object;
    
    tut::func(object, tut::global);
}
```

Gdy pracujemy z dużą bazą kodu lub gdy tworzymy bibliotekę, powinniśmy zawsze umieszczać nasz kod wewnątrz przestrzeni nazw.

## Przestrzenie nazw klas oraz struktur
Klasy oraz struktury mają swoje własne przestrzenie nazw.

Jeżeli stworzymy statyczną metodę wewnątrz klasy, czyli metodę, którą można używać bez tworzenia obiektu, to możemy ją wywołać z wykorzystaniem operatora dostępu ```::```.

```c++
class MyClass
{
public:
    MyClass() = default;
    static void staticFunc();
};

int main()
{
    MyClass::staticFunc();
}
```

## using namespace
W wielu poradnikach można spotkać się z użyciem dyrektywy ```using namespace``` w przestrzeni globalnej.

```c++
#include <iostream>
using namespace std;

int main()
{
    cout << "Nie rób tego" << endl;
}
```

Nie powinniśmy tego robić, dlatego że w większych bazach kodu, może to doprowadzić do konfliktów nazw.

Ewentualnie, jeśli to znacząco pomoże z czytelnością naszego kodu, możemy użyć ```using``` wewnątrz zasięgu funkcji lub klasy.

```c++
#include <iostream>
void print(int i)
{   
    using std::cout;
    using std::endl;

    cout << 5 << endl; // ok
}

int main()
{
    std::cout << 5 << std::endl;
    cout << 5 << endl; // błąd kompilacji
}
```

## Podsumowanie
* Powinniśmy umieszczać nasz kod wewnątrz przestrzeni nazw
* Klasy mają swoje własne przestrzenie nazw, w których zawarte są składowe oznaczone modyfikatorem ```static```.
* Nie powinniśmy używać ```using namespace```, szczególnie w przestrzeni globalnej.