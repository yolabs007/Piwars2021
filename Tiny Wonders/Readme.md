# Tiny Wonders - PiWars2021 - Up the Garden Path

### Click on this below link to see how the tiny robot follows the Line.
https://youtu.be/Q5xXFI_H1N4

#### ` Components Required`

Component name | Component | Component name | Component |
------------ | ------------- | ------------ | ------------- |
 Arduino Board | <img src="https://www.distrelec.biz/Web/WebShopImages/landscape_large/9-/01/arduino-a000066.jpg" width="200" height="120"> | Arduino Shield | <img src="https://www.electronicscomp.com/image/cache/catalog/l293d-motor-driver-shield-arduino-800x800.jpg" width="200" height="200">
IR sensors - 2no.s | <img src="https://5.imimg.com/data5/CY/LS/QT/SELLER-7726776/ir-sensor-500x500.jpg" width="200" height="200"> | Switch | <img src="https://sinolec.co.uk/1578-large_default/rocker-switch-miniature-13mm-19mm.jpg" width="200" height="200"> |
9V Battery | <img src="https://5.imimg.com/data5/WW/JT/PZ/SELLER-20589996/9v-battery-500x500.jpg" width="200" height="200"> | DC Barrel Jack | <img src="https://d3s11pzv7w3h1q.cloudfront.net/wp-content/uploads/CA-DC21-USB-3.jpg" width="200" height="200">
Li - Batteries - 2no.s | <img src="https://d1q4q7ketxgxfn.cloudfront.net/media/catalog/product/cache/312af16b4230f9639b105af4a9030f8d/1/9/193304_samsung_battery_25r_18650_001.png" width="200" height="200"> | Battery Holder | <img src="https://cdn3.volusion.com/btfzd.umflq/v/vspfiles/photos/AD519-2.jpg?v-cache=1570025583" width="200" height="200"> |
Motors - 2no.s | <img src="https://5.imimg.com/data5/YA/GD/PT/SELLER-28625428/n20-micro-gear-motor-500x500.jpg" width="200" height="200"> | Wheels - 2no.s | <img src="https://lankatronics.com/image/cache/catalog/Sub%20categories/wheel%20and%20accessories/D%20hole-43mm-2-550x550w.jpg" width="200" height="200">
 Vehicle Frame |<img src="https://sc01.alicdn.com/kf/HTB1vqosJVXXXXauXVXXq6xXFXXXa.jpg" width="200" height="150">| Caster Wheel | <img src="https://images-na.ssl-images-amazon.com/images/I/31UUIaIfIdL._SX342_.jpg" width="200" height="200"> |

![Arduino Board](https://www.distrelec.biz/Web/WebShopImages/landscape_large/0-/01/Arduino_UNO_WIFI_30117100-01.jpg)


#### `Testing of Arduino`

* Test the Arduino Board by using blinking an In-Built LED (Below code) 

```C++
/*
  This Code is written by Rahul Sharma for Yolabs. 
This is the  simplest code possible to blink in build LED  
Turns inbuild LED on and off at diff frequency to chk your arduino IDE, Arduino and cable is working
Note: please check the port in case you have error while uploadig 
 www.yolabs.in - 2020
  
*/

// the setup function runs once when you press reset or power the board

void setup()
{
  pinMode(13,OUTPUT);
  Serial.begin(9600);
}

void loop()
{
    digitalWrite(13, HIGH);
    
    Serial.println("I am High");
    delay(3000); // Wait for 1000 millisecond(s)
    digitalWrite(13, LOW);
    Serial.println("I am Low");
    delay(3000);
 
}


```

* Check the IR sensors with IR sensor test Code (Below one) first, then go with Line follower Code.

![IR Sensor](https://5.imimg.com/data5/WA/GS/MY-5726208/delta-plc-repair-service-500x500.jpg)

#### `Connections`


IR sensor | Arduino
------------ | -------------
OUT | Pin Number 7
VCC | 5V
GND | GND



#### `IR Sensor Testing code`

```C++

void setup() {
  pinMode(7,INPUT);    // Change this pin number to IR Sensor Connected pin
  Serial.begin(9600);
  pinMode(13,OUTPUT);   //Arduino In-Built LED pin
}

void loop() {
  
Serial.print("IRSensorip  ");
Serial.println(digitalRead(7));

if(digitalRead(7)==0)      // if IR sensor detects the bright color
{
  digitalWrite(13,HIGH);    // In- Built LED will Glow
  }
 else{
    digitalWrite(13,LOW);
    }

}

```

#### `Upload this code to Arduino after checking of Arduino & IR Sensors are working.`

 ```C++
 #include <AFMotor.h>

// Change these below Pins to connected pins of IR sensor

#define lefts A1 
#define rights A5 


AF_DCMotor motor1(1, MOTOR12_8KHZ);   // Here right side motor is connected to M1
AF_DCMotor motor2(2, MOTOR12_8KHZ);   // Here left side motor is connected to M4


void setup() {


  pinMode(lefts,INPUT);
  pinMode(rights,INPUT);

  Serial.begin(9600);
  
}

void loop(){
  //printing values of the sensors to the serial monitor
  Serial.println(digitalRead(lefts));
  Serial.println(digitalRead(rights));
  //line detected by both
  if(digitalRead(lefts)==0 && digitalRead(rights)==0){
    //FORWARD
    motor1.run(FORWARD);
    motor1.setSpeed(100);
    motor2.run(FORWARD);
    motor2.setSpeed(100);

  }
  //line detected by left sensor
  else if(digitalRead(lefts)==0 && digitalRead(rights)==1){
    //turn left
    motor1.run(FORWARD);
    motor1.setSpeed(125);
    motor2.run(BACKWARD);
    motor2.setSpeed(100);


  }
  //line detected by right sensor
  else if(digitalRead(lefts)==1 && digitalRead(rights)==0){;
    //turn left
    motor1.run(BACKWARD);
    motor1.setSpeed(100);
    motor2.run(FORWARD);
    motor2.setSpeed(125);


  }
  //line detected by none
  else if(digitalRead(lefts)==1 && digitalRead(rights)==1){
    //stop
    motor1.run(RELEASE);
    motor2.run(RELEASE);

  }
  
}
```


