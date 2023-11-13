## รูปภาพ
![image](https://github.com/64030301nam/Introduction-to-blynk/assets/115066329/38459e44-e72e-4cfe-8528-486345b9d309)
## CODE
```
#define BLYNK_TEMPLATE_ID           "TMPL6mvkPkIKH"
#define BLYNK_TEMPLATE_NAME         "Quickstart Template"
#define BLYNK_AUTH_TOKEN            "6XCdNty9nVl-YJZy1gB5Z5239gEvIzp3"

#define BLYNK_PRINT Serial

#include <WiFi.h>
#include <WiFiClient.h>
#include <BlynkSimpleEsp32.h>

#include "DHT.h"

#define DHTPIN 4 // ต่อ data <=====
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

#define LED_Pin 23 // ต่อ LED  <=====
#define LDR_Pin 39 // ต่อ LDR <====
#define Volume_Pin 34 // ต่อ Volume <====

char ssid[] = "NAM_2.4G";
char pass[] = "nam24122545";

BlynkTimer timer;

void myTimerEvent()
{
  float temp = dht.readTemperature();
  float humi = dht.readHumidity();
  int ldrValue = analogRead(LDR_Pin);
  int volumeValue = analogRead(Volume_Pin);
  if (isnan(temp) || isnan(humi)) {
    Serial.println("Failed to read from DHT sensor. Please check the wiring.");
  } else {
    Blynk.virtualWrite(V0, temp);
    Blynk.virtualWrite(V1, humi);
    Blynk.virtualWrite(V2, ldrValue);
    Blynk.virtualWrite(V3, volumeValue);
  }
}

int ledState = LOW;
BLYNK_WRITE(V4) {
  int value = param.asInt();
  if (value == 1) {
    ledState = HIGH;
  } else {
    ledState = LOW;
  }
  digitalWrite(LED_Pin, ledState);
}

void setup()
{
  Serial.begin(115200);
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);
  timer.setInterval(1000L, myTimerEvent);
  dht.begin();
  pinMode(LED_Pin, OUTPUT);
}

void loop()
{
  Blynk.run();
  timer.run();
}
```
## VDO
https://youtube.com/shorts/FKXrAnGtOnw?si=QX-PSUbmrAQXmx4s


