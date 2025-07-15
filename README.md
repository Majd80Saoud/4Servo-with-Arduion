# 4 Servo-with-Arduion

This project is built using Arduino Uno and 4 servo motors, designed to simulate basic motion and introduce simple humanoid movement logic. The servos first perform a sweep motion for 2 seconds, then hold a fixed position at 90°.

## Components Used

- Arduino Uno
- 4x SG90 Servo Motors
- Jumper wires

## Wiring Instructions

| Servo | Signal Pin | VCC (Red) | GND (Brown/Black) |
|-------|------------|-----------|-------------------|
| 1     | Pin 9      | 5V        | GND               |
| 2     | Pin 8      | 5V        | GND               |
| 3     | Pin 7      | 5V        | GND               |
| 4     | Pin 6      | 5V        | GND               |


## Algorithm for Humanoid Walking

1. Set all servos to neutral position (90 degrees)
2. Repeat the following steps to simulate a walking cycle:
    a. Move left leg forward (servo1 → 60)
    b. Move right leg backward (servo2 → 120)
    c. Lean body slightly forward (servo3 → 100), (servo4 → 80)
    d. Wait 500ms
    e. Return all servos to 90 degrees
    f. Move right leg forward (servo2 → 60)
    g. Move left leg backward (servo1 → 120)
    h. Lean body slightly forward (servo4 → 100), (servo3 → 80)
    i. Wait 500ms
    j. Return all servos to 90 degrees
3. Repeat loop to continue walking

   ## code
   #include <Servo.h>


Servo servo1;
Servo servo2;
Servo servo3;
Servo servo4;

int pos = 0;
unsigned long startTime;
bool sweeping = true;

void setup() {
  servo1.attach(9);  // السيرفو الأول
  servo2.attach(8);  // السيرفو الثاني
  servo3.attach(7);  // السيرفو الثالث
  servo4.attach(6);  // السيرفو الرابع

  startTime = millis(); // وقت بدء التشغيل
}

void loop() {
  if (sweeping) {
    unsigned long currentTime = millis();

    if (currentTime - startTime < 2000) {
    
      for (pos = 0; pos <= 180; pos += 1) {
        servo1.write(pos);
        servo2.write(pos);
        servo3.write(pos);
        servo4.write(pos);
        delay(15);
      }

      
      for (pos = 180; pos >= 0; pos -= 1) {
        servo1.write(pos);
        servo2.write(pos);
        servo3.write(pos);
        servo4.write(pos);
        delay(15);
      }
    } else {
     
      servo1.write(90);
      servo2.write(90);
      servo3.write(90);
      servo4.write(90);
      sweeping = false;
    }
  }
}
