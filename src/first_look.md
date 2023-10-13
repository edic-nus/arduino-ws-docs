# main.ino
When you first load up your Arduino IDE, you wil be greeted with the following sight: 

```cpp
void setup() {

}

void loop() {

}
```

> TLDR: setup is for code which runs once, loop is for code which runs foreverrrr

setup() and loop() are functions, with the *scope* of the function (the code which will execute when the function is called) denoted by curly braces.

When looking at a C/C++ function, we can break it down as so: 
```cpp
return_value function_name(type1 input1, type2 input2) {
 /* code to be executed by function goes here */
}
```
where you can have as many inputs to a function as you want. Types are the data type of the function, such as: 
- int for integers
- floats for floating point numbers 
- bool for boolean values
- char for characters (like 'a', 'b')
- void for representing no type 

and the many derivations of these. For an exhaustive list, you should refer to the documentation provided by the C++ language. 
