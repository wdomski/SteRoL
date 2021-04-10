# Zadanie 3 - ex3

ADC, DAC i DMA

Przedstawione zadania dotyczą:
- wykorzystania przetwornika analogowo-cyfrowego,
- wykorzystania przetwornika cyfrowo-analogowego,
- wykorzystania kontrolera DMA,
- konfiguracji układu liczącego do współpracy z 
powyższymi peryferiami.

Podczas wykonywania ćwiczeń wykorzystaj instrukcje laboratoryjną:

W. Domski, Sterowniki robotów, Laboratorium – ADC, DAC i DMA, 
Przetwoniki analogowo–cyfrowe, cyfrowo–analogowe oraz bezpośredni 
dostęp do pamięci, 2017


Napięcie referencyjne dla przetwornika ADC wynosi +3.3V.

Numer kanału przetwornika ADC można odczytać za pomocą programu 
STM32CubeMX najeżdżając myszką na odpowiedni pin mikrokontrolera 
przypisany do danego złącza.

## Przetwornik analogowo-cyfrowy (ADC) - ex3_1

Napisz program, który odczyta napięcie na złączach ADC3 oraz ADC4.
Następnie wylicz współczynnik *k* (zdefiniowany niżej).

Zadanie należy zrealizować przy użyciu przerwać, to jest 
wykorzystując:
```C
HAL_ADC_Start_IT();
HAL_ADC_ConvCpltCallback();
```

W programie STM32CubeIDE ustaw liczbę konwersji na 2. 
W pierwszym banku (rank) ustaw konwersję dla kanału podłączonego 
do złącza **ADC3** natomiast drugi bank ustaw na konwersję 
dla kanału podłączonego do złącza **ADC4**.

Pamiętaj o włączeniu przerwań dla przetwornika ADC.

Upewnij się, że regularna konwersja w trybie skanowania 
została wybrana oraz, że przerwanie będzie generowane każdorazowo po 
zakończeniu pojedynczej konwersji.

Wykorzystaj programowe wyzwolenie startu pomiaru.

W funkcji zwrotnej wykorzystaj
```C
LL_ADC_REG_SetSequencerRanks(adc, rank, channel);
```
w celu zmiany aktualnie wybranego kanału, na którym 
wykonywana jest konwersja. 

Wypisz wykonane pomiary, odpowiednio na złączu ADC3 oraz 
ADC4 na standardowe wyjście. Wykorzystaj do tego celu 
funkcję **printf()** (pamiętaj o przekierowaniu standardowego 
wyjścia).

Po wykonaniu pomiarów określ współczynnik *k*, który zdefiniowany 
jest jako * k = R2 / R3 *.

Projekt nazwij jako *ex3_1*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

## Przetwornik cyfrowo-analogowy (DAC) - ex3_2

Napisz program, który będzie sterował jasnością diody 
LED podłączonej do złącza **LED_ON_BOARD**. 

Skonfiguruj pin mikrokontrolera jako wyjście analogowe.

Rozdzielczość przetwornika DAC można wybrać 
jako dowolną, bądź wskazaną na zajęciach.

Napisz program, który cyklicznie będzie zmieniał napięcie 
generowane na złączu LED_ON_BOARD.

Napięcia powinny być generowane cyklicznie w następującej 
kolejności: 0.0, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.3V. 
Przelicz wartości napięcia na wartość jaką należy 
zapisać do rejestru danych przetwornika DAC.

Nowa wartość generowanego napięcia powinna zmieniać 
się cyklicznie co 2 sekundy.

Zaobserwuj działanie programu na podglądzie wideo.

**Wykorzystaj programowe wyzwalanie zapisywania **
**przeliczonego poziomu napięcia do rejestru danych **
**peryferium DAC.**

Wykorzystaj funkcje takie jak
```C
HAL_DAC_Start();
HAL_DAC_SetValue();
```

Projekt nazwij jako *ex3_2*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

## Przetwornik cyfrowo-analogowy (DAC) z licznikiem - ex3_3

Napisz program, który będzie sterował jasnością diody 
LED podłączonej do złącza **LED_ON_BOARD**. 

