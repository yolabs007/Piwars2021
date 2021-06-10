# Tiny Wonders - PiWars2021 - Up the Garden Path

#### ` Components Required`

Component name | Component | Component name | Component |
------------ | ------------- | ------------ | ------------- |
 Arduino Board | <img src="https://www.distrelec.biz/Web/WebShopImages/landscape_large/9-/01/arduino-a000066.jpg" width="200" height="120"> | Arduino Shield | <img src="https://www.electronicscomp.com/image/cache/catalog/l293d-motor-driver-shield-arduino-800x800.jpg" width="200" height="200">
IR sensors - 2no.s | <img src="https://5.imimg.com/data5/CY/LS/QT/SELLER-7726776/ir-sensor-500x500.jpg" width="200" height="200"> | Switch | <img src="https://sinolec.co.uk/1578-large_default/rocker-switch-miniature-13mm-19mm.jpg" width="200" height="200"> |
9V Battery | <img src="https://5.imimg.com/data5/WW/JT/PZ/SELLER-20589996/9v-battery-500x500.jpg" width="200" height="200"> | DC Barrel Jack | <img src="https://d3s11pzv7w3h1q.cloudfront.net/wp-content/uploads/CA-DC21-USB-3.jpg" width="200" height="200">
Li - Batteries - 2no.s | <img src="https://d1q4q7ketxgxfn.cloudfront.net/media/catalog/product/cache/312af16b4230f9639b105af4a9030f8d/1/9/193304_samsung_battery_25r_18650_001.png" width="200" height="200"> | Battery Holder | <img src="https://cdn3.volusion.com/btfzd.umflq/v/vspfiles/photos/AD519-2.jpg?v-cache=1570025583" width="200" height="200"> |
Motors - 2no.s | <img src="https://5.imimg.com/data5/YA/GD/PT/SELLER-28625428/n20-micro-gear-motor-500x500.jpg" width="200" height="200"> | Wheels - 2no.s | <img src="https://lankatronics.com/image/cache/catalog/Sub%20categories/wheel%20and%20accessories/D%20hole-43mm-2-550x550w.jpg" width="200" height="200">
 Vehicle Frame |<img src="https://sc01.alicdn.com/kf/HTB1vqosJVXXXXauXVXXq6xXFXXXa.jpg" width="200" height="150">| Caster Wheel | <img src="https://images-na.ssl-images-amazon.com/images/I/31UUIaIfIdL._SX342_.jpg" width="200" height="200"> |
 
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
