int M1=2;
int M2=3;
int M3=4;
int M4=5;
int motorLpwm=10;
int motorRpwm=11;

int motorSpeed=125;
int turn=40;

void setup() {
  Serial.begin(9600);
  Serial.flush();
  pinMode(M1,OUTPUT);
  pinMode(M2,OUTPUT);
  pinMode(M3,OUTPUT);
  pinMode(M4,OUTPUT);
  pinMode(motorLpwm,OUTPUT);
  pinMode(motorRpwm,OUTPUT);
}

void loop() {
  String input="";
  while(Serial.available()){
    input+=(char)Serial.read();
    Serial.println(input);
    delay(5);
  }
  
  if(input=="n"){
    stp();
  }
  else if(input=="F"){
    fwd();
  }
  else if(input=="R"){
    rev();
  }
  else if(input.indexOf("TL")>-1){
    lft();
  }
  else if(input.indexOf("TR")>-1){
    rght();
  }
  else if(input!=""){
    motorSpeed=input.toInt();
  }
}

void fwd(){
  analogWrite(motorLpwm,motorSpeed);
  analogWrite(motorRpwm,motorSpeed);
  digitalWrite(M1,1);
  digitalWrite(M2,0);
  digitalWrite(M3,1);
  digitalWrite(M4,0);
}

void rev(){
  analogWrite(motorLpwm,motorSpeed);
  analogWrite(motorRpwm,motorSpeed);
  digitalWrite(M1,0);
  digitalWrite(M2,1);
  digitalWrite(M3,0);
  digitalWrite(M4,1);
}

void lft(){
  analogWrite(motorLpwm,motorSpeed+turn);
  analogWrite(motorRpwm,motorSpeed+turn);
  digitalWrite(M1,1);
  digitalWrite(M2,0);
  digitalWrite(M3,0);
  digitalWrite(M4,1);
}

void rght(){
  analogWrite(motorLpwm,motorSpeed+turn);
  analogWrite(motorRpwm,motorSpeed+turn);
  digitalWrite(M1,0);
  digitalWrite(M2,1);
  digitalWrite(M3,1);
  digitalWrite(M4,0);
}

void stp(){
  analogWrite(motorLpwm,0);
  analogWrite(motorRpwm,0);
  digitalWrite(M1,0);
  digitalWrite(M2,0);
  digitalWrite(M3,0);
  digitalWrite(M4,0);
}
