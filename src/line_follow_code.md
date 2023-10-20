# Code 
## Configurations
At the top of the code, we first initialise a few constant parameters for our robot. This is so that we can easily change any pins or directions easily without having to dig through the code to find the specific spots for different robots.

```cpp 
//pins to be used 
const int L_LDR_PIN = A1;
const int R_LDR_PIN = A0;
const int L_MOTOR_DIR_PIN = 5;
const int R_MOTOR_DIR_PIN = 6;
const int L_MOTOR_SPD_PIN = 11;
const int R_MOTOR_SPD_PIN = 10;
//to flip direction, change from 0 to 1 and viceversa
const int LEFT_FORWARD = 0;
const int RIGHT_FORWARD = 1; 
```

Next, we have the calibration values. Due to differences in the light dependent resistor, the value where where a sensor is in the "white zone" might vary depending on the background, robot, and other factors. Motors are also not perfect, and one side might spin faster than the other. These values allow you to tune your robot so that it will detect the line and move in a straight line when intended.
Similar to above, this is declared at the top of the code so that these values will be easy to find.
```cpp
//calibration values, determine based on your robot
const int L_WHITE_THRESHOLD = 300;
const int R_WHITE_THRESHOLD = 300;
const int LEFT_SPEED  = 120;
const int RIGHT_SPEED = 120;
```

## Functions

We then declare functions to help us with controlling the robot. This makes it much easier to control the robot in the main part of the code (one line rather than 4!)
```cpp
//functions for controlling the robot
void turn_left(){
      digitalWrite(L_MOTOR_DIR_PIN, LEFT_BACKWARD);
      digitalWrite(R_MOTOR_DIR_PIN, RIGHT_FORWARD);
      int spd = abs((LEFT_BACKWARD) * 255)- LEFT_SPEED);
      analogWrite(L_MOTOR_SPD_PIN, spd);
      spd = abs((RIGHT_FORWARD)*255)- RIGHT_SPEED);
      analogWrite(R_MOTOR_SPD_PIN,spd);
}

void turn_right(){
      digitalWrite(L_MOTOR_DIR_PIN, LEFT_FORWARD);
      digitalWrite(R_MOTOR_DIR_PIN, RIGHT_BACKWARD);
      int spd = abs((LEFT_FORWARD*255)-LEFT_SPEED);
      analogWrite(L_MOTOR_SPD_PIN, spd);
      spd = abs((RIGHT_BACKWARD*255)-RIGHT_SPEED);
      analogWrite(R_MOTOR_SPD_PIN, spd);
}

void move_forward(){
      digitalWrite(L_MOTOR_DIR_PIN, LEFT_FORWARD);
      digitalWrite(R_MOTOR_DIR_PIN, RIGHT_FORWARD);
      int spd = abs((LEFT_FORWARD*255)-LEFT_SPEED);
      analogWrite(L_MOTOR_SPD_PIN, spd);
      spd = abs((RIGHT_FORWARD*255)-RIGHT_SPEED);
      analogWrite(R_MOTOR_SPD_PIN, spd);
}

void stop_robot(){
      digitalWrite(L_MOTOR_DIR_PIN, 0);
      digitalWrite(R_MOTOR_DIR_PIN, 0);
      analogWrite(L_MOTOR_SPD_PIN, 0);
      analogWrite(R_MOTOR_SPD_PIN, 0);
}
```

## Setup

We initialise the Serial port of the Arduino and the pins in this section. This part of the code only runs once every time the Arduino is reset or restarted.

```cpp
void setup() {
  //baudrate of 9600
  Serial.begin(9600);
  pinMode(L_LDR_PIN, INPUT);
  pinMode(R_LDR_PIN, INPUT); 
  pinMode(L_MOTOR_DIR_PIN, OUTPUT);
  pinMode(R_MOTOR_DIR_PIN, OUTPUT);
  pinMode(L_MOTOR_SPD_PIN, OUTPUT);
  pinMode(R_MOTOR_SPD_PIN, OUTPUT);
}
```

### If else

To implement logic in code, we use if and else statements to check for conditions. For the line following robot, our conditions will be tied closely to the values that we obtain from the LDR. 

In most programming languages including C++, the following operators can be used to compare two different variables:

| Operator | Description |  
| ----------- | ----------- |  
| A == B | Checks if A and B are equal |  
| A != B | Checks if A and B are NOT equal |  
| A >  B | Checks if A is more than B |  
| A <  B | Checks if A is less than B |  
| A >= B | Checks if A is more than or equals to B |  
| A <= B | Checks if A is less than or equals to B |    

In C, each if or else block needs to be surrounded by curly brackets. 
The general syntax for if statements in C++ is as follows:

```cpp
if (A == B){
  //code that runs if it is true
} else if (A < B) {
  //code that runs if A is not equals to B but A is less than B
} else {
  //code that runs otherwise, what condition is remaining?
}
```


For our line following robot, we need to check if each LDR is over a black line or in the white space. To do this, we can check the LDR value and compare it to what value it would be when it is over a white background.

```cpp
 int readingl, readingr;
  readingl = analogRead(L_LDR_PIN);
  readingr = analogRead(R_LDR_PIN);
  if (readingl <= L_WHITE_THRESHOLD){
  // do something
  }
  if (readingr <= R_WHITE_THRESHOLD) {
  //do another thing
  }
```

## Loop

This is the part of the code that runs continuously. Upon reaching the last delay(1000), it restarts back to the begging of the loop until the power to the Arduino is switched off.

The following is a basic loop which makes takes the LDR readings but doesn't do anything with them. The robot moves forward, stops, turns left, stops, turns right, stops, and the loop repeats.

```cpp
void loop() {
 int readingl, readingr;
  readingl = analogRead(L_LDR_PIN);
  readingr = analogRead(R_LDR_PIN);
  move_forward();
  delay(1000);
  turn_left();
  delay(1000);
  turn_right();
  delay(1000);
}
```



