## Objectives :
- Introduction to Java and Java Development Kit
- Working with Variables, Data Typse Operators and Constant
- Users Input and Output
## Java Programming:
### Introduction
Java is an object-oriented, statically typed programming language originally developed by Sun Microsystems and now maintained by Oracle. Designed for security, portability, and reliability, it is easy to maintain and remains a cornerstone for building desktop applications, web services, mobile apps (specifically Android), enterprise systems, and large-scale backend architectures.  
Java operates on the core principle of **"Write Once, Run Anywhere" (WORA)**. It achieves this cross-platform compatibility through the Java Virtual Machine (JVM). Once you finish writing your code, the Java compiler converts it into bytecode. The JVM then executes this bytecode, allowing the same program to run on any device or operating system that has a JVM installed.  
As a strictly object-oriented language, Java organizes every program into classes. Every executable application must contain a special entry point known as the `main()` method. By convention, Java source files are saved with the **`.java`** extension.
### Java Development Kit (JDK)
To build and run Java applications, we need the Java Development Kit (JDK). The JDK is a comprehensive software development environment that provides the tools necessary to develop, compile, and debug Java programs. It acts as the master set, containing both the Java Runtime Environment (JRE) which allows programs to run and the development tools like the compiler (`javac`) and debugger.  
The JDK sits at the top of the Java hierarchy. While the JVM is the engine that executes bytecode, the JRE provides the necessary libraries and environment for that execution. The JDK encompasses both, adding the professional tools required to transform human-readable source code into machine-executable bytecode.  
It includes:
- **javac**: The compiler that converts human-readable code into bytecode.
- **java**: The launcher that starts the JVM to run the compiled bytecode.
- **Standard Library (API)**: A vast collection of pre-written classes for tasks like networking, math, and data structures.
- **Javadoc**: A tool for generating documentation from comments.
- **jar**: A tool for packaging aggregated class files.


