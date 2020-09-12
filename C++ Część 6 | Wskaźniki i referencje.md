##### Wiktor Więcław 
# Wprowadzenie do języka C++ część 6

## Wskaźniki (Pointers)
Jak zapewne wiesz, wskaźnik jest to zmienna przechowująca adres do innej zmiennej. Można powiedzieć, że wskaźnik jest to po prostu liczba, która jest interpretowana jako adres.
```c++
int main()
{
  int variable = 5;
  int* pointer = &variable; // operator & w tej sytuacji oznacza adres zmiennej
  
  *pointer = 4; // wyłuskanie wskaznika
  std::cout << variable << std::endl // zostanie wypisana wartość 4
}
```

## Referencje (References)
Referencje są podobne do wskaźników, z tą różnicą, że nie są liczbą, tylko bezpośrednim wiązaniem do danych. Przeanalizujmy poniższy kod:

```c++
int main()
{
  int variable = 5;
  int &reference = variable; // operator & w tej sytuacji oznacza deklaracje referencji
  
  std::cout << reference << std::endl; // zostanie wypisana wartość 5
  
  reference = 4; 
  
  std::cout << variable << std::endl; // zostanie wypisana wartość 4
}
```
Referencja w tym wypadku jest to po prostu nowa, dodatkowa nazwa dla zmiennej ```variable```, tak zwany alias. Obie zmienne odnoszą się bezpośrednio do tej samej komórki pamięci.
Zwróć uwagę, że w przypadku użycia referencji uzyskujemy tę sąmą funkcjonalność, bez używania operatorów wyłuskania i adresu, dzięki czemu nasz kod jest bardziej przejrzysty.

## Przekazywanie zmiennych do funkcji
Mamy 3 sposoby na przekazanie zmiennych do funkcji. Poprzez kopie, wskaźnik lub referencje. Zastanówmy się nad poniższym kodem:
```c++
void func_copy(int arg) // przekazywanie przez kopię
{
  arg = 5;
}

void func_pointer(int *arg) // przekazywanie przez wskaźnik
{
  *arg = 5;
}

void func_reference(int &arg) // przekazywanie przez referencję
{
  arg = 5;
}

int main()
{
  int example_1 = 0;
  func_copy(example_1);
  std::cout << example_1 << std::endl; // zostanie wypisana wartość 0

  int example_2 = 0;
  func_pointer(&example_2);
  std::cout << example_2 << std::endl; // zostanie wypisana wartość 5
  
  int example_3 = 0;
  func_reference(example_3);
  std::cout << example_3 << std::endl; // zostanie wypisana wartość 5
}
```
Jeżeli chcemy móc zmienić naszą zmienną zadeklarowaną w funkcji ```main``` wewnątrz innej funkcji powinniśmy przekazywać ją poprzez referencję.
