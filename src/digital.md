# Highs and lows

MCUs are digital devices; they communicate by 2 states, a 1 or a 0. Internally, the MCUs use "digital logic" via logic gates to to carry out all of their functions. 

The Arduino UNO is 5V logic level device. The UNO will register any input voltage as *high* if it is above ~3 volts and a *low* if the voltage is below ~1.5 volts. It can also "output" voltage, with a high output being ~5 volts and a low output being ~0 volts.

> Not all digital devices run at 5V logic level!

## Setting it up 

```cpp
void setup() {
    pinMode(9, INPUT); // set pin D9 as a digital input 
    pinMode(10, OUTPUT); // set pin D10 as a digital output 
}

void loop() {
    int digital_value = 0; // create an integer variable and set it to 0

    digital_value = digitalRead(9); // read the value from pin D9

    digitalWrite(10, digital_value); // write to pin D10
}
```

There are 3 main functions being used here: 
- pinMode(pin, type) where type is INPUT or OUTPUT
- digitalRead(pin) which gives either 1 or 0
- digitalWrite(pin, state) where state is either 1 or 0

Before you write your code, it is important to refer to a **pinout diagram** of the MCU you are using. 

For example, this is the pinout diagram of the Arduino UNO Rev3:
![UNO Pinout](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcontent.arduino.cc%2Fassets%2FPinout-UNOrev3_latest.png&f=1&nofb=1&ipt=71dcad4ec2287a44de678066ce457c84a9fb7c08312cebfab35d553ecfdae1c9&ipo=images)


