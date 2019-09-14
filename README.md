Rebobinoide 
===========

![38461330_1378488775618051_1496400106671308800_n](https://user-images.githubusercontent.com/55008098/64902170-50f14a00-d657-11e9-9160-7df829bea61e.jpg)

The project consists of a few parts:
* A sequencer/drum machine program stored in the Arduino's flash memory.
* An array of four (4) AM-FM radios modified to individually switch on and off through triggering pulses produced by four (4) of Arduino's digital OUTPUT pins.
* A Yamaha DD-35 Drum Kit whose pads have been wired for external activation using opto-couplers- in addition to the factory triggering by striking - through a female VGA connector.

## The logic behind the sequencer

Each of the six (6) buttons connected to the Arduino's INPUT pins is programmed to trigger a sequence consisting of four (4) bars. Each bar is made up of four (4) beats, which in turn are divided into four (4) notes. 

Each note is defined by the `note()` function, which specifies the OUTPUT pin to activate, as well as how long it stays HIGH and LOW. All three parameters may have a value of 0, creating an empty note without going off beat.

To circumvent the limitations imposed by the hardware, the program calls the pick() function after every beat. pick() is set up to listen for activity (HIGH) on the INPUT buttons after each beat, allowing the sequence to respond depending on the following situations:

* If no INPUT pin is HIGH, the sequence continues to the next beat and eventually the next bar and so on until the sequence reaches the end.
* If the same INPUT pin that triggered the current sequence is HIGH, said sequence restarts from the beginning.
* A different INPUT pin triggers that pin's sequence.

Each of the 4 (four) pads is independently wired to be triggered by Arduino's OUTPUT pins 10 through 13 following a sequencer pattern stored in memory. The sequencer in turn is triggered by INPUT pins A0 through A5.

Functions
=========

## initial()
Triggers first sequence as per input pin returned by check()

## check()
Checks each of the 6 inputs and returns the pin number that's HIGH.








