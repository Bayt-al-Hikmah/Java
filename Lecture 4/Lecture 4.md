## Objectives
- Working with Collections Framework
- Exploring Modern Java Concepts
## Collections Framework
The Collections Framework is a set of classes and interfaces that implement commonly used data structures. It acts like a toolbox providing ready-to-use containers for our objects.
- **Dynamic Sizing**: Unlike arrays, collections can grow and shrink automatically as we add or remove elements.
- **Standard Methods**: They come with built-in methods to perform operations like searching, sorting, and shuffling.
### List
A `List` is an ordered collection. It allows us to store elements in the order they are inserted. We can access elements by their integer index, similar to arrays, The `List` is an interface, so we cannot instantiate it directly. We must use a class that implements it, such as `ArrayList`or `LinkedList`
#### ArrayList
`ArrayList` is the most widely used implementation of the `List` interface. It uses a dynamic array internally to store elements. When the array becomes full, Java automatically creates a larger array and copies the existing elements into it.  
To use `ArrayList`, we first need to import it using `import java.util.ArrayList;`. After that, you can create an `ArrayList` by specifying its type with `ArrayList<Type>`, where `Type` represents the data type of the elements the list will store.
```Java
import java.util.ArrayList;

public class Example10 {
    public static void main(String[] args) {
        ArrayList<String> shoppingList = new ArrayList<>();

        // Adding elements
        shoppingList.add("Milk");
        shoppingList.add("Eggs");
        shoppingList.add("Bread");
        shoppingList.add("Eggs"); 
        System.out.println("Item at index 0: " + shoppingList.get(0));
        shoppingList.remove("Bread");
        System.out.println("We have " + shoppingList.size() + " items.");
        System.out.println(shoppingList);
    }
}
```
`ArrayList` comes with a wide range of methods that make it easier to manage, manipulate, and access data efficiently.
- **add(E element)**: Adds an element to the end of the list.
- **add(int index, E element)**: Inserts an element at a specific position.
- **get(int index)**: Returns the element at the given index.
- **set(int index, E element)**: Replaces the element at the specified index with a new one.
- **remove(int index)**: Removes the element at the given index.
- **remove(Object o)**: Removes the first occurrence of the specified element.
- **size()**: Returns the number of elements in the list.
- **isEmpty()**: Checks if the list is empty.
- **contains(Object o)**: Checks whether the list contains a specific element.
- **clear()**: Removes all elements from the list.
- **indexOf(Object o)**: Returns the index of the first occurrence of an element.
- **lastIndexOf(Object o)**: Returns the index of the last occurrence.
- **toArray()**: Converts the `ArrayList` into an array.
- **addAll(Collection c)**: Adds all elements from another collection.
- **removeAll(Collection c)**: Removes all elements that exist in another collection.
- **retainAll(Collection c)**: Keeps only elements that exist in another collection.
- **iterator()**: Returns an iterator to loop through elements.
- **forEach(Consumer action)**: Performs an action on each element.
- **sort(Comparator c)**: Sorts the list using a comparator.
- **subList(int from, int to)**: Returns a portion of the list.
#### LinkedList
`LinkedList` is another widely used implementation of the `List` interface. Unlike `ArrayList`, it does **not** use a dynamic array. Instead, it stores elements in nodes, where each node contains the data and references to the next and previous nodes.   
Because of this structure, `LinkedList` is more efficient for inserting and deleting elements, especially in the middle of the list. However, accessing elements by index is slower compared to `ArrayList`.
To use `LinkedList`, we first need to import it using `import java.util.LinkedList;`. After that, you can create a `LinkedList` by specifying its type with `LinkedList<Type>`.
```Java
import java.util.LinkedList;

public class Example11 {
    public static void main(String[] args) {
        LinkedList<String> shoppingList = new LinkedList<>();

        shoppingList.add("Milk");
        shoppingList.add("Eggs");
        shoppingList.add("Bread");
        shoppingList.add("Eggs");


        System.out.println("Item at index 0: " + shoppingList.get(0));

        // Removing elements
        shoppingList.remove("Bread");

        System.out.println("We have " + shoppingList.size() + " items.");
        System.out.println(shoppingList);
    }
}

```
`LinkedList` provides many useful methods for managing and manipulating data:
- **add(E element)**: Adds an element to the end of the list.
- **add(int index, E element)**: Inserts an element at a specific position.
- **addFirst(E element)**: Adds an element at the beginning.
- **addLast(E element)**: Adds an element at the end.
- **get(int index)**: Returns the element at the given index.
- **getFirst()**: Returns the first element.
- **getLast()**: Returns the last element.
- **set(int index, E element)**: Replaces the element at the specified index.
- **remove(int index)**: Removes the element at the given index.
- **remove(Object o)**: Removes the first occurrence of the element.
- **removeFirst()**: Removes the first element.
- **removeLast()**: Removes the last element.
- **size()**: Returns the number of elements.
- **isEmpty()**: Checks if the list is empty.
- **contains(Object o)**: Checks if the list contains an element.
- **clear()**: Removes all elements.
- **indexOf(Object o)**: Returns the index of the first occurrence.
- **lastIndexOf(Object o)**: Returns the index of the last occurrence.
- **toArray()**: Converts the list to an array.
- **iterator()**: Returns an iterator.
- **forEach(Consumer action)**: Performs an action on each element.
### Set
A `Set` is a collection that **does not allow duplicate elements**. Each element in a `Set` must be unique. Unlike `List`, a `Set` does not support indexing, so elements cannot be accessed by position. The `Set` is an interface, so it cannot be instantiated directly. We must use a class that implements it, such as `HashSet` or `TreeSet`.
#### HashSet
`HashSet` is the most widely used implementation of the `Set` interface. It uses a hash table internally to store elements. The main characteristic of a `HashSet` is that it does not allow duplicate values, and it does not guarantee any specific order of the elements.  
It is highly efficient for checking if an element exists in the collection (`contains`), adding elements, and removing them.  
To use `HashSet`, we first need to import it using `import java.util.HashSet;`. After that, we can create a `HashSet` by specifying its type with `HashSet<Type>`.
```java
import java.util.HashSet;

public class Example12 {
    public static void main(String[] args) {
        HashSet<String> shoppingSet = new HashSet<>();

        // Adding elements
        shoppingSet.add("Milk");
        shoppingSet.add("Eggs");
        shoppingSet.add("Bread");
        // Adding a duplicate element (will be ignored)
        shoppingSet.add("Eggs"); 

        // Note: We cannot access elements by index like .get(0) in a Set

        System.out.println("We have " + shoppingSet.size() + " items.");
        
        shoppingSet.remove("Bread");
        
        System.out.println("Contains Milk? " + shoppingSet.contains("Milk"));
        System.out.println(shoppingSet);
    }
}
```
`HashSet` provides a focused set of methods for managing unique collections of data:
- **add(E element)**: Adds the specified element to the set if it is not already present. Returns `true` if this set did not already contain the element.
- **remove(Object o)**: Removes the specified element from the set if it is present.
- **contains(Object o)**: Returns `true` if the set contains the specified element.
- **size()**: Returns the number of elements in the set.
- **isEmpty()**: Checks if the set is empty.
- **clear()**: Removes all elements from the set.
- **iterator()**: Returns an iterator to loop through elements.
- **forEach(Consumer action)**: Performs an action on each element.
- **toArray()**: Converts the `HashSet` into an array.
- **addAll(Collection c)**: Adds all elements from another collection (Union).
- **retainAll(Collection c)**: Retains only the elements in this set that are contained in the specified collection (Intersection).
- **removeAll(Collection c)**: Removes from this set all of its elements that are contained in the specified collection (Difference).
#### TreeSet
`TreeSet` is another important implementation of the `Set` interface. Unlike `HashSet`, it stores elements in a sorted tree structure.  Because of this structure, `TreeSet` guarantees that the elements will be sorted in ascending order (natural ordering) or according to a custom comparator provided at creation. However, adding and checking for elements is slightly slower than `HashSet` because the tree must be rebalanced to maintain order.   
To use `TreeSet`, we first need to import it using `import java.util.TreeSet;`. After that, you can create a `TreeSet` by specifying its type with `TreeSet<Type>`.
```java
import java.util.TreeSet;

public class Example13 {
    public static void main(String[] args) {
        TreeSet<String> shoppingSet = new TreeSet<>();

        shoppingSet.add("Milk");
        shoppingSet.add("Eggs");
        shoppingSet.add("Bread");
        shoppingSet.add("Eggs"); // Duplicate ignored

        // The output will be sorted alphabetically: [Bread, Eggs, Milk]
        System.out.println(shoppingSet);

        System.out.println("First item: " + shoppingSet.first());
        System.out.println("Last item: " + shoppingSet.last());

        shoppingSet.remove("Bread");
        System.out.println("We have " + shoppingSet.size() + " items.");
    }
}
```
`TreeSet` provides standard `Set` methods plus specific methods for navigating the sorted data:
- **add(E element)**: Adds an element; keeps the set sorted.
- **remove(Object o)**: Removes the specified element.
- **contains(Object o)**: Checks if the set contains the element.
- **first()**: Returns the first (lowest) element currently in the set.
- **last()**: Returns the last (highest) element currently in the set.
- **ceiling(E e)**: Returns the least element greater than or equal to the given element.
- **floor(E e)**: Returns the greatest element less than or equal to the given element.
- **higher(E e)**: Returns the least element strictly greater than the given element.
- **lower(E e)**: Returns the greatest element strictly less than the given element.
- **pollFirst()**: Retrieves and removes the first (lowest) element.
- **pollLast()**: Retrieves and removes the last (highest) element.
- **subSet(E fromElement, E toElement)**: Returns a view of the portion of the set between two elements.
- **headSet(E toElement)**: Returns a view of the portion of the set less than the element.
- **tailSet(E fromElement)**: Returns a view of the portion of the set greater than or equal to the element.
- **size()**: Returns the number of elements.
- **isEmpty()**: Checks if the set is empty.
- **clear()**: Removes all elements.
### Map
A `Map` is a data structure that maps keys to values. Unlike `List` or `Set`, a `Map` is not a collection of single elements but rather a collection of pairs. A `Map` cannot contain duplicate keys; each key can map to at most one value. However, duplicate values are allowed. The `Map` interface does not support direct indexing like a `List`; instead, values are accessed via their associated keys. Like `Set`, `Map` is an interface and requires an implementation class like `HashMap` or `TreeMap`.
#### HashMap
`HashMap` is the most widely used implementation of the `Map` interface. It uses a hash table internally to store the key-value pairs. The main characteristic of a `HashMap` is that it allows null keys and values, and it does not guarantee any specific order of the keys. It is highly efficient for inserting mapping definitions (`put`), retrieving values (`get`), and checking if a key exists.  
To use `HashMap`, we first need to import it using `import java.util.HashMap;`. After that, we can create a `HashMap` by specifying the types for both key and value with `HashMap<KeyType, ValueType>`.
```Java
import java.util.HashMap;

public class Example14 {
    public static void main(String[] args) {
        // Map of Product Name (String) -> Price (Double)
        HashMap<String, Double> groceryPrices = new HashMap<>();

        // Adding key-value pairs
        groceryPrices.put("Milk", 2.50);
        groceryPrices.put("Eggs", 3.00);
        groceryPrices.put("Bread", 1.99);
        
        groceryPrices.put("Milk", 2.75);

        System.out.println("We have " + groceryPrices.size() + " items listed.");

        // Accessing a value by its key
        double milkPrice = groceryPrices.get("Milk");
        System.out.println("The price of Milk is: " + milkPrice);

        // Remove an item
        groceryPrices.remove("Bread");

        System.out.println("Is Bread listed? " + groceryPrices.containsKey("Bread"));
        System.out.println(groceryPrices);
    }
}
```
`HashMap` provides a robust set of methods for managing key-value pairs:
- **put(K key, V value)**: Associates the specified value with the specified key in the map. If the map previously contained a mapping for the key, the old value is replaced.
- **get(Object key)**: Returns the value to which the specified key is mapped, or `null` if the map contains no mapping for the key.
- **remove(Object key)**: Removes the mapping for the specified key from this map if present.
- **containsKey(Object key)**: Returns `true` if this map contains a mapping for the specified key.
- **containsValue(Object value)**: Returns `true` if this map maps one or more keys to the specified value.
- **size()**: Returns the number of key-value mappings in the map.
- **isEmpty()**: Checks if the map is empty.
- **clear()**: Removes all mappings from the map.    
- **keySet()**: Returns a `Set` view of the keys contained in this map.
- **values()**: Returns a `Collection` view of the values contained in this map.
- **entrySet()**: Returns a `Set` view of the mappings (key-value pairs) contained in this map.
- **replace(K key, V value)**: Replaces the entry for the specified key only if it is currently mapped to some value.
- **putIfAbsent(K key, V value)**: If the specified key is not already associated with a value (or is mapped to null), associates it with the given value.
#### TreeMap
`TreeMap` is another essential implementation of the `Map` interface. Unlike `HashMap`, it stores its keys in a sorted tree structure . Because of this structure, `TreeMap` guarantees that the keys will be sorted in ascending order (natural ordering) or according to a custom comparator provided at creation. While powerful for maintaining order, basic operations like adding and getting keys are generally slower than `HashMap` ($O(\log n)$ vs $O(1)$).   
To use `TreeMap`, we first need to import it using `import java.util.TreeMap;`. After that, you can create a `TreeMap` by specifying its types with `TreeMap<KeyType, ValueType>`.
```Java
import java.util.TreeMap;

public class Example15 {
    public static void main(String[] args) {
        TreeMap<String, Integer> examScores = new TreeMap<>();

        examScores.put("Alice", 88);
        examScores.put("Charlie", 92);
        examScores.put("Bob", 75);
        examScores.put("Alice", 90); 
        
        System.out.println(examScores);

        System.out.println("First student (alphabetically): " + examScores.firstKey());
        System.out.println("Last student (alphabetically): " + examScores.lastKey());
    }
}
```
`TreeMap` provides standard `Map` methods plus specific methods for navigating the sorted keys:
- **put(K key, V value)**: Adds a key-value pair; keeps the keys sorted.
- **get(Object key)**: Retrieves the value for the key.
- **firstKey()**: Returns the first (lowest) key currently in the map.
- **lastKey()**: Returns the last (highest) key currently in the map.
- **firstEntry()**: Returns a key-value mapping associated with the least key in this map.
- **lastEntry()**: Returns a key-value mapping associated with the greatest key in this map.
- **ceilingKey(K key)**: Returns the least key greater than or equal to the given key.
- **floorKey(K key)**: Returns the greatest key less than or equal to the given key.
- **higherKey(K key)**: Returns the least key strictly greater than the given key.
- **lowerKey(K key)**: Returns the greatest key strictly less than the given key.
- **pollFirstEntry()**: Removes and returns a key-value mapping associated with the least key.
- **pollLastEntry()**: Removes and returns a key-value mapping associated with the greatest key.
- **subMap(K fromKey, K toKey)**: Returns a view of the portion of the map whose keys range from `fromKey` to `toKey`.
- **headMap(K toKey)**: Returns a view of the portion of the map whose keys are strictly less than `toKey`.
- **tailMap(K fromKey)**: Returns a view of the portion of the map whose keys are greater than or equal to `fromKey`.
### Stack , Queue  and Deque 
#### Stack
A `Stack` is a collection that follows the LIFO principle (Last In, First Out). This means that the last element added is the first one removed, We can think of a stack like a stack of plates: you put plates on top and remove them from the top.  
In Java, stacks can be implemented Using the `Stack` class

