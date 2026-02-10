## Objectives
- Introduction to Object-Oriented Programming
- Working with Interfaces, Enums and Packages
## Object-Oriented Programming
Java follows the Object-Oriented Programming (OOP) paradigm, where we organize our code using classes and objects.
- **Classes**: A class is a blueprint that defines the structure and behavior of objects. For example, a `Car` class defines that all cars will have properties such as color and model, and behaviors such as being driven.
- **Objects**: An object is a self-contained entity created from a class. For example, we can create a `Car` object with specific data using the `Car` class. Each object has its own color and model. We can create multiple car objects, each with different values.
### Creating Our First Class:
To define a class, we use the `class` keyword followed by the class name and a pair of curly braces `{}`. Inside these braces, we write the body of the class, which includes its attributes and methods.  
Before declaring these attributes and methods, we specify their **visibility** using access modifiers such as `public`, `private`, or `protected`.
- Attributes represent the data and information that our class will have they are declared similarly to normal variables.
- Methods represent the functions and actions our class will perform.

In Java, each class is usually defined in its own file. Let’s create a file named `Person.java`. Inside this file, we define a public `Person` class.  
This class has two public attributes: `name`, which is a `String`, and `age`, which is an `int`. After that, we create a public method called `introduce` that displays the person’s name and age.
```java
public class Person {

    public String name;
    public int age;

    public void introduce() {
        System.out.println("Hi, my name is " + name + " and I am " + age + " years old.");
    }
}
```
Now we can create an object using our class. We do this by using the class name as the data type  and the `new` keyword to create a new instance of the class.
```java
public class Example1 {
    public static void main(String[] args) {

        Person teacher = new Person();
        me.name = "Alice";
        me.age = 30;
        me.introduce();
    }
}
```
To access an object’s **attributes** and **methods**, we use **dot notation** (`.`). For example, `teacher.name` accesses the `name` attribute, and `teacher.introduce()` calls the `introduce` method.
### Constructor
In our previous example, we created an object and then set its `name` and `age` manually. This is not a good practice because if we forget to do this, those attributes will keep their default values (`null` for `String` and `0` for `int`). Java solves this problem by using constructors.  
A constructor is a special method that is called automatically when an object is created. It is mainly used to initialize the object’s attributes.
- A constructor has the same name as the class.
- It does not have a return type, not even `void`.
- It can have parameters, which receive values when the object is created.
- These parameters are usually used to initialize the object’s attributes.
```java
public class Person {

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void introduce() {
        System.out.println("My name is " + name + " and I am " + age + " years old.");
    }
}
```
Here, we set the `name` and `age` attributes to be `private`, which means they cannot be accessed or modified directly from outside the class.   
We also created a `Person` constructor that takes two arguments: `name` and `age`. Inside the constructor, these values are assigned to the object’s attributes, we achieved that by using the `this` keyword, which refers to the current object. It allows us to distinguish between the class attributes and the constructor parameters.
```java
public class Example2 {
    public static void main(String[] args) {

        Person teacher = new Person("Alice", 30);
        me.introduce();
    }
}
```
### Static Members
Sometimes, when we design classes, we want to access certain attributes or methods without creating an instance (object) of the class. These elements are called static members. In Java, we declare attributes or methods as static using the `static` keyword.
```Java
public class Circle {

    public static final float PI = 3.14f;

    public static float surface(float r) {
        return r * r * PI; 
    }
}
```
Here, we created a `Circle` class that has two static members: the `PI` attribute, which stores the value of π, and the `surface` method, which takes the radius as a parameter and calculates the area of the circle.
```java
public class Example2 {
    public static void main(String[] args) {

        System.out.println(Circle.PI);
        System.out.println(Circle.surface(10));
    }
}
```
### Working with Methods
Methods represent the **actions** that a class or its objects can perform. To create a method, we need two main pieces of information:
1. The return type the data type of the value the method will return after execution.
2. The parameters  the inputs the method will take to perform its task.
```java
public class Calculator {

    public static int add(int a, int b) {
        return a + b;
    }
    public static int multiply(int a, int b) {
        return a * b;
    }
}
```
To use a method, we write the object or class for static methods followed by a dot (`.`), then the method name, and finally parentheses containing any arguments we want to pass to the method.
```java
public class Example3 {
    public static void main(String[] args) {

        System.out.println(Calculator.add(4,5));
        System.out.println(Calculator.multiply(2,10));
    }
}
```
#### Method Overloading
The `add` method has a small limitation: it works only for integers because it takes `int` parameters and returns an `int`. We could create separate methods for `float` or `double` and give them different names, but this would make our class unnecessarily complex with many methods that perform the same calculation.  
Java provides a solution for this using method overloading. With overloading, we can implement multiple methods with the same name but different parameter types or numbers. When we call the method, Java automatically determines which version to use based on the arguments we pass.
```java
public class Calculator {

    public static int add(int a, int b) {
	    System.out.println("adding int");
        return a + b;
    }
    public static double add(double  a, double  b) {
	    System.out.println("adding double");
        return a + b;
    }
    public static float add(float a, float  b) {
	    System.out.println("adding float");
        return a + b;
    }
}
```
Now we can call our method and pass different values. Java will automatically call the version of the method that matches the arguments we provide.
```java
public class Example4 {
    public static void main(String[] args) {
		System.out.println(Calculator.add(1, 2));
        System.out.println(Calculator.add(1.0, 2.0));
        System.out.println(Calculator.add(1.0f, 2.0f));
    }
}
```
#### Working with Varargs
The `add` method currently adds only two numbers. But what if we want to create a method that calculates the sum of any number of numbers? This method should be able to accept an arbitrary number of arguments whether the user provides one, two, or more.  
Java allows us to do this using varargs. We specify the data type of the parameter followed by three dots (`...`). This tells Java to take all the arguments provided by the user and store them in an array, which we can then process inside the method.
```java
public class Calculator {

    public static int sum(int... numbers) {
        int result = 0;
        for (int number: numbers){
            result += number;
        }
        return result;
    }
}
```
Now we can use our method
```java
public class Example5 {
    public static void main(String[] args) {
		System.out.println(Calculator.sum(1, 2,7,9,10));
    }
}
```
#### Recursive Methods
Recursive methods are special methods that have ability to call theirself untill a condition (that we call base state) is valid.   
lets suppose we want to create a function that calculate factorial of numbers  
we know that:

- 0! is equal to 1
- 1! is equal to 1=1\*0!
- 2! is equal to 2\*1=2\*1!
- 3! is equal to 3\*2\*1\=3\*2!
- 4 is equal to 4\*3\*2\*1=4*3!
- 5! is equal to 5\*4\*3\*2\*1 = 5\*4!

With that in mind, we can set the base condition as, if n == 0 we return 1,else we return n multiplied by the factorial of n-1
```java
public class Calculator {

    public static int fact(int n) {
        if(n == 0){
	        return 1;
        }
        return n * fact(n-1);
    }
}
```
We can test it like this:
```Java
public class Example5 {
    public static void main(String[] args) {
		System.out.println(Calculator.fact(5));
    }
}
```
### Object-Oriented Programming Pillars
We explored how to define classes and objects and how to work with methods and attributes. Now, we can dive into the four core pillars of object-oriented programming.
#### Inheritance
Inheritance represents the ability of a class to extend another class by inheriting its methods and attributes and then adding more functionality.   
For example, imagine we want to create `Cat` and `Dog` classes. We could create them separately, and both classes would have `name` and `age` attributes. They would also have a `speak()` method, but with different implementations.
```java
class Cat {
    String name;
    int age;
    public Cat(String name, int age, String ownerName) {
        this.name = name;
        this.age = age;
        this.ownerName = ownerName;
    }

    public void speak() {
        System.out.println("Meow");
    }
}

class Dog {
    String name;
    int age;
    public Dog(String name, int age, String ownerName) {
        this.name = name;
        this.age = age;
        this.ownerName = ownerName;
    }

    public void speak() {
        System.out.println("Woof");
    }
}
```
However, if we later decide to add a new attribute, such as `ownerName`, we would need to modify both classes. This leads to duplicated work and makes the code harder to maintain.     
A better solution is to use inheritance. Instead of creating only `Cat` and `Dog` classes, we can create a parent class called `Pet`. This class contains all the shared attributes and methods that both cats and dogs have.   
Then, when we create the `Cat` and `Dog` classes, we simply extend the `Pet` class and add only the features that are specific to each animal.
```java
class Pet {
    String name;
    int age;
    String ownerName;

    public Pet(String name, int age, String ownerName) {
        this.name = name;
        this.age = age;
        this.ownerName = ownerName;
    }

}

// Child class
class Cat extends Pet {
    public Cat(String name, int age, String ownerName) {
        super(name, age, ownerName);
    }
    public void speak() {
        System.out.println("Meow");
    }
}

class Dog extends Pet {
    public Dog(String name, int age, String ownerName) {
        super(name, age, ownerName);
    }
    public void speak() {
        System.out.println("Meow");
    }
    public void speak() {
        System.out.println("Woof");
    }
}
```
We inherit from a class using the `extends` keyword. When a class inherits from another class, it can call the parent class constructor using the `super` keyword.     
When we inherit from a class in Java, we do more than just reuse its attributes and methods. We can also override the methods of the parent class in our subclass. This means we can change how a method works by writing completely new logic, or we can reuse the existing implementation and add extra logic to it.
For example, suppose we are creating a `StrayCat` class that extends the `Cat` class. We can override the `speak()` method. Inside this method, we can call the parent class’s `speak()` method using `super`, and then add our own additional behavior.
```java
class StrayCat extends Cat {
    public StrayCat(String name, int age, String ownerName) {
        super(name, age, ownerName);
    }
    @Override
    void speak() {
        super.speak();
        System.out.println("The stray cat sounds tired and hungry.");
    }
}
```
#### Encapsulation
Encapsulation is one of the main pillars of Object-Oriented Programming (OOP). It means hiding the internal details of an object from the outside world and allowing access only through well-defined and controlled methods.  
We achieve encapsulation by using access modifiers in our classes and methods. In Java, the following access modifiers are available:
- `public`: Accessible from anywhere in the program.
- `protected`: Accessible within the same package and subclasses, even if they are in different packages.
- `default`: Accessible only within the same package. Used when no access modifier is specified.
-  `private`: Accessible only within the same class.

