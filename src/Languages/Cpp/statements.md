# Statements

<sub>**Author**
Pradyumna Ponkshe</sub>

This one is a short topic, but very important nonetheless. To sum up the entirety of this lesson in one snippet:

```cpp
int foo = 3; // Henceforth referred to as <Type 1>

int foo{3}; // Better, Henceforth referred to as <Type 2>

```

Now, after looking at this very confusing syntax and thinking to yourself, why is this guy telling me to initiate it in array like syntax.. let's get to the actual explanation.

---

## Type 1 Declaration

This is the type of variable declaration you must be familiar with. It's the generally accepted way in most programming languages. The actual difference between this and the type 2 declaration is very small.

**NOTE:** Thus the general consensus is that this way of variable declaration is observed when writing C++ code.

The difference being:

```cpp
// for a declaration of any type 
// such as <data_type> <var_name> = <value>;
int foo = 3;
float bar = 3.14;
// assigning a non-compatible value does not throw and error. Some lsp's may throw a 
// warning, but that's it
// E.g
int foo = 3.14; // the value stored in foo will be 3. (optimised by compiler)
```

In such cases, the compiler does implicit type-conversion of the given value in order to store it within the specified type of variable. This may cause memory safety issues when the program is given in the hands of inexperienced developers. This is especially the case in a student team of developers. This problem is solved majorly in the Type 2 declaration.

This type of declarations turn out to be especially lengthy, when initialising every variable to 0. As a variable initialised as just ***int var;***, may contain garbage value. Thus the required initialisation for variables becomes:

```cpp
int var = 0, var_1 = 0, var_2 = 0;
float foo = 0.0f, foo_1 = 0.0f;
/*... etc*/
```

---

## Type 2 Declaration

Even though type 2 may look very similar to how we instantiate arrays, it is not in any way related to arrays. This type of variable declaration simply ensures that no implicit type-conversion is done during program compilation.

```cpp
// The same declarations as above will be done as
int foo{3};
float bar{3.14};
char letter{'a'};
// In case, type-conversion is required, the compiler will throw an error.
// This helps with a lot of memory issues due to improper variable declaration in many cases.
```

This type of declarations turns out to be rather convenient, when initialising every variable to 0. As a variable initialised as just ***int var;***, may contain garbage value. Thus the required initialisation for variables becomes:

```cpp
int var{}, var_1{}, var_2{};
float foo{}, foo_1{};
/*... etc*/
```

**NOTE:** There are times, where we use macros or library files written by others. In such cases, avoiding memory leaks and overflows due to implicit type-conversion is like playing russian roulette. Writing your variables in such a way ensures that this doesn't happen in at least your case.

***TODO:***
Experiment with the same, try mixing it up with all types and values to understand where type conversion is needed, and where it isn't. Because if the compiler isn't trying to implicitly type-case something, it means you probably don't have to type cast it explicitly either if needed. 

( *I've seen people type casting int to float when giving an int value to a float variable* ).
