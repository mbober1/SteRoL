# Zadanie 1 - ex1

Debugowanie

Przedstawione zadania dotyczą:
- obsługi interfejsu szeregowego,
- zarządzania przerwaniami,
- funkcje zwrotne,
- przekierowania standardowego wyjścia.

Podczas wykonywania ćwiczeń wykorzystaj instrukcje laboratoryjną:

W. Domski, Sterowniki robotów, Laboratorium – Debugowanie, 
Zaawansowane techniki debugowania, 2018

W. Domski, Sterowniki robotów, Laboratorium – Liczniki i przerwania, 
Tryby pracy licznika oraz obsługa przerwań, 2018

## Przekierowanie standardowego wyjścia - ex1_1

Przekieruj standardowe wyjście na interfejs szeregowy 
UART dostępny za pośrednictwem peryferium UART2. 
Do wyświetlania komunikatu na interfejsie szeregowym 
wykorzystaj funkcję **printf()**.

Napisz program, który będzie wyświetlał napis 
"Witaj", po którym pojawi się liczba. Liczba 
ta ma być inkrementowana dla każdej kolejnej linii.

Nowy napis ma być wypisywany co 1 sekundę.

Do komunikacji poprzez port szeregowy wykorzystaj program 
**minicom** dostępny na serwerze. Ścieżka do urządzenia szeregowego 
jest przypisana indywidualnie do każdej z płytek. Można 
ją odczytać bezpośrednio przez serwer statusu.

Przykładowo:

```
Witaj 1
Witaj 2
Witaj 3
```

Projekt nazwij jako *ex1_1*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

### Jak to zrobić?
Stwórz projekt, ustaw serial port i wykorzystaj podany kod (tylko tam gdzie polskie komentarze)

## Odczytywanie danych z interfejsu szeregowego ex1_2

Napisz program, który będzie wypisywał na przekierowane standardowe 
wyjście napis "Witaj", bądź "Hej", po którym 
będzie znajdować się inkrementowana liczba dla każdej kolejnej 
linii.

Nowy napis ma być wypisywany co 1 sekundę.

Do komunikacji poprzez port szeregowy wykorzystaj program 
**minicom** dostępny na serwerze.

Aktualnie wypisywany napis ma zależeć od trybu jaki wybierze 
użytkownik za pośrednictwem interfejsu szeregowego. 
W przypadku, gdy użytkownik poda 'a' to wypisywany jest 
napis 'Witaj', dla 'b' wypisywany jest napis 'Hej'. W przypadku 
każdej innej wartości wypisywany jest komunikat 
"Niepoprawne dane" i kontynuowane jest wypisywane poprzedniego 
napisu.

Przykładowo:

```
Witaj 1
Witaj 2
Witaj 3   <- b
Hej 4
Hej 5     <- a
Witaj 6
Witaj 7   <- z
Niepoprawne dane
Witaj 8   
Witaj 9
Witaj 10
```

Tekst np. "<- b" wskazuje na moment wciśnięcia klawisza "b" oraz 
zatwierdzenia jego wprowadzenia klawiszem "Enter". Tekst 
ten ("<- b") nie powinien być wyświetlany na ekranie. Ma on jedynie 
na celu pokazanie interakcji użytkownika z oprogramowanie *minicom*.

Do realizacji zadania wykorzystaj przerwania, a w szczególności 
wykorzystaj funkcje zwrotne:
```C
HAL_UART_RxCpltCallback();
```

Pamiętaj o odpowiedniej deklaracji zmiennych, które będą wykorzystywane 
w obsłudze przerwania. Przestrzegaj zasady dotyczącej implementacji 
przerwań, obsługę przerwania należy zakończyć tak szybko jak jest 
to możliwe, m.in. nie powinno wykorzystywać się funkcji 
printf() i jej podobnych wewnątrz obsługi przerwania.

Projekt nazwij jako *ex1_2*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

### Jak to zrobić?
Stwórz projekt, ustaw serial port z obsługą przerwań i wykorzystaj podany kod (tylko tam gdzie polskie komentarze).
W mojej wersji nie trzeba zatwierdzać odebrania danych enterem, także poprawcie sobie.

## Włączanie i wyłączanie diody ex1_3

Napisz program, który będzie przełączał diody na złączach:
LED1, LED2 oraz TIMER4.

Program pozwala na wybór aktualnie sterowanej diody za pomocą 
interfejsu szeregowego. 
Diody wybierane są za pomocą komendy:

|Dioda|Komenda|
|-|-|
|LED1|a|
|LED2|b|
|TIMER4|c|

Domyślnie wybrana jest dioda podłączona do złącza LED1. 
Początkowo wszystkie diody są wyłączone.

W przypadku podania innej komendy jest ona ignorowana.

Włączenie lub wyłączenie diody odbywa się poprzez wydawanie akcji:

|Stan diody|Akcja|
|-|-|
|Dioda włączona|1|
|Dioda wyłączona|0|

Każda inna akcja jest ignorowana.

Przykładowo, użytkownik wprowadza sekwencję:

```
a   <- wybór sterowania diodą podłączoną do złącza LED1
1   <- włączenie diody LED1
b   <- wybór sterowania diodą podłączoną do złącza LED2
1   <- włączenie diody LED2
0   <- wyłączenie diody LED2
c   <- wybór sterowania diodą podłączoną do złącza TIMER4
1   <- włączenie diody podłączonej do złącza TIMER4
d   <- ignorowanie komendy, wciąż aktywne jest sterowanie diodą podłączonej do złącza TIMER4
0   <- wyłączenie diody podłączonej do złącza TIMER4
```

Tekst np. "<- wybór sterowania ..." wskazuje na moment wciśnięcia klawisza "a" oraz 
zatwierdzenia jego wprowadzenia klawiszem "Enter". Tekst 
ten ("<- wybór sterowania ...") nie powinien być wyświetlany na ekranie. Ma on jedynie 
na celu pokazanie interakcji użytkownika z oprogramowanie *minicom*.

Projekt nazwij jako *ex1_3*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

## Wskazówki

Wykorzystaj funkcje:
```C
HAL_UART_Receive_IT();
HAL_UART_Transmit();
```

Pamiętaj o włączeniu przerwań dla peryferium UART2.

Zastanów się jak zmusić program do natychmiastowego wypisania 
napisu na standardowe wyjście.

W przypadku odbierania danych ustaw liczbę odbieranych 
danych na odpowiednią liczbę. Ile powinna ona wynosić i dlaczego?

