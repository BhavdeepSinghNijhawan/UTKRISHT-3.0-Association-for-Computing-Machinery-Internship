<h1 align="center">UTKRISHT 3.0 ASSOCIATION FOR COMPUTING MACHINERY</h1>

Under the guidance of **Professor P. Mathur**, a report and case study related to **air quality index**. This **Arduino Tutorial** explain about how to make **air quality monitoring** and **alert system** using **MQ135 sensor** in **ppm**.

## COMPONENTS USED

- Arduino Board
- MQ135 sensor
- 16x2 LCD
- Potentiometer
- Resistor
- LED
- Buzzer
- Breadboard

## TECH STACK

### C

```
#include <LiquidCrystal.h>

const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
int buz = 8;
int led = 9;
const int aqsensor = A0;
int threshold = 250;
```

- Includes the `LiquidCrystal library` for `LCD control`.
- Defines the pins connected to the `LCD`, `buzzer`, `LED`, and `MQ135 sensor`.
- Initializes the threshold level for air quality.

```
void setup() {
  pinMode(buz, OUTPUT);
  pinMode(led, OUTPUT);
  pinMode(aqsensor, INPUT);

  Serial.begin(9600);

  lcd.clear();
  lcd.begin(16, 2);
}
```

- Sets the `buzzer` and `LED` as `outputs` and the `air quality sensor` as an `input`.
- Initializes `serial communication` at a `baud rate of 9600`.
- Clears and sets up the LCD.

```
void loop() {
  int ppm = analogRead(aqsensor);

  Serial.print("Air Quality: ");
  Serial.println(ppm);

  lcd.setCursor(0, 0);
  lcd.print("Air Quality: ");
  lcd.print(ppm);

  if (ppm > threshold) {
    lcd.setCursor(0, 1);
    lcd.print("AQ Level HIGH");
    Serial.println("AQ Level HIGH");
    tone(led, 1000, 200);
    digitalWrite(buz, HIGH);
  } else {
    digitalWrite(led, LOW);
    digitalWrite(buz, LOW);
    lcd.setCursor(0, 1);
    lcd.print("AQ Level Good");
    Serial.println("AQ Level Good");
  }

  delay(500);
}
```

- Reads the value from the `air quality sensor` and stores it in `ppm`.
- Prints the `air quality value` to the `serial monitor` and `LCD`.
- Checks if the air quality value exceeds the threshold.
  - If it does, displays a `high air quality level message`, `turns on the buzzer`, and `blinks the LED`.
  - If it doesn't, displays a `good air quality level message` and `turns off the buzzer` and `LED`.
- Delays the loop for `500 milliseconds`.

## CONTRIBUTORS

- Professor P. Mathur `(parijat.mathur@ipu.ac.in)`, University School of Information, Communication and Technology, Guru Gobind Singh Indraprastha University
- [Bhavdeep Singh Nijhawan](https://www.linkedin.com/in/bhavdeep-singh-nijhawan-739634280)
