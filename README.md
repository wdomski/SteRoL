# SteRoL

Sterowniki Robotów Laboratorium (SteRoL)

Repozytorium poświęcone kursowi Sterowniki Robotów na Politechnice Wrocławskiej.

## Strona kursu

Dodatkowe materiały do zadań, instrukcje laboratoryjne, noty katalogowe, itd. 
znajdują się na stronie kursu:

[edu.domski.pl](https://edu.domski.pl/kursy/sterowniki-robotow).

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

Poniżej przykład środowiska, na którym odbywa się praca zdalna.
Proszę zwrócić uwagę na diodę LED emitującą światło 
w kolorze czerwonym.

![Diody wyłączone](https://github.com/wdomski/SteRoL/blob/develop/images/boards_off.jpg "Płytki na stole wraz z wyłączonymi diodami")

![Diody włączone](https://github.com/wdomski/SteRoL/blob/develop/images/boards_on.jpg "Płytki na stole wraz z włączonymi diodami")

Do każdej płytki deweloperskiej podłączona jest płytka stykowa. 
Na dwie płytki deweloperskie przypada jedna płytka stykowana, 
na której znajdują się diody LED, symulatory oraz układy zewnętrzne.

Płytka stykowa znajduje się zawsze po lewej stronie zestawu startowego. 
Diody znajdujące się na górnej połowie płytki stykowej należą do zestawu, 
bezpośrednio obok, na górze. Diody i inne układy na płytce stykowej, 
które znajdują się w jej dolej części należą do dolnego zestawu deweloperskiego, 
co zostało pokazane na powyższych zdjęciach.

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
stanu. Numer portu można również wyliczyć przez zsumowanie 
liczby 3000 oraz numeru identyfikacyjnego **ID** płytki deweloperskiej,
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

## Przesyłanie zadań

Wykonane zadania należy przesłać na platformę eportal. Jednak uprzednio 
należy usunąć katalog *Debug* oraz zarchiwizować katalog projektu. 
Wspierane formaty to *.zip* oraz *.7z*.

# Materiały

W ramach kursu wykorzystywane są różne płytki ewaluacyjne. Można 
do nich zaliczyć:
- Nucleo-L476RG,
- Nucleo-L452RE,
- STM32L476G-Disco,
- STM32F429I-DISC1.

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

Ponadto dostępne są operacje, które umożliwiają:
- **Reset**, reset mikrokontrolera,
- **Halt** zatrzymanie działania rdzenia mikrokontrolera,
- **Resume** wznowienie działania rdzenia mikrokontrolera,
- **Restart OpenOCD** ponowne uruchomienie usługi związanej z 
debuggerem OpenOCD.

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
minicom --device /dev/ttyUrzadzenie0
```

Domyślna konfiguracja pozwala na otworzenie sesji o 
następujących parametrach (115200, 8N1):
- 115200 baud, prędkość transmisji,
- 8 bitów danych,
- N brak bitu parzystości,
- 1, jeden bit stopu.

Aby wyjść z programu *minicom* należy nacisnąć 
kombinację klawiszy **Ctrl+a**, a następnie wcisnąć przycisk **x**.

## Features

Do każdej z płytek przypisany jest indywidualny zestaw złącz (etykiet). 
Nie wszystkie płytki wyposażone są w ten sam zestaw złącz, przez 
co nie wszystkie możliwe konfiguracje są dostępne.

Przy wykorzystaniu schematu zestawu można określić jakie złącze 
jest przypisane, do którego portu mikrokontrolera. 
Przykładowo w liście złączy występuje wpis 
LED1, który jest przypisany do protu PB14 występującego 
w mikrokontrolerze.

# Dostępne moduły zewnętrzne

Każda z płytek posiada indywidualnie dobrany zestaw 
czujników. Lista dostępnych czujników może być odczytana 
za pośrednictwem serwera stanu. 

Poniżej znajduje się lista dostępnych czujników i modułów:

|Nazwa modułu|Nazwa układu|Interfejs komunikacyjny|Opis|
|-|-|-|-|
|OKY3248|ADXL345 |SPI|ADXL345 IIC / SPI Digital Gravity Sensor Accelerometer Sensor Module|
|LPS25HB|LPS25HB|SPI/I2C|Pressure/Altitude Sensor Carrier with Voltage Regulator|
|GY-521|MPU6050|I2C|3-Axis Acceleration Gyroscope 6DOF Module|
|GY-302|BH1750|I2C|Digital Light Intensity Sensor|
|KAmodHTS221|HTS221|SPI/I2C|KAmodHTS221 - moduł czujnika wilgotności / temperatury z układem HTS221|
|PmodALS (410-286)|ADC081S021|SPI|PmodALS (410-286) - moduł czujnika natężenia oświetlenia|
|PmodACL2 (410-255)|ADXL362|SPI|PmodACL2 (410-255) - moduł z akcelerometrem ADXL362|

## Interfejs SPI

W przypadku interfejsu Serial Peripheral Interface 
możliwe jest występowanie kilku różnych trybów konfiguracji, takich 
jak Full-Duplex, czy Half-Duplex. W zależności od 
konfiguracji znajdującej się na serwerze stanu możliwe jest 
określenie w jakiej konfiguracji występuje interfejs SPI.

Dostępne są następujące etykiety, które opisują wykorzystywane 
złącza, przykładowo:

- **SPI_SCK** - linia sygnałowa, 
- **SPI_MISO** - linia Master-Input Slave-Output, 
- **SPI_MOSI** - linia Master-Output Slave Input, 
- **SPI_CS1** - chip select dla pierwszego układu, 
- **SPI-CS1-ADXL345** - oznacza, że układ ADXL345 może zostać 
wybrany za pośrednictwem złącza **SPI_CS1**.

Wykorzystywane złącza pozwalają na określenie w jakiej konfiguracji 
należy ustawić interfejs SPI.

## Interfejs I2C

W odróżnieniu do interfejsu SPI konfiguracja złącz jest 
uproszczona. Wykorzystywane są zawsze dwie linie:
- **I2C_SCL** - linia sygnałowa,
- **I2C_SDA** - linia danych,
- **I2C-MPU6050** - oznacza, że do interfejsu I2C został podłączony 
układ MPU6050.

# Serwery

W ramach ćwiczeń laboratoryjnych jak i projektowych dostępne są 
trzy serwery:

- *aries*,
- *taurus*,
- *eridanus*.

Każdy z serwerów jest dostępny za pomocą przypisanego portu, 
na którym uruchomiona jest serwer usługi SSH.
W poniższej tabeli spisano numery portów SSH, do których można się 
połączyć.

|Serwer          |Numer portu|Numer zapasowego portu|Debugger|Serwer stanu|Serwer wideo|
|-|-|-|-|-|-|
|aries           | 2201      | 2301                 |x|x|x|
|taurus          | 2202      | 2302                 |x|x| |
|eridanus        | 2203      | 2303                 |x|x|x|

W przypadku, gdy usługa nie jest dostępna na podstawowym porcie 
należy skorzystać z zapasowego portu.

## Aries

Serwer wspiera usługi: OpenOCD, serwer stanu oraz serwer strumieniowania 
wideo.

## Taurus

Serwer wspiera usługi: OpenOCD oraz serwer stanu.

## Eridanus

Serwer wspiera usługi: OpenOCD, serwer stanu oraz serwer strumieniowania 
wideo.

# Sesja SSH

W celu pracy zdalnej z zestawami ewaluacyjnymi należy połączyć 
się za pomocą dowolnego klienta SSH, który umożliwia tunelowanie portów. 

## Linux

W przypadku systemu Linux należy posłużyć się komendą 

```bash
ssh LOGIN@DOMAIN -p 2201 -L 3001:localhost:3001 -L 8011:localhost:8081 -L 8012:localhost:8082
```

Powyższa komenda spowoduje, że zostanie otwarte połączenie z serwerem 
aries (ze względu na użyty numer portu 2201) oraz zostaną przekierowane trzy 
porty:
- port usługi OpenOCD (3001), 
- port usługi strumienia wideo dostępny na serwerze aries na porcie 8081. 
Usługa ta będzie dostępna lokalnie pod adresem localhost:8011,
- port usługi serwera stanu dostępny na serwerze aries na porcie 8082. 
Usługa ta będzie dostępna lokalnie pod adresem localhost:8012,

Proszę zwrócić uwagę, że numery portu dla serwera strumienia wideo 
oraz dla serwera stanu są różne w przypadku serwera oraz maszyny lokalnej, 
z której nawiązywane jest połączenie.

## Windows

Jeżeli do nawiązywania połączenia wykorzystywany jest system Windows, 
to wówczas przydatnym narzędziem może okazać się PuTTY. 
Konfiguracja za pomocą programu jest intuicyjna, natomiast poniżej została 
pokazana grafika w jaki sposób można ustawić tunelowanie portów.

![Konfiguracja PuTTY](https://github.com/wdomski/SteRoL/blob/develop/images/putty.png "Konfiguracja PuTTY")

# Rozwiązywanie problemów

## Brak możliwości połączenia się z serwerem

Po inicjalizacji sesji SSH nie pojawia się okno z zachętą odnośnie wpisania 
loginu lub pojawia się komunikat o przekroczeniu czas (**Connection timeout**).

Problem ten jest związany z czasowym nałożeniem blokady na 
połączenie z komputera. Nastąpiło to z powodu kilku nieudanych 
prób logowania (błędne hasło).

Zalecane jest kopiowanie hasła, a nie jego przepisywanie. 
Lepszym rozwiązaniem jest stworzenie pary kluczy SSH dzięki, 
którym można zautomatyzować proces logowania bez potrzeby 
wpisywania hasła.

## Problem uruchomienia sesji debuggera

Jeśli podczas rozpoczęcia pojawi się problem związany z uruchomieniem sesji debugowania 
wystąpi problem z połączeniem to należy sprawdzić:

1. Czy został poprawnie przekierowany port dla usługi OpenOCD?
2. Czy usługa OpenOCD jest aktywna? Reset usługi za pomocą serwera 
stanu może rozwiązać problem (pozycja **Restart OpenOCD**).

## Problem usunięcia pamięci podczas debugowania

Podczas uruchamiania sesji debugowania pojawia się błąd odnoszący 
się do próby usunięcia pamięci, który kończy się niepowodzeniem.
W tym celu za pomocą serwera statusu należy zresetować 
mikrokontroler (pozycja **Reset**).

## Urządzenie komunikacji szeregowej jest zajęte

W przypadku otrzymywania komunikatu **Device is busy** podczas 
próby uruchomienia programu *minicom* upewnij się, że 
nie ma innego procesu, który aktualnie wykorzystuje to urządzenie. 
Wykorzystaj do tego komendy **ps** oraz **kill**.







