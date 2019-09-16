### Rebobinoide 
===========

![38461330_1378488775618051_1496400106671308800_n](https://user-images.githubusercontent.com/55008098/64902170-50f14a00-d657-11e9-9160-7df829bea61e.jpg)

## Physical equipment
The project consists of a few parts:

* A sequencer/drum machine program stored in the Arduino's flash memory.

* An array of four (4) AM-FM radios modified to individually switch on and off through triggering pulses produced by four (4) of Arduino's digital output pins.

* A Yamaha DD-35 Drum Kit whose pads have been wired for external activation using opto-couplers- in addition to the factory triggering by striking - through a female VGA connector.

All the elements are also connected to the Arduino GND pin, of course.

## Overview


Each of the six (6) buttons connected to the Arduino's input pins is programmed to trigger a rhythm sequence consisting of four (4) bars. Each bar is made up of four (4) beats, which in turn are divided into four (4) notes. 


Here comes the tricky part. Partly to circumvent the limitations imposed by the hardware, each of the 6 sequences triggered is set to stop after every beat to check which of the input buttons is pressed (HIGH), if any. The `pick()` function then takes actions based on any of four conditions:


* If no input pin reads HIGH, the sequence continues to the next beat and eventually the next bar and so on until the sequence reaches the end, if all input pins remain LOW throughout the sequence.


* If the same input pin that triggered the current sequence is HIGH, said sequence restarts from the beginning of the current bar, which is being tracked by the global variable `bar`.


* A different input pin's HIGH state pin triggers the corresponding sequence starting at the first bar.

## The logic


Power-on calls `loop()`'s `initial()`, which runs`check()` to poll the input pins for the first one to display a HIGH state. `initial` then sets global variables `bar` and `beat` (which keep track of the bars and beats, obviously) to 0 and `before` and `after` to whatever sequence is returned by `check()`. These variables keep track of the current sequence (last button pressed) and the new one. More on this later.


NOTE: The reason `initial()` sets `bar` and `beat` to 0 even though they are initialized that way at the top is so that it resets their values everytime it is called, i.e., at the end of full cycle.


`initial()` then triggers the first sequence by calling the `seq()` function. `seq()` is is made up of a `while` loop that limits the bar count to four (4). The `while` loop in turn contains a `switch/case` loop based on the variable `beat`. This pretty much defines the pattern of 4 beats to 4 bars.


Each case of `beat` (0-3) triggers the `line()` function, which takes as parameter the sub-array `s[after][bar][beat]` containing 8 `ints`. 


> It is imperative to mention that the 4-dimensional global array `s[6][4][4][8]` contains all 6 sequences with each one's respective bars, beats and notes sub-arrays. The last 8-element sub-array carrying the individual notes is called using `after`, `bar` and `beat` as indexes on `s[][][][]`.


Using a `for` loop, `line()` then passes the 8-element array to 4 iterations of `note()`, each one taking the values in pairs, i.e. `note(array[i], array[i+1])`, and incrementing i by 2 after each iteration. The two arguments that `note()` takes in determine which output pin goes HIGH and how many times it is activated, respectively. To create an empty note, I simply set the times parameter to 0.



`s[after][bar][beat]` and its subarrays containing any of 6 sequences made up of 4 bars with 4 beats and 4 notes each. Each subarray containing the notes actually has eight (8) elements that represent individual notes in output pin/times triggered pairs. 






calls the `pick()` function after every beat - , which also calls `check()` to listen for HIGH input pins - if any - allowing the sequence to respond to the following situations:



Each note is defined by the `note()` function, which takes 3 arguments to specify the output pin to activate, as well as how long it stays HIGH, and how many times it is triggered within the space of one note. All three parameters may have a value of 0, creating an empty note without going off beat.




Each of the 4 (four) pads is independently wired to be triggered by Arduino's OUTPUT pins 10 through 13 following a sequencer pattern stored in memory. The sequencer in turn is triggered by INPUT pins A0 through A5.



https://www.khanacademy.org/humanities/music/music-basics2/notes-rhythm/v/lesson-1-note-values-duration-and-time-signatures



