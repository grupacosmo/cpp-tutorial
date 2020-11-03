# Nowoczesny C++
### Rozdział 1 | Część 1 | Śmiałe korzystanie z auto

### Wstęp
Język C++ doznał rewolucji z nadejściem wersji C++11. Kolejne wersje języka, C++14 oraz C++17, jeszcze bardziej zwiększyły jego możliwości. 
Ten poradnik ma na celu wyjaśnić jak korzystać z nowych funkcjonalności oraz jakich staromodnych praktyk unikać i dlaczego.

Zanim poruszymy paradygmat obiektowy, chciałbym zaprezentować *nowoczesne* sposoby na pisanie prostego kodu i na tym skupię się w tym rozdziale.
## auto (od C++11)
W otwierającej części poradnika zaczniemy od ```auto```. Jest to mechanizm, który pozwala na dedukcję typu zmiennej podczas jej inicjalizacji, 
w zależności od typu wyrażenia znajdującego się po prawej stronie. 
Przykład użycia:

```c++
void func()
{
  auto variable1 = 5;         // int
  auto variable2 = 5.5;       // double
  auto variable3 = 'c';       // char
  auto variable4 = "string";  // const char[7]
  auto variable5 = getVariable();  // typ wartości zwracanej
}
```
## Tylko po co?
```auto``` posiada wiele różnych zalet. Jeżeli posiadasz nawyk deklarowania każdej zmiennej jako auto wszędzie tam gdzie jest to odpowiednie,
możesz uniknąć wielu problemów. Zacznijmy od tych zalet które są najprostsze do zrozumienia.

### Mniej pisania
Czasem nazwy typów potrafią być na prawdę bardzo długie, również te znajdujące sie w bibliotece standardowej C++. Powoduje to często, że kod jest mniej czytelny.
 Korzystanie z ```auto``` pozwala rozwiązać ten problem. Na tym etapie może nie wydawać się to aż tak znaczące, ale zobaczycie w poźniejszych cżęściach poradnika, jak bardzo się przydaje.
 
### Zmienna auto musi zostać zainicjalizowana
Próba kompilacji poniższego kodu doprowadzi do błędu.
```C++
void func()
{
  auto variable;
  variable = 5;
}
```
Każda zmienna powinna zostać zainicjalizowana, nawyk używania ```auto``` nieumożliwi nam popełnienie błędu.

### Czasem po prostu trzeba użyć auto
Istnieją przypadki, w których użycie auto jest wymagane np. podczas deklarowania lambdy. Jeśli nie wiesz czym jest lambda, nie szkodzi, jest to temat na osobną część poradnika.

## Jak i kiedy używać?
Istota posiadania takiej funkjonalności jak ```auto``` powinna być już częściowo zrozumiała, przejdźmy więc do korzystania z niej.
```C++



