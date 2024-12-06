# Task 1

This task introduces you to the Arduino Uno. A handy board for
beginners and expert enthusiasts alike.

---

## Table of Contents

1. [Shit You Should Know](#shit-you-should-know)
2. [Shit You Should Prepare](#shit-you-should-prepare)
3. [The Task](#the-task)
4. [Task In Depth](#task-in-depth)

---

## Shit You Should Know

Arduino boards are generally based on AVR architecture, with a few
newer outliers. The one you'll be for this task is the Arduino Uno R3.

The Arduino Uno R3 is a developmental board, not a micro controller.
It's basic 'must know' details are :

### Arduino Uno R3 Hardware Specifications

Refer [Harware Specs](../../Arduino/hardware-specs.md) for the hardware specifications.
Information regarding the AVR architecture will be provided in later lessons, specifically at [AVR Family](../../Arduino/avr-intro.md).
For now knowing the hardware specs, and knowing them enough to not burn the electronics when you do the task is all you need.

---

## Shit You Should Prepare

In order to start the task you need to acquaint yourself with reading
documentations. At the moment, the [arduino.cc](https://docs.arduino.cc/programming/) documentation

Find the function **digitalWrite(int pin, bool value) {}**

---

## The Task

1. Take an LED, a resistor, some jumper wires and the Arduino Uno. (_if hardware is unavailable, use [TinkerCAD](https://www.tinkercad.com/circuits)_)
2. What you are going to do is Blink the LED at a fixed rate, using the Arduino UNO.
3. There's two ways to do this.

   1. **Latching Logic**

      - Suitable for beginners.
      - However, this approach is a **red flag** for beginner+ programmers.

   2. **Debounce Logic**
      - A better and more professional approach.
      - May take time to understand but is a valuable skill for embedded programming, even at the level of robot control.
        With the intent to teach y'all from an early onset, daddy shall take care of you.

4. This is enough to get you started, follow up with your seniors regarding any task related doubts. The links, and information provided within this [Documentation](../../) is good enough for you to be able to look for both the logics on your own online.

**NOTE:** _Not using chatgpt for the literal first task is recommended. ChatGPT as of Dec 24 is pretty bad when it comes to writing embedded code. It'll help
you right now, but if you get into a habit of relying on it in the future for embedded, you're fucked._

---

## Task in Depth