The `Stack` class is part of `java.util` and extends `Vector`. It provides built-in methods for stack operations, however, it is considered legacy and is generally not recommended for new programs because it is synchronized and slower.
```java
import java.util.Stack;

public class Example17 {
    public static void main(String[] args) {
        Stack<String> bookStack = new Stack<>();

        bookStack.push("Math");
        bookStack.push("Science");
        bookStack.push("English");

        System.out.println(bookStack);

        System.out.println("Top: " + bookStack.peek());

        bookStack.pop();

        System.out.println("After pop: " + bookStack);

        System.out.println("Is empty? " + bookStack.isEmpty());
    }
}

```
`Stack` come with some methods such us

- **push(E item)**: Adds an element to the top.
- **pop()**: Removes and returns the top element.
- **peek()**: Returns the top element without removing it.
- **empty()**: Checks if stack is empty.
- **search(Object o)**: Returns position from top (1-based index).
- **size()**: Returns the number of elements
- **IsEmpty()**: Check if empty
#### Queue
A `Queue` is implement the reverse logic of `Stack` it is a collection designed to store elements in FIFO order. The first element added is the first one removed.
The `Queue` interface is part of `java.util`. It provides built-in methods for queue operations. Since it is an interface, it cannot be instantiated directly, so we use classes like `LinkedList` or `PriorityQueue`.   
```Java
import java.util.LinkedList;
import java.util.Queue;

public class Example17 {
    public static void main(String[] args) {
        Queue<String> bookQueue = new LinkedList<>();

        // Add elements
        bookQueue.add("Math");
        bookQueue.add("Science");
        bookQueue.add("English");

        System.out.println(bookQueue);

        // View first element
        System.out.println("Front: " + bookQueue.peek());

        // Remove first element
        bookQueue.poll();

        System.out.println("After poll: " + bookQueue);

        System.out.println("Is empty? " + bookQueue.isEmpty());
    }
}
```
`Queue` come with the following methods:
- **add(E e)**: Adds an element to the end of the queue.
- **offer(E e)**: Adds an element without throwing an exception.
- **remove()**: Removes and returns the first element.
- **poll()**: Removes and returns the first element (returns `null` if empty).
- **peek()**: Returns the first element without removing it.
- **element()**: Returns the first element (throws exception if empty).
- **size()**: Returns the number of elements.
- **isEmpty()**: Checks if the queue is empty.
#### PriorityQueue
A `PriorityQueue` is a type of queue where elements are ordered based on **priority instead of insertion order**. By default, a `PriorityQueue` in Java arranges elements in **ascending (natural) order**, which means the smallest element has the highest priority and is removed first.
```java
import java.util.PriorityQueue;
import java.util.Queue;

public class Example18 {
    public static void main(String[] args) {
        Queue<Integer> numberQueue = new PriorityQueue<>();

        numberQueue.add(40);
        numberQueue.add(10);
        numberQueue.add(30);
        numberQueue.add(20);

        System.out.println(numberQueue);

        System.out.println("Front: " + numberQueue.peek());
        numberQueue.poll();

        System.out.println("After poll: " + numberQueue);

        System.out.println("Is empty? " + numberQueue.isEmpty());
    }
}

```
`PriorityQueue` comes with some methods such as:
- **add(E e)**: Adds an element to the queue.
- **offer(E e)**: Adds an element without throwing an exception.
- **remove()**: Removes and returns the highest-priority element.
- **poll()**: Removes and returns the highest-priority element (returns `null` if empty).
- **peek()**: Returns the highest-priority element without removing it.
- **element()**: Returns the highest-priority element (throws exception if empty).
- **size()**: Returns the number of elements.
- **isEmpty()**: Checks if the queue is empty.
#### Deque (Double-Ended Queue)
A **Deque** (double-ended queue) is a collection that allows insertion, removal, and examination of elements from both ends (head and tail). It combines the features of a **queue** (FIFO First In, First Out) and a **stack** (LIFO Last In, First Out).  
In Java, Deque is an interface (introduced in Java 6) in the ``java.util`` package. It extends the ``Queue`` interface and provides richer operations for working from both sides.    
``ArrayDeque`` is the most common and efficient implementation of the ``Deque`` interface.

