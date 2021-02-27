# SteRoL

Sterowniki Robotów Laboratorium (SteRoL)

Repozytorium poświęcone kursowi Sterowniki Robotów na Politechnice Wrocławskiej.

# Praca zdalna

Wszystkie zadania zostały przygotowane z myślą o pracy zdalnej. 
Każde z ćwiczeń zostało odpowiednio zmodyfikowane w taki sposób, 
aby wykorzystując bezpieczne połączenie SSH możliwe było ich kompletne 
zrealizowanie.

Adres serwera, do którego podłączone są płytki zostanie podany 
na zajęciach. Udostępnia on serwery debuggera OpenOCD dzięki 
czemu możliwa jest praca zdalna na udostępnionych płytkach 
deweloperskich. Dodatkowo, w zależności od serwera możliwe 
jest podłączenie do przekazu obrazu na żywo. W ten sposób można 
weryfikować pracę elementów podłączonych do zestawów startowych, 
którymi są np. diody LED.

## Przygotowanie do zajęć

W celu realizacji wszystkich zajęć laboratoryjnych należy mieć 
zainstalowane darmowe oprogramowanie *STM32CubeIDE* w wersji **1.4.0**. 
W przypadku wykorzystywania oprogramowania w nowszej wersji 
występują błędy, które uniemożliwiają zdalne podłączenie 
do debuggera OpenOCD.

Dodatkowo, wymagane jest posiadanie klienta SSH, który zapewni możliwość 
lokalnego przekierowania portów i dostęp do usług świadczonych 
przez serwer.

## Dostępne usługi

Każdy z serwerów oferuj następujące usługi:
- **serwer OpenOCD** do pracy zdalnej z zestawami startowymi, 
port usługi można uzyskać na podstawie odczytów z serwera 
stanu,
- **serwer stanu**, usługa webowa dostępna lokalnie na serwerze 
na porcie 8082. Dzięki niej możliwe jest sprawdzenie 
stanu serwera, podpiętych płytek deweloperskich i ich kondycji, 
a także ścieżek do portów szeregowych przypisanych do poszczególnych 
płytek deweloperskich,
- **serwer strumienia video** (usługa opcjonalna), pozwala 
na odbieranie strumienia wideo przydatnego podczas wizualnej 
weryfikacji przygotowanego oprogramowania. Usługa ta jest dostępna lokalnie 
porcie 8081.

# Zadania

Każdy z podkatalogów zawiera osobny zestaw ćwiczeń przewidziany w ramach 
ćwiczeń laboratoryjnych. Każde laboratorium składa się z kompozycji 
wybranych ćwiczeń.

