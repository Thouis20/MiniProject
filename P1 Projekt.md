# MiniProject
//detect can
#include <Wire.h>
#include <Zumo32U4.h>

//here we activate the sensors
Zumo32U4Motors motors;
Zumo32U4ProximitySensors proxSensors;
Zumo32U4ButtonA buttonA;





void setup() {
  Serial.begin(9600);
  proxSensors.initFrontSensor();


}

void detectType() {

  // Read the front proximity sensor and gets its left value (the
  // amount of reflectance detected while using the left LEDs)
  // and right value.



  int brightnessLevels[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
  int leftValue = proxSensors.countsFrontWithLeftLeds();
  int rightValue = proxSensors.countsFrontWithRightLeds();
  proxSensors.setBrightnessLevels(brightnessLevels, 10);

  proxSensors.read();



  Serial.println((String)leftValue + (String)rightValue);

  delay(100);

  //This is for the small container.
  if (leftValue <= 5 && leftValue >= 1 && rightValue  <= 5 && rightValue >= 1) {


    motors.setLeftSpeed(-50);
    motors.setRightSpeed(-50);

    delay(250);


    motors.setLeftSpeed(0);
    motors.setRightSpeed(0);

    //buttonA.waitForButton();


  }

//This is for the large container. 
  else if (leftValue <= 10 && leftValue >= 6 && rightValue  <= 10 && rightValue >= 6) {

    motors.setLeftSpeed(50);
    motors.setRightSpeed(50);

    delay(250);


    motors.setLeftSpeed(0);
    motors.setRightSpeed(0);

    // buttonA.waitForButton();

  }
}

void loop() {

  detectType();

}