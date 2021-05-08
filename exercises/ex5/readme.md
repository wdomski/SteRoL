# Zadanie 5 - ex5

Obsługa modułów pomiarowych z interfejsem SPI i I2C

Przedstawione zadania dotyczą implementacji 
komunikacji z wykorzystaniem interfejsów I2C oraz SPI.
W szczególności dotyczą one:
- konfiguracji interfejsu SPI oraz I2C,
- czytanie dokumentacji technicznej oraz not katalogowych,
- weryfikacji poprawności połączenia z urządzeniem,
- konfiguracji zewnętrznego urządzenia,
- odczytu danych pomiarowych,
- sterowanie pracą zewnętrznego urządzenia.

Podczas wykonywania ćwiczeń wykorzystaj instrukcje laboratoryjne:

W. Domski, Sterowniki robotów, Laboratorium – SPI i I2C, 
Interfejsy komunikacyjne w praktycznym wykorzystaniu, 2018

W trakcie laboratorium każdy otrzyma indywidualne zadane 
do realizacji, które będzie wykorzystywać komunikację 
SPI i I2C. 

Przykład:

Wykorzystaj czujnik ADXL345, 
który pozwala na pomiar przyspieszenia liniowego i odczytaj 
owe przyspieszenie w 3 osiach, a następnie wyraź je w 
jednostce przyspieszenia ziemskiego *g*. 
Czujnik ten konfiguruje się za pośrednictwem interfejsu 
SPI, a może być skonfigurowany w trybie 4-wire lub 3-wire.
Wykorzystaj konfigurację 3-wire.

## Dostępne moduły i czujniki

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

- SPI_SCK - linia sygnałowa, 
- SPI_MISO - linia Master-Input Slave-Output, 
- SPI_MOSI - linia Master-Output Slave Input, 
- SPI_CS1 - chip select dla pierwszego układu, 
- SPI-CS1-ADXL345 - oznacza, że układ ADXL345 może zostać 
wybrany za pośrednictwem złącza SPI_CS1.

Wykorzystywane złącza pozwalają na określenie w jakiej konfiguracji 
należy ustawić interfejs SPI.

## Interfejs I2C

W odróżnieniu do interfejsu SPI konfiguracja złącz jest 
uproszczona. Wykorzystywane są zawsze dwie linie:
- I2C_SCL - linia sygnałowa,
- I2C_SDA - linia danych,
- I2C-MPU6050 - oznacza, że do interfejsu I2C został podłączony 
układ MPU6050.

# Odczyt danych z modułu zewnętrznego - ex5_1

W przypadku implementacji komunikacji z urządzeniem 
wykorzystującym interfejs SPI należy:

- zapoznać się z notą katalogową urządzenia (oraz modułu),
- ustalić konfigurację interfejsu SPI (Full-Duplex, Half-Duplex, ...),
- ustalić maksymalną częstotliwość taktowania linii sygnałowej,
- analizując diagramy komunikacji wskazać polaryzację dla linii sygnałowej,
- analizując diagramy komunikacji wskazać fazę dla linii sygnałowej,
- określić rozmiar przesyłanego słowa,
- określić kolejność bitów w przesyłanym słowie,
- zidentyfikować jeden z rejestrów, który zawiera  
określone dane i zweryfikować poprawność komunikacji (jeśli to możliwe),
- zaimplementować konfigurację urządzenia (jeśli to możliwe),
- zaimplementować odczyt danych,
- dokonać konwersji zmierzonych wartości,
- wypisać dane na standardowe wyjście.

Podczas komunikacji z wykorzystaniem interfejsu SPI 
należy pamiętać o odpowiednim ustaleniu stanów wszystkich 
złączy *chip-select*.

W przypadku implementacji komunikacji z urządzeniem 
wykorzystującym interfejs I2C należy:

- zapoznać się z notą katalogową urządzenia (oraz modułu),
- ustalić konfigurację maksymalną częstotliwość pracy 
interfejsu I2C,
- ustalić adres urządzenia,
- dokonać konwersji adresu (jeśli to konieczne),
- zidentyfikować jeden z rejestrów, który zawiera  
określone dane i zweryfikować poprawność komunikacji (jeśli to możliwe),
- zaimplementować konfigurację urządzenia (jeśli to możliwe),
- zaimplementować odczyt danych,
- dokonać konwersji zmierzonych wartości,
- wypisać dane na standardowe wyjście.

## Przydatne funkcje

Zapis oraz odczyt za pośrednictwem SPI:
```C
HAL_SPI_Transmit();
HAL_SPI_Receive();
```

Włączenie wyłączenie interfejsu SPI. Przydatne podczas 
wymuszenia generowania sygnału zegarowego:
```C
__HAL_SPI_ENABLE();
__HAL_SPI_DISABLE();
```

Jednoczesna transmisja oraz odbiór danych dla SPI. 
Przydatne podczas komunikacji w trybie Full-Duplex:
```C
HAL_SPI_TransmitReceive();
```

Funkcje do wysyłania i odbierania danych (I2C):
```C
HAL_I2C_Master_Transmit();
HAL_I2C_Master_Receive();
```

Funkcje do wysyłania i odbierania danych z dodatkowym 
adresowaniem (I2C). Przydatne podczas komunikacji 
z urządzeniem posiadającym pamięć:
```C
HAL_I2C_Mem_Write();
HAL_I2C_Mem_Read();
```

Sprawdzenie gotowości urządzenia (I2C):
```C
HAL_I2C_IsDeviceReady();
```
