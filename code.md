```C++
#include <Adafruit_NeoPixel.h>

const int soundSensorPin = A0;
const int ledPin = 6;
const int numLeds = 30;
Adafruit_NeoPixel strip = Adafruit_NeoPixel(numLeds, ledPin, NEO_GRB + NEO_KHZ800);

void setup() {
  Serial.begin(9600);
  strip.begin();
  strip.show();
}

void loop() {
  int soundValue = analogRead(soundSensorPin);

  Serial.print("Sound Volume: ");
  Serial.println(soundValue);

  if (soundValue > 100) {
    for (int brightness = 0; brightness <= 255; brightness += 5) {
      setStripColor(brightness, brightness, brightness);
      delay(30);
    }

    delay(5000);

    for (int brightness = 255; brightness >= 0; brightness -= 5) {
      setStripColor(brightness, brightness, brightness);
      delay(30);
    }
  } else {
    setStripColor(0, 0, 0);
  }

  delay(100);
}

void setStripColor(int red, int green, int blue) {
  for (int i = 0; i < numLeds; i++) {
    strip.setPixelColor(i, strip.Color(red, green, blue));
  }
  strip.show();
}
```
