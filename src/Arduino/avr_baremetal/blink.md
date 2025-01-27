# Basic Blink

To make the built-in LED on the UNO blink, you need to understand the concept of bit-shifting first. If you are familiar with the same already, go on ahead to the required section using the TOC below.

---

## Table of Contents
1. [Bit shifting](#bit-shifting)
2. [Registers](#registers)
3. [Bare blink](#bare-blink)
4. [Code](#code)

---

## Bit shifting

Bit shifting is based on the use of bitwise operators to manipulate the arrangment of 1's and 0's at a particular address. This address can be a variable, a register pointed to by a pointer etc. 

The basic terminology to be understood henceforth is:
- **MSB** - Most significant bit ( *The leftmost bit* )
- **LSB** - Least significant bit ( *The rightmost bit* )

Bit shifting is a fundamental operation in AVR baremetal programming, allowing you to manipulate individual bits within registers efficiently. AVR microcontrollers use 8-bit or 16-bit registers, and bit shifting helps to modify these registers for hardware control tasks. 

- **Left Shift (`<<`)**: Moves bits toward higher-order positions, effectively multiplying the value by 2 for each shift.
- **Right Shift (`>>`)**: Moves bits toward lower-order positions, dividing the value by 2 for each shift.

#### Key Points
1. Shifting by `n` positions means moving bits `n` steps left or right.
2. Overflowed bits are lost, and vacant positions are filled with 0.
3. Signed integers can exhibit unexpected behavior when shifted, so unsigned data types are safer for predictable results.

#### Example Code: Left and Right Shifting
```c
#include <avr/io.h>

int main(void) {
    uint8_t value = 0x01; // 0b00000001
    uint8_t leftShifted, rightShifted;

    leftShifted = value << 2;  // Shift left by 2
    rightShifted = value >> 1; // Shift right by 1

    // Set PORTB to observe the results (for example, on LEDs)
    PORTB = leftShifted;  // Output the left-shifted value on PORTB
    while (1) {
        // Main loop
    }
}
```

#### Explanation
- `value << 2` shifts the bits of `value` (`0b00000001`) two places left, resulting in `0b00000100` (decimal 4).
- `value >> 1` shifts the bits of `value` (`0b00000001`) one place right, resulting in `0b00000000` (decimal 0).

#### Example Output
| Operation       | Input Value (Binary) | Output Value (Binary) | Decimal Output |
|------------------|----------------------|------------------------|----------------|
| `value << 2`    | `00000001`           | `00000100`            | 4              |
| `value >> 1`    | `00000001`           | `00000000`            | 0              |

#### Practical Applications
- **Set a Bit**: `PORTB |= (1 << 3);`  // Set bit 3 of PORTB
- **Clear a Bit**: `PORTB &= ~(1 << 3);` // Clear bit 3 of PORTB
- **Toggle a Bit**: `PORTB ^= (1 << 3);` // Toggle bit 3 of PORTB

#### Caution: Overflow and Data Loss
When shifting, ensure the value does not exceed the data type's bit-width. For example:
```c
uint8_t value = 0x80; // 0b10000000
uint8_t shifted = value << 1; // Result: 0b00000000 (overflow)
```

By understanding and using bit shifting, you can efficiently control bits in registers, making it a powerful tool for low-level AVR programming.
```
