# Wykrywacz dymu
________________________

O PROJEKCIE
W tym przykładzie odczytasz napięcie wyjścia czujnika, a gdy dym osiągnie określony poziom, wyda dźwięk i zapali się czerwona dioda LED.
Gdy napięcie wyjściowe spadnie poniżej tego poziomu, zapali się zielona dioda LED.

Potrzebne komponenty:
- arduino UNO;
- MQ-9 czujnik dymu;
- diody LED;
- buzzer;
- rezystory 221 0hm.
### (https://create.arduino.cc/projecthub)
 ![img](./Arduino_UNO_pinout_2_numery)
## Etap 1
```cpp
int czerwonaDioda = 12;
int zielonaDioda = 11;     //definicja portów 
int buzzer = 10;
int czujnikDymu = A5;
int wartoscProgowa = 400; //wartość progowa - jeśli stężenie gazów w powietrzy przekroczy ten próg to dioda zaświeci się na kolor czerwony i buzzer wyda dźwięk(można ją zmieniać)
void setup() {
  pinMode(czerwonaDioda, OUTPUT);
  pinMode(zielonaDioda, OUTPUT);
  pinMode(buzzer, OUTPUT);            //definicja wejść i wyjść
  pinMode(czujnikDymu, INPUT);
  Serial.begin(9600);
}

void loop() {
  int sensor = analogRead(czujnikDymu); //czujnik zczytuje zawartość gazów w powietrzu  

  Serial.print("Pin A0: ");
  Serial.println(sensor); //wyświetlenie na monitorze  portu szeregowego dla dodatkowego zobrazowania
  //stawiamy warunek, jeśli wartość gazów w powietrzu jest niższa niż nasza wartość podana na początku(sensorThres) to zaświeci się dioda zielona i buzzer nie wyda dźwięku,
  //natomiast jeśli przekroczy zaświeci się didoa czerwona i buzzer wyda dźwięk
  if (sensor > wartoscProgowa)
  {
    digitalWrite(czerwonaDioda, HIGH); //czerowna zapali się
    digitalWrite(zielonaDioda, LOW);   //zielona gaśnie
    tone(buzzer, 1000, 200);   //buzzer wyda dźwięk
  }
  else
  {
    digitalWrite(czerwonaDioda, LOW); //czerwona gaśnie
    digitalWrite(zielonaDioda, HIGH); //zielona zapali się
    noTone(buzzer);
  }
  delay(100);
}```
