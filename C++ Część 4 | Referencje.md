##### Wiktor Więcław 
# C++ Część 4 | Referencje

## Wskaźnik (Pointer)
Jak zapewne wiesz, wskaźnik jest to zmienna przechowująca adres do innej zmiennej. Można powiedzieć, że wskaźnik jest to po prostu liczba, która jest interpretowana jako adres.

```c++
int main()
{
  int variable = 5;
  int* pointer = &variable; // operator & w tej sytuacji oznacza adres zmiennej
  
  *pointer = 4; // wyłuskanie wskaznika

  std::cout << variable << std::endl // output: 4
}

```
## Referencja (Reference)
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

## Przekazywanie zmiennych do funkcji
Możemy wyróżnić 3 sposoby na przekazanie zmiennych do funkcji. Poprzez kopie, wskaźnik lub referencje. Zastanówmy się nad poniższym kodem:

```c++
void incrementByCopy(int param) // funkcja przyjmuje kopie
{
    ++param;
}

void incrementByPointer(int* param) // funkcja przyjmuje wskaźnik
{
    ++(*param); // wyłuskanie wskaźnika
}

void incrementByReference(int& param) // funkcja przyjmuje referencje
{
    ++param;
}

int main()
{
  int variable = 0;
  incrementByCopy(variable);
  std::cout << variable << std::endl; // zostanie wypisana wartość 0, wartość zmiennej nie zmieniła się

  incrementByPointer(&variable);
  std::cout << variable << std::endl; // zostanie wypisana wartość 1

  incrementByReference(variable);
  std::cout << variable << std::endl; // zostanie wypisana wartość 2
}

```
Jeżeli chcemy zmienić przekazaną zmienną wewnątrz funkcji, powinniśmy korzystać z przekazywania przez referencje zamiast wskaźnika, aby nie używać niepotrzebnie operatora adresu ```&``` i operatora wyłuskania ```*```.

## Podsumowanie
* Referencja jest to nowe, bezpośrednie wiązanie do danych, które są już przypisane do pewnej zmiennej.
* Jeśli funkcja otrzymuje argument poprzez referencję, to  uzyskuje bezpośredni dostęp do zewnętrznego obiektu.