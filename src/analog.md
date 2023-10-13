# Analog?

Sadly, the real world is very much analog. How does a MCU interface with such analog devices? 

## Pulse Width Modulation
Leveraging a concept known as **Pulse Width Modulation** or PWM. By turning a digital line on and off, the **average** voltage perceived at the end of the line changes. Using this, voltages between 0V and 5V can be achieved!

Generating a sine-wave from a digital signal using PWM: 
![PWM Sine](https://i.stack.imgur.com/bBNPA.gif)

PWM waveforms have 2 important characteristics:
- the frequency of the waveform
- the duty cycle

Frequency, just like in any **periodic** waveform, is the rate at which the wave repeats itself. A PWM signal running at 1 Hz will repeat itself every second. 

Duty cycle is **percentage of time** the signal stays 'high' in a *single period*.

An example from Wikipedia: 
![Duty Cycle](https://upload.wikimedia.org/wikipedia/commons/b/b8/Duty_Cycle_Examples.png)

A 1 Hz PWM signal with a duty cycle of 25% will have it's high portion be 0.25s, while its low portion will be 0.75s.

## PWM on Arduino

> Make sure the selected pins are capable of PWM!

```cpp
void setup() {
    pinmode(9, output);
}

void loop() {
    // you can pass in values from 0 to 255 to analogwrite
    // 8 bits -> 256 possible values
    analogwrite(9, 255);
}
```

## Reading analog values 

```cpp 
void setup() {
    Serial.begin(9600); 
}

void loop() {
    int analog_value = 0;

    analog_value = analogRead(A0); // read the value 
    Serial.println(analog_value); // print out the read value
}
```

> When using analog pins on the Arduino UNO, there is no need to set them up using pinMode. This is because these pins can **only function as input pins**. This isn't the case with all MCUs!
