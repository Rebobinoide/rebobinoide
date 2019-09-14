Rebobinoide 
===========

![38461330_1378488775618051_1496400106671308800_n](https://user-images.githubusercontent.com/55008098/64902170-50f14a00-d657-11e9-9160-7df829bea61e.jpg)

The project revolves around a modified Yamaha whose pads have been wired for external activation - in addition to triggering by hitting - through a female VGA connector.

## Arduino

Each of the 4 (four) pads is independently wired to be triggered by Arduino's OUTPUT pins 10 through 13 following a sequencer pattern stored in memory. The sequencer in turn is triggered by INPUT pins A0 through A5.

Functions
=========

## initial()
Triggers first sequence as per input pin returned by check()

## check()
Checks each of the 6 inputs and returns the pin number that's HIGH.