```java
class Person {
    private String name;
    private int age;

    // Public constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

}
```
To access and modify an object’s attributes, we use **getter and setter methods**. These methods provide a controlled way to read and update private variables while maintaining encapsulation.
- **Getters** are used to retrieve (get) the value of a variable.
- **Setters** are used to update (set) the value of a variable, often with validation to ensure the data remains valid.
```java
class Person {

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setAge(int age) {
        if (age > 0) { // Validation
            this.age = age;
        }
    }
}
```
#### Abstraction
Abstraction is another fundamental pillar of Object-Oriented Programming (OOP). It focuses on showing only the essential features of an object while hiding the unnecessary details.  
This allows programmers to work with high-level concepts without worrying about the complex inner workings. In Java, abstraction can be achieved using Abstract classes or Interfaces.   
An abstract class is a class that cannot be instantiated directly. It is designed to be a blueprint for other classes. Abstract classes can contain:
- **Abstract methods**: Methods without a body, which must be implemented by any subclass.
- **Concrete methods**: Regular methods with a body, which can be used or overridden by subclasses.
- **Fields (variables)**: Like any regular class, an abstract class can have instance variables.
```java

abstract class PaymentProcessor {

    protected double balance;

    public PaymentProcessor(double initialBalance) {
        this.balance = initialBalance;
    }

    public void showBalance() {
        System.out.println("Current balance: $" + balance);
    }

    public abstract boolean processPayment(double amount);
    public abstract String getPaymentType();
}

class CreditCardPayment extends PaymentProcessor {

    private String cardNumber;
    public CreditCardPayment(double balance, String cardNumber) {
        super(balance);
        this.cardNumber = cardNumber;
    }

    @Override
    public boolean processPayment(double amount) {
        if (amount > balance) {
            System.out.println("Credit card declined: insufficient funds");
            return false;
        }
        balance -= amount;
        System.out.println("Credit card payment successful: $" + amount);
        return true;
    }

    @Override
    public String getPaymentType() {
        return "Credit Card (**** " + cardNumber.substring(cardNumber.length()-4) + ")";
    }
}

class PayPalPayment extends PaymentProcessor {

    private String email;

    public PayPalPayment(double balance, String email) {
        super(balance);
        this.email = email;
    }

    @Override
    public boolean processPayment(double amount) {
        if (amount > balance) return false;
        balance -= amount;
        System.out.println("PayPal payment of $" + amount + " successful");
        return true;
    }

    @Override
    public String getPaymentType() {
        return "PayPal (" + email + ")";
    }
}
```
Here we created a general blueprint for processing payments. The abstract class ``PaymentProcessor`` declares the essential behavior every payment method must support (like ``processPayment()`` and ``getPaymentType()``) while providing a shared balance field and a common ``showBalance()`` method. Concrete classes ``CreditCardPayment`` and ``PayPalPayment`` inherit from it and implement the specific payment logic for each method.

