## Objectives
- Multithread Programming in Java
- Packages Managing and Building Tools
## Multithread Programming
When we open an application or run a program, the operating system (OS) creates a **process**. A process is a heavy-weight entity that has its own separate memory space. For example, if we open a text editor and a web browser, these are two different processes. If one crashes, it usually does not affect the other because they do not share memory.  
This separation helps the OS run multiple programs at the same time. In the early days of computing, this approach was used to make programs non-blocking. Applications were divided into smaller parts that could run in parallel. However, this method consumed many system resources because each process had its own memory space.   
Another problem was communication and data sharing. Variables created in one process were difficult to access from another process, which made inter-process communication complex and slow.   
To solve these issues, multithreading was introduced. 
### Threads
Threads are lighter-weight units of execution that run inside a process. Multiple threads share the same memory space, they can instantly access the same variables and objects, which allows faster communication, lower resource consumption, and better performance.
### Multithreading In Java
By default, Java runs our code in the `main` thread. This is a sequential flow. If we have a task that takes 10 seconds (like downloading a large file), the main thread stops and waits. This creates a blocking application the UI freezes, and the user cannot do anything else.  
To fix this we can use Multithreading, which allows us to write asynchronous, non-blocking code. We can offload the heavy task to a separate worker thread while the main thread continues to handle user interaction. It also allows us to utilize modern multi-core CPUs efficiently by performing calculations in parallel.
### Creating Threads
Java give us multiples ways to create threads.
#### Extending the Thread Class
The most common and easiest way to create a thread in Java is by extending the `Thread` class and overriding the `run()` method. The `run()` method contains the code that will be executed in the new thread.
```java
class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Worker Thread: " + i);
            try {
                Thread.sleep(500); // Pause for 500ms
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```
To start the thread, we create an instance of our class and call the `start()` method. This method creates a new thread and executes the `run()` method in that thread. If we call the `run()` method directly, it will simply execute in the current thread instead of creating a new one.
```java
public class Main {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread();
        thread1.start(); // Starts a new thread

        // The main thread continues running independently
        for (int i = 0; i < 5; i++) {
            System.out.println("Main Thread: " + i);
        }
    }
}
```
#### Implementing the Runnable Interface
Extending the `Thread` class has a major drawback: Java supports only single inheritance. If a class already extends another class, it cannot also extend `Thread`. A better and more flexible approach is to implement the `Runnable` interface. This interface represents a task that can be executed by a thread.
```java
class MyTask implements Runnable {
    @Override
    public void run() {
        System.out.println("Task is running inside: " + Thread.currentThread().getName());
    }
}
```
To use it, we first create an object of our `MyTask` class. Then, we create an object of the `Thread` class and pass our object to it. Finally, we call the `start()` method to start the thread.
```java
public class Main {
    public static void main(String[] args) {
        MyTask task = new MyTask();
        
        // Pass the task to a Thread object
        Thread thread = new Thread(task);
        thread.start();
    }
}
```
`Runnable` is a functional interface and has only one method, `run()`. This allows us to replace it with a lambda expression, where the lambda provides the implementation of the `run()` method.
```java
public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            System.out.println("Thread using lambda");
        });
        t.start();
    }
}
```
#### Using Callable and Future
The problem with the `Thread` class and the `Runnable` interface is that they **cannot return a value** from the thread after execution. To solve this, Java introduced the **`Callable` functional interface** along with the **`Future`** interface.
- **`Callable`** is similar to `Runnable` but more powerful:
    - Its `call()` method **can return a value**.
    - It can throw checked exceptions, unlike `Runnable`.
    - Being a functional interface, it can also be implemented using **lambda expressions**.
- **`Future`** represents the result of an **asynchronous computation**:
    - When a `Callable` task is submitted to an executor, it returns a `Future` object.
    - `Future` allows us to **check if the task is complete** (`isDone()`), **wait for the result** (`get()`), or **cancel the task** (`cancel()`).


To run `Callable` tasks (or even `Runnable` tasks) in Java, we need an **`ExecutorService`**. Which is part of the ``java.util.concurrent`` package and provides a high-level framework to manage threads. Instead of creating and managing Thread objects manually, we submit tasks to an executor, and it handles the threading for us, `ExecutorService` come with the following methods
- `submit(Runnable/Callable task)`: Submits a task for execution; returns a `Future` for `Callable`.
- `shutdown()`: Stops accepting new tasks but lets existing tasks finish.
- `shutdownNow()`: Attempts to stop all running tasks immediately.
- `invokeAll()`: Executes a collection of `Callable` tasks and returns a list of `Future`s.
```java
import java.util.concurrent.*;

public class ExecutorServiceExample {
    public static void main(String[] args) throws Exception {
        Callable<Integer> task = () -> {
            Thread.sleep(500);
            return 100;
        };

        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<Integer> future = executor.submit(task);

        System.out.println("Task submitted, waiting for result...");
        Integer result = future.get(); 
        System.out.println("Result: " + result);
        
        executor.shutdown();
    }
}
```
Java provides several ways to create and use **ExecutorService** through the **`Executors`** factory class:
- **Single-thread executor:** Created using `Executors.newSingleThreadExecutor()`, This executor runs tasks sequentially using only one thread, It is useful when you want to ensure that tasks are executed **one at a time in order**.
- **Fixed-size thread pool:** Created using `Executors.newFixedThreadPool(int n)`. A thread pool is a collection of worker threads that are **reused to execute multiple tasks**, instead of creating a new thread for each task,  Using a fixed-size pool limits the number of concurrent threads, which helps control resource usage and improve performance.
- **Cached thread pool:** Created using `Executors.newCachedThreadPool()`, This pool creates new threads as needed but reuses previously created threads when they are available.  
- **Scheduled thread pool:** Created using `Executors.newScheduledThreadPool(int n)`. This executor allows us to schedule tasks to run after a delay or periodically at fixed intervals.
5. **Work-stealing pool** (Java 8+): Created using ``Executors.newWorkStealingPool()``.Uses multiple threads that “steal” tasks from other threads’ queues when they are idle, optimizing parallel computation.

