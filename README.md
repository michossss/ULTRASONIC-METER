# ULTRASONIC-METER
A METER THAT WORKS WITH ULTRASONİC DİSTANCE SENSOR

HOW İS İT WORK:

  OUR DİSTANCE METER İS WORK WİTH DİSTANCE SENSOR.<img width="766" height="524" alt="image" src="https://github.com/user-attachments/assets/6260773d-5a42-4200-b563-449c60c092df" />

FİRST THE DİSTANCE SENSOR MEASURE THE DİSTANCE BETWEEN ITSELF AND THE WALL.

AFTER THAT İT SENDS DATA TO ARDUNİO NANO WİTH TRİG AND ECHO PİNS.

THEN OUR NANO TRANSFORM OUR DİGİTS FROM THE ULTRASONİC SENSOR İNTO ENGLİSH FOR THE DİSPLAY SCREEN.

THİS İS THE CODE THAT İT USES TO TRANSFORM DİGİTS İNTO ENGLİSH.

#include <LiquidCrystal.h>

// Senin eski pinlerin: RS, E, D4, D5, D6, D7 -> (12, 11, 5, 4, 3, 2)
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

const int trigPin = 9;
const int echoPin = 8;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  // Ekranı her döngüde sıfırladığımız için setup'ı boş bırakabiliriz
}

void loop() {
  // Ekranı her seferinde tazeleyerek hataları ve kaymaları engelliyoruz
  lcd.begin(16, 2); 
  lcd.clear();
  lcd.noAutoscroll();

  long sure;
  float cm, metre;

  // Mesafe Ölçümü
  digitalWrite(trigPin, LOW);
  delayMicroseconds(5);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  sure = pulseIn(echoPin, HIGH);
  cm = sure / 58.2;
  metre = cm / 100.0;

  // --- EKRAN YAZDIRMA ---

  // 1. Sağ Üst Köşeye "Miço" Yazdır (11. sütun, 0. satır)
  lcd.setCursor(11, 0);
  lcd.print("MİCHO");

  // 2. Sol Üste CM Değerini Yazdır
  lcd.setCursor(0, 0);
  lcd.print("cm:");
  lcd.print(cm, 1);

  // 3. Alt Satıra Metre Değerini Yazdır
  lcd.setCursor(0, 1);
  lcd.print("Metre: ");
  lcd.print(metre, 2);
  lcd.print(" m");

  delay(800); // Ekranın okunabilir olması için bekleme
}

THİS SİGNAL İS THEN SENT TO OUR DİSPLAY, WİCH HAS AN I2C MODULE İNSTALLED. THE I2C MODULE İS VERY İMPORTANT BECAUSE THE PRODUCTS SİZE NECESSİTATES THE USE OF FEWER CABLES.