```Java
import java.util.ArrayDeque;
import java.util.Deque;

public class ExampleArrayDequeAsStack {
    public static void main(String[] args) {
        // Using Deque as a Stack (LIFO)
        Deque<String> bookStack = new ArrayDeque<>();

        bookStack.push("Math");     // add to top (front)
        bookStack.push("Science");
        bookStack.push("English");

        System.out.println(bookStack);           // [English, Science, Math]
        System.out.println("Top: " + bookStack.peek());   // English (peek top)
        System.out.println("Top: " + bookStack.peekFirst()); // same

        bookStack.pop();   // removes English
        System.out.println("After pop: " + bookStack);   // [Science, Math]

        System.out.println("Is empty? " + bookStack.isEmpty());
    }
}
```
`Deque` provides methods for working at both ends:
- **addFirst(E e)**: Adds at front.
- **addLast(E e)**: Adds at end.
- **offerFirst(E e)**: Adds at front (no exception).
- **offerLast(E e)**: Adds at end (no exception).
- **removeFirst()**: Removes first element.
- **removeLast()**: Removes last element.
- **pollFirst()**: Removes first (returns `null` if empty).
- **pollLast()**: Removes last (returns `null` if empty).
- **getFirst()**: Returns first element.
- **getLast()**: Returns last element.
- **peekFirst()**: Returns first (or `null`).
- **peekLast()**: Returns last (or `null`).
- **push(E e)**: Adds to front.
- **pop()**: Removes from front.
- **peek()**: Views top element.
- **size()**: Return the size
- **isEmpty()**: Check if Empty
- **clear()**: Clear the Deque
- **contains(Object o)**: Check if it contain the object


