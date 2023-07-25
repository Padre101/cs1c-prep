# Table of Contents
1. [Header Files](#header-files)
2. [Chrono Explained](#chrono-explained)


# Header Files

## idea's of headerfile's
If I have a driver.cpp and a function.cpp, is the way I connect them is by making a .h file?  And if I had multiple functions then i just add more definitions to function.cpp then the declareations in the .h file? 

The answer is yes; thats how they work, pretty simple asf and I will probs use them from now on
Header files are commonly used not only to declare functions and data types, but also to define global constants and macros that can be used throughout a program.

## general structure of a header file(.h):

*the words after **bold** are called macros, in terms of names by convention their the same as the name of your .h file BUT everything is capitalized and the “.” is replaced with “_” also words are seperated by “_”*

> #**ifndef** HEADER_FILE_NAME_H

> #**define** HEADER_FILE_NAME_H

> //Declarations of functions, classes, constants, etc.

> #**endif** // HEADER_FILE_NAME_H

And when you want to use it in like another .cpp you do #include [headerfile name] for ex:

#include "my_header.h”    //The quotes are included
//this is used in the .cpp where you define the functions AND in the driver

//////// end of header files ////////////:

# Chrono Explained

> #include <chrono>  // include the chrono library for measuring time

*the reason we going to be using the data type auto instead of a specific type like int or double is that the type returned by the high_resolution_clock::now() function and the duration_cast() function may not be known ahead of time.
By using auto, we let the compiler automatically deduce the type of the variable based on the return type of the function call*

## How to time how long it takes to sort:

### you just time the function so do the following:

> auto start = high_resolution_clock::now();  //  the clock

> // bubble sort algorithm

> auto stop = high_resolution_clock::now();   // stop the clock

### then calculate the elapsed time by subtracting the start time from the end time and storing the result in the duration variable:

> auto duration = std::chrono::duration_cast<std::chrono::seconds>(stop - start);

### Finally, we output the elapsed time to the console using the count() function:

> cout << "Sorting time: " << duration.count() << " seconds" << endl;

This will output the elapsed time in microseconds to the console when the program finishes running. You can adjust the time unit by changing the argument passed to duration_cast function.

# Pointer's and Dynamic Arrays

## Pointer syntax 

>> [variableType]* [variableName1] = &[variableName2]

(VaurableName2 should be declared before pointed)






