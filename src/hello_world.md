# Hello, World!

When you connect your Arduino to your computer, one of the first things you can do to make sure everything is "working" is to send a message from your Arduino to your computer. We can do this via serial, a type of communication protocol where bits are transferred one after another to the end of the line. For a brief introduction to the protocol, check [this](https://edic-nus.github.io/elec-mech-systems-docs/signal_lines.html#serial) out.

```cpp
void setup() {
    Serial.begin(9600); // initialize the communication
}

void loop() {
    Serial.println("Hello, World!"); // send message over serial
    delay(1000); // delay by 1000 milliseconds
}
```

Let's dive a bit deeper into the code. 

```cpp
    Serial.begin(9600); // initialize the communication
```

9600 represents the rate at which bits will be sent and received on, in bits per second. 

The message we are sending over the line is "Hello, World!", but this is currently a *chain of characters*. Serial (and any digital protocol), only deals with bits. As such, there is an internal conversion converting these characters into bits. We call this **encoding**. 

An example of an encoding standard is ASCII: 

![ASCII Table](https://cdn.shopify.com/s/files/1/1014/5789/files/Standard-ASCII-Table_large.jpg?10669400161723642407)

```cpp 
    Serial.println("Hello, World!"); // send message over serial
```

Finally, println is one method to send data over serial; it's defining characteristic is that it automatically adds a 'newline' character at the end.A newline character, denoted by '\n', is equivalent to pressing Enter on the keyboard in a text editor.

