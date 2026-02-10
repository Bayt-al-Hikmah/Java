## Objectives
- Working with Strings and Arrays
- Comparison and Logical Operators
- Conditional Statements
- Working with Loops
## Strings & Arrays
### Strings
Strings are a collection of characters in Java. We use them to store names, words, paragraphs, and sentences. A string can contain letters, numbers, symbols, and spaces, Strings are objects, not primitive data types.
#### Creating Strings
There are two main ways to create strings in Java:  
**Using String Literal:** which create string and stores it in the **String Pool** for memory efficiency.
```java
String name = "John";
```
**Using the new Keyword:** This creates a new string object in memory.
```java
String name = new String("John");
```
We can also define a multi-line string using triple quotes instead of single quotes (`""`):
```java
String sentence = """
This is a multi-line
string in Java.
It preserves line breaks.
""";
```
#### String Pool 
The String Pool is a special memory area in Java where string literals are stored.  
Its main purpose is to save memory and improve performance by reusing existing strings instead of creating new ones.
```java
String s1 = "Hello";
String s2 = "Hello";
```
- `"Hello"` is created and stored in the String Pool.
- `s1` points to this string.
- When `"Hello"` appears again, Java does NOT create a new object.
- `s2` points to the same string.
-  Both `s1` and `s2` refer to the same memory location.

Java provides a method called `intern()`, It puts a string into the pool.
```java
String s5 = new String("Hello");
String s6 = s5.intern();
```
#### String Immutability
In Java, strings are immutable, which means their value cannot be changed after they are created, if we assigne new value to string we are creating new string object with the new value and not changing the string value
```java
String text = "Hello";
text = text + " World";
```
A new string `"Hello World"` is created instead of changing `"Hello"`.
#### String Concatenation
We can concate and  join strings together using ``+`` Operator or the ``concat()`` Method.
```java
String result = "Hello" + " " + "World";
String result = "Hello".concat(" World");
```
#### String Methods
The String object come with useful methods to simplify the work with text data.
- `length()`: Returns the length of the string|
- `charAt()`: Returns a character at a specific position
- `toUpperCase()`: Converts to uppercase
- `toLowerCase()`:  Converts to lowercase
- `substring()`:  Extracts part of a string
- `contains()`: Checks if string contains text
- `equals()`: Compares content
- `equalsIgnoreCase()`:  Compares without case sensitivity
- `replace()`: Replaces characters
#### StringBuilder and StringBuffer
String are immutable, each time we edit the value of string we end up creating new one If we do this many times, it wastes memory and reduces performance.  
To solve this problem, Java provides:
- `StringBuilder`
- `StringBuffer`

Both allow us to change strings without creating new objects.