In the `main` method, we can use the abstract class `PaymentProcessor` as the **type** for `CreditCardPayment` and `PayPalPayment`. This allows us to work with these objects without needing to know their internal implementation details, relying only on the behavior defined in the abstract class.
```Java
public class Main {

    public static void main(String[] args) {
        PaymentProcessor payment = new CreditCardPayment(500, "1234-5678-9012-3456");

        payment.showBalance();
        payment.processPayment(150);
        payment.showBalance();

        System.out.println("Used: " + payment.getPaymentType());

        payment = new PayPalPayment(300, "ali@example.com");
        payment.processPayment(80);
    }
}

```
#### Polymorphism
Polymorphism means "many forms." It is the ability of a single object or method to behave differently depending on the context. In Java, this allows us to use a parent class reference to hold a child class object, enabling us to write more flexible and reusable code.  
There are two main types of polymorphism in Java: Compile-time Polymorphism (Method Overloading) and Runtime Polymorphism (Method Overriding).  
**Method Overloading (Compile-time)** This occurs when multiple methods in the same class share the same name but have different parameters. The compiler determines which method to call based on the arguments passed.
```java
class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    public double add(double a, double b) {
        return a + b;
    }
}
```
**Method Overriding (Runtime)** It occurs when a subclass provides a specific implementation for a method that is already defined in its parent class.The decision of which method to run is made while the program is running, based on the actual object being referred to, not the reference variable type.
```java
class Pet {
    String name;
    int age;
    String ownerName;

    public Pet(String name, int age, String ownerName) {
        this.name = name;
        this.age = age;
        this.ownerName = ownerName;
    }

    public void speak() {
        System.out.println("Some generic pet sound...");
    }

    public void introduce() {
        System.out.println("Hi, I'm " + name + " and I'm " + age + " years old.");
    }
}

class Cat extends Pet {
    public Cat(String name, int age, String ownerName) {
        super(name, age, ownerName);
    }

    @Override
    public void speak() {
        System.out.println("Meow meow!");
    }
}

class Dog extends Pet {
    public Dog(String name, int age, String ownerName) {
        super(name, age, ownerName);
    }

    @Override
    public void speak() {
        System.out.println("Woof woof!");
    }
}
```
Now we can use polymorphism is the main program:
```java
public class Main {
    public static void main(String[] args) {
        Pet myPet1 = new Cat("Luna", 3, "Ali");
        
        Pet myPet2 = new Dog("Max", 5, "Sara");

        myPet1.speak();   // prints: Meow meow!
        myPet2.speak();   // prints: Woof woof!

        Pet[] pets = {myPet1, myPet2, new Cat("Milo", 2, "Ali")};
        for (Pet pet : pets) {
            pet.speak();     // Each pet speaks differently!
            pet.introduce(); // This method is not overridden → same behavior
        }
    }
}
```
Even though the reference type is ``Pet`` in all cases, Java knows the real type at runtime and calls the correct ``speak()`` version.
#### Pattern Matching 
We have seen how we can use a **`Pet`** type to create methods and loop through collections of both `Cat` and `Dog` objects, leveraging polymorphism.  
But what if we want to run extra logic for a specific subclass, like counting the number of `Dog` objects, without losing polymorphism?   
The traditional approach uses the **`instanceof`** keyword to check the object type, and then optionally casts it to the specific subclass to run extra logic.
```java
public class Main {
    public static void main(String[] args) {
        Pet myPet1 = new Cat("Luna", 3, "Ali");
        
        Pet myPet2 = new Dog("Max", 5, "Sara");

        myPet1.speak();   // prints: Meow meow!
        myPet2.speak();   // prints: Woof woof!

        Pet[] pets = {myPet1, myPet2, new Cat("Milo", 2, "Ali")};

        int dogCount = 0;

        for (Pet pet : pets) {
            pet.speak();
            if (pet instanceof Dog) { 
                dog = (Dog) pet; // cating
                dogCount++;
            }
        }
        System.out.println("Total dogs: " + dogCount);
    }
}
```
In modern Java, we have pattern matching, which allows us to check the type and cast it in a single step. This is important because, if we have a method that accepts a `Dog` as a parameter, we cannot pass a `Pet` variable directly even if the object is actually a `Dog`. 
```java
public class Main {
	private static void bringBall(Dog dog){
		System.out.println("bringing the ball");
	}
    public static void main(String[] args) {
        Pet myPet1 = new Cat("Luna", 3, "Ali");
        
        Pet myPet2 = new Dog("Max", 5, "Sara");

        myPet1.speak();   // prints: Meow meow!
        myPet2.speak();   // prints: Woof woof!

        Pet[] pets = {myPet1, myPet2, new Cat("Milo", 2, "Ali")};

        int dogCount = 0;

        for (Pet pet : pets) {
            pet.speak();
            if (pet instanceof Dog dog) { 
                bringBall(dog);
                dogCount++;
            }
        }
        System.out.println("Total dogs: " + dogCount);
    }
}
```
We can do the same for `Cat` or any other class that inherits from `Pet` using multiple `else if` statements.  However, to make our code cleaner and easier to maintain, modern Java allows us to use pattern matching with `switch`. which allow us to check both the type and value of an object in a single, concise statement.
```java
public class Main {
    public static void main(String[] args) {
        Pet pet = new Cat("Luna", 3, "Ali");
        String message = switch (pet) {
	        case Cat cat -> {
		        cat.speak();
	            if (cat.ownerName.equals("Ali")){
                yield "This is Ali's cat!";
	            }
                yield "It was a cat!";
            }
            case Dog dog -> {
                dog.speak();
                yield "It was a dog!";
            }
            default -> "Unknown pet type";
        };

        System.out.println(message);
    }
}
```
### Sealed Classes
Sealed classes  allow a class or interface to restrict which other classes can extend or implement it.  
This is useful when we want controlled inheritance.  
We define sealed class using the `sealed` keyword, followed by the `permits` clause that lists all allowed subclasses. Only the listed subclasses can extend the sealed class.
```java
public sealed class Shape permits Circle, Rectangle, Triangle {
    public abstract double area();
}
```
Here:
- `Shape` is a **sealed class**.
- Only `Circle`, `Rectangle`, and `Triangle` can inherit from `Shape`.
- No other class outside the `permits` list can extend `Shape`.

