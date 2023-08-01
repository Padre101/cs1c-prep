# Table of Content's
- [Classes](#classes)
- [Access Levels Explained](#access-levels-explained-ex-public)
- [Objects](#objects)
- [Constructors/Destructors](#constructorsdestructors)
- [Encapsulation](#encapsulation)
- [Inheritance](#inheritance)
- [Abstraction](#abstraction)
- [Polymorphism](#polymorphism)
- [Storage Duration and Scope in C++](#storage-duration-and-scope-in-c)
- [Accessor/Mutator Functions](#accessormutator-functions)
- [Constant Member Functions (Const Methods)](#constant-member-functions-const-methods)
- [Abstract Data Types (ADT)](#abstract-data-types-adt)
- [Inline Functions in C++](#inline-functions-in-c)
- [Static Members](#static-membersmembers-are-variablefunction-in-classes)
- [Class Invariants](#class-invariants)
- [Namespace](#namespace)

# Disclaimer
This goes over the basics of OOP including classes, object, encapsulation, abstraction and inheritance , except for polymorphism which will have its own notes


*When a class is instantiated, it means that an object of that class is created.*
*when I declare something i create it(Declaration). when i initialize something it means i give it a value(Initialization)*


OOP is a paradigm(a way of doing something). Procedural programming paradigm is like task by task whereas OOP paradigm is like having multiple actors(objects) with different jobs and making a world where they all work together.

OOP is a paradigm based off objects, classes help make up objects. And these objects interacting is what primarily makes up oop

# Classes

Class is composed of two main things: attributes and methods 
A class is like a blueprint or a template for creating objects. It defines what **attributes** (data) and **methods** (behavior) any object created from the class will have

In class notes both attributes and methods are combined and called “class member” but its same shit just combining the words

**Attributes** (also known as fields or properties) are variables defined within a class. They represent the data or state of an object created from the class.

**Methods** are functions defined within a class. They represent the behaviors or actions that an object can perform. 

this is an example of a class:

```c++
*if you remove the access specifier(public:) that access level is private: by default 

class Dog {
public:
    // Attributes
    string name;
    string breed;
    int age;

    // Methods
    void bark() {
        cout << "Woof!" << endl;
    }

    void describe() {
        cout << "The dog's name is " << name << ", it is a " << breed << " and it is " << age << " years old." << endl;
    }
};
```

# access levels explained (ex. public:)

There are three access levels in C++:

public: Members declared under public can be accessed from anywhere the object is accessible. This is the least restrictive access level.

protected: Members declared under protected can be accessed by the class itself, its subclasses (if any), and its friend classes/functions (a special type of relationship that allows another class or function to access private and protected members of the class). This is more restrictive than public.

private: Members declared under private can only be accessed by the class itself and its friend classes/functions. This is the most restrictive access level, and it's also the default in C++ if no access level is specified.

Here's an example:

```c++
class MyClass {
private:   // Private access specifier
    int myPrivateAttribute;

public:    // Public access specifier
    int myPublicAttribute;
};
```

In this example, myPrivateAttribute can only be accessed from within MyClass, while myPublicAttribute can be accessed from anywhere an object of MyClass is accessible.

*If all member variables of a class are	public and	there are no member	functions use a struct instead*

# Objects

“An object is an instance of a class” means that an object is made based out of what the class is made of. You can’t have an object without a class. You cant have a house(object) without a blueprint(class). You create objects from a class

An object is an instance of a class. It has the attributes and methods defined by the class, but can also hold its own specific values for the attributes.

## creating/instantiating object syntax(instantiating an object)

```c++
NameofClass objectName;
```

## Accessing an Object

the dot (.) operator is used to access the methods and attributes of an object.

When you create(instantiate) an object of a class, you can use the dot operator to access its members. Here's the syntax:

```c++
objectName.memberName
```

```c++
for Ex.
myCar.color = "Red"; //accesing class attribute
myCar.speed = 60; //accesing class attribute
myCar.displayInfo();  // Accessing a method using the dot operator

You treat the method the same as a function: if it returned a value you would just do:

int result = math.add(5, 3);  // Invoking(calling) the method and storing the returned value
```

# Constructors/destructors 

These are functions(methods) without a return type(void,int, etc) defined in the class that has the same name as the class

Think of it like a void function, where you pass whatever you want to initalize. Then you just call it and thats it

Constructors	guarantee that 	data members are initialized when an object	is declared
– A default constructor has no parameters

Their useful when you would have to initialize multiple variables and object from the same class.


A non default constructor is called an alternate/overload constructor 

## Default constructor

When you create a class, a constructor is made by default. And the values of the attributes(variables) in my class are uninitialized in the default constructor. 

For ex.

```c++

class Example {
private:
    int num;
    float value;
    std::string name;

public:
    // Default constructor is implicitly provided
    // No need to explicitly define it
};

int main() {
    Example example;  // Object of the Example class

    // Values of data members after default initialization:
    // num is 0. value is 0.0. name is "" (empty string)

    // ...
    return 0;
}
```
## initialization list(part of a constructor)

The initialization list initializes attributes when an object is created from a class. This is because the initialization list is part of the constructor of the class, and the constructor is invoked when an object is instantiated. In this process, the initialization list provides the initial values for the attributes, setting up the initial state of the object.

```c++
Here's the syntax:
*members are attributes here

class ClassName {
    // ... class members ...

public:
    ClassName(Type1 arg1, Type2 arg2)
        : member1(arg1), member2(arg2)  // This is the initializer list
    {
        // ... constructor body ...
    }
};
```

The part after the colon ```: member1(arg1), member2(arg2)``` is the initialization list. It directly initializes member1 and member2 with the values of arg1 and arg2, respectively, at the moment the ClassName object is created. The initialization list ends when the constructor body begins (denoted by {).

To instantiate an object of ClassName, you'd simply call the constructor and pass in the appropriate arguments. Here's how it would look:

```c++
ClassName obj(arg1_value, arg2_value);
```

## Destructor
Destructors are special member functions in C++ that are responsible for cleaning up resources allocated by an object when it goes out of scope or is explicitly destroyed. They are opposite to constructors, which initialize the object's state.

The syntax for a destructor is exactly the same as a constructor, but their’s is a tilde(~) before the name.


1. Their functions without a return type
2. A class can only have one destructor
3. They take no parameters: ()
 *Invoked just means “to call”*
4. The destructor is automatically invoked when the object goes out of scope.

*When an object is out of scope that means it’s braces end*


Once the destructor is executed, the object's lifetime has ended, and it is considered destroyed. Attempting to use the object after its destructor has been called would result in undefined behavior.

## summary I literally made of destructors, in my own words
Destructors are special functions that clean up resources used when making an object. A class can only have one destructor.  When an object goes out of scope(its braces end) the destructor will be automatically executed. When a destructor executes on an object, it can no longer be used since its lifetime(same as scope?) has ended and its considered deleted. If you have multiple objects from the same class, each object will have its own destructor(which has the same implementation as the one you defined) associated with it. If you don't create a destructor the c++ compiler will make one for you and will function the same as above. 

for example:

```c++

class Example {
public:
    // Constructor
    Example() {
        // Initialization code, if needed
    }

    // Destructor
    ~Example() {
        // Cleanup code
    }
};
int main() {
    {
        Example obj;  // Object of the Example class

        // Use obj...
    }  // obj goes out of scope, destructor automatically executed

    // ...

    return 0;
}
```

# encapsulation

encapsulation is a relatively straightforward concept in object-oriented programming (OOP), but its simplicity belies its power and importance. It provides several key benefits that are fundamental to good OOP design:

## tldr
encapsulation is just the process of bundling attributes and methods in a class. Also specifying the access levels of them. By creating a class you're already doing this.

## real explanation

Encapsulation is a fundamental concept in object-oriented programming. It's the practice of keeping fields (attributes) and methods within a class, making it self-contained to prevent any outside interference and misuse of data.

The main benefit of encapsulation is the ability to modify our implemented code without breaking the code of others who use our code. With this feature, Encapsulation gives maintainability, flexibility, and extensibility to our code.

Encapsulation also leads to data hiding as it prevents outsiders from accessing the inner workings of a class. This is achieved by making the class attributes private or protected and providing public get and set methods (often called getters and setters) to access and modify the private variables.

```c++

class EncapsulatedDog {
private:   // Encapsulated attributes
    string name;
    string breed;
    int age;

public:
    // Setter methods
    void setName(string n) {
        name = n;
    }
    
    void setBreed(string b) {
        breed = b;
    }

    void setAge(int a) {
        age = a;
    }

    // Getter methods
    string getName() {
        return name;
    }
    
    string getBreed() {
        return breed;
    }

    int getAge() {
        return age;
    }
};

```

In this example, the data (name, breed, and age) is hidden from outside access. It can only be accessed and modified via the provided public methods. This is a basic example of encapsulation.



# inheritance
Inheritance is the process of creating a new class (called the derived class or subclass) from an existing class (called the base class or superclass). This helps reduce code size

“Is a” relationship means a derived class inherits traits/properties from base class. A triangle class inherits  from shape(base) class

The derived class inherits the properties and behaviors of the base class and can add its own additional attributes and methods or modify the inherited ones. 

private members of a base class are private to the base class(meaning only base class can acces it)
– Derived class cannot directly access them

## "public members of the base class are inherited as public/private members"

this statement means that the public members of the base class become part of the derived class and their access level in the derived class is determined by the type of inheritance. If the inheritance is public, they remain public in the derived class. If the inheritance is private, they become private in the derived class.

```c++
An example of this is 
class Base {
public:
    int x;
};

class DerivedPublic : public Base {
    // x is inherited as a public member
};

class DerivedPrivate : private Base {
    // x is inherited as a private member
};
```

## “The derived class can include additional members (data and/or functions)”

this means I can define methods in the derived class. Meaning a derived class will contain all the members of the base class(unless its private) and the members in its own class. This means if i have a method in the base class thats public. You can call that method in 2 ways: using an object of the base class, and using the object of the derived class.

For example if u have these 2 classes:

```c++
class Animal {  // This is the base class
public:
    void eat() { std::cout << "I'm eating generic food."; }
};

class Cat : public Animal {  // Cat is derived from Animal
public:
    void meow() { std::cout << "Meow!"; }  // Additional member function
};
```

You can create an object of the Animal class and call eat() on it:

```c++
Animal anAnimal;
anAnimal.eat();  // Outputs: "I'm eating generic food."
```

And you can also create an object of the Cat class and call eat() on it as well, thanks to inheritance:

```c++
Cat aCat;
aCat.eat();  // Outputs: "I'm eating generic food."
```

### Overriding method

if you have overridden a method in a derived class and you want to specifically call the base class version of that method from the derived class, you use the scope resolution operator :: with the base class name to do so.
This tells the compiler that you want to use the version of the method defined in the base class, not the version defined in the derived class.

Here's an example:
```c++
class Base {
public:
    void sayHello() { std::cout << "Hello from Base!\n"; }
};

class Derived : public Base {
public:
    void sayHello() { std::cout << "Hello from Derived!\n"; }
    void sayBaseHello() { Base::sayHello(); }
};

int main() {
    Derived d;
    d.sayHello();       // This will output "Hello from Derived!"
    d.sayBaseHello();   // This will output "Hello from Base!"
    return 0;
}
```

## "The derived class can redefine public member functions of the base class - Applies only to the objects of the derived class."

is just saying that the derived class can redefine/override methods. The overridden function in the derived class must have the same name, return type, and parameters as the function in the base class. This new definition of the function will be used for objects of the derived class, while objects of the base class will continue to use the original version.

For example: 

```c++
class Base {
public:
    void sayHello() { std::cout << "Hello from Base!\n"; }
};

class Derived : public Base {
public:
    void sayHello() { std::cout << "Hello from Derived!\n"; } // Overriding sayHello
};

int main() {
    Base b;
    b.sayHello(); // Outputs: "Hello from Base!"

    Derived d;
    d.sayHello(); // Outputs: "Hello from Derived!"
}
```

## "All member variables of the base class are also member variables of the derived class" 
 
 is just saying that a derived class inherits the member variables of the base class . If a base class has a public or protected member variable, and a class is derived from that base class, then that member variable can be accessed in two ways:

1. Through an object of the base class
2. Through an object of the derived class

*private members of a base class are private to the base class*

*A derived class cannot directly access private members of it base class – To give it direct access, declare that member as protected 
*

## inheritance syntax

the syntax for inheritance involves specifying the base class after a colon (:) in the derived class declaration. So similar to normal syntax but you add  “: accessSpecifier BaseClassName” after the class name Here's the general syntax:

```c++
class DerivedClassName : accessSpecifier BaseClassName {
    // Additional members and functions of the derived class
};
```

DerivedClassName is the name of the derived class.

accessSpecifier specifies the access level for the inherited members from the base class. It can be public, protected, or private. This determines how the inherited members are accessible within the derived class and its derived classes.

BaseClassName is the name of the base class from which the derived class is inheriting

# abstraction
 
Abstraction refers to the process of hiding unnecessary details and presenting only essential information to the users or clients. and exposing only the essential aspects, providing a simplified view code.

Data abstraction refers to, providing only essential information to the
outside world and hiding their background details, i.e., to represent the
needed information in program without presenting the details.

For example, a database system hides certain details of how data is
stored and created and maintained. Similar way, C++ classes provides
different methods to the outside world without giving internal detail about those methods and data

Idk How to actually implement this in oop, ill add when i need to use it

# polymorphism
Polymorphism in C++ is the ability of objects of different classes, derived from a common base class, to be treated as objects of the base class. It allows you to write code that can work with objects of different classes interchangeably, providing a high degree of flexibility and code reusability.

Idk How to actually implement this in oop, ill add when i need to use it; i just know you use pointers


# Storage Duration and Scope in C++

 In C++, the terms **automatic** and **static** are used in the context of both storage duration and variables. 
 
 **Automatic variables** are variables that get automatically allocated and deallocated, while **static variable** maintain their values between function calls. :

When we say that **Automatic variables** are variables that get automatically allocated and deallocated," we mean that memory for these variables is allocated when they're declared and it is deallocated when they go out of scope, or when the block of code in which they're declared is done executing.

 ```c++

#include<iostream>
using namespace std;

void auto_example() {
    int auto_var = 0; // Automatic variable
    auto_var++;
    cout << "Automatic variable: " << auto_var << endl;
}

void static_example() {
    static int static_var = 0; // Static variable
    static_var++;
    cout << "Static variable: " << static_var << endl;
}

int main() {
    for(int i=0; i<5; i++) {
        auto_example();
        static_example();
    }
    return 0;
}

```

In the `auto_example` function, `auto_var` is an automatic variable. This means it is created each time `auto_example` is called and destroyed each time the function ends. As a result, its value is always initialized to `0` and then incremented to `1` each time `auto_example` is called.

In contrast, `static_var` in the `static_example` function is a static variable. It is initialized to `0` only once, when the function is called for the first time. In subsequent calls to `static_example`, `static_var` is not reinitialized; instead, it retains its previous value, which is then incremented each time the function is called.

The output of this program would be:

```c++
Automatic variable: 1
Static variable: 1
Automatic variable: 1
Static variable: 2
Automatic variable: 1
Static variable: 3
Automatic variable: 1
Static variable: 4
Automatic variable: 1
Static variable: 5
```

This shows that the automatic variable is reset each time its function is called, while the static variable maintains its value across function calls.



 ## Understanding Storage Duration

- When we say "declaration is reached," we're referring to the point in the program execution where a variable or an object is declared.
- The lifetime of a variable or an object, meaning when it's created and destroyed, is defined by its **storage duration**.
- There are two main types of storage duration: **automatic** and **static**.

### Automatic Storage Duration

- Variables or objects with automatic storage duration are created when their declaration is reached and destroyed when the control flow leaves the scope (block of code) where they're declared. These are typically local variables or objects.

Here is an example:

    ```c++
    void someFunction() {
        int autoVar = 5;  // This is a variable with automatic storage duration
    }
    ```

### Static Storage Duration

- Variables or objects with static storage duration are created when their declaration is reached and destroyed when the program ends. These are typically global variables or objects or local variables declared with the `static` keyword.

- Here is an example:

    ```c++
    void someFunction() {
        static int staticVar = 0;  // This is a variable with static storage duration
        staticVar++;
        cout << staticVar << endl;
    }
    ```

## Understanding Scope

- The part of the code where a variable or an object can be accessed is defined by its **scope**.
- There are two main types of scope: **local** and **global**.

### Local Scope
If a variable or an object is declared within a function or block, it can only be accessed from within that function or block. This is known as local scope.

### Global Scope
If a variable or an object is declared outside all functions, it can be accessed from any part of the code. This is known as global scope.

## Putting them both(scope and storage duration) Together
A variable or an object declared within a function or block without the static keyword has automatic storage duration and local scope. This variable is also referred to as an **automatic variable.**

A variable or an object declared within a function or block with the static keyword has static storage duration but still local scope. This variable is also referred to as a **static variable.**

A variable or an object declared outside all functions has static storage duration and global scope, and is called global variable

Remember: Access specifiers (public, private, protected) in classes control the accessibility of the class members, not their storage duration or scope.

# accessor/mutator functions

An accessor function is just a method that accesses attributes(member variables) of a class

An mutatior function is just a method that modifies attributes(member variables) of a class

# Constant Member Functions (Const Methods)

A constant member function (or const method) is a method that guarantees it will not modify any of the class's member variables (or call any non-const member functions). These functions are typically used for operations that should not alter the state of the object they are called on.

The syntax for declaring a const method in C++ is as follows(same as normal but add const in the end):

```c++
return_type function_name() const {
    // Function body
}
```

For example, let's say we have a class called Example with a const method getValue() that returns an integer:

'''c++
class Example {
public:
    int getValue() const {
        // Function body
    }
}
``

# Abstract Data Types (ADT)

An Abstract Data Type (ADT) is a concept that separates the logical properties (what it can do) from the implementation details (how it's implemented in code). In the context of object-oriented programming (OOP), an ADT typically takes the form of a class or a structure.

ADTs are used to represent concepts or entities by encapsulating the associated data and operations that can be performed on that data.

Three components are associated with an ADT:

1. **Type name:** The name of the ADT.
2. **Domain:** The set of values belonging to the ADT. In the context of OOP, this would correspond to the class's attributes or member variables.
3. **Set of operations:** The operations that can be performed on the data. In the context of OOP, these would be the methods of a class.

# Inline Functions in C++

An inline function in C++ is a function that is defined directly within the class definition. Instead of separating the function declaration and definition into different parts (like in a header file and an implementation file), the function's definition is provided within the class definition itself.

Inline functions are primarily used to suggest to the compiler that it should generate code (inline code) in place of the function call. This can eliminate the overhead of a function call. 

This strategy is particularly useful when the function contains a very short piece of code. Inlining a large function can increase the size of the binary, which could potentially impact performance negatively.

# Static members(members are variable/function in classes)

An instance of a class, is just an object from that class

So syntaxwise, static members are just regular members with a static keyword before them. And you access them with scope resolution operator(::) instead of dot operator

When you declare a member function or variable as static, it means that it belongs to the class itself, rather than being associated with individual objects (instances) of the class. Static members are shared among all instances of the class.

Unlike non-static member variables, which require the existence of an object to be accessed, static member variables exist even if there are no objects (instances) of the class. They are associated with the class itself rather than with any specific instance. This means you can access static member variables using the class name, even without creating an object of that class.

	1.	Multiple objects of a class each have their own copy of non-static member variables: When you create multiple objects (instances) of a class, each object maintains its own copy of non-static member variables. Non-static member variables are unique to each object, meaning that changes to one object’s non-static member variable do not affect the same variable in other objects.
	2.	All objects of a class share any static member of the class: In contrast to non-static members, static members of a class are shared among all objects (instances) of that class. Regardless of the number of objects created, there is only one instance of each static member variable or function in memory. Any changes made to a static member variable are visible to all objects of the class. Similarly, static member functions are not associated with any specific object and can be called using the class name.

Instance variables are non static attributes in a class. So pretty much a “normal” variable in a class.

# Class Invariants 

Its means an object is in a valid space for its entire lifetime

the key idea of class invariants is that Data members have to be in valid states in all time, so you expect expected behavior rather than undefined behaviors

Key features of class invariants:
1. **Validity of object states:** The class invariant guarantees that the object's data members are in valid states at all times. This ensures that you can expect predictable behavior rather than undefined behaviors.
2. **Established during construction:** Class invariants are typically established during the construction of an object and should be preserved by all member functions of the class.

By maintaining the class invariant, you ensure the stability and predictability of the object's state, which can help to prevent bugs and simplify the debugging process.

# namespace

A namespace is a feature in C++ that allows you to group related code elements, such as classes, functions, variables, and other namespaces, into a named scope.

Namespaces are used to organize code into logical groups and to prevent name collisions that can occur especially when your code base includes multiple libraries.

```c++
namespace namespace_name { // Declarations and definitions of code elements (classes, functions, variables, etc.) }
```

You access code elements from the namespace using the scope resolution operator ::

here's and example:

```c++
namespace MyNamespace {
    int myVar = 5;
    void myFunction() {
        std::cout << "Hello from MyNamespace!" << std::endl;
    }
}

int main() {
    std::cout << MyNamespace::myVar << std::endl;  // Accessing variable from MyNamespace
    MyNamespace::myFunction();  // Calling function from MyNamespace
    return 0;
}
```

In the example above, MyNamespace::myVar and MyNamespace::myFunction() are used to access the myVar variable and myFunction() function in MyNamespace, respectively.

Note that using the using keyword, you can make a namespace's contents directly 