We can use **`Executors`** together with lambda expressions. First, we create an instance of an executor, and then we use the `execute()` method to submit a lambda expression as a task to be run by the executor.
```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        executor.execute(() -> {
            System.out.println("Thread from pool");
        });

        executor.shutdown();
    }
}
```
#### Using Fork/Join Framework
The Fork/Join Framework allows us to split tasks (“fork”) into subtasks, executed in parallel, and then combined (“joined”) to get the final result, to use it we first create a class that extends ``RecursiveTask`` if we want the task to return a result, or ``RecursiveAction`` if no result is needed. The main method ``compute()`` contains the logic for splitting and combining tasks.
```java
import java.util.concurrent.RecursiveTask;

class SumTask extends RecursiveTask<Long> {
    private int[] array;
    private int start, end;
    private static final int THRESHOLD = 10;

    public SumTask(int[] array, int start, int end) {
        this.array = array;
        this.start = start;
        this.end = end;
    }

    @Override
    protected Long compute() {
        if (end - start <= THRESHOLD) {
            long sum = 0;
            for (int i = start; i < end; i++) {
                sum += array[i];
            }
            return sum;
        } else {
            int mid = (start + end) / 2;
            SumTask left = new SumTask(array, start, mid);
            SumTask right = new SumTask(array, mid, end);

            left.fork(); // Fork left task
            long rightResult = right.compute(); // Compute right task
            long leftResult = left.join(); // Join left task

            return leftResult + rightResult;
        }
    }
}
```
Here we created the **`SumTask`** class to calculate the sum of elements in an array using parallel computation with the Fork/Join framework.  
The Constructor: takes three arguments: the array of elements, the starting index, and the ending index.   
The `compute()` method represent the main logic of the task.    
- If the number of elements is less than or equal to a threshold (here 10), it calculates the sum directly in a simple loop.
- If the segment is larger than the threshold:    
    - The array is split into two smaller subarrays.
    - Two new `SumTask` instances are created for each half.        
    - `left.fork()` starts the left task asynchronously in a separate thread.        
    - `right.compute()` computes the right half in the current thread.        
    - `left.join()` waits for the left task to finish and retrieves its result.
    - Finally, the results of the two halves are combined and returned.

#### Virtual Threads
Virtual threads are lightweight threads introduced in **Project Loom**. They allow us to run thousands or even millions of concurrent tasks without consuming the heavy OS thread resources. Unlike traditional threads, virtual threads are managed by the Java runtime rather than the operating system.   
Creating a virtual thread is extremely simple. We can use `Thread.startVirtualThread()` and pass a `Runnable` or lambda representing the task:
```java
public class Main {
    public static void main(String[] args) {
        Thread vThread = Thread.startVirtualThread(() -> {
            System.out.println("Running in virtual thread: " + Thread.currentThread().getName());
        });

        // Wait for the virtual thread to finish
        try {
            vThread.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
### Thread Lifecycle and Priority
Understanding how to create a thread is only half the battle. To write robust concurrent applications, we must understand the state of a thread at any given moment. A thread is not simply "running" or "stopped"; it transitions through specific states managed by the Java Virtual Machine (JVM) and the Operating System.
#### The Lifecycle States
In Java, a thread can exist in one of six states (defined in the `Thread.State` enum).
1. **New**: The thread object is created (using `new Thread()`), but `start()` has not been called yet. It’s just a Java object in memory.
2. **Runnable**: In Java, "Runnable" means the thread is eligible to run. It might be actually executing on the CPU, or it might be waiting in the OS scheduler's queue for its turn.
3. **Blocked**: The thread is trying to enter a `synchronized` block of code but cannot because another thread currently holds the lock. It is effectively "frozen" until the lock becomes available.
4. **Waiting**: The thread is waiting indefinitely for another thread to perform a specific action (like notifying it). This happens when calling methods like `Object.wait()` or `Thread.join()`.
5. **Timed Waiting**: Similar to Waiting, but with a timeout. The thread waits for a specified time (e.g., `Thread.sleep(1000)`). It will wake up either when the time expires or when it receives a notification.
6. **Terminated**: The `run()` method has completed execution or an unhandled exception killed the thread. The thread is dead and cannot be restarted.
#### Thread Priority
The Operating System's scheduler decides which thread runs when. However, we can provide "hints" to the scheduler using Thread Priority. Java provides priorities ranging from 1 (`MIN_PRIORITY`) to 10 (`MAX_PRIORITY`), with 5 (`NORM_PRIORITY`) being the default.
```java
Thread t = new Thread(task);
t.setPriority(Thread.MAX_PRIORITY);
t.start();
```
Priority behavior varies wildly between Operating Systems. A high-priority thread on Windows might behave differently than on Linux,  If we rely heavily on high priorities, lower-priority threads might effectively never run (resource starvation).
### Synchronization and Thread Safety
As mentioned earlier, threads share memory. While efficient, this sharing is the root of the most dangerous concurrency bug: the Race Condition. This occurs when multiple threads try to read and write to the same shared variable simultaneously, leading to corrupted data. To prevent this, we need Thread Safety. We achieve this primarily through Synchronization, which ensures that only one thread can access a critical resource at a time.
#### The `synchronized` Keyword
Java provides a built-in locking mechanism called an "intrinsic lock" or "monitor lock." Every object in Java has an internal lock. We can use the `synchronized` keyword in two ways:  
**1. Synchronized Methods** When we add `synchronized` to a method signature, the thread must acquire the lock of the object instance (`this`) before executing the method.
```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++; // Only one thread can execute this at a time
    }
}
```
**2. Synchronized Blocks** Synchronizing an entire method can be inefficient if only a small part of the code needs safety. It forces threads to wait even for non-critical operations. A synchronized block allows us to lock only the specific lines of code that modify shared state.
```java
public void addName(String name) {
    // Non-critical code runs in parallel
    System.out.println("Adding name...");

    // Critical section: locking specifically on 'this' object
    synchronized(this) {
        list.add(name);
    }
}
```
Only one thread at a time can enter and run `ist.add(name);` block for the same object instance,  If another thread tries to enter any synchronized block locked on the same object, it will wait until the first thread exits the block.
#### Explicit Locks (`ReentrantLock`)
While `synchronized` is simple, it is also rigid. If a thread tries to acquire a synchronized lock and fails, it waits forever. There is no way to say "try to get the lock for 2 seconds, then give up." For advanced scenarios, Java provides the `Lock` interface, specifically `ReentrantLock`.
```java
import java.util.concurrent.locks.ReentrantLock;