### Comparable & Comparator
We have explored the Java Collections Framework, and we learned that many collections have their own ways of ordering elements.  
Ordering primitive types such as `int`, `double`, and `String` is easy because Java already knows how to compare and sort them.   
But what if we have more complex objects, such as `Student`, `Employee`, or `Book`, and we want to store and sort them inside collections?   
Java provides a solution for this problem by using the **`Comparable`** and **`Comparator`** interfaces.
#### Comparable
The **Comparable** interface is used when a class wants to define its default way of comparison.  A class that implements `Comparable` must override the **`compareTo()`** method. Which is used by sorting functions to decide the position of objects inside a collection.
```java
public class Student implements Comparable<Student> {
    int id;
    String name;

    public int compareTo(Student other) {
        return this.id - other.id; // sort by id
    }
}
```
In this example, we created a `Student` class that implements the `Comparable` interface. The `compareTo()` method compares the `id` of the current object with the `id` of another `Student` object. 
It returns an integer value that determines the order:
- Negative: Current object comes before the other
- Zero: Both objects are equal
- Positive: Current object comes after the other
#### Comparator
Unlike Comparable, the Comparator interface helps us define custom ways of comparison that are separate from the class itself, with `Comparator`, we can create multiple different sorting rules for the same class.  
There are several ways to implement `Comparator` in Java.   
The traditional way is to create a separate class that represents a custom comparison rule. this class must:
- Implement the `Comparator` interface
- Override the `compare()` method