Each subclass of a sealed class must declare one of the following modifiers:
- `final` cannot be extended further
- `sealed` have controlled inheritance
- `non-sealed` open for unrestricted inheritance
```java
public final class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

public non-sealed class Rectangle extends Shape {
    private double width, height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}
```
Sealed class help us to prevents unwanted classes from extending oour base class and make our hierarchy tree clear and trackable
### Records
Records are a special type of class that allows us to define a data structure with just a single line of code. When we define a record, the Java compiler automatically generates:
- A **canonical constructor** for all fields.
- **Accessor methods** (getters) for every field.
- The **`equals()`** and **`hashCode()`** methods.
- A clean **`toString()`** implementation.

Records are immutable by design, meaning once we create the object, its data can't be changed. This makes them perfect for Data Transfer Objects (DTOs) or holding temporary state.
#### Defining a Record
We can define a record using the `record` keyword followed by the parameters (the components of the record):
```java
public record User(String name, int age) { }
```
With that one line, we've created a class with two private final fields, a constructor, and all the standard methods mentioned above.
#### Using a Record
Because the fields are final, we can't edit them after the object is created. We access the data using methods named exactly like the fields.
```java
public class Main {
    public static void main(String[] args) {
        User user = new User("Alice", 30);


        System.out.println("Name: " + user.name()); // Alice
        System.out.println("Age: " + user.age());   // 30

        System.out.println(user); // Output: User[name=Alice, age=30]

        User anotherUser = new User("Alice", 30);
        System.out.println(user.equals(anotherUser)); // true
    }
}
```
## Interface, Enums and Packages
### Interfaces
An Interface is a completely abstract type that contains only abstract methods (methods without a body) and constant variables. While an abstract class is like a partial blueprint, an interface is like a contract or a protocol. If a class implements an interface, it must provide the actual code for all the methods defined in that interface. To define an interface, we use the `interface` keyword.
```java
public interface Swimmable {
    void swim();
}
```
In an interface, methods are implicitly public and abstract by default.

