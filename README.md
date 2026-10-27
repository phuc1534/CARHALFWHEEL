# CARHALFWHEEL - Xe Ba Bánh

![GitHub License](https://img.shields.io/github/license/phuc1534/CARHALFWHEEL)
![GitHub Release](https://img.shields.io/github/v/release/phuc1534/CARHALFWHEEL)

Đây là một cơ sở mã mẫu. - This is an example code base.

## Topic - Chủ đề 

<img src="thử%20xe%20ba%20bánh%20-%20nhanh%20-%20chậm/IMG_3069.jpeg" align="right" width="30%">

Đây là một ví dụ về việc thử xe ba bánh bằng động cơ
- Đầu tiên: xe sẽ tiến về phía trước nhanh dần đều
- Thứ 2: xe sẽ lùi về phía sau nhanh dần đều
- Thứ 3: xe sẽ quay bánh bên trái


## Code

This is the code:

```cpp
// Đây là một ví dụ về việc thử xe ba bánh bằng động cơ
// Đầu tiên: xe sẽ tiến về phía trước nhanh dần đều
// Thứ 2: xe sẽ lùi về phía sau nhanh dần đều
// Thứ 3: xe sẽ quay bánh bên trái
//
// Motortest T100 with PWM for Marie Curie School
// Connected to L298N H-Bridge
// 10 - IN1 - motor 1 speed (PWM)
// 11 - IN4 - motor 2 speed (PWM)
// 12 - IN2 - motor 1 direction
// 13 - IN3 - motor 2 direction

const int IN1 = 10;  // motor A, PWM
const int IN2 = 12;  // motor A, digital
const int IN3 = 13;  // motor B, digital
const int IN4 = 11;  // motor B, PWM

void setup() {
  pinMode(IN1, OUTPUT); pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT); pinMode(IN4, OUTPUT);
  Serial.begin(115200);
  Serial.println("Motortest v1.0 2026-10-16");
  delay(3000);
}

// speed: -255..255, positive = forward
void motorA(int speed) {
  int s = constrain(abs(speed), 0, 255);
  if (speed >= 0) {            // forward: IN2 low, PWM on IN1
    digitalWrite(IN2, HIGH);
    analogWrite(IN1, 255 - s);
  } else {                     // reverse: IN2 high, inverted PWM on IN1
    digitalWrite(IN2, LOW);
    analogWrite(IN1, s);
  }
}

void motorB(int speed) {
  int s = constrain(abs(speed), 0, 255);
  if (speed >= 0) {            // forward: IN3 high, inverted PWM on IN4
    digitalWrite(IN3, HIGH);
    analogWrite(IN4, 255 - s);
  } else {                     // reverse: IN3 low, PWM on IN4
    digitalWrite(IN3, LOW);
    analogWrite(IN4, s);
  }
}

void loop() {
  Serial.println("Forward ramp");
  for (int s = 0; s <= 255; s += 5) { motorA(s); motorB(s); delay(30); }
  for (int s = 255; s >= 0; s -= 5) { motorA(s); motorB(s); delay(30); }
  delay(1000);

  Serial.println("Backward ramp");
  for (int s = 0; s <= 255; s += 5) { motorA(-s); motorB(-s); delay(30); }
  for (int s = 255; s >= 0; s -= 5) { motorA(-s); motorB(-s); delay(30); }
  delay(1000);

  Serial.println("Forward ramp");
  for (int s = 0; s <= 255; s += 5) { motorA(s); delay(30); }
  for (int s = 255; s >= 0; s -= 5) { motorA(s); delay(30); }
  delay(1000);

  Serial.println("Forward ramp");
  for (int s = 0; s <= 255; s += 5) { motorB(s); delay(30); }
  for (int s = 255; s >= 0; s -= 5) { motorB(s); delay(30); }
  delay(1000);
}
```

Và hy vọng là các tương tác giờ đây đã bằng tiếng Việt. At least that’s what we hope for.
