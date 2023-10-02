# Table of Contents
1. [Header Files](#header-files)
2. [Chrono Explained](#chrono-explained)
3. [Pointer's and Dynamic Arrays](#pointers-and-dynamic-arrays)
4. [Pointer's and Array's](#pointers-and-arrays)
5. [C++ Text Files](#c++-text-files)
6. [new and delete operator](#new-and-delete-operator)
7. [Dynamoic Memory Allocation](#dynamic-memory-allocation)
8. [Review Notes in class](#review-notes-in-class)


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


 ## Scope Resolution Operator and HeaderFile Example

It deals with the methods of the class, not the class don't confuse that.

The Scope Resolution Operator ("ClassName::MethodName") notation is used when defining/implementing a class's member function outside of its declaration. It tells the compiler that you're providing the implementation for the `MethodName` of the `ClassName` class. This notation ensures clarity and prevents ambiguity, especially when multiple classes have methods with the same name.

### Purpose of Scope Resolution Operator (::):
- Clearly indicate which class's method or constructor you're implementing.
- Dont confuse it with class, you use sro for methods of the class not the class

How to read the notation:

1. For Methods:
   Format: ReturnType ClassName::MethodName
   Interpretation: "Implementing the MethodName method of the ClassName class, which returns ReturnType."

2. For Constructors:
   Format: ClassName::ClassName
   Interpretation: "Implementing the constructor of the ClassName class."
*/

### How is this related to Headerfiles?

You usually define your class in the header files(.h), then you implement(define) in a .cpp file aka *your defining it outside of its declaration*, which is when you use this

### example of how to use scope resolution operator with 1. using a constructor and 2. using a method. 

I need two examples to understand because I can't just add a return type to the constructor example because that would make it a method, which is what I wanted, but a method can't have the same name as it's class, that's a constructor.

#### 1. If you were implementing a constructor and wanted to define/implement it in the same spot you declare it, you normally do something like this(you don't need the scope resolution operator here): 

//Let's say this is Box.h(because you usually only define here in headerfiles, but we are also implementing the method in this example), you would probably do this, which is the "normal way"

```c++
class Box {
    int length;
    int width;
public:
    Box(int l, int w);  // This is a declaration of the constructor(the method were focusing on)
};
```

#### If you were implementing a method, outside of where it was defined you would use the scope resolution operator

This is the header file(only declaring this time).
When we declare, that means were just not using the braces(which is whats defining/implementing a function)
```c++
//
#ifndef BOX_H  // Header guard to prevent double inclusion
#define BOX_H

class Box {
    int length;
    int width;
public:
    Box(int l, int w);  // Declaration of the constructor
    // Additional public member function declarations would go here
};

#endif // BOX_H
```

//this is the corresponding .cpp of the header file(where you implement/define the method). Here you have to use the scope resolution operator because you implementing a method that's outside of its main

```c++
// Box.cpp
#include "Box.h"

Box::Box(int l, int w)  //this is telling the compiler your "implementing a method named box of the box class, which returns nothing"
{
    length = l;  // assignment
    width = w;   // assignment
}
```

**recall:
How to read the scope operator notation on methods:
1. For Methods:
   Format: ReturnType ClassName::MethodName
   Interpretation: "Implementing the MethodName method of the ClassName class, which returns ReturnType."

2. For Constructors:
   Format: ClassName::ClassName
   Interpretation: "Implementing the constructor of the ClassName class."

#### 2. If you were implementing a method, and wanted to define/implement it in the same spot you declare it, you normally do something like this(you don't need the scope resolution operator here): 

//Let's say this is Box.h (because you usually only declare here in header files, but we are also implementing the method in this example):


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

this syntax means variableName1 points to a memory address(variableName2)

## dereference operator (*)

Its used to get grab(access and modify) the value of whatever a pointer is pointing to(here its variableName1)

If you use it during declaration:
> ([dataType]* [variableName1])
, it makes a pointer variable. When not, it acts as a dereference operator(grabs value of what pointer is pointing to)

After declaring the pointer variable, you can use the dereference operator to access or modify the value that the pointer is pointing to:

> *pointerVariable = value;  // Set the value pointed to by pointerVariable

> value = *pointerVariable;  // Get the value pointed to by pointerVariable

In these lines of code, *pointerVariable refers to the value of the variable that pointerVariable points to.

Remember that you should always make sure that your pointer is pointing to a valid memory location (like a variable or an allocated portion of memory) before you try to access or modify the value it points to with the dereference operator. Otherwise, you could encounter a null pointer error or other unexpected behavior.

# Pointer's and Array's

In C++, the name of an array is a pointer to the first element of the array. For example:

> int numbers[5] = { 2, 3, 5, 7, 9 };


Yes, your notes capture the fundamental relationship between pointers and arrays in C++. The notes could be made clearer with some refinements:

Pointers and Arrays

In C++, *the name of an array is a pointer to the first element of the array*. For example:

>> int numbers[5] = { 2, 3, 5, 7, 9 };

If you output the array name, it gives the memory address of the first element:

> cout << numbers;  // outputs address of first element (2)

This is because the array name, numbers in this case, is actually a pointer to the first element of the array.

You can manipulate this pointer to access other elements of the array:

> cout << (numbers + 2);  // outputs address of third element (5)

By using the dereference operator (*), you can get the value at the address:

> cout << *(numbers + 2);  // outputs value of third element (5)

Here, (numbers + 2) gives you the address of the third element, and *(numbers + 2) dereferences it to get the value of the third element.

Therefore, numbers[2] is equivalent to *(numbers + 2). Both provide a way to access the third element in the array.

This demonstrates how pointers can be used to access and manipulate arrays in C++.

Note: Remember, array indices in C++ start from 0, so numbers[2] or *(numbers + 2) refers to the third element, not the second.

# C++ Text Files

ifstream and ofstream are classes defined in the <fstream> library, and they are used to handle file input and output operations respectively.

## Opening Files
You can open files for reading with ifstream and for writing with ofstream. For example

> ifstream infile("input.txt");  // open 'input.txt' for reading

> ofstream outfile("output.txt");  // open 'output.txt' for writing

Here, infile is an object of the ifstream class, which is tied to the file input.txt for reading operations. Similarly, outfile is an ofstream object tied to output.txt for writing operations.

## Reading and Writing

Once the files are open, you can use these objects to read from and write to the files.

### Reading data from a file:

```c++
int arr[100], n = 0;  // array to hold file data and counter
while (infile >> arr[n]) {  // read integers from file into array
    n++;
}
```

### Writing data to a file

```c++
for (int i = 0; i < n; i++) {  // write data from array to file
    outfile << arr[i] << " ";
}
```

In both these cases, infile and outfile act like the cin and cout objects, allowing you to use the stream extraction (>>) and insertion (<<) operators.

## Closing File

After performing all the operations, you should close the files:

```c++
infile.close();  // close 'input.txt'
outfile.close();  // close 'output.txt'
```

## Summary

In C++, the ifstream class is typically used to open a file for reading, and ofstream is typically used to open a file for writing. Once opened, you can use these objects to read from and write to the files, respectively, much like you would with cin and cout. Once all operations are done, don't forget to close the files.

# new and delete operator
In C++, dynamic memory allocation is facilitated by two operators: new and delete. These operators manage memory allocation and deallocation for variables and arrays on the heap at runtime.

kind of like borrowing a toy(new/allocating) and once your done you put it back(delete/deallocating). 

## new operator

the new operator is used with data types(int, byte, etc), instead of specifying the exact byte size of the memory to be allocated (like in assembly), in C++ you specify the type of the object that you want to allocate memory for and new handles the details of how much memory to allocate

The new operator is used to allocate memory on the heap during runtime. It returns the address of the allocated memory. For example, if you want to dynamically allocate an integer, you would do the following:

```c++
int* ptr = new int;
```

In this example, new int allocates memory sufficient to hold an int on the heap, and then returns the address of the allocated memory. That address is then stored in the int pointer ptr.

If you want to allocate an array, you can specify the number of elements like this:

```c++
int* arr = new int[10];
```

In this case, new int[10] allocates enough memory to hold 10 int values and returns the address of the first allocated int. That address is stored in the int pointer arr.

## delete operator
The delete operator is used to deallocate memory that was previously allocated with new. It frees up the memory on the heap so it can be reused for other purposes. To use delete, you provide it the address of the allocated memory:

```c++
delete ptr;

```
In this case, delete ptr deallocates the memory at the address stored in ptr.

If you have allocated an array, you should use delete[] to deallocate all of the memory:

```c++
delete[] arr;
```

In this case, delete[] arr deallocates all the int values in the array at the address stored in arr.



## Important Notes
Always match each new with a delete and each new[] with a delete[] to avoid memory leaks. Also, don't use delete or delete[] on any memory not allocated with new or new[].

After using delete or delete[] on a pointer, it's a good practice to set the pointer to NULL to avoid dangling pointers:


# Dynamic Memory Allocation

In C++, dynamic memory allocation allows the programmer to allocate and deallocate memory during runtime. This is unlike standard arrays, which must have their size determined at compile time.

## Compile Time vs. Runtime
Compile Time: This is the phase when the compiler translates the source code into machine code. This phase happens before the program is run. The size of standard arrays, among other things, must be determined at this time. The compiler must know the size of these arrays to properly allocate memory for them in the compiled program.

Runtime: This is the phase when the compiled program is actually running and performing its tasks. Actions taken during runtime can be based on user input, system conditions, or other unpredictable factors.

Dynamic memory allocation is an example of an operation that occurs at runtime. The program can request memory, use it, and then free it when it's no longer needed, all while the program is running.

## Allocating and Deallocating Memory
Dynamic memory is allocated using the new keyword and deallocated using the delete keyword. Every time you allocate memory using new, you should eventually deallocate it using delete to prevent memory leaks.

## Dynamic Arrays
A dynamic array is an array where the size is determined at runtime. This is done by storing a pointer to the first element of the array.

Here is how to create a dynamic array:

```c++
int* myArray = new int[size]; // 'size' can be a variable determined at runtime
```

In this line, myArray is a pointer that points to the start of a new integer array of size size. This array is allocated dynamically

## Dynamic Array Example
Here is an example of how to create and use a dynamic array:

```c++
int main() {
    // Get the array size from the user at runtime
    int size;
    cout << "Enter array size: ";
    cin >> size;

    // Create a dynamic array
    int* myArray = new int[size];

    // Get array elements from the user
    for (int i = 0; i < size; i++) {
        cout << "Enter element " << i << ": ";
        cin >> myArray[i];
    }

    // Print the array elements
    for (int i = 0; i < size; i++) {
        cout << myArray[i] << " ";
    }
    cout << endl;

    // Deallocate memory
    delete[] myArray; // delete memory allocated by 'myArray'

    // Set myArray to NULL to ensure it does not point to deallocated memory
    myArray = NULL;

    // Pause the system (Note: This is system-dependent and generally not recommended)
    // system("pause>0");

    return 0;
}
```

Remember that deallocating the dynamic array memory with delete[] and setting the pointer to NULL is crucial to avoid dangling pointers and potential issues with accessing memory you no longer own. The system("pause>0"); command is generally not recommended as it is system-dependent and can introduce security risks.


## Dynamic 2d Array Concepts

A dynamic 2D array is essentially an array of arrays. You can think of a 2d array as a table, where each row might have a different number of columns. In a dynamic 2D array, both the number of rows and the number of columns can be determined during runtime.

Here's how it works:

1. A dynamic 2D array is created by first declaring a double pointer, e.g., int** arr;. This double pointer will point to an array of pointers.

2. Each pointer in the array of pointers will then point to a dynamically allocated array. The size of these arrays (the number of elements they hold) can be determined during runtime.

This structure creates a table-like array with n rows (the array of pointers) and variable number of columns (the dynamically allocated arrays each pointer points to).

Here's an example:

```c++
int main() {
    int rows = 5;
    
    // Allocate memory for an array of pointers
    int** arr = new int*[rows];
    
    // Allocate memory for each row (array) dynamically
    for (int i = 0; i < rows; i++) {
        int columns;
        cout << "Enter number of columns for row " << i << ": ";
        cin >> columns;
        
        // Allocate an array for this row
        arr[i] = new int[columns];
    }
    
    // Now, arr is a 2D array with 'rows' number of rows, and each row having dynamically determined number of columns
    
    // Don't forget to delete the memory after use
    for (int i = 0; i < rows; i++) {
        delete[] arr[i];
    }
    delete[] arr;
    
    return 0;
}
```

The above example allows you to create a 2D array with a user-specified number of rows and columns. Remember to always deallocate any memory you've allocated dynamically once you're done using it. This includes both the individual rows and the array of pointers itself.

Note: As in the case of dynamic arrays, always be sure to check that memory allocation was successful before using the array. In real-world applications, it's always possible that the new operation could fail if there isn't enough memory available.

# Review Notes in class

## Memory

Memory in computer science refers to devices that store data or programs either temporarily or permanently. RAM is a volatile type of memory. The word size, such as 32-bit or 64-bit, indicates how much data a CPU can process at once, and it may influence the size of instructions. However, instructions can vary in size. A single bit in memory represents either a 0 or 1, while a byte comprises 8 bits. On a 32-bit system, the direct addressable memory limit is 4 GB, which corresponds to 2^32 bytes of RAM.

## Pointer
I already have this so skips

## Pointers, Arrays, and Pointer Arithmetic
sdds
# Pointers, Arrays, and Pointer Arithmetic

- Assign a pointer to the first element in an array.
- Access array elements by incrementing the pointer.

## Example:

```c++
int main()
{
   
    const int SIZE = 5;
    int numbers[SIZE] = {6, 8, 9, 3, 7};
    int *ptr;
    
    ptr = numbers; // Assigns the address of numbers[0] to ptr; // No & when assigning an array address.
    for (int i = 0; i < SIZE; i++)
    {
        cout << *ptr << endl;
        ptr++; // Increments the address of numbers[0] to numbers[1].
               // Therefore, the address is incremented by 4, because integers are 4 bytes.
    }
    
    return 0;
}
```

## Pointers as Function Parameters

- A pointer can be used as a function parameter.
- When a pointer is passed to a function, the pointer holds an address of a variable that can be accessed by the function.
- A pointer gives a function access to the original variable, much like a reference variable does.

**Note**: When a variable is passed by reference, the reference variable acts as an alias to the original variable. This gives the function access to the original variable.

- Generally, passing reference variables is easier than passing pointers as arguments.
  - However, pointers to c_strings work well and are easy.

```c++
#include <iostream>
using namespace std;

void getName(char *);
void displayName(char *);
const int SIZE = 30;

int main()
{
    char name[SIZE];
    char* ptr = name; // The address of the first byte of the array is assigned to the pointer.
    getName(ptr);
    displayName(ptr);

    return 0;
}

void getName(char* pName)
{
    cout << "Enter name:  ";
    cin.getline(pName, SIZE);
}

void displayName(char* pName)
{
    cout << "Hi " << pName << ".\n";
}

/* OUTPUT:
Enter name:  Tom Lee
Hi Tom Lee.
Press any key to continue */
```

## Array: Implicit Conversion to a Pointer

When an array is passed to a function, there is an implicit conversion to a pointer. The memory address of the first byte is passed.

```c++
#include <iostream>
using namespace std;

void showNumbers(int numbers[], const int NUM_ITEMS);

int main()	  
{
    const int SIZE = 3;
    int numbers[SIZE] = {5,6,7}; // The base address (e.g., AB1234F1) is passed to the function.
    showNumbers(numbers, SIZE);
    return 0; // A value of 3 is passed to the function.                                  
}

void showNumbers(int values[], const int NUM_ITEMS)
{
    for (int i = 0; i < NUM_ITEMS; i++)
    {
        cout << values[i] << endl;
    }
}
```
For the array int numbers[SIZE] = {5,6,7};:

The base address (e.g., AB1234F1) is the memory address of the first byte of the array.

AB1234F1  00000101    // 5 = 00000000000000000000000000000101
AB1234F2  00000000      
AB1234F3  00000000  
AB1234F4  00000000  
AB1234F5  00000110    // 6 = 00000000000000000000000000000110
AB1234F6  00000000	    
AB1234F7  00000000	
AB1234F8  00000000	
AB1234F9  00000111    // 7 = 00000000000000000000000000000111
AB1234FA  00000000      
AB1234FB  00000000    
AB1234FC  00000000  

This visualization shows how the integer array occupies memory, assuming a 32-bit architecture where each integer takes up 4 bytes.

## Range based for loop

The **for-each loop** (also known as a range-based for loop) was introduced in 2011. It provides an alternative way to iterate through every element in an array (or other list-type structures).

The for-each loop allows for swift access to array elements without the need for initialization, testing, or increment/decrement. Essentially, a for-each loop acts on every array element, rather than performing an action `n` times.

### Advantages of For-each Loop:
1. Enhances code readability.
2. Minimizes the risk of programming errors.

### Difference between traditional for loop and range based(for-each loop)
Traditional for loop: You control the initialization, condition, and iteration step. This means you can iterate in any way you want—forward, backward, every other element, etc.

Range-based for loop: It's used to iterate over every element in a container or an array, from the beginning to the end, in a straightforward manner. It abstracts the process of accessing and iterating through the elements.

#### Syntax
The general format is: `variable : array`

```c++
#include <iostream>
using namespace std;

int main()
{
    float testScores[5] = { 92.5, 77.0, 88.0, 93.5, 81.0 };

    for (float score : testScores) 	// iterate through the array
        cout << score << '\t'; 		// Output one score with each iteration 
    return 0;
}
```

In this context, score isn't an array index. Instead, with each iteration of the loop, it takes on the value of the current array element. The loop continues iterating, assigning the value of each subsequent array element to the score variable.

Note: It's essential that the variable type in the loop matches the array's type. Otherwise, type conversion will occur.

## For each loops and the auto keyword

Because the variable score should have the same type as the array, this is an ideal case in which to use the auto keyword, and let C++ deduce the data type of score.

### above example using `auto`:

```c++
int main()
{
    float testScores[5] = { 92.5, 77.0, 88.0, 93.5, 81.0 };
    for (auto score : testScores) 	// iterate through the array
        cout << score << '\t'; 		// Output one score with each iteration 
}
```

## For Each Loops and References:

In the for-each examples provided, element declarations are made by value. This approach means that the loop copies each array value into the variable score during every iteration. Such copying can be computationally expensive, especially when we typically just want a reference to the original element. The solution is to use references.

```c++
int main()
{
    float testScores[5] = { 92.5, 77.0, 88.0, 93.5, 81.0 };
    for (auto &score : testScores) 	// iterate through the array
        cout << score << '\t'; 		// Output one score with each iteration 
}
```

With this approach, each output value references the original array element without making any copies.

Note: Modifying the variable score will reflect changes in the original array.

For those cases when you don't want to alter the array's values, you can make the variable score constant:

```c++

int main()
{
    float testScores[5] = { 92.5, 77.0, 88.0, 93.5, 81.0 };
    for (const auto &score : testScores) 	// iterate through the array
        cout << score << '\t'; 	// Output one score with each iteration 
}
```

## Rule:

In for-each loops, if the variable is of type struct or class (i.e., not basic data types like int, float, char, etc.), always utilize references or const references. This is crucial for performance optimization.

## For-each loop with 2-dimensional array

This code demonstrates how to use a range-based for loop (often referred to as a for-each loop) to iterate through a 2-dimensional array.

```c++

#include <iostream>
using namespace std;

int main()
{
    const int ROWS = 2;
    const int COLS = 5;

    int twoDArray[ROWS][COLS] = { {1, 2, 3, 4, 5 }, {6, 7, 8, 9, 10} };

    for (auto& array1 : twoDArray)
    {
        for (auto& numbers : array1)
        {
            cout << numbers << '\t';
        }
        cout << endl;
    }
    return 0;
}
```

## For-each loop with STL list

The code below demonstrates two methods of iterating through an STL list container. The first method uses a traditional iterator, while the second method utilizes the for-each loop.

```c++

#include <iostream>
#include <string>
#include <list>
using namespace std;	

int main()
{
	list<int> numbers { 1,2,3,4,5 };

	// Using traditional iterator
	for (list<int>::iterator it = numbers.begin(); it != numbers.end(); it++)
	{
		cout << *it << endl;
	}
	
	// Using range-based for loop
	for (auto value : numbers)
	{
		cout << value << endl;
	}

	return 0;
}
```



In the first iteration method, a typical iterator ("it") is utilized to navigate from the beginning to the end of the list. The iterator dereferences the current element using "*it". In contrast, the for-each loop offers a more concise and readable approach by automatically deducing the type of elements in the list and providing direct access to the values.



