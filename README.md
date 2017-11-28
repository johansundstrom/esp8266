# ESP8266
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


