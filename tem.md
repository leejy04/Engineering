1. 아두이노 센서회로 작성
1![과제](https://github.com/leejy04/Engineering/assets/145010514/c7abe214-81df-4fdb-8d01-5b6551b9c0dc)


2![image](https://github.com/leejy04/Engineering/assets/145010514/9fae9129-c068-4ce1-88df-edefaefa0bd0)

아두이노 코드
void setup() {
  Serial.begin(9600);
}
double th(int v) {
  double t; // http://en.wikipedia.org/wiki/Thermistor
  t = log(((10240000/v) - 10000));
  t = 1 /(0.001129148 + (0.000234125*t) + (0.0000000876741*t*t*t));
  t = t - 273.15; // 화씨를 섭씨로 바꾸어줌
  return t;
}
void loop() {
  int a = analogRead(A0);
  Serial.println(th(a));
  delay(500);
}
시리얼 통신을 컴퓨터와 아두이노 데이터 송수신 속도를 9600으로 하고 값을 th를 이용해서 온도로 바꾼후 반복적으로 실행하여 0.5초 단위로 출력한다.

프로세싱 코드
import processing.serial.*;
Serial p;
void setup(){
  size(400,400);
  p = new Serial(this,"COM3",9600);
}
void draw(){
  if(p.available()>0){
    String m = p.readStringUntil('\n');
    if(m != null){
      print(m);
      background(0,255,0);
      textSize(128);
      text(m, 20, 250);
    }
  }
}
아두이노의 값을 전달받아서 초록색 화면에 온도를 출력하는 코드.