`StringBuilder` is a mutable string class that allows modification.
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
System.out.println(sb);
```
`StringBuffer` is similar to `StringBuilder`, but slower and thread-safe, which means it can be used by multiple threads at the same time without causing errors or incorrect results
```java
StringBuffer sb = new StringBuffer("Hello");
sb.append(" World");
System.out.println(sb);
```
`StringBuilder` and `StringBuffer` give us additional methods when working with string: 
- `append()`: Adds text at the end
- `insert()`: Inserts text at a specific position
- `replace()`: Replaces characters between indexes
- `delete()`: Removes characters between indexes
- `deleteCharAt()`: Removes one character at a position
- `reverse()`: Reverses the sequence of characters
- `charAt()`: Returns a character at a specific position
- `setCharAt()`: Changes a character at a position
- `length()`: Returns the number of characters
- `capacity()`: Returns current storage capacity
- `ensureCapacity()`: Increases minimum capacity
- `substring()`: Extracts part as a String
- `toString()`: Converts to String
### Arrays
Arrays are a collection of elements of the same data type stored in a fixed-size structure.  
They are used to store multiple values in a single variable instead of using many separate variables, They can store, numbers, characters, strings, objects and any other data type.
#### Creating Arrays
To create variable that represent arrays we add `[]` after the data type.
```java
int[] numbers;
String[] names;
```
This only declares the array. No memory is allocated yet, to allocate and create the actual array we use the `new` keyword
```java
numbere = new int[5]
```
This creates an array that can store 5 integers, We can declare and create an array in one line.
```java
int[] numbers = new int[5];
```
When we create an array, Java assigns default values.

| Data Type | Default Value |
| --------- | ------------- |
| int       | 0             |
| double    | 0.0           |
| boolean   | false         |
| char      | '\u0000'      |
| Object    | null          |
We can create and initialize an array directly using curly braces `{}`.
```java
int[] numbers = {10, 20, 30, 40, 50};
String[] names = {"Ali", "Sara", "John"};
```
#### Arrays Immutability
Same as strings, arrays are immutable, which means their value cannot be changed after they are created, if we assigne new value to array we are creating new array object with the new value and not changing the string value
```java
int[] numbers = {10, 20, 30, 40, 50};
int[] numbers = {1, 2, 3, 4, 5};
```
A new array `{1, 2, 3, 4, 5}` is created instead of changing `{10, 20, 30, 40, 50}`.
In Java, arrays are treated as objects, and variables store references to them in memory. If you create an array and assign it to another variable, both variables will point to the same array object.
```java
int[] a = new int[3];
int[] b = a;
```
Both `a` and `b` point to the same array, changing one affects the other.
#### Accessing Array Elements
We access elements of an array using their index. The first element has an index of **0**. After accessing an element, we can read or modify its value.
```java
int[] numbers = {10, 20, 30};

System.out.println(numbers[0]); // 10
numbers[1] = 5;
System.out.println(numbers[1]); // 5
```
#### Array Length
Java provides a property called `length` to get array size.
```java
int[] arr = {1, 2, 3, 4};
System.out.println(arr.length); // 4
```
#### Array Methods
Arrays in Java are objects, and while they don’t have built-in methods like Strings, the **`Arrays`** class in `java.util` provides many useful operations:
- `Arrays.toString()`: Converts the array to a readable string
- `Arrays.copyOf()`: Creates a copy of an array
- `Arrays.sort()`: Sorts the array
- `Arrays.equals()`: Compares two arrays for equality (checks content, not reference)
- `Arrays.fill()`: Fills the array with a value
- `Arrays.binarySearch()`: Searches for a value in a sorted array
- `Arrays.stream()`: Converts array to a Stream for advanced operations (Java 8+)

```java
import java.util.Arrays; // Needed for Arrays utility methods

public class ArrayExample {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 9, 1, 3};
        System.out.println("Length: " + numbers.length);  // Access length

        System.out.println("First element: " + numbers[0]);
        
        Arrays.sort(numbers);
        System.out.println("Sorted: " + Arrays.toString(numbers));

        int[] copy = Arrays.copyOf(numbers, numbers.length); 
        System.out.println("Copy: " + Arrays.toString(copy));

        boolean isEqual = Arrays.equals(numbers, copy);
        System.out.println("Arrays equal? " + isEqual);

        Arrays.fill(copy, 0); 
        System.out.println("Filled copy: " + Arrays.toString(copy));
    }
}
```
#### ArrayList
Arrays in Java have a fixed size. Once created, we can't change their length, This can be a problem if we need a collection that grows or shrinks dynamically.   
To solve this problem, Java provides the `ArrayList` class.   
`ArrayList` is a resizable array that allows us to add, remove, or modify elements without worrying about the size.
```Java
import java.util.ArrayList;

ArrayList<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.add("Cherry");
System.out.println(list); // [Apple, Banana, Cherry]

list.remove("Banana");
System.out.println(list); // [Apple, Cherry]

