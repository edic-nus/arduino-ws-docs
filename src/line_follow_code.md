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
      analogWrite(L_MOTOR_SPD_PIN, LEFT_SPEED);
      analogWrite(R_MOTOR_SPD_PIN, RIGHT_SPEED);
}

void turn_right(){
      digitalWrite(L_MOTOR_DIR_PIN, LEFT_FORWARD);
      digitalWrite(R_MOTOR_DIR_PIN, RIGHT_BACKWARD);
      analogWrite(L_MOTOR_SPD_PIN, LEFT_SPEED);
      analogWrite(R_MOTOR_SPD_PIN, RIGHT_SPEED);
}

void move_forward(){
      digitalWrite(L_MOTOR_DIR_PIN, LEFT_FORWARD);
      digitalWrite(R_MOTOR_DIR_PIN, RIGHT_FORWARD);
      analogWrite(L_MOTOR_SPD_PIN, LEFT_SPEED);
      analogWrite(R_MOTOR_SPD_PIN, RIGHT_SPEED);
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
  pinMode(LEFT_LDR, INPUT);
  pinMode(RIGHT_LDR, INPUT); 
  pinMode(LEFT_MOTOR_DIR, OUTPUT);
  pinMode(RIGHT_MOTOR_DIR, OUTPUT);
  pinMode(LEFT_MOTOR_SPEED, OUTPUT);
  pinMode(RIGHT_MOTOR_SPEED, OUTPUT);
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

The following is the actual implementation of the method discussed. Take some time to go over each line of the code. If you get lost, compare it to the diagrams in [Design](./line_follow_design.md).
```cpp
void loop() {
 int readingl, readingr;
  readingl = analogRead(L_LDR_PIN);
  readingr = analogRead(R_LDR_PIN);
  if (readingl <= WHITE_THRESHOLD){
    if (readingr <= WHITE_THRESHOLD){
      //both left and white LDRs are currently in the white
      //check what previous edge was
      if (previous_edge == left_edge){
        turn_right();
      } else if (previous_edge == right_edge){
        turn_left();
      }
    } else {
      //left side is in white, right side is in black  
      previous_edge = left_edge;
      move_forward();
    }
  } else if (readingr <= WHITE_THRESHOLD) {
      //left side is black, right side is white
      previous_edge = right_edge;
      move_forward();
  } else {
    //both left and right side is in black, checkpoint?
    move_forward();
  }
  delay(10);
}
```


