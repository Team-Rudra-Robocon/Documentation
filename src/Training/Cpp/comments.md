# Comments  
<sub>**Author**
Pradyumna Ponkshe</sub>

Table of Contents:
1. [File Level](#file-level-comments)
2. [Function Level](#function-level-comments)
3. [Variable](#variable-comments)
4. [Implementation Level](#implementation-comments)
---

## Why Comment Code?
Any code is shit code, when read after 6 months. This holds true for every developer on earth, till the day he stops learning. To atleast preserve some embarassment for yourself, and write code that is legible and understandable by you or any person attempting to clean your mess, well-written comments are recommended.

Below are a few norms to be followed to comment code, which will definitely help you through your years as a programmer in the industry or as a researcher.

---

### File Level Comments
Each user's final code file should start with **File Level Comments** in the format as follows:
```cpp
/*
* Author List: <Name of the team members who worked on this file>
* Push Date:   <Date of Latest Modification> 
* Functions:   <Comma separated list of Functions defined in this file>
* Global Var:  <List of global variables defined in this file, if any>
*/
```

The author list is your way of letting your peers know, who is responsible, for what they see. This gives you clear credit when it works, and teaches you to take accountability if it fails. A push date that was done a while back, gives a programmer confidence that yes, this module works. 

The functions are good comments for libraries in general. Write them with their access-specifiers if the functions are a part of a class. This lets a new programmer, quickly see how to interface a library written by you. They can search specific public functions to see how they work, rather than have to go through the entire library to understand it's working.

Global Variables are a necessity to be listed, as they may cause trouble when a programmer includes or links this file along with theirs. If their file contains global variables of the same name, the compiler will throw an error. This may cause chaos in a large project. Having file level comments, allows them to quickly go through common globals by fuzzy finding the word.

### Function Level Comments
These comments should be a small section of 1 to 5 lines max, from the first line inside the function.
```cpp
void function() {
/*
* Logic: <Description of the function performed and logic used in 1 to 2 lines>
* Call:  <Example of how to call this function>
*/
.....implementation
}
```
The logic should quickly explain to a developer, what this function is supposed to do, and what role it plays in the file as a whole.

The function call, lets the programmer know, what inputs are valid for the function, in case some sort of cases are implemented. **E.g** - A function meant to sort an array/vector of max length 100, won't work if given a pointer to an array/vector of size 150.

### Variable Comments
These are of **utmost** importance to the work we do, as embedded/robotics programmers. This is because each variable can have some soft limits, that aren't hard-coded into the program, as they are taken to be obvious.

Well, there are many developers who don't think of such cases and may misuse your libraries or files. To ensure this doesn't happen, do the following:
```cpp
static uint8_t motor_a_pwm = x; // variable can only have values from 0-255 
```
Even though it is ensured that a *uint8_t* will only take values from 0-255, it's good to mention the same, to avoid type-casting/overflow issues, by just commenting the same.

### Implementation Comments
Most times, well written code explains itself, and code readability is something for which many programmers sacrifice performance. In case, you can't make this tradeoff, or must write code that is as efficient as can be, implementation level comments are a must. As such:
```cpp
int first = 0, second = 1, next;
printf("First %d terms of Fibonacci series are :-\n", num_elements);
//counter: will iterate from 0 to (num_elements - 1)
for ( int counter = 0 ; counter < num_elements ; counter++ ) {
    if ( counter <= 1 )
        next = counter;
    else {
        //The next element is equal to the sum of the current element (second variable) and the previous element (first variable)
        next = first + second;
        // first element becomes the second element and second element becomes the next element for the next loop iteration
        first = second;
        second = next;
    }
    printf("%d\n", next);
    }
}
```
Implementation level code is not necessary if program flow is self explanatory. But it is a must if a very complicated or niche way is taken to solve a problem in an efficient manner.