list.set(1, "Orange"); // Replace element at index 1
System.out.println(list); // [Apple, Orange]
```
`ArrayList` gives us additional methods when working with dynamic arrays:
- `add()`: Adds an element at the end
- `add(index, element)`: Inserts an element at a specific position
- `get(index)`: Returns the element at a position
- `set(index, element)`: Replaces the element at a position
- `remove(index/object)`: Removes an element by index or value
- `size()`: Returns the number of elements
- `contains()`: Checks if an element exists
- `isEmpty()`: Checks if the list is empty
- `clear()`: Removes all elements
- `indexOf()`: Returns the index of the first occurrence of an element
- `toArray()`: Converts the list to an array
#### Multidimensional Array
Arrays in Java can store any type of object, including other arrays. When an array stores other arrays, it creates a multidimensional array. We have already seen 1D arrays, which store elements in a single line.

In 2D arrays, the main array contains arrays as its elements, forming a table-like structure of rows and columns. We access the elements of a 2D array using two indices: the first index for the row and the second index for the column.
```Java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6}
};

System.out.println(matrix[0][1]); // 2
System.out.println(matrix[1][2]); // 6
```
Following same principle we can create 3D 4D arrays and so on.

## Comparison and Logical Operators
### Comparison
These operators compare values and return a boolean (`true` or `false`).

- `>` (Greater than)
- `<` (Less than)
- `==` (Equal to)
- `!=` (Not equal to)
- `>=` (Greater than or equal to)
- `<=` (Less than or equal to)

```Java
System.out.println(5 > 4);        // true
System.out.println(4 == 4);       // true
```
### Logical Operators
We use the logical operators to combine multiple boolean conditions.
#### `||` (OR)
Returns `true` if **at least one** condition is true.
```Java
System.out.println(true || false);  // true
System.out.println(false || false); // false
```
#### `&&` (AND)
Returns `true` only if **all** conditions are true.
```Java
System.out.println(true && true);   // true
System.out.println(true && false);  // false
```
#### `!` (NOT)
Reverses the logical state.
```java
System.out.println(!true);  // false
System.out.println(!false); // true
```
#### Truth Table

|A|B|A && B|A \| B|!A|
|---|---|---|---|---|
|true|true|true|true|false|
|true|false|false|true|false|
|false|true|false|true|true|
|false|false|false|false|true|
## Conditional Statements
Up to this point, our programs have been running in a straight line from the first instruction at the top to the last one at the bottom. However, real-world programs often need more flexibility. Sometimes we want to run certain code only when a specific condition is true, or choose between different paths depending on what is happening in the program. Java provides conditional statements such as if, else if, else, and switch to handle these situations.
### Single Condition with if
Sometimes we want a piece of code to run only when a condition is true. If the condition is false, Java simply skips that block and continues. We can create this with a single `if` block:
```java
int age = 18;

if (age >= 18) {
    System.out.println("You are an adult.");
}
```
We begin with the keyword `if`, followed by the condition in parentheses `()`. After that, we write a block of code in curly braces `{}` that will run only if the condition is true.
### Alternative Path with if-else
We can improve this by adding an alternative path. If the condition is true, one block runs; otherwise, the `else` block runs:

```Java
boolean isRaining = false;

if (isRaining) {
    System.out.println("Bring an umbrella.");
} else {
    System.out.println("No umbrella needed today.");
}
```
The `else` block does not need a condition. It simply runs as the alternative code when the `if` condition is not met.
### Multiple Conditions with else if
When we have more than two possible outcomes, we can chain conditions using `else if`. Java will check them in order and execute the first one that is true:
```Java
int score = 85;

if (score >= 90) {
    System.out.println("Excellent performance");
} else if (score >= 80) {
    System.out.println("Good job");
} else {
    System.out.println("Room for improvement");
}
```
### Ternary Operator
Java provides a concise way to write simple if-else statements in a single line using the ternary operator ``? :``, It is especially useful when you want to assign a value or choose between two options based on a condition.
```java
int age = 17; String status = (age >= 18) ? "adult" : "minor"; 
System.out.println("You are a " + status + ".");
```
### if with a short variable declaration 
Since Java 14, we can declare a variable inside the if condition using pattern matching and local variable declaration.
```Java
if (Integer n = 3; n > 5) {
    System.out.println("n is greater than 5");
} else {
    System.out.println("n is 5 or less");
}
```
Classic / more compatible style :
```Java
int n = 3;
if (n > 5) {
    System.out.println("n is greater than 5");
} else {
    System.out.println("n is 5 or less");
}
```
### The switch Statement
When we need to check a value against multiple possible options, Java provides the `switch` statement. It allows us to write cleaner and more organized code compared to chaining many `else if` conditions. With `switch`, we evaluate a single value and match it against different cases, running the code for the first case that matches:
```Java
String day = "Monday";

