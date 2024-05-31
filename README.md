int isikmiktar = 50;
int s = 500;
int s1 = 0;  
int s2 = 0;

#include "NewPing.h"
#include <FastLED.h>

#define TRIGGER_PIN 11
#define ECHO_PIN 12
#define MAX_DISTANCE 400  
#define sensor1 A0
#define sensor2 A1
#define NUM_LEDS 2
#define DATA_PIN 13
#define motor1 6
#define donus1 7
#define motor2 5
#define donus2 4
#define isik A6

NewPing sonar(TRIGGER_PIN, ECHO_PIN, MAX_DISTANCE);

float duration, distance;

CRGB leds[NUM_LEDS];

void setup() {
  pinMode(motor1, OUTPUT);pinMode(motor2, OUTPUT);pinMode(donus1, OUTPUT);pinMode(donus2, OUTPUT);
  Serial.begin(9600);
  FastLED.addLeds<WS2811, DATA_PIN, RGB>(leds, NUM_LEDS);
}

void loop() {

  delay(500);

  distance = sonar.ping_cm();
  
  if (analogRead(isik)<isikmiktar){leds[0]=led[1]=CRGB::White;FastLED.show();}
  if (distance <= 10){Serial.println("Çok Yakın");leds[1]=leds[0]=CRGB::Green;FastLED.show();digitalWrite(motor1,LOW);digitalWrite(motor2,LOW);digitalWrite(donus1,LOW);digitalWrite(donus1,LOW);}
  else {

    s1 = analogRead(sensor1);s2 = analogRead(sensor2);

    if (s1 > s && s2 > s) {Serial.println("düz git");digitalWrite(motor1,HIGH);digitalWrite(motor2,HIGH);digitalWrite(donus1,LOW);digitalWrite(donus1,LOW);}
    else if (s1 < s && s2 > s) {Serial.println("sağa git");digitalWrite(motor1,HIGH);digitalWrite(motor2,LOW);digitalWrite(donus1,LOW);digitalWrite(donus1,LOW);}
    else if (s1 > s && s2 < s) {Serial.println("sola git");digitalWrite(motor1,LOW);digitalWrite(motor2,HIGH);digitalWrite(donus1,LOW);digitalWrite(donus1,LOW);} 
    else if (s1 < s && s2 < s) {Serial.println("yoldan çıktı");digitalWrite(motor1,LOW);digitalWrite(motor2,LOW);digitalWrite(donus1,LOW);digitalWrite(donus1,LOW);
    
    }}}