class SharedResource {
    private final ReentrantLock lock = new ReentrantLock();
    private int counter = 0;

    public void increment() {
        // Try to acquire the lock
        lock.lock(); 
        try {
            counter++;
            System.out.println(Thread.currentThread().getName() + " incremented counter to " + counter);
            
            Thread.sleep(500);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    public int getCounter() {
        return counter;
    }
}

public class ReentrantLockExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        // Create multiple threads trying to access the same resource
        Runnable task = () -> {
            for (int i = 0; i < 3; i++) {
                resource.increment();
            }
        };

        Thread t1 = new Thread(task, "Thread-1");
        Thread t2 = new Thread(task, "Thread-2");
        Thread t3 = new Thread(task, "Thread-3");

        t1.start();
        t2.start();
        t3.start();

        try {
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final counter value: " + resource.getCounter());
    }
}
```
In this example, multiple threads try to increment a shared `counter` safely. We use a **`ReentrantLock`** to control access to the critical section. When a thread calls `lock.lock()`, it acquires the lock and prevents other threads from entering the critical section until it releases the lock with `unlock()`. Placing `unlock()` in a `finally` block ensures the lock is always released, even if an exception occurs. This approach is more flexible than `synchronized`, because `ReentrantLock` allows advanced features like timed or interruptible locking, giving finer control over thread synchronization.
```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.TimeUnit;

class SharedResource {
    private final ReentrantLock lock = new ReentrantLock();

    public void tryTimedAccess(String threadName) {
        try {
            if (lock.tryLock(1, TimeUnit.SECONDS)) {
                try {
                    System.out.println(threadName + " acquired the lock");
                    Thread.sleep(2000); // Simulate work
                } finally {
                    lock.unlock();
                    System.out.println(threadName + " released the lock");
                }
            } else {
                System.out.println(threadName + " could not acquire the lock and gave up");
            }
        } catch (InterruptedException e) {
            System.out.println(threadName + " was interrupted while waiting for the lock");
        }
    }
}

public class TimedLockExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        Runnable task = () -> resource.tryTimedAccess(Thread.currentThread().getName());

        Thread t1 = new Thread(task, "Thread-1");
        Thread t2 = new Thread(task, "Thread-2");

        t1.start();
        t2.start();
    }
}
```
`tryLock(timeout, TimeUnit)` lets a thread attempt to acquire the lock for a limited time. If the lock isn’t available within the specified time, the thread gives up instead of waiting indefinitely, avoiding potential blocking. Additionally, if a thread is interrupted while waiting, it throws `InterruptedException`, allowing the program to handle it gracefully. This gives much finer control over thread synchronization compared to a standard `synchronized` block.
#### `wait()` and `notify()`
Sometimes, threads need to **coordinate based on conditions** rather than just mutual exclusion. `wait()` and `notify()` allow threads to **communicate safely** while holding a lock.
- **`wait()`**: Makes the current thread release the lock and wait until another thread signals it.
- **`notify()`**: Wakes up one waiting thread.
- **`notifyAll()`**: Wakes up all waiting threads.

These methods must be used **inside a synchronized block** on the same object.
```java
import java.util.LinkedList;
import java.util.Queue;

class SharedQueue {
    private final Queue<Integer> queue = new LinkedList<>();
    private final int CAPACITY = 5;

    public synchronized void produce(int value) throws InterruptedException {
        while (queue.size() == CAPACITY) {
            wait(); 
        }
        queue.add(value);
        System.out.println("Produced: " + value);
        notify(); // Notify waiting consumers
    }

