# Data Types and Variables

When writing embedded systems or robotics code, understanding primitive data types and their sizes is crucial for achieving efficient, reliable, and portable software. This guide focuses on primitive data types, `stdint.h` types, and nuances that can affect your code's performance and correctness.

---

## Table of Contents
1. [Primitive Data Types in C](#primitive-data-types-in-c)
2. [Fixed-Width Integer Types](#fixed-width-integer-types)
3. [Type Ranges and Overflows](#type-ranges-and-overflows)
4. [Practical Tips](#practical-tips)
5. [Debugging and Verification](#debugging-and-verification)

---

## Primitive Data Types in C

C provides basic data types like `int`, `float`, `char`, etc., but their sizes and ranges can vary depending on the platform and compiler. This variability can introduce subtle bugs in embedded and robotics systems where memory and performance are constrained.

| **Data Type** | **Typical Size** | **Range**                                |
|---------------|------------------|------------------------------------------|
| `char`        | 1 byte           | `-128` to `127` (signed), `0` to `255` (unsigned) |
| `short`       | 2 bytes          | `-32,768` to `32,767`                   |
| `int`         | 2 or 4 bytes     | `-32,768` to `32,767` (2 bytes) or `-2,147,483,648` to `2,147,483,647` (4 bytes) |
| `long`        | 4 bytes          | `-2,147,483,648` to `2,147,483,647`     |
| `long long`   | 8 bytes          | `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807` |

### **Key Considerations for Primitive Types**

1. **Portability Issues**: The size of `int` and `long` can differ between platforms. Always confirm the architecture you're working on (e.g., 8-bit, 16-bit, 32-bit).
2. **Nature of Char**: 
   - 'char' is generally handled as an unsigned integer (*char can be unsigned or signed*). Hence performing arithmetic operations on a char variable is possible. E.g:- 
   ```c
   char a = 'a';
   printf("%c\n", (a+1));
   ```
   **Output:**
   ```sh
   b
   ```
3. **Lack of errors when interchanging data types**:
    - If you assign the value of a variable with _x_ data  type to a variable of _y_ data type, C does not see it as an error. This causes problems if done with data types of different sizes. E.g:
    ```c
    long long a = 6969696969696969;
    printf("%d", a);
    ```
    This is a common mistake. __%d__ is the int placeholder. Int is smaller in size to long long. The modern C compiler will throw a warning but it won't be considered an error and code will execute. For some micro controller's the toolchain's  compiler won't throw a warning either. Try executing the program on your local machine by:-
    ```sh
    gcc program_name.c -o exec_name
    ./exec_name
    ```
    
---

## Fixed-Width Integer Types

The `stdint.h` header introduced in C99 standard provides precise control over integer sizes, ensuring portability across platforms. These types are especially useful in embedded systems and robotics where size and alignment are critical.

| **Type**             | **Size**   | **Range**                                |
|-----------------------|------------|------------------------------------------|
| `int8_t`             | 1 byte     | `-128` to `127`                          |
| `uint8_t`            | 1 byte     | `0` to `255`                             |
| `int16_t`            | 2 bytes    | `-32,768` to `32,767`                    |
| `uint16_t`           | 2 bytes    | `0` to `65,535`                          |
| `int32_t`            | 4 bytes    | `-2,147,483,648` to `2,147,483,647`      |
| `uint32_t`           | 4 bytes    | `0` to `4,294,967,295`                   |
| `int64_t`            | 8 bytes    | `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807` |
| `uint64_t`           | 8 bytes    | `0` to `18,446,744,073,709,551,615`      |

### **Key Considerations for `stdint.h` Types**

1. **Deterministic Sizes**: These types guarantee the same size regardless of the platform, making them ideal for hardware registers, communication protocols, and serialization.
2. **Mixing Signed and Unsigned Types**: Be cautious when performing arithmetic between signed (`intX_t`) and unsigned (`uintX_t`) types, as it can lead to unexpected results due to implicit type promotion.
3. **Minimizing Memory Usage**: Use the smallest possible type (e.g., `uint8_t` for 8-bit values) to reduce memory usage and improve cache performance. This is critical in memory-constrained environments.

---

## Type Ranges and Overflows

### **Signed Overflow**
In C, signed integer overflow causes undefined behavior. For example:
```c
int8_t x = 127;
x += 1; // Undefined behavior: x can wrap around or trigger a fault
```

### **Unsigned Overflow**
Unsigned integer overflow wraps around to zero modulo `2^n` where `n` is the number of bits:
```c
uint8_t x = 255;
x += 1; // x becomes 0 (wrap-around)
```

---

## Practical Tips

1. **Use `stdint.h` Types**: Always prefer fixed-width types to avoid surprises with type sizes.
   ```c
   uint8_t motor_pwm = 255; // Always 8 bit, regardless of platform.
   ```

2. **Avoid Implicit Promotions**: When mixing smaller types like `uint8_t` with larger ones, explicit casting helps maintain correctness.
   ```c
   uint8_t a = 200;
   uint8_t b = 100;
   uint16_t result = (uint16_t)a + b; // Prevent overflow
   //Alternatively
   data_type result = data_type(a+b); // is also used. 
   //Google the difference or ask your seniors and test their knowledge
   ```

3. **Alignment Awareness**: Check your compiler and platform documentation for data alignment requirements. Misaligned accesses can slow down operations or cause faults on some architectures.

4. **Endianness**: Be mindful of the platform's endianness when interpreting multi-byte types (e.g., `int16_t` or `uint32_t`) in communication protocols.

5. **Avoid Over-Allocation**: Do not use larger types unless necessary. For example, using `uint32_t` instead of `uint8_t` unnecessarily increases memory usage and bus load.

6. **Range Checking**: Always validate input data before assigning it to variables, especially when interfacing with external devices or sensors.

---

## Debugging and Verification

- Use compiler warnings (`-Wall`, `-Wextra`) to catch potential type-related issues.
- Verify assumptions about type sizes with `sizeof` during debugging:
  ```c
  printf("Size of int: %zu bytes\n", sizeof(int));
  ```

---