The `compare()` method defines how two objects are compared.
```java
import java.util.Comparator;

public class NameComparator implements Comparator<Student> {

    public int compare(Student s1, Student s2) {
        return s1.name.compareTo(s2.name); // sort by name
    }
}
// Then we can use it as second argument for sorting method
Collections.sort(list, new NameComparator());

```
Since Java 8, we can create comparators using lambda expressions. which are anonymous function that allows us to write shorter and cleaner code.
```java
Collections.sort(list, (a, b) -> a.name.compareTo(b.name));
```
Finally we can use the `comparing` method from the `Comparator` class which make sorting even easier:
```java
list.sort(Comparator.comparing(s -> s.name));
```

### Iterators
An **Iterator** allows us to traverse a collection one element at a time without needing to know how the collection is internally implemented. It provides methods to check whether more elements exist and to retrieve them sequentially.  
The main methods of the `Iterator` interface are:
- `hasNext()` Checks if there is another element in the collection
- `next()` Returns the next element and moves the cursor forward
- `remove()` Removes the current element (optional operation)

An Iterator works like a cursor. When we create an iterator for a collection, it initially points to the beginning of the collection. We can then check if the collection is empty or no by using `hasNext()`,If it returns `true` this mean it not empty, we can then retrive the first element by using `next()` which retrieve the element and move the cursor forward, by using `hasNext()` and `next()` we move our cursor through all the elements of the collection and retrive them.
```java
import java.util.ArrayList;
import java.util.Iterator;

ArrayList<String> names = new ArrayList<>();

names.add("Ali");
names.add("Sara");
names.add("Omar");

Iterator<String> it = names.iterator();

while (it.hasNext()) {
    String name = it.next();
    System.out.println(name);
}
```
In this example, we created an `ArrayList` of names and used an `Iterator` to loop through it.  
The `hasNext()` method checks if there are more elements, and `next()` returns the next element in the collection.
#### Removing Elements Using Iterator
One important advantage of using an `Iterator` is that it allows us to remove elements safely while looping. If we try to remove elements directly from a collection while using a loop, Java may throw a `ConcurrentModificationException`.    
Using `remove()` from the `Iterator` avoids this problem.
```java
Iterator<String> it = names.iterator();  
while (it.hasNext()) {     
	String name = it.next();      
	if (name.equals("Sara")) {         
		it.remove(); // safe removal     
	} 
}
```
#### For-Each Loop
We saw before the for-each loop, which is a simpler way to loop through collections.
```java
for (String name : names) {     
	System.out.println(name); 
}
```
This method is easier to read and write, but it has limitations:
- We cannot remove elements safely
- We do not have control over the iteration process
#### ListIterator
For `List` collections (such as `ArrayList` and `LinkedList`), Java provides a more powerful iterator called **`ListIterator`**, it allows us to:
- Move forward and backward
- Add elements while iterating
- Modify elements
```java
import java.util.ListIterator;  
// other code
ListIterator<String> listIt = names.listIterator();  
while (listIt.hasNext()) {
     System.out.println(listIt.next()); 
}  
while (listIt.hasPrevious()) {     
	System.out.println(listIt.previous()); 
}
```
This example shows how `ListIterator` can move in both directions.

