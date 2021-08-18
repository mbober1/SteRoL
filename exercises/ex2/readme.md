# Zadanie 2 - ex2

Liczniki i przerwania

Przedstawione zadania dotyczą:
- konfiguracja licznika w trybie generatora podstawy czasu,
- konfiguracja licznika jako generatora sygnału PWM,
- konfiguracja licznika w trybie Input Capture,
- zarządzania przerwaniami.

Podczas wykonywania ćwiczeń wykorzystaj instrukcje laboratoryjną:

W. Domski, Sterowniki robotów, Laboratorium – Liczniki i przerwania, 
Tryby pracy licznika oraz obsługa przerwań, 2018

## Generator podstawy czasu - ex2_1

Napisz program, który będzie mrugał diodą LED podłączoną do 
złącza **LED1**. W tym celu wykorzystaj dowolny licznik 
np. TIM6 oraz przerwania. Skonfiguruj licznik tak, aby 
przerwanie było generowana **dokładnie** co 1 sekundę, 
czyli z częstotliwością 1 Hz.

Dlaczego warto wykorzystywać liczniki jako generatory podstawy 
czasu zamiast opóźnień programowych takich jak **HAL_Delay()**? 
### Bo są dokładniejsze i nie blokują nam procka

Skonfiguruj przerwania i wykorzystaj funkcję zwrotną
```C
HAL_TIM_PeriodElapsedCallback()
```

Projekt nazwij jako *ex2_1*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

### Jak to zrobić?
Stwórz projekt, ustaw odpowiedni timer (taki do którego podłączona jest dioda) z obsługą przerwań i wykorzystaj podany kod (tylko tam gdzie polskie komentarze).

## Generator sygnału PWM - ex2_2

Napisz program, który będzie regulował jasność świecenia diody, 
w kilku poziomach:
- 0 (0% wypełnienia, dioda wyłączona),
- 1 (25% wypełnienia),
- 2 (50% wypełnienia),
- 3 (75% wypełnienia),
- 4 (100% wypełnienia).

Poziom (0, 1, 2, 3 lub 4) jest zadawany za pośrednictwem 
interfejsu szeregowego jako znaki '0', '1', ... 
Inne wartości przesłane za pomocą 
interfejsu szeregowego mają być ignorowane.

Częstotliwość sygnału PWM powinna zostać ustawiona 
na 1kHz.

Do realizacji tego zadania wykorzystaj diodę LED 
podłączoną do złącza TIMER4.

Projekt nazwij jako *ex2_2*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

### Jak to zrobić?
Stwórz projekt, ustaw odpowiedni timer (taki do którego podłączona jest dioda) w trybie PWM i ustaw UART. Wykorzystaj podany kod (tylko tam gdzie polskie komentarze).

## Tryb Input Capture - ex2_3

Skonfiguruj złącze TIMER1 jako cyfrowe wyjście, natomiast 
złącze TIMER5 jako wejście do układu liczącego skonfigurowane 
w trybie Input Capture.
Oba złącza TIMER1 oraz TIMER5 są ze sobą połączone.

Układ liczący powinien być tak skonfigurowany, aby wykrywał 
zmiany na wejściu Input Capture z rozdzielczością 
**dokładnie** 400 mikrosekund.

Napisz program, który będzie zmieniał stan cyfrowego wyjścia 
(złącze TIMER1) w oparciu o dane przychodzące z interfejsu 
szeregowego. Komenda, która będzie powodować zmianę stanu 
złącza TIMER1 to 'z'. Wszystkie inne znaki powinny być ignorowane.

Po wysłaniu znaku program powinien podać czas w sekundach 
jaki upłynął od ostatniej zmiany. W tym celu należy wykorzystać 
wartość zatrzaskiwaną w odpowiednim rejestrze, który 
jest skojarzony z wejściem Input Capture przypisanym do 
złącza TIMER5.

Aktywuj przerwania dla Input Capture oraz zaimplementuj 
obsługę przerwań wykorzystując 
```C
HAL_TIM_IC_CaptureCallback()
```

Projekt nazwij jako *ex2_3*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.
