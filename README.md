# Program-Nieliniowe-Uk-ady-Sterowania
Program z nieliniowych układów sterowania
#define X_STEP_PIN         54
#define X_DIR_PIN          55
#define X_ENABLE_PIN       38

#define Y_STEP_PIN         60
#define Y_DIR_PIN          61
#define Y_ENABLE_PIN       56

#define Z_STEP_PIN         46
#define Z_DIR_PIN          48
#define Z_ENABLE_PIN       62

#define X_MAX_PIN          2
#define Y_MAX_PIN          15
#define Z_MAX_PIN          19

String a;
int krok1=0;
int krok2=0;
int krok3=0;          
int kierunek1=0;
int kierunek2=0;
int kierunek3=0;
int flaga=0;


void setup() {
  // put your setup code here, to run once:
Serial.begin(115200);

 //SILNIK X
pinMode(X_ENABLE_PIN, OUTPUT);
pinMode(X_STEP_PIN, OUTPUT);
pinMode(X_DIR_PIN,OUTPUT);
pinMode(X_MAX_PIN,INPUT_PULLUP);
pinMode(Y_MAX_PIN,INPUT_PULLUP);
pinMode(Z_MAX_PIN,INPUT_PULLUP);
digitalWrite(X_DIR_PIN, HIGH);
digitalWrite(X_ENABLE_PIN, LOW);

//SILNIK Y
pinMode(Y_ENABLE_PIN, OUTPUT);
pinMode(Y_STEP_PIN, OUTPUT);
pinMode(Y_DIR_PIN,OUTPUT);
digitalWrite(Y_DIR_PIN, HIGH);
digitalWrite(Y_ENABLE_PIN, LOW);

//SILNIK Z
pinMode(Z_ENABLE_PIN, OUTPUT);
pinMode(Z_STEP_PIN, OUTPUT);
pinMode(Z_DIR_PIN,OUTPUT);
digitalWrite(Z_DIR_PIN, HIGH);
digitalWrite(Z_ENABLE_PIN, LOW);

}
int krok=0;
int kierunek=1;


void loop() {
  // put your main code here, to run repeatedly:

krok=krok+1;
/*
if(krok==500)
{
kierunek=!kierunek; 
digitalWrite(X_DIR_PIN, kierunek);
digitalWrite(Y_DIR_PIN, kierunek);
digitalWrite(Z_DIR_PIN, kierunek);  
krok=0;
Serial.println("\nZmiana Kierunku: ");
Serial.print(kierunek);
}


if(digitalRead(X_MAX_PIN)==0)
{
  digitalWrite(X_STEP_PIN,HIGH);
}
if(digitalRead(Y_MAX_PIN)==0)
{
  digitalWrite(Y_STEP_PIN,HIGH);
}
if(digitalRead(Z_MAX_PIN)==0)
{
  digitalWrite(Z_STEP_PIN,HIGH);
}
delay(1);
digitalWrite(X_STEP_PIN,LOW);
digitalWrite(Y_STEP_PIN,LOW);
digitalWrite(Z_STEP_PIN,LOW);
delay(1);
*/


if(((digitalRead(X_MAX_PIN)==0 && kierunek1==0) || kierunek1==1)                 && krok1>0)
{
  digitalWrite(X_STEP_PIN,HIGH);
  krok1--;
}
delay(1);
digitalWrite(X_STEP_PIN,LOW);
delay(1);

if(((digitalRead(Y_MAX_PIN)==0 && kierunek2==0) || kierunek2==1) && krok2>0)
{
  digitalWrite(Y_STEP_PIN,HIGH);
  krok2--;
}
delay(1);
digitalWrite(Y_STEP_PIN,LOW);
delay(1);

if(((digitalRead(Z_MAX_PIN)==0 && kierunek3==0) || kierunek3==1) && krok3>0)
{
  digitalWrite(Z_STEP_PIN,HIGH);
  krok3--;
}
delay(1);
digitalWrite(Z_STEP_PIN,LOW);
delay(1);

while(Serial.available()>0)
{
 a = Serial.readStringUntil('\n');
 sscanf(a.c_str(),"a %d b %d c %d",&krok1, &krok2, &krok3);
 flaga =1;
if(krok1<0)
{
 kierunek1=1;
 digitalWrite(X_DIR_PIN,kierunek1);
  krok1=-krok1;

}
else
{
 kierunek1=0;
 digitalWrite(X_DIR_PIN,kierunek1);
}

if(krok2<0)
{
 kierunek2=1;
 digitalWrite(Y_DIR_PIN,kierunek2);
  krok2=-krok2;

}
else
{
 kierunek2=0;
 digitalWrite(Y_DIR_PIN,kierunek2);
}

if(krok3<0)
{
 kierunek3=1;
 digitalWrite(Z_DIR_PIN,kierunek3);
  krok3=-krok3;

}
else
{
 kierunek3=0;
 digitalWrite(Z_DIR_PIN,kierunek3);


}
/*
 Serial.println("\nA: ");
 Serial.println(krok1);
  Serial.println("\nB: ");
 Serial.println(krok2);
  Serial.println("\nC: ");
 Serial.println(krok3);
 */
 
}

if (krok1 == 0 && krok2 == 0 && krok3 == 0 && flaga == 1)
{
  Serial.println("ok");
  flaga = 0;
}

}