## Modern Java Concepts
### Functional Interfaces
A functional interface is a special type of interface that contains exactly one abstract method. This single method represents the core action that the interface is intended to perform. A functional interface **can still have** `default` or `static` methods, but only one abstract method is allowed.  
Functional interfaces are usually annotated with `@FunctionalInterface`. This annotation instructs the compiler to enforce the single-abstract-method rule, preventing compilation if more than one abstract method exists. This helps catch errors at compile time rather than at runtime.
```Java
@FunctionalInterface
public interface Calculator {

    int calculate(int a, int b);
}
```
We can implement a functional interface using a regular class and override its abstract method:
```Java
public class SimpleCalculator implements Calculator {
    @Override
    public int calculate(int a, int b) {
        return a + b;
    }
}
```
However, the true beauty of functional interfaces lies in their integration with lambda expressions and method references.
#### Lambdas expression
Lambdas expression are a short way to write methods without creating a full class. they allow us to create and write the method behavior directly.    
The general syntax of a lambda expression is:
```java
(parameter1, parameter2) -> {
    // function body
}
```
If the function body contains only one statement, we can simplify it further:
```java
(parameter1, parameter2) -> function body
```
if we have only one parameter we can use it as following
```java
parameter1 -> function body
```
Lambdas are **powerful** because they allow us to use functional interfaces without creating a separate class. For example, we can implement our `Calculator` interface like this:
```Java
Calculator add = (a,b)-> a + b;
```
Here, Java automatically treats the lambda expression as the implementation of the `calculate` method in our functional interface. We have effectively overridden the method without writing a full class.   
Now, we can use `add` just like a regular object implementing the interface:
```java
add.calculate(4,5);
```
Another powerful feature of lambda expressions is that they can be passed as arguments to other methods. Since a lambda is essentially an implementation of a functional interface, any method that accepts a functional interface as a parameter can also accept a lambda.   
For example, suppose we have a method that takes a `Calculator` as a parameter:
```Java
public static int operate(int a, int b, Calculator calculator) {
    return calculator.calculate(a, b);
}
```
We can now pass a lambda expression directly to this method:
```java
int product = operate(5, 3, (x, y) -> x * y);
```
#### Built-in Functional Interface
Java provides several built-in functional interfaces in the `java.util.function` package as well as in `java.lang`. These interfaces save time because we don’t have to define our own every time we want to use a lambda. They cover common scenarios like performing actions, supplying values, testing conditions, or transforming data.
#### Runnable
The `Runnable` interface represents a task that can be executed it take no argument and don't return any value :
```java
@FunctionalInterface
public interface Runnable {
    void run();
}
```
We can use it as following:
```java
Runnable task = () -> System.out.println("Task is running!");
task.run()
```
#### Supplier\<T\>
The `Supplier` interface represents a function that supplies and returns a value without taking any argument:
```java
@FunctionalInterface
public interface Supplier<T> {
    T get();
}
```
It usefull to generate data for example we can use it to generate random number
```java
Supplier<Double> randomValue = () -> Math.random();
System.out.println(randomValue.get());
```
#### Consumer\<T\>
The `Consumer` interface represents an operation that accepts a single input and returns no result:
```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```
We can use it to log data
```Java
Consumer<String> printer = s -> System.out.println(s);
printer.accept("Hello, Consumer!"); 
```
#### Predicate\<T\>
The `Predicate` interface represents a boolean-valued function of one argument it always return boolean , usually used for filtering:
```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}
```
Example we can use it to test if number is even
```java
Predicate<Integer> isEven = n -> n % 2 == 0;
System.out.println(isEven.test(10));
```
#### BinaryOperator\<T\> & UnaryOperator\<T\>
- **UnaryOperator**: takes one argument and returns the same type.
- **BinaryOperator**: takes two arguments of the same type and returns the same type.
```java
UnaryOperator<Integer> square = x -> x * x;
System.out.println(square.apply(5)); // prints 25

BinaryOperator<Integer> add = (a, b) -> a + b;
System.out.println(add.apply(3, 4)); // prints 7
```
#### Function\<T, R\>
Finally the function interface represents a function that takes an inputs and produces an outputs:
```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```
We can use it to work with any operation or function we want
```java
Function<String, Integer> lengthCalculator = s -> s.length();
System.out.println(lengthCalculator.apply("Hello")); // prints 5
```
#### Method References 
Method references are a **shortcut for lambda expressions** that call an existing method. Instead of writing a full lambda, we can reference a method directly.
The general syntax is:
```java
ClassName::methodName
```
For example, instead of writing a lambda like this:
```java
Function<String, Integer> lengthCalculator = s -> s.length();
System.out.println(lengthCalculator.apply("Hello")); 
```
We can use a method reference to achieve the same result more concisely:
```java
Function<String, Integer> lengthCalculator = String::length;
System.out.println(lengthCalculator.apply("Hello")); 
```
Here, `String::length` is a reference to the `length()` method of the `String` class. Method references are especially useful when a lambda simply calls an existing method.
### Stream API
When working with collections, we often use iterators and for-each loops to go through elements. However, manipulating and modifying collections in this way can be complex and difficult to manage.   
Java provides the Stream API to simplify this process. With streams, we can manipulate and process collection objects in a functional and more readable way. The Stream API allows us to perform operations such as filtering, mapping, sorting, and reducing data efficiently.  
#### `forEach()` Method
The `forEach()` method is used to perform an action on each element of a collection or stream. It allows us to process elements one by one in a simple and readable way using a lambda expression.
It does not return a value. Instead, it applies the given operation to every element in the stream. It is mainly used for displaying data, printing values, or performing actions such as saving or updating elements.
```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Ali", "Sara", "John", "Emma");
        names.stream().forEach(name -> System.out.println(name));
    }
}
```
#### `filter()` Method
The `filter()` method is used to select elements from a stream based on a condition. Only the elements that match the condition are kept, while the others are removed.
```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(10, 25, 5, 40, 15);

        List<Integer> filtredNumbers = numbers.stream()
	        .filter(n -> n > 15).toList();

        System.out.println(filtredNumbers);
    }
}
```
#### `map()` Method
The `map()` method is used to transform each element in a stream into another form. It changes the data without modifying the original collection.  
It is commonly used for converting values, such as changing strings to uppercase or numbers to their squares.
```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("ali", "sara", "john");

        names.stream()
             .map(name -> name.toUpperCase())
             .forEach(name -> System.out.println(name));
    }
}
```
#### `sorted()` Method
The `sorted()` method is used to arrange elements in a stream in a specific order. By default, it sorts elements in ascending order.   
It can also be customized to sort in descending order or by other rules using lambdas expression.
```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(30, 10, 40, 20);

        numbers.stream()
               .sorted((a,b)-> b-a) //descending sort
               .forEach(n -> System.out.println(n));
    }
}
```
#### `reduce()` Method
The `reduce()` method is used to combine all elements in a stream into a single value. It applies a repeated operation, such as adding numbers or joining strings.   
It is useful when you want a total, sum, product, or combined result.
```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 10, 15);

        int sum = numbers.stream()
                         .reduce(0, (a, b) -> a + b); // `0` is the starting value 

        System.out.println(sum);
    }
}
```
#### `collect()` Method
The `collect()` method is used to gather the processed stream elements into a collection such as a `List`, `Set`, or `Map`.
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Ali", "Sara", "John", "Emma");

        List<String> result = names.stream()
                                  .filter(name -> name.length() > 4)
                                  .collect(Collectors.toList());

        System.out.println(result);
    }
}
```
#### `groupingBy()` Method
The `groupingBy()` method is used with the ``collect`` method it organize elements into groups based on a specific key.   
The result is stored in a `Map`, where:
- The key is the grouping condition.
- The value is a list of matching elements.
```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Ali", "Adam", "Sara", "Sam", "John");

        Map<Character, List<String>> grouped =
                names.stream()
                     .collect(Collectors.groupingBy(name -> name.charAt(0)));

        System.out.println(grouped);
    }
}
```
Names will be grouped by first character `name -> name.charAt(0)` the output will be:
```
{A=[Ali, Adam], S=[Sara, Sam], J=[John]}
```
#### `partitioningBy()` Method
This method also work with the `collect` method it divides elements into exactly two groups based on a condition:
- `true` elements that match the condition
- `false` elements that do not match

The result is a `Map<Boolean, List<T>>`.
```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 12, 8, 20, 3, 15);

        Map<Boolean, List<Integer>> partitioned =
                numbers.stream()
                       .collect(Collectors.partitioningBy(n -> n > 10));

        System.out.println(partitioned);
    }
}
```
### Generics
When we worked with collections, we used `<Type>` to define the datatype of elements we want to store. This is exactly what Generics do, they allow a class or method to operate on various types of data while still enforcing compile-time type safety.  
We define a generic class by using a type parameter `<T>` after the class name.
```java
public class Box<T> {
    private T content; // The type T can be anything

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}
```
Here, we created a generic `Box` class that can work with any type. When we create an object, we replace `T` with the specific type we want the box to hold.
```java
public class Main{
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.setContent("Hello Generics");
        System.out.println("String box contains: " + stringBox.getContent());