switch (day) {
    case "Monday":
        System.out.println("Start of the week");
        break;
    case "Friday":
        System.out.println("Almost the weekend!");
        break;
    case "Saturday":
    case "Sunday":           // multiple values in one case
        System.out.println("It’s the weekend!");
        break;
    default:
        System.out.println("Just another weekday");
}
```
- Each `case` begins with the `case` keyword followed by a value to match.
- `break` is used to exit the `switch` after a case has run; otherwise, Java continues executing the next cases (fall-through behavior).
- The `default` case handles any situation where none of the previous cases match.
### Modern switch 
Since Java 14 and Java 17+ , we can use switch expressions which are much cleaner:
```java
String day = "Monday";

String message = switch (day) {
    case "Monday"     -> "Start of the week";
    case "Friday"     -> "Almost the weekend!";
    case "Saturday", "Sunday" -> "It’s the weekend!";
    default           -> "Just another weekday";
};

System.out.println(message);
```
**Advantages of switch expression**:
- No break needed
- Uses arrow syntax  ``->`` 
- Returns a value that can be assigned to a variable
## Loops
Sometimes we need to repeat an action multiple times for example, processing all elements in an array, performing a calculation repeatedly, or running a block of code until a condition is met. Instead of writing the same code over and over, we use loops. A loop lets us run a piece of code multiple times efficiently. Java provides several types of loops to handle different repeating tasks: `for`, `while`, and `do-while`.
### The Traditional `for` Loop
The traditional `for` loop is used when we know in advance how many times we want to repeat a block of code. It consists of three main parts:
1. Initialization usually creates a counter variable (e.g., `int i = 0`)
2. Condition the loop continues as long as this condition is `true` (e.g., `i < 5`)
3. Update changes the counter after each iteration (e.g., `i++`)
```java
for (int i = 0; i < 5; i++) {
    System.out.println("Count: " + i);
}
```
- The loop starts with `i = 0`
- It runs while `i < 5`
- After each iteration, `i` increases by 1
    
### The Enhanced for Loop 
Java’s enhanced for loop (also called for-each) used to iterate over collections like arrays, ArrayList, or other iterables. It automatically gives us each element one by one no manual index management needed.
```java
String[] fruits = {"apple", "banana", "cherry"};

for (String fruit : fruits) {
    System.out.println(fruit);
}
// Prints:
// apple
// banana
// cherry
```
### The while Loop
We use while loop when we want to repeat code as long as a condition is true, and we don’t necessarily know in advance how many iterations will happen. The condition is checked before each execution.
```java
int i = 0;
while (i < 3) {
    System.out.printf("i is %d\n", i);
    i++;  // Don't forget to update the variable!
}
// Prints:
// i is 0
// i is 1
// i is 2
```
If the condition is initially false, the loop body never runs.
### The do-while Loop
The do-while loop is very similar to while, but it guarantees that the code block executes at least once, because the condition is checked after the body runs.
```java
int j = 0;
do {
    System.out.printf("j is %d\n", j);
    j++;
} while (j < 3);
// Prints:
// j is 0
// j is 1
// j is 2
```
Even if the condition is false from the start, the loop body still executes once:
```
int k = 10;
do {
    System.out.println("This runs once even though k >= 10");
} while (k < 5);
// Still prints the message once
```
### break and continue
Java provides `break` and `continue` to give more control over loops:
- **`break`** immediately exits the loop:
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        break; // stop the loop when i is 3
    }
    System.out.println(i);
}
// Prints 1, 2
```
- **`continue`** skips the current iteration and moves to the next one:
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue; // skip printing when i is 3
    }
    System.out.println(i);
}
// Prints 1, 2, 4, 5
```