To use this interface, a class uses the `implements` keyword, a class can implement multiple interfaces. Let's create a `Fish` class and a `Dog` class. Even though they are very different animals, they both can share the `Swimmable` behavior.
```java
class Fish implements Swimmable {
    @Override
    public void swim() {
        System.out.println("The fish swims by moving its fins.");
    }
}

class Dog implements Swimmable {
    @Override
    public void swim() {
        System.out.println("The dog does the doggy paddle.");
    }
}
```
Now we can create instances of these classes and treat them as `Swimmable` objects.
```java
public class Example6 {
    public static void main(String[] args) {
        Swimmable myFish = new Fish();
        Swimmable myDog = new Dog();

        myFish.swim();
        myDog.swim();
    }
}
```
#### Multiple Interfaces
One of the biggest advantages of interfaces over abstract classes is that Java does not support multiple inheritance, but it does support implementing multiple interfaces. For example, a `Duck` is an animal that can both swim and fly. We can define a second interface called `Flyable`.
```java
public interface Flyable {
    void fly();
}
```
Now, we can create a `Duck` class that implements both `Swimmable` and `Flyable`. We separate the interfaces with a comma.
```java
class Duck implements Swimmable, Flyable {
    
    @Override
    public void swim() {
        System.out.println("The duck floats on the water.");
    }

    @Override
    public void fly() {
        System.out.println("The duck flies to the south.");
    }
}
```
This allows us to write flexible code where a `Duck` object can be treated as a `Swimmable` object when we are at the lake, or a `Flyable` object when we are looking at the sky.
```java
public class Example7 {
    public static void main(String[] args) {
        Duck mallard = new Duck();
        
        mallard.swim();
        mallard.fly();
    }
}
```
#### Default Methods
A default method is a new feature added to Java 8 and later versions , which allow interface to have method with a body, unlike regular abstract methods, it allow us to add new functionality to an interface without breaking existing implementations, Classes implementing the interface can use the default implementation or override it if needed.
```Java
public interface Vehicle {
    void start(); // abstract method

    default void honk() { // default method
        System.out.println("Beep beep!");
    }
}
```
Here, any class implementing `Vehicle` automatically has the `honk()` method.
```java
public class Car implements Vehicle {

    @Override
    public void start() {
        System.out.println("Car is starting...");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle v = new Car();
        v.start(); 
        v.honk();  // Beep beep! (default method used)
    }
}
```
### Enums
An Enum (short for "enumeration") is a special Java type used to define a collection of constants. It is essentially a class that represents a fixed set of values that cannot be changed. Enums are particularly useful when we have a variable that can only take one out of a small set of possible values, such as days of the week (`MONDAY`, `TUESDAY`...), colors (`RED`, `GREEN`, `BLUE`), or difficulty levels (`EASY`, `MEDIUM`, `HARD`).
#### Creating an Enum
To create an enum, we use the `enum` keyword (instead of `class` or `interface`), and then list the constants separated by commas. By convention, the constants are written in uppercase letters.
```java
public enum Level {
    LOW,
    MEDIUM,
    HIGH
}
```
We can now access these constants using the dot syntax, just like accessing static members of a class.
```java
public class Example8 {
    public static void main(String[] args) {
        Level myLevel = Level.MEDIUM;
        System.out.println(myLevel);
    }
}
```
#### Using Enums in Switch Statements
Enums are often used in `switch` statements to check for corresponding values. This makes the code much more readable than using integers (like 0, 1, 2) or strings to represent states.
```java
public class Game {
    public static void main(String[] args) {
        Level currentLevel = Level.MEDIUM;

        switch (currentLevel) {
            case LOW:
                System.out.println("Low level");
                break;
            case MEDIUM:
                System.out.println("Medium level");
                break;
            case HIGH:
                System.out.println("High level");
                break;
        }
    }
}
```
#### Iterating Over Enums
Sometimes we need to get a list of all defined constants in an enum. The enum type has a static method called `values()` that returns an array containing all of the enum constants.
```java
public class Example9 {
    public static void main(String[] args) {
        for (Level level : Level.values()) {
            System.out.println(level);
        }
    }
}
```
#### Enums with Fields and Methods
In Java, an `enum` is actually a class, which means it can have attributes, methods, and constructors. This is very powerful because it allows us to attach data to each constant. For example, let’s create a `PizzaSize` enum. Instead of just listing sizes, we want to associate a specific radius with each size.
- We define a `private` attribute `radius`.
- We create a **constructor** to initialize this attribute. Note that enum constructors are always private (or package-private) because we cannot create new enum instances from outside; they are created automatically by Java.
- We add a **getter** method so we can access the radius.
```java
public enum PizzaSize {
    SMALL(15),
    MEDIUM(20),
    LARGE(25),
    EXTRA_LARGE(30);

    private final int radius;

    // Constructor
    PizzaSize(int radius) {
        this.radius = radius;
    }

    public int getRadius() {
        return radius;
    }
    
    public double getArea() {
         return Math.PI * radius * radius;
    }
}
```
Now, each constant (`SMALL`, `MEDIUM`, etc.) carries its own data. When we refer to `PizzaSize.MEDIUM`, we can ask for its specific radius or calculate its area.
```java
public class PizzaShop {
    public static void main(String[] args) {
        PizzaSize myOrder = PizzaSize.LARGE;
        
        System.out.println("You ordered a " + myOrder + " pizza.");
        System.out.println("Radius: " + myOrder.getRadius() + "cm");
        System.out.println("Area: " + myOrder.getArea() + "cm²");
    }
}
```
### Packages
A package is essentially a folder that contains related classes and interfaces. It helps us organize our code, prevents naming conflicts (e.g., having two `Scanner` classes in different libraries), and controls access to classes. To define a package, we use the `package` keyword as the first line of our Java file. Let's create a specialized package for mathematical operations. We will create a folder named `tools` and inside it, a file named `MathHelper.java`.
```java
package tools;

public class MathHelper {
    
    public static int square(int number) {
        return number * number;
    }
    
    public void printMessage() {
        System.out.println("Math helper is running.");
    }
}
```
Now, if we want to use this class in another file (outside the `tools` folder), we must import it using the `import` keyword. Java uses the full path (package name + class name) to locate the file.
```java
import tools.MathHelper;

public class App {
    public static void main(String[] args) {
        
        // Using a static method from the package
        int result = MathHelper.square(5);
        System.out.println("Square is: " + result);

        // Creating an object from the package class
        MathHelper helper = new MathHelper();
        helper.printMessage();
    }
}
```
If we want to import _all_ classes from a package, we can use the wildcard `*`: `import tools.*;`. However, it is often better practice to import only the specific classes we need to keep the code clear.
#### Sub-packages
Packages can also be **nested** using sub-folders to create a hierarchical structure. This is common in larger projects to better organize classes. For example, we might have a folder structure like this:
```
src/
 └─ com/
     └─ example/
         └─ tools/
             └─ MathHelper.java
```
In this case, the package name reflects the folder structure. So the `MathHelper.java` file would start with:
```java
package com.example.tools;

public class MathHelper {
    
    public static int square(int number) {
        return number * number;
    }
    
    public void printMessage() {
        System.out.println("Math helper in nested package is running.");
    }
}
```
To use this class in another file outside the `com.example.tools` package, we must import it with the full package path:
```java
import com.example.tools.MathHelper;

public class App {
    public static void main(String[] args) {
        
        int result = MathHelper.square(7);
        System.out.println("Square is: " + result);

        MathHelper helper = new MathHelper();
        helper.printMessage();
    }
}
```