        Box<Integer> intBox = new Box<>();
        intBox.setContent(42);
        System.out.println("Integer box contains: " + intBox.getContent());
    }
}
```
#### Multiple Type Parameters in Generics
Generics don’t have to be limited to a single type. We can define a class or method with multiple type parameters by using more than one placeholder, like `<T, R>`.  
This is useful when our class or method needs to work with more than one type of data.
```java
public class Pair<T, R> {
    private T first;
    private R second;

    public Pair(T first, R second) {
        this.first = first;
        this.second = second;
    }

    public T getFirst() {
        return first;
    }

    public R getSecond() {
        return second;
    }
}

public class Main {
    public static void main(String[] args) {
        Pair<String, Integer> pair1 = new Pair<>("Age", 25);
        System.out.println(pair1.getFirst() + ": " + pair1.getSecond());

        Pair<Double, Double> pair2 = new Pair<>(3.14, 2.71);
        System.out.println("Values: " + pair2.getFirst() + " and " + pair2.getSecond());
    }
}
```
#### Generic Methods
We can also create generic methods by declaring `<T>` before the method name. If the method returns a generic type, we can use `T` or `R` as the return type. Similarly, we can use these type parameters for the method’s parameters, such as `T t` or `R r`.
```java
public static <T, R> R getSecond(T first, R second) {
    return second; // returns the second parameter
}
```
Java will automatically determine the type of the variable.
#### Bounded Type Parameters
Sometimes, we don’t want our generic type `<T>` to accept any type. Instead, we may want it to accept only a certain group of types, such as numbers. This is where bounded type parameters come in. They allow us to restrict a type parameter by using the extends keyword.
```java
public class NumericBox<T extends Number> {
    private T number;

    public NumericBox(T number) {
        this.number = number;
    }

    public T getNumber() {
        return number;
    }

    public double doubleValue() {
        return number.doubleValue(); // safe because T extends Number
    }
}
```
Here `T extends Number` ensures that `T` can only be `Number` or its subclasses (`Integer`, `Double`, `Float`, etc.).
#### Multiple Bounds
A type parameter can also have multiple bounds using `&`. This means the type must extend a class and implement one or more interfaces.
```java
public class Printer<T extends Document & Printable> {
    private T item;

    public Printer(T item) {
        this.item = item;
    }

    public void printItem() {
        item.print();
    }
}
```
The type parameter `T` is restricted to types that **extend the `Document` class** and implement the `Printable` interface,
#### Wildcards
When we use `<T>` with a class, we are specifying a type parameter, which allows us to define the type that the class should work with. For example, we can tell the class to work with `Integer`, `String`, or any other specific type.  
But what if we don’t know exactly what type we will use? Java provides a way to handle this using an unbounded wildcard `<?>`. This allows the class or method to accept **any type**, without needing to know it in advance.
```java
import java.util.List;

public class WildcardExample {
    public static void printList(List<?> list) {
        for (Object element : list) {
            System.out.println(element);
        }
    }

    public static void main(String[] args) {
        List<Integer> intList = List.of(1, 2, 3);
        List<String> stringList = List.of("A", "B", "C");

        printList(intList);    // Works
        printList(stringList); // Works
    }
}
```
Here the `List<?>` can accept a list of any type. Inside the method, we don’t know the exact type, so elements are treated as `Object`.

#### Upper Bounded Wildcard `<? extends T>`
We use this this when we want a wildcard restricted to a type or its subclasses. It’s useful when you only need to read from a collection, not modify it.
```java
import java.util.List;

public class WildcardExample {

    public static double sumNumbers(List<? extends Number> list) {
        double sum = 0.0;
        for (Number n : list) {
            sum += n.doubleValue();
        }
        return sum;
    }

