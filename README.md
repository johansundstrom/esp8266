 # WEMOS D1 R2 - ESP8266

Nyttig info om ESP8266

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
* Från mobilen surfa in på 
* Läs kommentaren på rad 1-8 för koppling och användning

## Blynk.cc
Fullständig instruktion https://www.blynk.cc/getting-started/

Min instruktion...
1. Surfa till blynk.cc och skapa konto
2. Ladda ned, zippa upp och mapparna ```libraries``` och ```tool```
3. Ovanstående mappar kallar jag för <blynk library>
placera ```blynk library``` i PC) c:\Users\<user>\Arduino\library\<blynk library> MAC) HD/Users/<user>/Document/Arduino/libraries/<blynk library>
4. Ladda ned blynk-app för iPhone eller Android i telefonen
5. I Blynk-appen i telefonen Create New Project
6. Skriv Projektnamn
7. Välj Device WeMos D1
8. Välj WiFi som Connection type 
9. Create
10. Ett projekt är nu skapat och ett Auth Token sänds automatiskt till det epostkonto som är knutet till Blynkkontot
11. Klicka på + symbolen och ur Widget Box välj Button
12. Placera denna på arbetsytan i telefonen genom longpress
13. Markera utanför knappen men inom knappens yta för att komma in i Buttons Settings
14. Välj Output D9, 0, 1 i de tre rutorna
15. Välj också att kanppen ska vara en switch
16. Gå tillbaks till Projektytan
17. Gå till Arduino IDE och omstarta
18. Under File - Examples - (Examples from custom libraries) finns nu Blynk
19. Välj där ... - Blynk - BoardsWiFi - ESP8266_Standalone
20. Redigera rad 41, 45, och 46.
21. Uppladda
  
Klart
