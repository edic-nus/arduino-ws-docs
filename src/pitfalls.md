# Common pitfalls

Anything can go wrong when working on a project, and Arduino's are no exception. This page is a compilation of common problems you may encounter on your Arduino/MCU journey, with possible fixes for them! 

> Nothing is working! 

Double check your connections. Often, a wire is missing somewhere or isn't fully plugged in.

> The Arduino keeps turning off and on 

The Arduino is most probably providing more current than it can handle. It turning off is a safety feature. Try and find out what component in your design could be drawing so much current. 

> I can't see any message from the Arduino over Serial 

Check if the bit rate set in the code matches that set in the Serial Monitor. Sometimes, bit rate is reffered to as baud rate. If you're using an external USB-TTL converter, check the max bit rate supported by it. 

> Two motors are given the same signal in code but one spins faster than the other

The motors, while fancy, are not perfect. Variances in resistances here and there can cause one motor to spin faster than the other. This is perfectly normal. "Calibrate" your motors by adjusting the signal provided to them until they both spin in unison. 