Instrukcje laboratoryjne zawierające opis ćwiczeń wraz 
z wprowadzeniem do poruszanych zagadnień można znaleźć na 
stronie kursu 
[edu.domski.pl](https://edu.domski.pl/kursy/sterowniki-robotow/sr-laboratorium/).

Wszystkie zadania można znaleźć w katalogu **exercises**.

# Materiały

W ramach kursu wykorzystywane są różne płytki ewaluacyjne. Można 
do nich zaliczyć:
* Nucleo-L476RG,
* Nucleo-L452RE,
* STM32L476G-Disco.

W katalogu **boards** znajdują się poglądowe schematy, które przedstawiają 
w jaki sposób udostępnione płytki ewaluacyjne zostały połączone. 
Należy podkreślić, że nie wszystkie dostępne płytki posiadają 
wyprowadzone wszystkie złącza. Przykładowo, na schemacie płytki 
*Nucleo-L476RG* zaznaczone są złącza **LED1** oraz **LED2**. Jednakże 
w danym egzemplarzu płytki może być dostępne jedynie złącze **LED1**.
Z uwagi na to, każda płytka ma załączony indywidualny opis, które 
złącza w danym egzemplarzu są obecne, a tym samym możliwe do wykorzystania.

Opis dostępnych złącz znajduje się w statusie zwracanym 
przez **serwer stanu**.

## Opis złącz płytek ewaluacyjnych

- **LED_ON_BOARD**, 
wbudowana dioda, może działać jako 
wyjście GPIO, DAC oraz wyjście układu liczącego,
- **PUSH_BUTTON_ON_BOARD**
wbudowany fizyczny przycisk dla użytkownika, 
- **INT1**, **INT2**,
zewnętrzne wejście/wyjście, które podłączone jest do 
osobnej płytki ewaluacyjnej, (patrz *Opis połączeń między płytkami* 
*ewaluacyjnymi*), może służyć ono jako wejście przerwania 
zewnętrznego,
- **LED1**, **LED2**, 
diody LED (kolory mogą różnić się w zależności od egzemplarza),
- **GPIO1**, **GPIO2**, **GPIO3**, **GPIO4**, 
wejścia/wyjścia ogólnego przeznaczenia,
- **ADC1**, **ADC2**, **ADC3**, **ADC4**, **ADC5**,
wejścia analogowe,
- **DAC1**,
wyjście analogowe,
- **TIMER1**, **TIMER2**, **TIMER3**, **TIMER4**, **TIMER5**, 
**TIMER6**, **TIMER7**, 
wejścia/wyjścia układów liczących np. wejście input capture, 
wyjście generatora sygnału PWM,
- **I2C_SCL**, **I2C_SDA**, 
linie magistrali I2C,
- **SPI_SCK**, **SPI_MISO**, **SPI_MOSI**, 
linie magistrali SPI,
- **SPI_CS1**, **SPI_CS2**, **SPI_CS3**, **SPI_CS4**, 
linie aktywujące układy podłączone do magistrali SPI.

## Opis połączeń między płytkami ewaluacyjnymi

Wszystkie złącza opisane w *Opis złącz płytek ewaluacyjnych* 
są złączami lokalnymi, które mogą łączyć się jedynie z 
elementami i modułami znajdującymi się w obrębie zestawu 
startowego. Wyjątkiem są złącza **INT1** oraz **INT2**, 
które łączą złączą ze sobą dwa zestawy ewaluacyjne.
Dzięki temu możliwa jest interakcja pomiędzy dwoma różnymi 
zestawami ewaluacyjnymi.

Złącza **INT** łączone są parami. Oznacza to, że złącze 
**INT1** płytki np. o numerze 5 jest połączone z wyprowadzeniem 
**INT1** płytki np. o numerze 6. Aby określić, z którą 
płytką złącze **INT** jest połączone zastosowano następującą 
notację **INTx-id**, gdzie *x* to 1 lub 2, a *id* to 
numer zestawu ewaluacyjnego, do którego podłączone 
jest złącze. Przykładowo płytka o numerze 11 posiada 
w swoim opisie wpis **INT2-12**. Oznacza to, że 
złącze **INT2** płytki o numerze 11 jest połączone z 
złączem **INT2** płytki o numerze 12.

## Zewnętrzne moduły w zestawach ewaluacyjnych

Do wybranych zestawów ewaluacyjnych zostały podłączone zewnętrzne 
moduły, take jak np. akcelerometry, czujniki natężenia światła itp.
Każda płytka w swoim opisie posiada listę obsługiwanych czujników. 
Przykładowo:
- **I2C-BH1750**, oznacza, że dany zestaw posiada podłączony 
czujnik BH1750, który dostępny jest za pośrednictwem magistrali I2C,
- **SPI-CS1-MPL115A1**, oznacza, że dołączony został czujnik 
MPL115A1 do magistrali SPI. W celu jego aktywacji należy wykorzystać 
złącze **SPI_CS1** (*pozostałe złącza wybierające układy podłączone* 
*do magistrali SPI muszą być w stanie wysokim*).

# Status płytek

Status płytek można sprawdzić za pomocą serwera webowego.
Dostępny jest on na każdym z serwerów na porcie 8082.
Zwraca on następujące dane dla każdego z podłączonych 
modułów do minikomputera Raspberry Pi:
- **ID**, 
numer identyfikacyjny płytki deweloperskiej,
- **Port**, 
numer portu sieciowego serwera OpenOCD,
- **Status**,
dostępność danej płytki deweloperskiej,
- **Board**, 
rodzaj płytki deweloperskiej,
- **Serial**,
nazwa urządzenia szeregowego,
- **Features**,
zestaw dostępnych złącz oraz modułów podłączonych do  
zestawu startowego.

## ID

Unikalny numer identyfikacyjny zestawu startowego.
Za jego pomocą możliwe jest np. określenie numeru 
złącza przerwania zewnętrznego.

## Port

Numer portu sieciowego, pod którym dostępna 
jest usługa debuggera OpenOCD. Dostępność portu 
jest możliwa dzięki wykorzystaniu tunelowania 
za pośrednictwem tunelu SSH i lokalnego przekierowania 
portu.

## Status

Każde z urządzeń posiada swój status, który reprezentowany 
jest za pomocą emotikony. W przypadku, gdy 
piktogram reprezentuje uśmiechniętą twarz urządzenie 
działa poprawnie, można się do niego podłączyć 
za pośrednictwem usługi OpenOCD.

## Board

Określa jedną z dostępnych płytek ewaluacyjnych. 
Dzięki temu możliwe jest odpowiednie skonfigurowanie 
środowiska STM32CubeMX w celu wykonania ćwiczeń 
laboratoryjnych jak i projektowych.

## Serial

Ścieżka do urządzenia szeregowego, które umożliwia dwustrunną 
komunikację za pośrednictwem portu UART obecnego na 
płytce zestawu startowego. Podłączenie 
do portu szeregowego możliwe jest za pomocą oprogramowania 
minicom. Podłączenie do portu szeregowego może być zrealizowane 
w następujący sposób:

```bash
minicom --device /dev/ttyAMC0
```

Domyślna konfiguracja pozwala na otworzenie sesji o 
następujących parametrach (115200, 8N1):
- 115200 baud, prędkość transmisji,
- 8 bitów danych,
- N brak bitu parzystości,
- 1, jeden bit stopu.

## Features

TBD

# Dostępne moduły zewnętrzne

TBD