    public synchronized int consume() throws InterruptedException {
        while (queue.isEmpty()) {
            wait(); // Wait if queue is empty
        }
        int value = queue.remove();
        System.out.println("Consumed: " + value);
        notify(); // Notify waiting producers
        return value;
    }
}
```
Here we creating a thread-safe shared queue using a `LinkedList` with a fixed capacity of 5. The `produce` method allows a producer thread to add items to the queue. If the queue is full, the thread **waits** until space becomes available. Once an item is added, it calls `notify()` to wake up any waiting consumer threads. The `consume` method allows a consumer thread to remove items from the queue. If the queue is empty, the thread **waits** until a producer adds an item. After removing an item, it calls `notify()` to wake up any waiting producer threads. Both methods are **synchronized**, ensuring that only one thread at a time can access the critical section, preventing race conditions and enabling efficient coordination between producers and consumers.
Example of usage
```java
public class ProducerConsumerExample {
    public static void main(String[] args) {
        SharedQueue queue = new SharedQueue();

        Thread producer = new Thread(() -> {
            for (int i = 1; i <= 10; i++) {
                try {
                    queue.produce(i);
                    Thread.sleep(200); 
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "Producer");

        // Consumer thread
        Thread consumer = new Thread(() -> {
            for (int i = 1; i <= 10; i++) {
                try {
                    queue.consume();
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "Consumer");

        producer.start();
        consumer.start();

        try {
            producer.join();
            consumer.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Finished producing and consuming.");
    }
}
```
We create two threads: one acting as a producer and the other as a consumer. The producer thread repeatedly adds elements to the shared queue using the `produce()` method. If the queue reaches its maximum capacity, the producer waits until the consumer removes an element. The consumer thread repeatedly takes elements from the queue using the `consume()` method. If the queue is empty, the consumer waits until the producer adds a new element. The `wait()` and `notify()` methods handle the coordination between the threads: a waiting producer is notified when the consumer removes an element, and a waiting consumer is notified when the producer adds an element. Both methods are **synchronized**, so only one thread can access the queue at a time, ensuring **thread safety** and preventing race conditions. This demonstrates how threads can efficiently communicate and work together using a shared resource.

### Common Problems in Concurrency
When we introduce locks to solve race conditions, we accidentally introduce a new class of problems. These are often difficult to debug because they are timing-dependent.
#### Deadlock
Deadlock describes a situation where two or more threads are blocked forever, waiting for each other. Imagine two friends, Alice and Bob, at a dinner table. There is only one fork and one knife.
1. Alice grabs the Fork.
2. Bob grabs the Knife.
3. Alice waits for the Knife to eat.
4. Bob waits for the Fork to eat. Neither will ever release what they hold, and neither will ever eat. In software, this happens when Thread A holds Lock 1 and waits for Lock 2, while Thread B holds Lock 2 and waits for Lock 1.
#### Livelock
Livelock is similar to Deadlock, but the threads are technically "active." Imagine two people trying to pass each other in a hallway.
1. Person A moves left to let B pass.
2. Person B moves right to let A pass.
3. They are still blocking each other, so they switch sides again simultaneously. They are constantly moving (using CPU resources), but making zero progress. This often happens when threads try to be "polite" by releasing a lock and retrying immediately, effectively synchronized in a failed loop.
### Solving Deadlocks and Livelocks
While deadlocks and livelocks are common pitfalls in concurrent programming, they can be mitigated using proper strategies and high-level concurrency tools.  
**Deadlocks** can be avoided by consistent lock ordering, timed locks, and keeping critical sections short. For example, using `ReentrantLock.tryLock(timeout)` allows a thread to attempt acquiring a lock but give up if it takes too long, preventing indefinite waiting:
```java
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.TimeUnit;

class DeadlockSafeResource {
    private final ReentrantLock lock1 = new ReentrantLock();
    private final ReentrantLock lock2 = new ReentrantLock();

    public void safeAccess() {
        try {
            if (lock1.tryLock(1, TimeUnit.SECONDS)) {
                try {
                    if (lock2.tryLock(1, TimeUnit.SECONDS)) {
                        try {
                            System.out.println(Thread.currentThread().getName() + " accessed both locks safely");
                        } finally {
                            lock2.unlock();
                        }
                    } else {
                        System.out.println(Thread.currentThread().getName() + " could not acquire lock2, giving up");
                    }
                } finally {
                    lock1.unlock();
                }
            } else {
                System.out.println(Thread.currentThread().getName() + " could not acquire lock1, giving up");
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
In this example, threads **don’t block forever**; they try to acquire locks for a limited time and give up if the lock is unavailable, preventing deadlock situations.

**Livelocks** occur when threads repeatedly retry actions without making progress. They can be solved using **backoff strategies**, where threads wait a short random time before retrying, reducing collisions:
```java
public void livelockExample(ReentrantLock lock) {
    boolean acquired = false;
    while (!acquired) {
        try {
            acquired = lock.tryLock();
            if (acquired) {
                System.out.println(Thread.currentThread().getName() + " entered critical section");
                // Simulate work
                Thread.sleep(200);
            } else {
                // Backoff before retrying
                Thread.sleep((long)(Math.random() * 100));
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            if (acquired) lock.unlock();
        }
    }
}
```
Here, threads retry with random delays instead of continuously contending for the lock, breaking the cycle that causes livelock.
### Advanced Utilities (`java.util.concurrent`)
Using raw synchronization (`wait`, `notify`, `synchronized`) is error-prone and low-level. Java’s `java.util.concurrent` package provides high-level, thread-safe building blocks.
#### Concurrent Collections
Standard collections like `HashMap` and `ArrayList` are **not thread-safe**. Using them in a multi-threaded environment can lead to crashes or corrupted data. One option is `Collections.synchronizedMap()`, but it locks the entire collection for each operation, which hurts performance. A modern solution is **`ConcurrentHashMap`**, which allows multiple threads to read and write to different parts of the map simultaneously without blocking each other.
```java
import java.util.concurrent.ConcurrentHashMap;
import java.util.Map;

public class ConcurrentMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new ConcurrentHashMap<>();

        // Thread 1
        new Thread(() -> map.put("A", 1)).start();

        // Thread 2
        new Thread(() -> map.put("B", 2)).start();

        // Thread 3
        new Thread(() -> System.out.println("Map contains: " + map)).start();
    }
}
```
Here, multiple threads safely put and read values from the `ConcurrentHashMap` without explicit locks. Unlike synchronized maps, threads don’t block each other when accessing different segments of the map, improving performance in highly concurrent scenarios.
#### Synchronization Aides
Java provides **high-level utilities** to coordinate threads efficiently beyond simple locks. Two common tools are **`CountDownLatch`** and **`Semaphore`**.  
#### CountDownLatch
A `CountDownLatch` allows a thread to wait until a specific number of other threads complete their tasks, Imagine a server that needs to load config, connect to a database, and verify cache before starting. We can use a `CountDownLatch` initialized to 3. Each task calls `countDown()` when finished. The main thread calls `await()` and will stay paused until the count reaches zero.
```java
import java.util.concurrent.CountDownLatch;

public class LatchExample {
    public static void main(String[] args) throws InterruptedException {
        CountDownLatch latch = new CountDownLatch(3);

        Runnable task = () -> {
            System.out.println(Thread.currentThread().getName() + " finished task");
            latch.countDown(); // Decrease the count
        };

        new Thread(task, "Task-1").start();
        new Thread(task, "Task-2").start();
        new Thread(task, "Task-3").start();

        latch.await(); // Main thread waits until count reaches 0
        System.out.println("All tasks completed. Main thread proceeds.");
    }
}
```
The main thread calls `await()` and waits until all three tasks finish. Each worker thread calls `countDown()` when done, allowing the main thread to continue. This is useful for **initialization steps** or waiting for multiple tasks to complete before proceeding.
#### Semaphore
A Semaphore is used to control access to a resource. Think of it like a resturant with a capacity limit. If we have a pool of 5 database connections, we can initialize a Semaphore with 5 permits.
- A thread calls `acquire()` to get a permit.
- If permits are 0, the thread waits.
- When finished, the thread calls `release()` to return the permit.
```java
import java.util.concurrent.Semaphore;

public class SemaphoreExample {
    public static void main(String[] args) {
        Semaphore semaphore = new Semaphore(2); // 2 permits

        Runnable task = () -> {
            try {
                semaphore.acquire(); // Request a permit
                System.out.println(Thread.currentThread().getName() + " acquired permit");
                Thread.sleep(1000); // Simulate resource usage
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                semaphore.release(); // Return permit
                System.out.println(Thread.currentThread().getName() + " released permit");
            }
        };

        for (int i = 1; i <= 5; i++) {
            new Thread(task, "Thread-" + i).start();
        }
    }
}
```
Here, only two threads can access the resource simultaneously because the semaphore has 2 permits. Other threads wait until a permit is released. This is ideal for limiting access to resources like database connections, thread pools, or file handles.


### CompletableFuture & Structured Concurrency
We previously discussed `Future`, which represents a result that will arrive later. The limitation of standard `Future` is that calling `.get()` blocks the thread until the result is ready. This defeats the purpose of asynchronous programming if we just end up waiting anyway.
#### CompletableFuture
`CompletableFuture` allows us to write reactive, non-blocking pipelines. Instead of waiting, we tell Java: "When this task finishes, automatically trigger this next task."
```java
CompletableFuture.supplyAsync(() -> {
    // Task 1: Fetch data (runs in a separate thread)
    return "Data fetched"; 
}).thenApply(data -> {
    // Task 2: Process data (starts automatically when Task 1 finishes)
    return data + " and processed";
}).thenAccept(result -> {
    // Task 3: Print result
    System.out.println(result);
});
```

This chain of execution is completely non-blocking. The main thread is free to do other work while this pipeline executes.

#### Structured Concurrency (Modern Java)

A common problem with `CompletableFuture` is that if we spawn 10 sub-tasks and the main task is cancelled, the 10 sub-tasks might keep running, wasting resources (this is called "thread leakage"). **Structured Concurrency** (introduced in newer Java versions like Java 21) treats a group of related tasks as a single unit of work. If the parent task fails or is cancelled, all child tasks are automatically cancelled. It uses the `StructuredTaskScope` (preview feature) to ensure that code structure mirrors the runtime execution.

Java

```
try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
    // Fork two tasks effectively in parallel
    Future<String> user = scope.fork(() -> fetchUser());
    Future<Integer> order = scope.fork(() -> fetchOrder());

    // Wait for BOTH to finish, or fail if ONE fails
    scope.join(); 
    scope.throwIfFailed();

    // Combine results
    System.out.println(user.resultNow() + " " + order.resultNow());
}
```
### CompletableFuture & Structured Concurrency
In previous sections, we discussed `Future`, which represents a result that will arrive later. The problem with a standard `Future` is that calling `.get()` blocks the thread until the result is ready. This defeats the purpose of asynchronous programming if the main thread just ends up waiting.
#### CompletableFuture
**`CompletableFuture`** allows us to write **non-blocking, reactive pipelines**. Instead of blocking, we can tell Java: “When this task finishes, automatically trigger the next task.”
```java
import java.util.concurrent.CompletableFuture;

public class CompletableFutureExample {
    public static void main(String[] args) {
        CompletableFuture.supplyAsync(() -> {
            // Task 1: Fetch data asynchronously
            return "Data fetched";
        }).thenApply(data -> {
            // Task 2: Process data automatically after Task 1
            return data + " and processed";
        }).thenAccept(result -> {
            // Task 3: Print the final result
            System.out.println(result);
        });

        // Main thread is free to do other work
        System.out.println("Main thread continues running...");
    }
}
```
The `supplyAsync()` method runs a task in a separate thread without blocking the main thread, after that the  `thenApply()` starts automatically when the previous task completes, processing the result. Finally `thenAccept()` consumes the final result. The main thread is free to continue doing other work while the tasks run asynchronously.
#### Structured Concurrency
A common problem with `CompletableFuture` is unmanaged tasks: if we spawn 10 sub-tasks and the main task is cancelled, those sub-tasks might continue running, wasting resources (called thread leakage). Structured Concurrency, introduced in modern Java (Java 21), treats a group of related tasks as a single unit of work. If the parent task fails or is cancelled, all child tasks are automatically cancelled. This ensures cleaner, safer concurrency.
```java
import java.util.concurrent.Future;
import jdk.incubator.concurrent.StructuredTaskScope;

public class StructuredConcurrencyExample {
    public static void main(String[] args) throws Exception {
        try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
            // Fork two tasks in parallel
            Future<String> user = scope.fork(() -> fetchUser());
            Future<Integer> order = scope.fork(() -> fetchOrder());

            // Wait for BOTH tasks to finish, or fail if ONE fails
            scope.join();
            scope.throwIfFailed();

            // Combine results
            System.out.println(user.resultNow() + " " + order.resultNow());
        }
    }

    static String fetchUser() throws InterruptedException {
        Thread.sleep(500);
        return "Alice";
    }

    static int fetchOrder() throws InterruptedException {
        Thread.sleep(700);
        return 123;
    }
}
```
The `StructuredTaskScope` treats multiple tasks as a single structured unit, allowing them to be managed together. The `fork()` method starts each task asynchronously, while `scope.join()` waits for all child tasks to complete before proceeding. If any child task fails, `scope.throwIfFailed()` ensures that the exception is propagated and the scope stops further execution. Additionally, when the `try` block ends, all child tasks are automatically cleaned up, which prevents **thread leakage** and ensures that no background tasks continue running unintentionally.
## Packages Managing, and Building Tools
In the past, when we worked on our programs, we often wrote everything inside a single project. However, this approach becomes problematic when we create something that should be reused. For example, if we build a utility to generate PDF reports, we may need to use it in our Finance application, our HR application, and our Inventory system.   
Novice developers sometimes copy the `PdfGenerator.java` file into every new project. This quickly turns into a maintenance nightmare. If a bug is discovered in the PDF logic, it must be fixed in multiple projects, which increases the risk of inconsistencies and wasted effort.   
To address this issue, we can use compiled class files. By compiling our code into `.class` files and sharing them, we make reuse easier. However, this solution also has limitations. A real library may contain hundreds of class files organized in a complex directory structure. Asking another developer to “download these 500 files and place them in the correct folders” is both error-prone and inefficient.   
A better approach is to package these class files into a single, organized library, making distribution, reuse, and maintenance much simpler.
### The Standard Unit: JAR Files
Java solves this with the JAR (Java ARchive).A JAR is conceptually simple: it is just a compressed ZIP file that acts as a container for everything an application needs. It usually contains:
1. **Compiled Code:** All compiled `.class` files organized by package.
2. **Resources:** Images, configuration files, database scripts, etc.
3. **Metadata:** A special file called the **Manifest** that describes the archive (for example, which class contains the `main` method to start the application).
#### Creating a JAR File
To create a JAR (Java Archive), we use the `jar` command-line tool that comes with the Java Development Kit (JDK). The process usually involves two main steps. First, we compile our source code into bytecode (`.class` files). Then, we package those compiled files into a single JAR file.
```shell
javac com/example/*.java
```
With this command the Java compiler (`javac`) to compile all `.java` files in the `com/example` directory.
```
jar cf utils.jar com
```
Here we package the compiled classes into a JAR file.
- **`jar`**: the tool used to create, update, or extract JAR files.
- **`c`**: stands for _create_, meaning we want to create a new archive.
- **`f`**: stands for file, which tells the tool that the next argument is the name of the JAR file.
- **`utils.jar`**: the name of the JAR file that will be created.
- **`com`**: the directory to include in the archive. This ensures the correct package structure is preserved inside the JAR.
#### Creating an Executable JAR
If our application contains a `main` method, we can make the JAR file executable. This allows us to run the application directly using the `java -jar` command. To do this, we need a **manifest file** that tells Java which class contains the program’s entry point.   
Example `manifest.txt`:
```
Main-Class: com.example.Main
```
This file specifies the class `Main.java` that has the `main` method. It must use the fully qualified class name (including the package). Also, the manifest file must end with a new line, or Java may not read it correctly.
```shell
jar cfm app.jar manifest.txt com
```
Here we add:
- `m` to include manifest
- **`manifest.txt`**: the file containing the entry point information.

After creating the JAR, we can run the application using:
```
java -jar app.jar
```
When creating a JAR file, the **`-C` flag** allows us to change the working directory before adding files to the archive.
```
jar cfm app.jar manifest.txt -C out .
```
**`-C out`**: changes the working directory to the `out` folder (where compiled `.class` files are stored).
#### Including a JAR Files
We can include other Jar files in our project and add them to our project compilation we use the (`-cp`) flag which tell the JVM where to look for external libraries..
```
javac -cp utils.jar com/example/Main.java
```
If our project uses multiple libraries, we can separate them with a colon (`:`) on Linux and macOS, or a semicolon (`;`) on Windows:
```
javac -cp utils.jar:logging.jar com/example/Main.java
```
This tells Java: "Look for classes in the current folder (`.`) AND inside `utils.jar`."   
We can also store all JAR files inside a `lib` folder and include them at once using a wildcard.
```shell
javac -cp "lib/*" com/example/Main.java
```
This command tells the Java compiler to include all JAR files in the `lib` directory when compiling the source file.

Jar file can also be used at runtime by adding them to the classpath when running the application:
```
java -cp "lib/*:." com.example.Main
```
- `lib/*` loads all external libraries.
- `.` allows Java to find our own compiled classes.

When compiling our project, we can specify the destination directory for the compiled `.class` files using the `-d` flag.
```
javac -d out com/example/*.java
```
- **`-d`** stands for destination, It tells the Java compiler where to place the generated `.class` files.
- **`out`** is the folder where the compiled classes will be stored. The compiler automatically creates the required package structure inside this directory.


### The Modern Problem: Dependency Hell
JARs solved the packaging problem, but they introduced a new one: Dependency Management.
Imagine we create `PDFGenerator.jar` and this package uses a third-party library called `Apache Commons`. If we want to use this package, we can't just download `PDFGenerator.jar`. we also have to find and download `Apache Commons`. And what if `Apache Commons` relies on another library? This tree of requirements is called Transitive Dependencies. Managing this manually (downloading JARs, setting Classpaths) is tedious and breaks easily. This is known as "Dependency Hell."    
To solve Dependency Hell, we use automated Build Tools. These tools connect to a central repository (like a giant App Store for code libraries) and automatically download everything our project needs.
### Maven
Maven is the most widely used build tool in the Java ecosystem. It focuses on convention over configuration. It expects our project to have a specific folder structure (e.g., source code in `src/main/java`, tests in `src/test/java`).It uses an XML file called pom.xml (Project Object Model) to describe the project.
#### Installing Maven
Unlike the `jar` command, Maven does not come pre-installed with the JDK. We must install it manually.
First we ned to download the "Binary zip archive" from the official [Apache Maven website](https://maven.apache.org/install.html). After that we extract  the zip file to a folder  `C:\Program Files\Maven` for Windows or `/opt/maven` for  Mac/Linux.
Finally we add Maven `bin` folder to our system's **PATH**.
- In Linux/Mac: add `export PATH=/opt/maven/bin:$PATH` to your `.bashrc` or `.zshrc`.
- In Windows: Edit System Environment Variables -> Path -> Add `C:\Program Files\Maven\apache-maven-3.x.x\bin`.

We can verify that our installation was successful by running:
```shell
mvn -version
```
#### Setting The Configuration
Maven, use a file named `pom.xml` to keep track of our project configuration, This file must sit in the root of our project. It is the blueprint that describes our project to Maven.
```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0.0</version>

    <dependencies>
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.8.9</version>
        </dependency>
    </dependencies>
</project>
```
Here how the configuration work:
- `<modelVersion>`: Specifies the POM model version Maven uses. `4.0.0` is the standard for modern Maven projects.
- `<groupId>`: A unique identifier for our project’s organization or group, usually following a reverse domain name convention (`com.example`).
- `<artifactId>`: The name of our project (or module). This is used when Maven builds the artifact (e.g., `my-app-1.0.0.jar`).
- `<version>`: Specifies the project version. Maven uses this when packaging and deploying our project.
- `<dependencies>`: This section lists all external libraries your project needs. Each `<dependency>` specifies:
    - `<groupId>`: The organization or group that publishes the library.
    - `<artifactId>`: The library name.
    - `<version>`: The specific version of the library you want to use.
        

Whenever we need to add a new library, we simply add another `<dependency>` entry inside `<dependencies>`. Maven will automatically download the library from the central repository and include it in our project.
#### The Standard Directory Layout
Maven relies on "Convention over Configuration." This means if we follow the standard folder structure, we don't need to configure anything it just works.
```
my-app/
├── pom.xml              (The Project Object Model)
└── src/
    ├── main/
    │   ├── java/        (Your Application Code goes here)
    │   └── resources/   (Properties, images, non-java files)
    └── test/
        ├── java/        (Your Unit Tests go here)
        └── resources/   (Test-specific configurations)
```
- **`src/main/java`**: Maven _only_ looks here for source code to compile for the final product.
- **`src/test/java`**: Maven looks here for test scripts. These are compiled but _never_ included in the final JAR.
#### Building The Project
Instead of running `javac` manually, we use the `mvn` command. Maven divides the build process into Phases.     
**Compile**
```
mvn compile
```
This command reads your `pom.xml`, downloads any missing dependencies to your local repository, and compiles the Java code in `src/main/java`. The compiled `.class` files are placed in the **`target/classes`** folder.   
Running tests
```
mvn test
```
This command first runs the `compile` phase, then compiles any test code in `src/test/java` and executes it using a test runner like **JUnit**. If any test fails, the build stops, ensuring you only package code that passes your tests.   
**Packaging**
```
mvn package
```
This phase compiles our code, runs the tests, and if everything passes, packages your project into a **JAR** file. The JAR is placed in the `target` folder, and its name is generated from our project coordinates, e.g., `my-app-1.0.0.jar`. This is the Maven equivalent of running `jar cf` manually.

**Cleaning the Project**
```
mvn clean
```
This command deletes the `target` folder, removing previous compiled classes and packaged artifacts. We can combine it with packaging:
```
mvn clean package
```
This ensures we always build a fresh, clean version of our project.     
**Installing Locally**
```
mvn install
```
After packaging, `mvn install` does everything `package` does and then **installs the artifact into our local Maven repository** (`~/.m2/repository` on Linux/Mac, `C:\Users\<username>\.m2\repository` on Windows). This allows other Maven projects on our machine to use our project as a dependency.
#### Running Excutable
If the project is executable, we need to tell Maven which class contains the `main` method. Instead of specifying it manually when creating a JAR, we can add the following configuration to `pom.xml` after the `<dependencies>` section:
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-jar-plugin</artifactId>
            <version>3.2.2</version>
            <configuration>
                <archive>
                    <manifest>
                        <mainClass>com.example.Main</mainClass>
                    </manifest>
                </archive>
            </configuration>
        </plugin>
    </plugins>
</build>
```
This configuration tells Maven which class to use as the **entry point** when running the JAR. After building, you can run your project with:
```
java -jar target/my-app-1.0.0.jar
```
### Gradle
Gradle is a modern build automation tool widely used in the Java ecosystem. Unlike Maven, which relies on XML, Gradle uses a **DSL (Domain-Specific Language)**, typically in Groovy or Kotlin (`build.gradle` or `build.gradle.kts`). Gradle also follows convention over configuration but offers more flexibility and faster builds through incremental compilation and caching.   
It is the standard build tool for Android development. A `build.gradle` file looks like this:
#### Installing Gradle
Like Maven, Gradle does not come pre-installed with the JDK. To install it w first download the **Binary-only zip** from the official [Gradle website](https://gradle.org/install/). After that we extract it to a folder:
- Windows: `C:\Program Files\Gradle`
- Linux/Mac: `/opt/gradle`.

Finally we add the `bin` folder to our system’s **PATH**:   
- Linux/Mac: add `export PATH=/opt/gradle/bin:$PATH` to `.bashrc` or `.zshrc`
- Windows: Edit System Environment Variables → Path → Add `C:\Program Files\Gradle\gradle-x.x\bin`

We can verify that our installation was successful by running:
```
gradle -v
```
#### Setting The Configuration
Gradle uses a file named `build.gradle` (or `build.gradle.kts` for Kotlin DSL) to define project configuration. This file must sit at the **root** of your project. Here’s a simple example using Groovy DSL:
```
plugins {
    id 'java'
    id 'application'
}

group = 'com.example'
version = '1.0.0'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.google.code.gson:gson:2.8.9'
    testImplementation 'junit:junit:4.13.2'
}

application {
    mainClass = 'com.example.Main'
}
```
Here is how the configuration works:
- **`plugins`**: Applies pre-built logic to our project. The `java` plugin adds Java compilation, testing, and bundling capabilities. The `application` plugin helps run the app as an executable.
- **`group` & `version`**: Similar to Maven, these identify our project and its current version.
- **`repositories`**: Tells Gradle where to look for dependencies. `mavenCentral()` is the most common public repository.
- **`dependencies`**: Lists external libraries. The format is concise: `'group:artifact:version'`.
    - **`implementation`**: Libraries required to compile and run the production code.
    - **`testImplementation`**: Libraries needed only for testing (e.g., JUnit).
- **`application`**: Configures the main entry point of the application (required by the `application` plugin).
#### The Standard Directory Layout
Gradle follows the same conventions as Maven:
```
my-app/
├── build.gradle          (Project configuration)
└── src/
    ├── main/
    │   ├── java/         (Application source code)
    │   └── resources/    (Non-Java resources)
    └── test/
        ├── java/         (Test source code)
        └── resources/    (Test-specific resources)
```
- **`src/main/java`** – Gradle compiles code here for the final product.
- **`src/test/java`** – Gradle compiles test scripts here. Tests are never included in the final JAR.

#### Building The Project
Gradle provides **tasks** instead of Maven’s phases. Common tasks include:

**Compile**
```
gradle compileJava
```
This task compiles the code in `src/main/java` and stores the `.class` files in `build/classes/java/main`.

**Running Tests**
```
gradle test
```
This task first compiles the code, then compiles tests in `src/test/java`, and finally executes them using the configured test framework (e.g., JUnit). If any test fails, the build stops.

**Packaging**
```
gradle jar
```
This task packages the compiled code into a JAR file located in `build/libs`, for example: `my-app-1.0.0.jar`. Resources from `src/main/resources` are included automatically.

**Cleaning the Project**
```
gradle clean
```
Deletes the `build` folder. Combine it with packaging:
```
gradle clean jar
```
This ensures a fresh build every time.

Gradle does not have a direct equivalent to Maven’s `install` command, but we can publish our artifact locally using the Maven Publish plugin:
```
plugins {
    id 'maven-publish'
}

publishing {
    publications {
        mavenJava(MavenPublication) {
            from components.java
        }
    }
    repositories {
        maven {
            url = uri("${buildDir}/repo")
        }
    }
}
```
Then run:
```
gradle publish
```
Our JAR will be available locally in `build/repo` for other projects to use as a dependency.
#### Running Executable JAR
We can use Gradle to run our project directly without creating a JAR by using:
```
gradle run
```
This command is available when we apply the `application` plugin, and it runs the class specified in the `mainClass` configuration.   
If we want to generate an executable JAR from our Gradle project, we need to specify the main class in the `jar` task so that Gradle knows the entry point of the application:
```
jar {
    manifest {
        attributes(
            'Main-Class': 'com.example.Main'
        )
    }
}
```
After building the project:, we can run the generated JAR file with:
```
java -jar build/libs/my-app-1.0.0.jar
```
### The Gradle Wrapper
The Gradle Wrapper is a set of scripts and configuration files that allow a project to run Gradle without requiring a global Gradle installation. Instead of depending on a version installed on the developer’s machine, the wrapper automatically downloads and uses the correct Gradle version specified by the project. 
#### Setting The Gradle Wrapper
If Gradle is already installed globally, we can generate the wrapper inside our project by running:
```
gradle wrapper
```
This creates the following files:
```
gradlew
gradlew.bat
gradle/
└── wrapper/
```
- **`gradlew`** – Script for Linux and Mac.
- **`gradlew.bat`** – Script for Windows.
- **`gradle/wrapper`** – Contains configuration and version details.

We can also specify a Gradle version:
```
gradle wrapper --gradle-version 8.5
```
If we are creating a project from the beginning, we can initialize it and generate the wrapper at the same time:
```
gradle init
```
This command creates a basic project structure and automatically adds the Gradle Wrapper. During initialization, Gradle may ask questions about the project type (Java application, library, etc.).

If we want to set a specific Gradle version after initialization:
```
gradle wrapper --gradle-version 8.5
```
#### Working With The Gradle Wrapper
Once the wrapper is created, we should use it instead of the global `gradle` command.
```shell
gradlew build      #Linux/Mac
./gradlew build    #Windows
```
Once the Gradle Wrapper is set up, we can access all Gradle tasks using it. The wrapper works exactly like the global Gradle command, but it guarantees that the correct Gradle version is used.

For example:
```
./gradlew compileJava
./gradlew test
./gradlew jar
./gradlew clean
./gradlew run
```