Skonfiguruj pin mikrokontrolera jako wyjście analogowe.

Rozdzielczość przetwornika DAC można wybrać 
jako dowolną, bądź wskazaną na zajęciach.

Napisz program, który cyklicznie będzie zmieniał napięcie 
generowane na złączu **LED_ON_BOARD**.

Napięcia powinny być generowane cyklicznie w następującej 
kolejności: 0.0, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.3V. 
Przelicz wartości napięcia na wartość jaką należy 
zapisać do rejestru danych przetwornika DAC.

Nowa wartość generowanego napięcia powinna zmieniać 
się cyklicznie co 2 sekundy.

Zaobserwuj działanie programu na podglądzie wideo.

**Wykorzystaj przerwanie od dowolnego licznika skonfigurowanego **
**w trybie generatora podstawy czasu do zapisywania **
**nowych wartości w rejestrze danych peryferium DAC.**

```C
HAL_TIM_Base_Start_IT();
HAL_TIM_PeriodElapsedCallback();
HAL_DAC_Start();
HAL_DAC_SetValue();
```

Projekt nazwij jako *ex3_3*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

## Przetwornik cyfrowo-analogowy (DAC) z kontrolerem DMA - ex3_4

Napisz program, który będzie sterował jasnością diody 
LED podłączonej do złącza **LED_ON_BOARD**. 

Skonfiguruj pin mikrokontrolera jako wyjście analogowe.

Rozdzielczość przetwornika DAC można wybrać 
jako dowolną, bądź wskazaną na zajęciach.

Napisz program, który cyklicznie będzie zmieniał napięcie 
generowane na złączu **LED_ON_BOARD**.

Napięcia powinny być generowane cyklicznie w następującej 
kolejności: 0.0, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.3V. 
Przelicz wartości napięcia na wartość jaką należy 
zapisać do rejestru danych przetwornika DAC.

Kolejne wartości, które będą przepisywane do rejestru danych 
DAC powinny znajdować się w tablicy, a ich kolejność 
powinna być taka jak określona w zadaniu.

Nowa wartość generowanego napięcia powinna zmieniać 
się cyklicznie co 2 sekundy.

Zaobserwuj działanie programu na podglądzie wideo.

Do realizacji zadania wykorzystaj kontroler DMA.
Transfer DMA ma być wyzwalany za pomocą przerwania 
pochodzącego od licznika.
Z każdym przepełnieniem licznika kontroler DMA będzie 
otrzymywać polecenie transferu danych (z pamięci do 
peryferium). Dzięki temu częstotliwość generowanego 
sygnału za pomocą przetwornika DAC na złączu **DAC1** 
będzie taka sama jak częstotliwość licznika. 

Pamiętaj aby skonfigurować kontroler DMA w trybie cyklicznym.
Dzięki temu po dojściu do końca tablicy kontroler DMA 
samodzielnie ustawi wskaźnik adresu na początek tablicy.

Weź również pod uwagę długość przepisywanego 
słowa. Powinna być ona zgodna z ustaloną rozdzielczością 
przetwornika DAC oraz typem danych przepisywanych wartości.

Wykorzystaj funkcje takie jak
```C
HAL_TIM_Base_Start_IT();
HAL_DAC_Start_DMA();
```

Projekt nazwij jako *ex3_4*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

## Przetwornik ADC i DAC - ex3_5

Napisz program, który sekwencyjnie będzie 
zadawał napięcia na złączu **DAC1**, a które następnie będą 
odczytywane na złączu **ADC1**.

Zarówno dla **ADC1** jak i **DAC1** wykorzystaj programowe 
wyzwalanie konwersji. Częstotliwość zadawania nowych wartości dla 
DAC to 2 Hz. Częstotliwość pomiarów na ADC to 1 Hz.

Nie wprowadzaj do programu opóźnień dłuższych niż 10 ms, to jest 
```C
HAL_Delay();
```
W tym celu wykorzystaj
```C
HAL_GetTick();
```
aby odczytać aktualną liczbę mikrosekund, które upłynęły od 
startu pracy oprogramowania na mikrokontrolerze.

