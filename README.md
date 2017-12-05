# WEMOS D1 R2 - ESP8266

Nyttig info om ESP8266
Läs mer på 
* https://tttapa.github.io/ESP8266/Chap01%20-%20ESP8266.html

## Spänning
* ESP8266 är en µController för 3.3V. Mer än 3.6V kan förstöra den
* Inbyggd Switching Power Supply: Input Voltage Range: 9V to 12V
* Output: 5V at 1A Max
* Strömkonsumtion: 10µA – 170mA

## GPIO
* ESP8266 har 17 GPIO pins (0-16), men endast 11 av dessa är åtkomliga. GPIO 6 - 11 används för att flash'a minnet.
* Imax från en GPIO är 12mA driv(Source) ~20mA jord (Sink), 16*12mA
* Alla I/O anslutningar är interrupt-, pwm-, I2C-, one-wirekompatibla, UTOM D0
```
pinMode(pin, INPUT);           // set pin to input
pinMode(pin, OUTPUT);          // set pin to output
```

### Interna pull-up/-down motstånd
* GPIO 0-15 har inbyggda pullup, samma som Arduio. GPIO16 har intern pull-down motstånd
* Atmega har 20k pullup, olika modeller ger 20k - 150k
```
pinMode(pin, INPUT_PULLUP);    // set pin to input
```

### Läsa från GPIO
```value = digitalRead(pin);```   // read the input pin
```digitalWrite(pin, value);```   // sets the LED to the button's value

### Fördefinierade constanter
* ```HIGH```     // Digital 1
* ```LOW```      // DIgiltal 0
* ```LED_BUILTIN```    // Definierar pin för inbyggd LED
* ```true```           // motsvarar 1 eller Sant
* ```false```          // motsvarar 0 eller falskt

### Biblioteket ESP8266WiFi.h
När vi inkluderar biblioteket ESP8266WiFi.h genom ```#include <ESP8266WiFi.h>``` så får vi med konstanter för varje pinout för varje board enligt i filen pins_arduino.h.

```c
#ifndef Pins_Arduino_h
#define Pins_Arduino_h

#include "../generic/common.h"

#define PIN_WIRE_SDA (4)
#define PIN_WIRE_SCL (5)

static const uint8_t SDA = PIN_WIRE_SDA;
static const uint8_t SCL = PIN_WIRE_SCL;


static const uint8_t LED_BUILTIN = 2;//new ESP-12E GPIO2
static const uint8_t BUILTIN_LED = 2;//new ESP-12E GPIO2

static const uint8_t D0   = 3;
static const uint8_t D1   = 1;
static const uint8_t D2   = 16;
static const uint8_t D3   = 5;
static const uint8_t D4   = 4;
static const uint8_t D5   = 14;
static const uint8_t D6   = 12;
static const uint8_t D7   = 13;
static const uint8_t D8   = 0;
static const uint8_t D9   = 2;
static const uint8_t D10  = 15;
static const uint8_t D11  = 13;
static const uint8_t D12  = 12;
static const uint8_t D13  = 14;
static const uint8_t D14  = 4;
static const uint8_t D15  = 5;
```

Ett exempel som läser en ingångs värde och skriver det på en utgång kan därför vara

```c
const int knapp = 2;    // D2 (GPIO16)
const int lampa = 3;    // D3 (GPIO5)

void setup() {
   pinMode(knapp, INPUT_PULLUP);    // switch mellan D0 och jord
   pinMode(lampa, OUTPUT);          // LED och 220R mellan D1 och jord
}

void loop() {
   if (digitalRead(knapp) == HIGH) {
      digitalWrite(lampa, HIGH);    // tänd LED
   } else {
      digitalWrite(lampa, LOW);     // släck LED
   }
}
```

## Interupt och GPIO
* ISP (Interupt Service Routine) 

```javascript
attachInterrupt(digitalPinToInterrupt(pin), ISR, mode);  //recommended
```

Parametrar

* interrupt: interuptport (int)
* pin: pinnummer (Arduino Due, Zero, MKR1000 only)
* ISR: ISR-anrop vid interrupt; functionen kan inte ta emot parametrar och returnerar ingenting
* mode: definierar var interrupt ska trigga på. Fyra konstanter är fördefinierade:
1. LOW triggar vid låg (endast låg)
2. CHANGE triggar vid förändringar (hög-låg och låg-hög)
3. RISING triggar vid förändring (låg-hög)
4. FALLING triggar vid förändring (hög-låg)
The Due, Zero and MKR1000 boards allows also:
5. HIGH LOW triggar vid hög (endast hög)


## Analog
* En analog ingång
* 1024 steg (10 bit)


## Minne
* Flash Memory: 4MB


## Ritning
* https://dl.dropboxusercontent.com/content_link/ZrUoAmhvhvmlgLXWsos4OseExF6Jscdi9IFrYGz2xGfnocBH7wqoB1cC3NhT009v/file


## Kompatibel
* Kompatibel med Arduino
* Kompatibel med nodemcu

## Styr via mobiltelefon
* Starta Arduino IDE
* Sätt upp Tools - Board - WeMos D1 R2 samt port och hastighet
* Hämta in exempelkod från File - Examples - (Examples for WeMos D1 Rs & Mini) ESP8266WiFi - WiFiWebServer
* Notera att koden kräver redigering på rad 12 och 13.
* Kompilera/länka och ladda upp till WEMOS D1 R2
* Från mobilen surfa in på <ip>/get/1
* Läs kommentaren på rad 1-8 för koppling och användning

## Blynk.cc
Fullständig instruktion https://www.blynk.cc/getting-started/

Min instruktion...
1. Surfa till blynk.cc och skapa konto
2. Ladda ned, zippa upp mapparna ```libraries``` och ```tool```
3. Ovanstående mappar kallar jag för _blynk library_. 
4. Placera ```blynk library``` i PC) c:\Users\{user}\Arduino\library\{blynk library} eller för MAC) HD/Users/{user}/Document/Arduino/libraries/{blynk library}
4. Ladda ned blynk-app för iPhone eller Android i telefonen
5. I Blynk-appen i telefonen Create New Project
6. Skriv Projektnamn
7. Välj Device WeMos D1
8. Välj WiFi som Connection type 
9. Create
10. Ett projekt är nu skapat och ett Auth Token sänds automatiskt till det epostkonto som är knutet till Blynkkontot
11. Klicka på + symbolen och ur Widget Box välj Button
12. Placera denna på arbetsytan i telefonen genom longpress
13. Markera utanför knappen men inom knappens yta för att komma in i Button Settings
14. Välj Output D9, 0, 1 i de tre rutorna
15. Välj också att knappen ska vara en switch
16. Gå tillbaks till Projektytan
17. Gå till Arduino IDE och omstarta så att de nya biblioteken läses in 
18. Under File - Examples - (Examples from custom libraries) finns nu Blynk
19. Välj där ... - Blynk - BoardsWiFi - ESP8266_Standalone
20. Redigera rad 41, 45, och 46.
21. Kompilera/Uppladda
  
Klart
