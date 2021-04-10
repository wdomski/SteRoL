# Zadanie 4 - ex4

Regulator PID

Przedstawione zadania dotyczą implementacji 
regulatora PID w oparciu o:
- przetwornik DAC,
- licznik w konfiguracji generatora sygnału PWM.

Podczas wykonywania ćwiczeń wykorzystaj instrukcje laboratoryjne:

W. Domski, Sterowniki robotów, Laboratorium – ADC, DAC i DMA, 
Przetwoniki analogowo–cyfrowe, cyfrowo–analogowe oraz bezpośredni 
dostęp do pamięci, 2017

W. Domski, Sterowniki robotów, Laboratorium – Regulator PID, 
Implementacja i strojenie regulatora PID na bazie symulatora 
silnika, 2018

Napięcie referencyjne dla przetwornika ADC wynosi +3.3V.

Numer kanału przetwornika ADC można odczytać za pomocą programu 
STM32CubeMX najeżdżając na odpowiedni pin mikrokontrolera 
przypisany do danego złącza.

Przedstawione ćwiczenia dotyczą sterowania silnikiem 
prądu stałego. W tym celu można wykorzystać symulator takiego 
silnika w formie filtru dolnoprzepustowego. 
Symulator ten pozwala na sterowanie silnikiem z wykorzystaniem 
pomiaru prędkości obrotowej.

## Regulator PID z wyjściem DAC - ex4_1

Napisz program, który będzie sterował obrotami silnika prądu 
stałego. Do sterowania silnikiem wykorzystaj wyjście 
przetwornika cyfrowo-analogowego **DAC1**. Pomiar 
napięcia stanowiący informację zwrotną o prędkości 
obrotowej odbywa się poprzez wykorzystanie kanału 
przetwornika analogowo-cyfrowego dostępnego na złączu **ADC1**.

Zaimplementuj w programie główną pętlę sterującą, 
która będzie działać z częstotliwością 100 Hz. 
Do realizacji tej części zadania wykorzystaj dowolny licznik 
w konfiguracji generatora podstawy czasu.

Zaimplementuj regulator PID, który będzie 
posiadał człon proporcjonalny, całkujący oraz różniczkujący, 
Pamiętaj o odpowiednim skalowaniu wartości i ograniczaniu 
wyjść regulatora.

Stwórz interfejs programowy, który będzie co 200 milisekund 
wyświetlał aktualną prędkość obrotową w procentach. 
Należy przyjąć skalę linową, gdzie minimalna wartości 
mierzona przez przetwornika ADC to 0%, natomiast 100% 
odpowiada maksymalnej możliwej wartości zmierzonej. 
Dodatkowo należy umożliwić wprowadzanie wartości zadanej. 
Użytkownik może poprzez interfejs szeregowy wprowadzić 
kilka predefiniowanych wartości podanych w poniższej tabeli.

|Prędkość zadana|Procent maksymalnej prędkości|
|-|-|
|0 |  0|
|1 | 25|
|2 | 50|
|3 | 75|
|4 |100|

Przykładowo użytkownik wprowadza wartość 2, co odpowiada 
50% maksymalnej prędkości. Dla takiej wartości na kanale pomiarowym 
przetwornika ADC powinno byś obserwowane napięcie wynoszące 
około połowę zakresu pomiarowego, to jest (3.3 V * 0.5 = 2.65 V).

Projekt nazwij jako *ex4_1*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

### Warianty zadania

Zadanie można zrealizować łącznie w kilku różnych wariantach, 
które zróżnicowane są poprzez tryby działania konwerterów ADC i DAC.

W przypadku konwertera ADC możliwe jest:
- programowe wyzwalanie pomiaru,
- programowe wyzwalanie pomiaru poprzez wykorzystanie przerwania 
od licznika,
- automatyczne wyzwalanie pomiaru za pomocą zdarzenia pochodzącego od licznika,
- pomiar napięcia w trybie ciągłym,
- wykorzystanie kontrolera DMA do automatycznego odczytu pomiaru.

W przypadku konwertera DAC możliwe jest:
- programowe zadawanie nowej wartości generowanego napięcia,
- wykorzystanie układu liczącego do programowego 
zadawania nowej wartości,
- wykorzystanie przerwania od układu liczącego do 
wyzwolenia transferu DMA w celu zapisania nowej wartości 
w rejestrze danych peryferium DAC.

## Regulator PID z wyjściem PWM - ex4_2

Napisz program, który będzie sterował obrotami silnika prądu 
stałego. Do sterowania silnikiem wykorzystaj wyjście 
generatora sygnału PWM **TIMER3**. Częstotliwość 
generowanego sygnału PWM to 1 kHz. Pomiar 
napięcia stanowiący informację zwrotną o prędkości 
obrotowej odbywa się poprzez wykorzystanie kanału 
przetwornika analogowo-cyfrowego dostępnego na złączu **ADC2**.

Zaimplementuj w programie główną pętlę sterującą, 
która będzie działać z częstotliwością 100 Hz. 
Do realizacji tej części zadania wykorzystaj dowolny licznik 
w konfiguracji generatora podstawy czasu.

Zaimplementuj regulator PID, który będzie 
posiadał człon proporcjonalny, całkujący oraz różniczkujący, 
Pamiętaj o odpowiednim skalowaniu wartości i ograniczaniu 
wyjść regulatora.

Stwórz interfejs programowy, który będzie co 200 milisekund 
wyświetlał aktualną prędkość obrotową w procentach. 
Należy przyjąć skalę linową, gdzie minimalna wartości 
mierzona przez przetwornika ADC to 0%, natomiast 100% 
odpowiada maksymalnej możliwej wartości zmierzonej. 
Dodatkowo należy umożliwić wprowadzanie wartości zadanej. 
Użytkownik może poprzez interfejs szeregowy wprowadzić 
kilka predefiniowanych wartości podanych w poniższej tabeli.

|Prędkość zadana|Procent maksymalnej prędkości|
|-|-|
|0 |  0|
|1 | 25|
|2 | 50|
|3 | 75|
|4 |100|

Przykładowo użytkownik wprowadza wartość 2, co odpowiada 
50% maksymalnej prędkości. Dla takiej wartości na kanale pomiarowym 
przetwornika ADC powinno byś obserwowane napięcie wynoszące 
około połowę zakresu pomiarowego, to jest (3.3 V * 0.5 = 2.65 V).

Projekt nazwij jako *ex4_2*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

### Warianty zadania

Zadanie można zrealizować łącznie w kilku różnych wariantach, 
które zróżnicowane są poprzez tryby działania konwertera DAC.

W przypadku konwertera DAC możliwe jest:
- programowe zadawanie nowej wartości generowanego napięcia,
- wykorzystanie układu liczącego do programowego 
zadawania nowej wartości,
- wykorzystanie przerwania od układu liczącego do 
wyzwolenia transferu DMA w celu zapisania nowej wartości 
w rejestrze danych peryferium DAC.