    public static void main(String[] args) {
        List<Integer> ints = List.of(1, 2, 3);
        List<Double> doubles = List.of(2.5, 3.5);

        System.out.println(sumNumbers(ints));    // 6.0
        System.out.println(sumNumbers(doubles)); // 6.0
    }
}
```
 `List<? extends Number>` can accept any list of `Number` or its subclasses (`Integer`, `Double`, etc.). We cannot add elements to the list (except `null`) because the exact subtype is unknown.
#### Lower Bounded Wildcard `<? super T>`
Lower Bounded Wildcard restricte us to a type or its **superclasses**. We use itto add elements to collection.
```java
import java.util.ArrayList;
import java.util.List;

public class WildcardExample {

    public static void addIntegers(List<? super Integer> list) {
        list.add(1);
        list.add(2);
        list.add(3);
    }

    public static void main(String[] args) {
        List<Number> numbers = new ArrayList<>();
        addIntegers(numbers);
        System.out.println(numbers); // [1, 2, 3]

        List<Object> objects = new ArrayList<>();
        addIntegers(objects);
        System.out.println(objects); // [1, 2, 3]
    }
}
```
`List<? super Integer>` can accept any list of `Integer` or its superclasses (`Number`, `Object`), we can safely add elements of type `Integer`.
### Wrapper Classes
In Java, primitive types (like `int`, `double`, and `boolean`) are designed for speed and memory efficiency. However, because they aren't objects, they can't be used with Generics or Collections (like `ArrayList<T>`).    
To bridge this gap, Java provides Wrapper Classes. These allow primitives to be "wrapped" inside an object so they can play nicely with the rest of the Java ecosystem.   
#### Autoboxing
Autoboxing is the automatic conversion the Java compiler makes between the primitive type and its corresponding object wrapper class.
```java
// Manual way (old school)
Integer manual = Integer.valueOf(10);

// Autoboxing (modern/automatic)
Integer auto = 10; 
```
#### Unboxing
Unboxing is the reverse, converting an object of a wrapper class back to its corresponding primitive value.
```java
Integer wrapper = 25; // Autoboxing
int primitive = wrapper; // Unboxing
```
### Optional Class
The Optional class is a container object used to represent a value that may or may not exist. We can see it as box that is either empty or contains a single non-null value.  
Its primary purpose is to provide a type-level solution for representing "no value," helping us avoid the dreaded `NullPointerException` without cluttering code with `if (obj != null)` checks.
#### Creating an Optional
There are three main ways to initialize an `Optional` object:
- **`empty()`**: Returns an empty `Optional` instance.
- **`of(T value)`**: Returns an `Optional` with the specified value. Throws `NullPointerException` if the value is null.
- **`ofNullable(T value)`**: Returns an `Optional` with the value if non-null, otherwise returns an empty one.
```java
Optional<String> empty = Optional.empty();
Optional<String> found = Optional.of("Hello World");
String name = null;
Optional<String> maybeName = Optional.ofNullable(name);
```
#### Retrieving Data
- **`get()`**  Returns the value if present. We use this when we are 100% sure the `Optional` is not empty, otherwise it throws a `NoSuchElementException`.
- **`orElse(T other)`**  Returns the value if present; otherwise, returns the default value we provide.
- **`orElseGet(Supplier<? extends T> supplier)`**  Similar to `orElse`, but the default value is produced by a Supplier function. Use this if creating the default value is expensive.
- **`orElseThrow()`**  Returns the value if present, otherwise throws a `NoSuchElementException`.
- **`orElseThrow(Supplier<? extends X> exceptionSupplier)`**  Returns the value if present; otherwise, throws a custom exception provided by the supplier.
```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        Optional<String> optionalName = Optional.ofNullable(null); // Could be null
        String name1 = optionalName.get(); // Throws NoSuchElementException
        
        String name2 = optionalName.orElse("Default Name");
        System.out.println("orElse: " + name2);

        String name3 = optionalName.orElseGet(() -> "Generated Default");
        System.out.println("orElseGet: " + name3);
        
        String name4 = optionalName.orElseThrow(); // throw error
        
        String name5 = optionalName.orElseThrow(() -> new IllegalArgumentException("Name is missing!"));  // throw error
    }
}
```
#### Checking & Conditional Action

- **`isPresent()`** Returns `true` if there is a value present, otherwise `false`. This is the classic way to check if the "box" is full before acting.    
- **`isEmpty()`** The inverse of `isPresent()`. Returns `true` if the `Optional` is empty.
- **`ifPresent(Consumer<? super T> action)`** If a value is present, it performs the given action (like printing or saving to a database). If empty, it does nothing at all.
- **`ifPresentOrElse(Consumer<? super T> action, Runnable emptyAction)`** If a value is present, it performs the action with that value. If the `Optional` is empty, it executes the fallback "Runnable" logic instead.
```JAVA
import java.util.Optional;

public class OptionalCheckExample {
    public static void main(String[] args) {
        Optional<String> optionalMessage = Optional.ofNullable("Hello Java!");

        // 1. Using isPresent() and isEmpty()
        if (optionalMessage.isPresent()) {
            System.out.println("Value is there!");
        }

        if (optionalMessage.isEmpty()) {
            System.out.println("The box is empty.");
        }

        // 2. Using ifPresent() to act only if data exists
        optionalMessage.ifPresent(msg -> System.out.println("Message: " + msg));

        // 3. Using ifPresentOrElse() for a complete 'if-else' flow
        Optional<String> emptyBox = Optional.empty();
        
        emptyBox.ifPresentOrElse(
            value -> System.out.println("Found: " + value),
            () -> System.out.println("Nothing was found here!") // Runs if empty
        );
    }
}
```