1번
1. 스마트폰에서 와이파이로 데이터를 서버로 보내고, 서버는 시리얼로 아두이노의 led를 제어하는 창의 작품을 만들 수 있게 된다.
2. 팀 과제로 팀원들고 협업하여 iot 기기를 설계하고 제작하여 시연하는 시스템을 제작하고 발표할 수 있게 된다.
3. 급변하는 시대에 공학의 즐거움과 미래의 전망에 대해서 친구들과 말할 수 있게 된다.
4. 아두이노를 활용하여 밝기값 조도를 읽고, 전등을 점멸하는 시스템을 구현하고 확장 응용할 수 있게 된다.
5. 주제와 관련된 논문과 특허를 검색하여 자료를 찾고 참고하여 iot 시스템을 제작하고 보고서를 작성할 수 있게 된다.

2번
먼저  스마티폰으로 집의 전등을 켜고 끄는 시스템을 제작하려면 시스템을 먼저 설계해야한다.
요구사항이나 릴레이 선택이나 무선 통신 기술 선택과 같은 이러한 일들을 끝내고 나면 제작과정에 돌입하는데 먼저 무선 통신 모듈을 연결한다.
예를 들면 와이파이가 있다. 해당 모듈을 스마트폰과 통신할 수 있도록 설정하고 릴레이 모듈을 전원에 연결하고 전등과도 연결하여 릴레이를 통해 
전등을 제어할 수 있도록 한다. 그 다음 스마트폰 앱과 시스템을 연동하여 스마트폰으로 앱으로 명령을 전송하면 무선 통신을 거쳐 시스템이 해당
명령을 받아 릴레이를 제어하여 전등을 켜거나 끈다.

아두이노 코드

int sw = 13;

void setup() {
  pinMode(sw, INPUT_PULLUP);
  Serial.begin(9600);
}
void loop() {
  int switcha = digitalRead(sw);
  if (switcha == LOW) {
    Serial.println('1');
  } else {
    Serial.println('0');
  }
  delay(1000);
}

프로세싱 코드
import processing.serial.*;
Serial p;
int sw; 
void setup() {
  size(400, 400);
  p = new Serial(this, "COM3", 9600);
}
void draw() {
  if (p.available() > 0) {
    sw = p.read(); 
    if (sw == '1') {
      background(0, 255, 0); 
    }
    if (sw == '0') {
      background(0); 
    }
  }
}

4번
![image](https://github.com/leejy04/Engineering/assets/145010514/085e858e-6dbd-457b-8f48-d5251565947c)

앱 인벤터를 열심히 만져봤지만 앱 프로세싱 코드 짜보기도 전에 실패했습니다.


5번
아두이노 코드
int ledPin = 7;
void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}
void loop() {
  if (Serial.available() > 0) {
    char command = Serial.read();
    if (command == 'on') {
      digitalWrite(ledPin, HIGH);
    } else if (command == 'off') {
      digitalWrite(ledPin, LOW);
    }
  }
}
프로세싱 코드
import processing.net.*;
Client client;
int ledPin = 7;
void setup() {
  size(200, 200);
  client = new Client(this, "", 80);
}
void draw() {
  background(255);
  fill(0);
  textSize(24);
  textAlign(CENTER);
  text("LED 제어", width / 2, 50);
}
void mousePressed() {
  if (mouseX < width / 2) {
    client.write("on");
  } else {
    client.write("off");
  }
}
void keyPressed() {
  if (key == 'q') {
    client.stop();
    exit();
  }
}
