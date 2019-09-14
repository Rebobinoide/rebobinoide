Rebobinoide 
===========

![38461330_1378488775618051_1496400106671308800_n](https://user-images.githubusercontent.com/55008098/64902170-50f14a00-d657-11e9-9160-7df829bea61e.jpg)

The project consists of a few parts:
* A sequencer/drum machine program stored in the Arduino's flash memory.
* An array of four (4) AM-FM radios modified to individually switch on and off through triggering pulses produced by four (4) of Arduino's digital OUTPUT pins.
* A Yamaha DD-35 Drum Kit whose pads have been wired for external activation using opto-couplers- in addition to the factory triggering by striking - through a female VGA connector.

## The logic behind the sequencer

Each of the six (6) buttons is programmed to trigger a sequence consisting of four (4) bars, each of which containing four (4) beats, which in turn are divided into four (4) notes.

To circumvent the limitations imposed by the hardware, the program is set up to listen for activity (HIGH) on the INPUT buttons after each bar, allowing to respond depending of the following situations:

* If 

Each of the 4 (four) pads is independently wired to be triggered by Arduino's OUTPUT pins 10 through 13 following a sequencer pattern stored in memory. The sequencer in turn is triggered by INPUT pins A0 through A5.

Functions
=========

## initial()
Triggers first sequence as per input pin returned by check()

## check()
Checks each of the 6 inputs and returns the pin number that's HIGH.








