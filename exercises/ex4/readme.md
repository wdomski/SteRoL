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
wyświetlał aktualną prędkość obrotową MV w procentach 
jak również surową (nieprzetworzoną) wartość wykonanego 
pomiaru.

Należy przyjąć skalę linową, gdzie minimalna wartości 
zmierzona przez przetwornik ADC to 0%, natomiast 100% 
odpowiada maksymalnej możliwej wartości zmierzonej. 
Ponadto oprócz aktualnej prędkości obrotowej należy wyświetlać:
- wartość sygnału sterującego CS, 
- wartość zadaną SP (w procentach oraz przeliczona 
do zakresu przetwornika ADC).

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

Przykładowe logi z procesu sterowania:
```
DAC: MV:    8,   0%, CS:    0, SP:    0,   0%
DAC: MV:    7,   0%, CS:    0, SP:    0,   0%
DAC: MV:    9,   0%, CS:    0, SP:    0,   0%
DAC: MV:    8,   0%, CS:    0, SP:    0,   0%
DAC: MV:    4,   0%, CS:    0, SP:    0,   0%
DAC: MV:    5,   0%, CS:    0, SP:    0,   0%
DAC: MV:  642,  15%, CS: 4095, SP: 4095, 100%
DAC: MV: 1231,  30%, CS: 4095, SP: 4095, 100%
DAC: MV: 1711,  41%, CS: 4095, SP: 4095, 100%
DAC: MV: 2100,  51%, CS: 4095, SP: 4095, 100%
DAC: MV: 2422,  59%, CS: 4095, SP: 4095, 100%
DAC: MV: 2683,  65%, CS: 4095, SP: 4095, 100%
DAC: MV: 2899,  70%, CS: 4095, SP: 4095, 100%
DAC: MV: 3075,  75%, CS: 4095, SP: 4095, 100%
DAC: MV: 2743,  66%, CS:    0, SP: 1023,  25%
DAC: MV: 2242,  54%, CS:    0, SP: 1023,  25%
DAC: MV: 1835,  44%, CS:    0, SP: 1023,  25%
DAC: MV: 1504,  36%, CS:    0, SP: 1023,  25%
DAC: MV: 1233,  30%, CS:    0, SP: 1023,  25%
DAC: MV: 1012,  24%, CS:    0, SP: 1023,  25%
DAC: MV:  831,  20%, CS:    0, SP: 1023,  25%
DAC: MV:  687,  16%, CS:  344, SP: 1023,  25%
DAC: MV:  755,  18%, CS: 1476, SP: 1023,  25%
DAC: MV:  885,  21%, CS: 1538, SP: 1023,  25%
DAC: MV:  970,  23%, CS: 1362, SP: 1023,  25%
DAC: MV: 1010,  24%, CS: 1210, SP: 1023,  25%
DAC: MV:  989,  24%, CS:    0, SP:    0,   0%
DAC: MV:  809,  19%, CS:    0, SP:    0,   0%
DAC: MV:  665,  16%, CS:    0, SP:    0,   0%
DAC: MV:  551,  13%, CS:    0, SP:    0,   0%
DAC: MV:  448,  10%, CS:    0, SP:    0,   0%
DAC: MV:  370,   9%, CS:    0, SP:    0,   0%
DAC: MV:  306,   7%, CS:    0, SP:    0,   0%
DAC: MV:  253,   6%, CS:    0, SP:    0,   0%
DAC: MV:  208,   5%, CS:    0, SP:    0,   0%
DAC: MV:  175,   4%, CS:    0, SP:    0,   0%
DAC: MV:  145,   3%, CS:    0, SP:    0,   0%
DAC: MV:  120,   2%, CS:    0, SP:    0,   0%
DAC: MV:  102,   2%, CS:    0, SP:    0,   0%
```

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
wyświetlał aktualną prędkość obrotową MV w procentach 
jak również surową (nieprzetworzoną) wartość wykonanego 
pomiaru.

Należy przyjąć skalę linową, gdzie minimalna wartości 
zmierzona przez przetwornik ADC to 0%, natomiast 100% 
odpowiada maksymalnej możliwej wartości zmierzonej. 
Ponadto oprócz aktualnej prędkości obrotowej należy wyświetlać:
- wartość sygnału sterującego CS, 
- wartość zadaną SP (w procentach oraz przeliczona 
do zakresu przetwornika ADC).

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

Przykładowe logi z procesu sterowania:
```
PWM: MV:    0,   0%, CS:    0, SP:    0,   0%
PWM: MV:    0,   0%, CS:    0, SP:    0,   0%
PWM: MV:    0,   0%, CS:    0, SP:    0,   0%
PWM: MV:  204,   4%, CS: 1000, SP: 1023,  25%
PWM: MV:  874,  21%, CS: 1000, SP: 1023,  25%
PWM: MV: 1039,  25%, CS:  592, SP: 1023,  25%
PWM: MV: 1035,  25%, CS:  120, SP: 1023,  25%
PWM: MV: 1089,  26%, CS:    0, SP: 1023,  25%
PWM: MV: 1020,  24%, CS:    0, SP: 1023,  25%
PWM: MV: 1175,  28%, CS:    0, SP: 1023,  25%
PWM: MV: 1327,  32%, CS: 1000, SP: 4095, 100%
PWM: MV: 1790,  43%, CS: 1000, SP: 4095, 100%
PWM: MV: 2174,  53%, CS: 1000, SP: 4095, 100%
PWM: MV: 2485,  60%, CS: 1000, SP: 4095, 100%
PWM: MV: 2741,  66%, CS: 1000, SP: 4095, 100%
PWM: MV: 2950,  72%, CS: 1000, SP: 4095, 100%
PWM: MV: 3122,  76%, CS: 1000, SP: 4095, 100%
PWM: MV: 3262,  79%, CS: 1000, SP: 4095, 100%
PWM: MV: 3378,  82%, CS: 1000, SP: 4095, 100%
PWM: MV: 3473,  84%, CS: 1000, SP: 4095, 100%
PWM: MV: 3553,  86%, CS: 1000, SP: 4095, 100%
PWM: MV: 3618,  88%, CS: 1000, SP: 4095, 100%
PWM: MV: 3671,  89%, CS:    0, SP: 1023,  25%
PWM: MV: 2995,  73%, CS:    0, SP: 1023,  25%
PWM: MV: 2451,  59%, CS:    0, SP: 1023,  25%
PWM: MV: 1999,  48%, CS:    0, SP: 1023,  25%
PWM: MV: 1635,  39%, CS:    0, SP: 1023,  25%
PWM: MV: 1332,  32%, CS:    0, SP: 1023,  25%
PWM: MV: 1087,  26%, CS:    0, SP: 1023,  25%
PWM: MV:  886,  21%, CS:    0, SP:    0,   0%
PWM: MV:  722,  17%, CS:    0, SP:    0,   0%
PWM: MV:  588,  14%, CS:    0, SP:    0,   0%
PWM: MV:  475,  11%, CS:    0, SP:    0,   0%
PWM: MV:  386,   9%, CS:    0, SP:    0,   0%
PWM: MV:  310,   7%, CS:    0, SP:    0,   0%
PWM: MV:  247,   6%, CS:    0, SP:    0,   0%
PWM: MV:  198,   4%, CS:    0, SP:    0,   0%
PWM: MV:  155,   3%, CS:    0, SP:    0,   0%
PWM: MV:  121,   2%, CS:    0, SP:    0,   0%
```

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