To get started with Java, install the latest JDK from the official site: https://www.oracle.com/java/technologies/downloads/ or use OpenJDK: https://openjdk.org/.    
After finishing the installation, we can verify that everything is installed correctly by opening the terminal and running the following commands:
```shell
java -version 
javac -version
```
We will use Visual Studio Code (VS Code) to write our programs. We can download and install it from [https://code.visualstudio.com/download](https://code.visualstudio.com/download).
### Running our First Program
Once we have Java and VS Code installed, we are ready to run our first Java program.  
Java programs are made up of classes, and each file usually represents one class. If a class is the entry point of the program and should be executable, it must contain a main method.  
Let’s create a new file named `HelloWorld.java`. Inside this file, add the following code:
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```
We created a `public` class with same name as our file `HelloWorld`, the keyword `public` means that this class can be accessed from anywhere in the program.
Inside the class, we added the `main` method. This method is the starting point of every Java application.
- **`public`**: This ensures the JVM can access the method to start the program.
- **`static`**: This allows the method to be called without creating an instance (object) of the class first.
- **`void`**: This indicates that the method does not return any value.
- **`String[] args`**: This represents command-line arguments. These are inputs we can pass to our program when we run it from the terminal.

Finally inside the `main` method we use **`System.out.println`** to print message in the user terminal.
- `System` is a built-in Java class that allows us to access system-related resources and utilities.
- `out` is an output stream connected to the terminal (standard output).
- `println` prints text to the screen and then moves the cursor to a new line.

Now we can compile our code and generate the bytecode.
```shell
javac HelloWorld.java
```
After compiling the program, Java creates a `.class` file that contains the bytecode. This bytecode can be executed by the Java Virtual Machine (JVM).
```
java HelloWorld
```
This will make JVM excute the bytecode and display **"Hello World!"**  in the terminal.
## Variables and Data Typse
### Variables
Variables are fundamental building blocks in Java programs; they act like labeled containers that store data. These containers can hold different kinds of information, such as numbers, text (strings), and true/false values (booleans).   
Java is a statically typed language. This means that once a variable is declared to hold a certain type of data, it can only hold that type of data. This helps prevent many common bugs.
### DataTypes
Before we start working with variables, it’s important to understand the different types of information that Java allows us to store. Java provides a rich set of data types to represent numbers, text, truth values, collections, and more.

Each data type serves a specific purpose and determines how data is stored and handled in memory. For simplicity, we can divide data types into two main categories:

#### Primitive Data Types
**Primitive Data Types** are the simplest building blocks. They represent a single value, like number (`int`, `float`), logical state (`bool`), or character (`char`), they are divided into:

**Numeric Types:**    
**Integer** used to represent whole numbers without decimal points.
- **byte** (8-bit): Range from `-128` to `127`  
- **short** (16-bit): Range from `-32,768` to `32,767`  
- **int** (32-bit): Most commonly used integer type.
- **long** (64-bit): Used for very large numbers.

**Floating-point** used to represent used to represent decimal values.
- **float** (32-bit): Less precision, uses less memory  
- **double** (64-bit): More precision, default for decimals  

**Boolean Type:** 
The Boolean type it represent truth values., It has only two possible values: `true` and `false`.   
**Character Types:** 
Finally the `char` used to store single characters.
- `char` is a 16-bit Unicode character
- It can store letters, digits, and symbols
#### Reference Data Types
**Reference Types** refer to objects. They do not store the value directly but store a reference (address) to where the data is in memory.

A **String** is a sequence of characters enclosed in double quotes. Although it is used often, it is not a primitive type in Java; it is a Class. Example: `"Hello, World!"`.

An **Array** is a fixed-size collection of elements of the same type. An integer array (`int[]`) might look like `{10, 20, 30}`.

A **Class/Object** represents complex data. If we defined a `Person` class, we could create an instance of it: `Person p = new Person("Alice", 28);`.
### Creating Variables
To create and declare variables in Java, we need two pieces of information: the data type of the variable and the name of the variable.
```java
int age;
```
We can also initialize a variable with a value when creating it by using the assignment operator (`=`):
```java
int age = 25;
```
It is also possible to declare multiple variables on a single line:
```java
int x, y, z;
int hours = 24, minutes = 60, seconds = 60;
```
### Constants
Sometimes, we want to create variables that hold fixed values which do not change while our program is running, such as **Pi**, which has a known constant value. We create these using **constants**. In Java, constants are declared with the `final` keyword.  
By convention, constants in Java are written in `UPPER_SNAKE_CASE` to distinguish them from regular variables.
```java
final double PI = 3.14159;
```
### Comments:
Comments are lines of code that the compiler will ignore. They are used to add explanatory notes and improve the readability of our code. There are two ways to create comments in Java  
#### Single-line comments:
Begin with `//` and continue until the end of the current line. All text following `//` on the same line is ignored by the compiler.
```go
// this single line comment
```
#### Multi-line comments:
Begin with `/*` and end with `*/`. Any text between these two symbols, including multiple lines, will be ignored by the compiler.
```go
/*
	This
	multi-line
	comment
*/
```
### Arithmetic Operators
Java provides basic arithmetic operators for manipulating numbers. These include Addition (`+`), Subtraction (`-`), and Multiplication (`*`).   
Two operators require special attention: **Division (`/`)** and **Modulo (`%`)**.
- When using **Division (`/`)**, the behavior depends on the type. For `double` types, it performs standard decimal division (e.g., `5.0 / 2.0` is `2.5`). For `int` types, it performs integer division, which truncates the decimal part (e.g., `5 / 2` is `2`).
- The **Modulo (`%`)** operator returns the remainder of a division (e.g., `5 % 2` is `1`).

Java also has Increment (`++`) and Decrement (`--`) operators.
```java
public class MathDemo {
    public static void main(String[] args) {
        int a = 10;
        int b = 3;
        
        int sum = a + b;  // 13
        int diff = a - b; // 7
        int prod = a * b; // 30
        
        // Integer division
        int quot = a / b; // 3
        
        // Modulo
        int rem = a % b;  // 1
        
        a++; // a is now 11
        System.out.println("new a = " + a);
    }
}
```
#### Compound Assignment Operators
Java provides a quick and simple syntax for performing arithmetic operations using the current value of a variable and another value, and then storing the result back in the same variable. This is done using compound assignment operators, which combine an arithmetic operation with an assignment (`=`). For example, `a += 4` is equivalent to `a = a + 4`.

This works for the main arithmetic operators:
- `+=` (Add and assign)
- `-=` (Subtract and assign)
- `*=` (Multiply and assign)
- `/=` (Divide and assign)
- `%=` (Modulo and assign)
```java
public class CompoundDemo {
    public static void main(String[] args) {
        int a = 10;
        a += 5; // a is now 15
        a *= 2; // a is now 30
        System.out.println(a);
    }
}
```
### Escape Sequences
**Escape sequences** are special character combinations used to represent hard-to-type or invisible characters within a string or char literal. They start with a backslash (`\`).

Common examples include:

- `\n` (Newline): Moves the cursor to the next line.
- `\t` (Tab): Inserts a tab character.
- `\"` (Double quote): Inserts a literal double quote inside a string.
- `\\` (Backslash): Inserts a literal backslash.
```java
public class EscapeDemo {
    public static void main(String[] args) {
        System.out.println("Hello\nWorld");
        System.out.println("Column1\tColumn2");
        System.out.println("She said, \"Java is fun.\"");
    }
}
```
### Type Conversion
#### Implicit Conversion
Implicit conversion happens automatically when a smaller data type is converted to a larger one. This type of conversion is safe because no data is lost.
```java
int x = 10;
double y = x; // int is automatically converted to double
```
#### Explicit Conversion 
Explicit conversion is required when converting a larger data type to a smaller one. This is done manually using casting and may result in data loss.
```java
double pi = 3.14;
int value = (int) pi; // Decimal part is truncated
```
#### Number to String
In Java, we convert numbers to strings using built-in methods such as `String.valueOf()` or wrapper class methods.
- `String.valueOf(value)` Converts any data type to a string
- `Integer.toString(int)` Converts an integer to a string
- `Double.toString(double)` Converts a double to a string
- `String.format()` Formats numbers as strings
#### String to Number 
Converting a string to a number in Java is called parsing. This process can fail if the string does not contain a valid number.  
Java provides parsing methods in wrapper classes such as `Integer`, `Double`, and `Float`. These methods throw exceptions if the conversion fails.
- `Integer.parseInt(String)` → `int`
- `Double.parseDouble(String)` → `double`
- `Float.parseFloat(String)` → `float`
- `Long.parseLong(String)` → `long`
## User Input and Output
Our programs aren't complete without interacting with users. So far, we've seen how to create variables, but all our data has been "hard-coded" (written directly into the program). Java offers us ways to get information and data from the user and also ways to display information back _to_ the user's screen.
### Displaying Output to the User
We use `System.out` to write to the console.
- **`System.out.println()`**: Prints the content followed by a **new line**.
- **`System.out.print()`**: Prints the content **without** a new line.
- **`System.out.printf()`**: Allows for formatted output using specifiers like `%s` (string), `%d` (integer), and `%f` (float).

```java
public class OutputDemo {
    public static void main(String[] args) {
        String name = "Alice";
        int age = 30;
        
        System.out.println("Hello User");
        System.out.printf("Name: %s, Age: %d\n", name, age);
    }
}
```

### Getting Input from the User
To get input, we use the **`Scanner`** class from the `java.util` package. We must import it first. We create a `Scanner` object connected to `System.in` (the keyboard).   
Different methods are used for different data types:
- **`next()`**: Reads a single word (stops at space).
- **`nextInt()`**: Reads an integer.
- **`nextDouble()`**: Reads a double.
- **`nextLine()`**: Reads the entire line of text including spaces.
```java
import java.util.Scanner; // Import the Scanner class

public class InputDemo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter your age: ");
        int age = scanner.nextInt();
        
        System.out.printf("You are %d years old.\n", age);
        
        // Always close the scanner when done
        scanner.close(); 
    }
}
```
A common issue arises when mixing `nextInt()` and `nextLine()`. `nextInt()` reads the number but leaves the newline character (Enter key) in the buffer. If we  call `nextLine()`, it will read that leftover newline and finish instantly. To fix this, we add an extra `nextLine()` to consume the leftover newline.

```java
import java.util.Scanner;

public class FullLineDemo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter ID: ");
        int id = scanner.nextInt();
        
        // Consume the leftover newline
        scanner.nextLine(); 
        
        System.out.print("Enter full name: ");
        String fullName = scanner.nextLine();
        
        System.out.println("ID: " + id + ", Name: " + fullName);
    }
}
```
## Tasks:
### Task 1:
Write a Java program that reads the radius of a circle from the user (as a `double`) and then displays its surface area. (Area = $\pi \times radius^2$). You can use the constant `Math.PI` from the `java.lang.Math` class.
**Hint:**
First import it using
```java
import java.lang.Math;
```
Then you can access to PI value using
```java
Math.PI
```
### Task 2:
Write a Java program that reads the temperature in Fahrenheit and converts it to Celsius.
$$Celsius=\frac{5}{9}×(Fahrenheit−32)$$