Sekwencja napięć zadawanych na **DAC1** to: 
0, 0.5, 1.5, 2.5, 3.0, 3.3 V.

Przelicz wartości napięcia na wartości jakie należy 
zapisać do rejestru danych przetwornika DAC.

Rozdzielczość przetwornika DAC można wybrać 
jako dowolną, bądź wskazaną na zajęciach.

Wykorzystaj funkcje takie jak
```C
HAL_ADC_Start();
HAL_ADC_GetValue();
HAL_ADC_PollForConversion();

HAL_DAC_Start();
HAL_DAC_SetValue();
```

Projekt nazwij jako *ex3_5*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

## Przetwornik ADC wyzwalany licznikiem i DAC - ex3_6

Napisz program, który sekwencyjnie będzie 
zadawał napięcia na złączu **DAC1**, a które następnie będą 
odczytywane na złączu **ADC1**.

Wartości dla **DAC1** zadawaj programowo co 2 sekundy.

W przypadku **ADC1** wykorzystaj licznik skonfigurowany w trybie 
generatora podstawy czasu, a jego przerwanie podłącz 
jako wyzwalacz do peryferium ADC. 
Częstotliwość licznika ustaw na 2 Hz i z taką samą 
częstotliwością wypisuj pomiary na interfejs szeregowy przy 
wykorzystaniu funkcji printf().

Sekwencja napięć zadawanych na **DAC1** to: 
0, 0.5, 1.5, 2.5, 3.0, 3.3 V.

Przelicz wartości napięcia na wartość jaką należy 
zapisać do rejestru danych przetwornika DAC.

Rozdzielczość przetwornika DAC można wybrać 
jako dowolną, bądź wskazaną na zajęciach.

Wykorzystaj funkcje takie jak
```C
HAL_TIM_Base_Start_IT();

HAL_ADC_Start_IT();
HAL_ADC_GetValue();
HAL_ADC_ConvCpltCallback();

HAL_DAC_Start();
HAL_DAC_SetValue();
```

Projekt nazwij jako *ex3_6*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.

## Przetwornik ADC, DAC i DMA z licznikami - ex3_7

Napisz program, który sekwencyjnie będzie 
zadawał napięcia na złączu **DAC1**, a które następnie będą 
odczytywane na złączu **ADC1**.

Wykorzystaj dwa liczniki w trybie generatora podstawy 
czasu. Pierwszy licznik (dla DAC) będzie działał z częstotliwością 
0.5 Hz, natomiast drugi (dla ADC) z częstotliwością 2 Hz.

Skonfiguruj kanał DMA zarówno dla ADC jak i DAC. 
Pamiętaj o włączeniu konwersji dla DMA oraz wybraniu odpowiedniego 
wyzwalacza (sygnał z licznika). Oba kanały DMA powinny być 
skonfigurowane w trybie cyklicznym.
Dzięki temu w przypadku peryferium ADC można bezpośrednio sięgać po 
dane, które będą automatycznie aktualizowane przez kontroler DMA 
pod stałym wskazanym adresem w pamięci.

Sekwencja napięć zadawanych na **DAC1** to: 
0, 0.5, 1.5, 2.5, 3.0, 3.3 V.
Przelicz wartości napięcia na wartość jaką należy 
zapisać do rejestru danych przetwornika DAC.
Zapisz te dane w formie tablicy w celu właściwej 
konfiguracji kontrolera DMA.

Wypisuj na interfejs szeregowy zmierzone napięcie na złączu 
**ADC1** z częstotliwością pracy licznika przypisanego do 
peryferium ADC.

Rozdzielczość przetwornika DAC można wybrać 
jako dowolną, bądź wskazaną na zajęciach.

Wykorzystaj funkcje takie jak
```C
HAL_TIM_Base_Start_IT();

HAL_ADC_Start_DMA();

HAL_DAC_Start_DMA();
```
oraz odpowiednie funkcje zwrotne.

Projekt nazwij jako *ex3_7*.
Po wykonaniu zadania usuń katalog *Debug* z projektu, spakuj 
jako archiwum zip lub 7zip oraz wyślij na eportal.
