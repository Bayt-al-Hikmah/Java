## Objectives
- Working with Files (I/O)
- Error Handling and Annotations
## Working with Files
When we create programs, all our data and calculations are stored in memory (RAM). The problem is that when we exit the program or restart the computer, all this data is lost. To solve this problem, we store our progress on a hard drive instead of in memory.   
There are multiple ways to store data permanently, such as using databases, images, videos, or files, depending on the type of data. One of the easiest methods is using files. Files allow us to store data permanently (persistence) so it is not lost when the program stops.   
In Java, input and output operations are handled using **streams**. A stream is a sequence of data that flows from a source (such as a file) to a destination (such as a program). Streams make it possible to read and write data efficiently between programs and storage devices.
### The File Class
To work with files in Java, we use the `java.io.File` class. This class represents a file or directory path. It does **not** read or write data. Instead, it is used to:
- Create files and directories
- Check file properties
- Delete files
- Get file information
```java
import java.io.File;
import java.io.IOException;

public class FileExample {
    public static void main(String[] args) {
        File file = new File("data.txt");
		if (file.createNewFile()) {
			System.out.println("File created: " + file.getName());
		} else {
			System.out.println("File already exists.");
		}
    }
}
```
Some methods from `java.io.File`:
- `createNewFile()`: Creates a new file
- `exists()`: Checks if file exists
- `getName()`: Returns file name
- `getPath()`: Returns file path
- `canRead()`: Checks if file is readable
- `canWrite()`: Checks if file is writable
- `length()`: Returns file size
- `delete()`: Deletes the file
- `mkdir()`: Creates a directory
- `mkdirs()`: Creates directories including parents
- `listFiles()`: Lists files in directory
```java
import java.io.File;
import java.io.IOException;

public class FileMethodsExample {
    public static void main(String[] args) {
    
            File dir = new File("testDir/subDir");
            if (dir.mkdirs()) {
                System.out.println("Directories created: " + dir.getPath());
            } else {
                System.out.println("Directories already exist.");
            }
            File file = new File(dir, "example.txt");

            if (file.createNewFile()) {
                System.out.println("File created: " + file.getName());
            } else {
                System.out.println("File already exists.");
            }
            System.out.println("File exists? " + file.exists());
            System.out.println("File name: " + file.getName());
            System.out.println("File path: " + file.getPath());
            System.out.println("Can read? " + file.canRead());
            System.out.println("Can write? " + file.canWrite());
            System.out.println("File size (bytes): " + file.length());

            // 9. mkdir() (single directory)
            File singleDir = new File("singleFolder");
            if (singleDir.mkdir()) {
                System.out.println("Single directory created: " + singleDir.getName());
            } else {
                System.out.println("Single directory already exists.");
            }

            File parentDir = new File("testDir");
            File[] files = parentDir.listFiles();

            System.out.println("\nFiles inside 'testDir':");
            for (File f : files) {
                if (f.isFile()) {
                    System.out.println("File: " + f.getName());
                } else if (f.isDirectory()) {
                    System.out.println("Directory: " + f.getName());
                }
            }
        
            if (file.delete()) {
                System.out.println("\nFile deleted: " + file.getName());
            } else {
                System.out.println("Failed to delete file.");
            }

            // Delete directories (must be empty first)
            if (dir.delete()) {
                System.out.println("Sub directory deleted.");
            }

            if (parentDir.delete()) {
                System.out.println("Parent directory deleted.");
            }
    }
}
```
### Reading and Writing
Java provides multiple ways to read and write data to files. These methods differ depending on our needs. If we want to work with simple text, we can use text-based classes such as `FileReader` and `FileWriter`. If we want to read and write binary data, such as images, audio, or videos, we can use byte-based classes like `FileInputStream` and `FileOutputStream`.
### Writing to a File
#### FileWriter
The first class that Java provides for writing data to files is **`FileWriter`**. We use this class to write **text data** to a file. It allows us to store characters, strings, and text content easily.   
To use `FileWriter`, we first import it, then create an object using the file path. After that, we can write data using the `write()` method. Finally, we must close the file to save the data properly.
```java
import java.io.FileWriter;
import java.io.IOException;

public class WriteExample {
    public static void main(String[] args) {
        FileWriter writer = new FileWriter("data.txt");
		writer.write("Hello, this is written using FileWriter.");
        writer.write("\nJava makes file writing easy.");
        writer.close();
        System.out.println("Data written successfully.");
    }
}
```
The `FileWriter` class comes with several built-in methods, such as:
- `write(String str)`: Writes a string to the file
- `write(int c)`: Writes a single character
- `write(char[] c)`: Writes an array of characters
- `flush()`: Forces data to be written immediately
- `close()`: Closes the file and saves data

By default, `FileWriter` overwrites the file. To add new data without deleting the old content, we use append mode by adding `true` as second argument to ``FileWriter()`` constructor
```java
FileWriter writer = new FileWriter("data.txt", true);
```
#### BufferedWrite
The **`BufferedWriter`** class is used to write text data to a file more efficiently than `FileWriter`. It works by storing data in a buffer (temporary memory) before writing it to the file. This reduces the number of direct disk operations and improves performance, especially when working with large files.   
`BufferedWriter` is usually used together with `FileWriter`. We first create a `FileWriter` object, then wrap it inside a `BufferedWriter` object. After that, we can write data using the `write()` method. Finally, we close the writer to save the data.
```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class BufferedWriteExample {
    public static void main(String[] args) throws IOException {

        BufferedWriter writer = new BufferedWriter(
                new FileWriter("data.txt")
        );

        writer.write("Hello, this is written using BufferedWriter.");
        writer.newLine(); // Adds a new line
        writer.write("Buffered writing is faster.");

        writer.close();

        System.out.println("Data written successfully.");
    }
}
```
The `BufferedWriter` class comes with several built-in methods, such as:
- `write(String str)`: Writes a string to the file
- `write(int c)`: Writes a single character
- `write(char[] c)`: Writes an array of characters
- `newLine()`: Writes a line separator
- `flush()`: Forces buffered data to be written immediately
- `close()`: Closes the writer and saves data

Like `FileWriter`, `BufferedWriter` can also work in append mode. We enable this by passing `true` to the `FileWriter` constructor:
```java
BufferedWriter writer = new BufferedWriter(
        new FileWriter("data.txt", true)
);
```
This will add new data at the end of the file instead of overwriting it.
#### FileOutputStream
Finally The **`FileOutputStream`** class is used to write binary data to a file. Unlike `FileWriter` and `BufferedWriter`, which are used for text, `FileOutputStream` works with bytes. It is commonly used to write files such as images, audio, videos, and other non-text data.  
We use `FileOutputStream` when we want to store raw binary data. First, we import the class, then create an object using the file path. After that, we write data using the `write()` method. Finally, we close the stream to save the data properly.
```java
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputStreamExample {
    public static void main(String[] args) throws IOException {

        FileOutputStream output = new FileOutputStream("data.bin");

        // Write bytes to file
        output.write(65); // Writes 'A'
        output.write(66); // Writes 'B'
        output.write(67); // Writes 'C'

        output.close();

        System.out.println("Binary data written successfully.");
    }
}
```
The `FileOutputStream` class comes with several built-in methods, such as:
- `write(int b)`: Writes one byte to the file
- `write(byte[] b)`: Writes an array of bytes
- `write(byte[] b, int off, int len)`: Writes part of a byte array
- `flush()`: Forces buffered data to be written immediately
- `close()`: Closes the stream and saves data


Instead of writing one byte at a time, we can write multiple bytes at once:
```java
byte[] data = {65, 66, 67, 68, 69}; // A B C D E

FileOutputStream output = new FileOutputStream("data.bin");
output.write(data);
output.close();
```
By default, `FileOutputStream` overwrites the file. To enable append mode, we pass `true` as the second argument to the constructor:
```java
FileOutputStream output = new FileOutputStream("data.bin", true);
```
### Reading from a File
#### FileReader
The **`FileReader`** class is used to read text data from a file character by character. It is the counterpart of `FileWriter`.   
To use it, we first import the class, create a `FileReader` object with the file path, and then read the data using the `read()` method. Finally, we close the reader.
```java
import java.io.FileReader;
import java.io.IOException;

public class FileReaderExample {
    public static void main(String[] args) throws IOException {
        FileReader reader = new FileReader("data.txt");
        int c;

        // Read characters one by one
        while ((c = reader.read()) != -1) {
            System.out.print((char) c);
        }

        reader.close();
    }
}
```
The `FileReader` class comes with several built-in methods, such as:
- `read()`: Reads a single character and returns its ASCII code
- `read(char[] c)`: Reads characters into an array
- `close()`: Closes the reader
#### BufferedReader
The **`BufferedReader`** class is used to read text data **efficiently**, especially for large files. It reads data in blocks (buffered), reducing the number of disk operations. It also provides convenient methods like `readLine()` to read an entire line at a time.
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class BufferedReaderExample {
    public static void main(String[] args) throws IOException {
        BufferedReader reader = new BufferedReader(new FileReader("data.txt"));
        String line;

        // Read file line by line
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }

        reader.close();
    }
}
```
The `BufferedReader` class comes with several built-in methods, such as:
- `read()`: Reads a single character
- `readLine()`: Reads an entire line as a string
- `close()`: Closes the reader
- `ready()`: Checks if the reader is ready to be read
#### Scanner
The **`Scanner`** class can also be used to read files. It is simple and convenient for reading lines, words, or tokens from a text file.
```java
import java.io.File;
import java.io.IOException;
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) throws IOException {
        File file = new File("data.txt");
        Scanner sc = new Scanner(file);

        // Read file line by line
        while (sc.hasNextLine()) {
            String line = sc.nextLine();
            System.out.println(line);
        }

        sc.close();
    }
}
```
- `nextLine()`: Reads the next line    
- `next()`: Reads the next token
- `hasNextLine()`: Checks if there is another line
- `hasNext()`: Checks if there is another token

Token is the chunk of text separated by **delimiters** (by default, whitespace: space, tab, or newline), we can change the default delimiter using `sc.useDelimiter(",");`
#### FileInputStream
Finally the **`FileInputStream`** class is used to read binary data from a file, `FileInputStream` works with bytes, making it ideal for reading images, audio, video, and other non-text files.  
To use `FileInputStream`, we first import it, then create an object using the file path. After that, we read data using the `read()` method. Finally, we close the stream to release resources.
```java
import java.io.FileInputStream;
import java.io.IOException;

public class FileInputStreamExample {
    public static void main(String[] args) throws IOException {

        FileInputStream input = new FileInputStream("data.bin");
        int b;

        // Read bytes one by one
        while ((b = input.read()) != -1) {
            System.out.print((char) b); // cast byte to char for display
        }

        input.close();
        System.out.println("\nBinary data read successfully.");
    }
}
```
`FileInputStream` come with other methods such us
- `read()`: Reads **one byte** at a time, returns -1 at end of file
- `read(byte[] b)`: Reads multiple bytes into an array
- `read(byte[] b, int off, int len)`: Reads part of a byte array
- `available()`: Returns the number of bytes available to read
- `close()`: Closes the stream

Instead of reading one byte at a time, we can read multiple bytes into a byte array for better performance:
```java
import java.io.FileInputStream;
import java.io.IOException;

public class FileInputStreamArray {
    public static void main(String[] args) throws IOException {
        FileInputStream input = new FileInputStream("data.bin");

        byte[] data = new byte[input.available()]; // create array of file size
        input.read(data); // read all bytes into array

        for (byte b : data) {
            System.out.print((char) b);
        }

        input.close();
    }
}
```

### Modern File Handling (`java.nio.file`)
Java introduced the **`java.nio.file`** package in Java 7 to provide a modern, efficient, and flexible way to handle files and directories. The NIO.2 offers:
- Easier file manipulation (create, delete, copy, move)
- Better support for paths and directories
- Improved error handling through exceptions
- Non-blocking I/O support (`AsynchronousFileChannel`)
- Stronger support for symbolic links and file attributes

It come with collection of classes that simplify the working with files:
- `Path`: Represents a path to a file or directory (replaces `File`)
- `Files`: Provides static methods to create, read, write, copy, move, and delete files
- `Paths`: Helper class to create `Path` objects
- `FileSystem`: Represents the file system (advanced usage)
- `WatchService`: Monitors file system changes (create, modify, delete)
- `AsynchronousFileChannel`: Supports async I/O operations for high-performance apps
#### Creating and Writing to Files
When we work with NIO.2,  Package we dom't use File object directly, we start with a Path Object which represent the file location on our hard drive, After that we can use `Files.write()` method to write data into the file.   
The `write` take the following arguments
- **`path`**  The `Path` object representing the file location.
- **`bytes` or `lines`** The content to write
- **`OpenOption... options`** Optional flags to control writing behavior. If omitted, the file will be created if it doesn’t exist and overwritten if it exists.

The common glags we can use are the following
- `StandardOpenOption.CREATE`: Create the file if it doesn’t exist
- `StandardOpenOption.CREATE_NEW`: Create a new file, fail if it exists
- `StandardOpenOption.APPEND`: Append to the file instead of overwriting
- `StandardOpenOption.TRUNCATE_EXISTING`: Truncate the file to zero length before writing
- `StandardOpenOption.WRITE`: Open the file for writing
- `StandardOpenOption.READ`: Open the file for reading (used with channels)
```java
import java.nio.file.*;
import java.io.IOException;

public class NIOWriteExample {
    public static void main(String[] args) {
        Path path = Paths.get("nioData.txt");
        String content = "Hello NIO.2! This is a modern way to handle files.";

        try {
            // Converts String to bytes and writes in one shot
            Files.write(path, content.getBytes(), StandardOpenOption.CREATE, StandardOpenOption.TRUNCATE_EXISTING);
            System.out.println("File created and written successfully.");
        } catch (IOException e) {
            System.err.println("Failed to write file: " + e.getMessage());
        }
    }
}
```
#### Reading from Files
With `File` object we can also read data from files, the common methods to read files are the following

1. **`Files.readAllBytes(Path path)`**: Reads the entire file content as a byte array. Good for small files because it loads everything into memory.
2. **`Files.readAllLines(Path path)`**: Reads all lines of the file into a `List<String>`. Convenient if you want to process the file line by line.
3. **`Files.lines(Path path)`**: Returns a **`Stream<String>`**, which allows lazy reading and processing of large files line by line. Useful when we want to process files efficiently without loading the entire content into memory.
4. **`Files.newBufferedReader(Path path)`**: Returns a `BufferedReader` to read the file using standard reader methods. Allows more control over reading, such as reading line by line, skipping lines, or reading in custom encodings.
5. **`Files.newInputStream(Path path, OpenOption... options)`** : Returns an `InputStream` to read raw bytes from the file. Can be combined with options like `StandardOpenOption.READ` for fine-grained control.


**Using `readAllBytes`**
```java
import java.nio.file.*;
import java.io.IOException;

public class NIOReadBytesExample {
    public static void main(String[] args) {
        Path path = Paths.get("nioData.txt");

        try {
            byte[] data = Files.readAllBytes(path);
            String content = new String(data);
            System.out.println("File content: " + content);
        } catch (IOException e) {
            System.err.println("Failed to read file: " + e.getMessage());
        }
    }
}
```
**Using `readAllLines`**
```java
import java.nio.file.*;
import java.io.IOException;
import java.util.List;

public class NIOReadLinesExample {
    public static void main(String[] args) {
        Path path = Paths.get("nioData.txt");

        try {
            List<String> lines = Files.readAllLines(path);
            lines.forEach(System.out::println);
        } catch (IOException e) {
            System.err.println("Failed to read file: " + e.getMessage());
        }
    }
}
```
**Using `lines()` with Stream**
```java
import java.nio.file.*;
import java.io.IOException;
import java.util.stream.Stream;

public class NIOReadStreamExample {
    public static void main(String[] args) {
        Path path = Paths.get("nioData.txt");

        try (Stream<String> lines = Files.lines(path)) {
            lines.forEach(System.out::println);
        } catch (IOException e) {
            System.err.println("Failed to read file: " + e.getMessage());
        }
    }
}
```
**Using `newBufferedReader`**
```java
import java.nio.file.*;
import java.io.IOException;
import java.io.BufferedReader;

public class NIOBufferedReaderExample {
    public static void main(String[] args) {
        Path path = Paths.get("nioData.txt");

        try (BufferedReader reader = Files.newBufferedReader(path)) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Failed to read file: " + e.getMessage());
        }
    }
}
```
**Using `newInputStream` with options**
```java
import java.nio.file.*;
import java.io.IOException;
import java.io.InputStream;

public class NIOInputStreamExample {
    public static void main(String[] args) {
        Path path = Paths.get("nioData.txt");

        try (InputStream in = Files.newInputStream(path, StandardOpenOption.READ)) {
            int b;
            while ((b = in.read()) != -1) {
                System.out.print((char) b);
            }
        } catch (IOException e) {
            System.err.println("Failed to read file: " + e.getMessage());
        }
    }
}
```
#### Copying, Moving, and Deleting Files
The `Files` utility class provides straightforward methods to manipulate the file system. These operations are typically atomic if the underlying file system supports it, and they often use **`CopyOption`** to define how the operation should behave.
1. **`Files.copy(Path source, Path target, CopyOption... options)`**: Copies a file from one location to another. Use `StandardCopyOption.REPLACE_EXISTING` to overwrite a file if it already exists.
2. **`Files.move(Path source, Path target, CopyOption... options)`**: Moves or renames a file. This is more efficient than copying and deleting.
3. **`Files.delete(Path path)`**: Deletes the file or directory. It throws an `IOException` if the file doesn't exist or the directory is not empty.
4. **`Files.deleteIfExists(Path path)`**: A safer version of delete that returns a boolean and does not throw an exception if the file is missing.

```java
import java.nio.file.*;
import java.io.IOException;

public class NIOFileOperations {
    public static void main(String[] args) {
        Path source = Paths.get("source.txt");
        Path target = Paths.get("target.txt");
        Path moved = Paths.get("backup/moved_file.txt");

        try {
            // Copying
            Files.copy(source, target, StandardCopyOption.REPLACE_EXISTING);
            System.out.println("File copied.");

            // Moving (renaming and shifting to another directory)
            Files.createDirectories(moved.getParent()); // Ensure backup folder exists
            Files.move(target, moved, StandardCopyOption.ATOMIC_MOVE);
            System.out.println("File moved.");

            // Deleting
            boolean deleted = Files.deleteIfExists(moved);
            System.out.println("File deleted: " + deleted);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### Working with Directories
NIO makes directory traversal and creation much cleaner than the old `File` API. It provides tools to either create single folders or entire nested paths.
1. **`Files.createDirectory(Path path)`**: Creates a single directory. Fails if the parent doesn't exist.
2. **`Files.createDirectories(Path path)`**: Creates a directory and any missing parent directories in the path (recursive creation).
3. **`Files.newDirectoryStream(Path dir)`**: Iterates over the immediate children of a directory. It is more memory-efficient than `File.listFiles()`.
4. **`Files.walk(Path start)`**: Returns a `Stream<Path>` that traverses the directory tree depth-first.
```java
import java.nio.file.*;
import java.io.IOException;

public class NIODirectoryExample {
    public static void main(String[] args) {
        Path dirPath = Paths.get("myProjects/javaNIO");

        try {
            // Recursive directory creation
            Files.createDirectories(dirPath);

            // Listing contents using DirectoryStream
            try (DirectoryStream<Path> stream = Files.newDirectoryStream(Paths.get("."))) {
                System.out.println("Directory contents:");
                for (Path entry : stream) {
                    System.out.println(entry.getFileName() + " | Directory: " + Files.isDirectory(entry));
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
#### File Attributes
NIO allows us to access file metadata (size, timestamps, permissions) in a single bulk operation, which is significantly faster than requesting each attribute individually.
1. **`BasicFileAttributes`**: Provides standard metadata like creation time, last access time, and file size.
2. **`Files.readAttributes(Path, Class)`**: Reads a group of attributes in one go.

```java
import java.nio.file.*;
import java.nio.file.attribute.BasicFileAttributes;
import java.io.IOException;

public class NIOAttributesExample {
    public static void main(String[] args) {
        Path path = Paths.get("nioData.txt");

        try {
            BasicFileAttributes attr = Files.readAttributes(path, BasicFileAttributes.class);

            System.out.println("Creation Time: " + attr.creationTime());
            System.out.println("Last Modified: " + attr.lastModifiedTime());
            System.out.println("Is Directory: " + attr.isDirectory());
            System.out.println("Size: " + attr.size() + " bytes");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
We also have access to the following methods: 
- **`Files.exists(path)`**: A quick check to see if the file is there.
- **`Files.size(path)`**: Returns the file size in bytes.
- **`Files.getLastModifiedTime(path)`**: Useful for backup systems to check if a file has changed.
- `Files.isHidden(path)`: check hidden files
- `Files.getLastModifiedTime(path)`: get last modified timestamp
- `Files.getOwner(path)`: get file owner
- `Files.getPosixFilePermissions(path)`: file permissions (on UNIX systems)
#### Watching File System Changes
The **`WatchService`** is an API that allows us to "listen" for changes to a directory, such as when a file is created, modified, or deleted. This is highly useful for auto-reloading configurations or logging systems.
1. **`FileSystems.getDefault().newWatchService()`**: Creates the watcher.
2. **`register()`**: Links the path to the watcher for specific events.
3. **`WatchKey`**: Represents the registration; we poll this key to see if any events have occurred.
```java
import java.nio.file.*;
import static java.nio.file.StandardWatchEventKinds.*;

public class NIOWatchServiceExample {
    public static void main(String[] args) throws Exception {
        WatchService watcher = FileSystems.getDefault().newWatchService();
        Path dir = Paths.get(".");
        
        // Register for creation and deletion events
        dir.register(watcher, ENTRY_CREATE, ENTRY_DELETE);

        System.out.println("Watching directory for changes...");

        while (true) {
            WatchKey key = watcher.take(); // Wait for an event
            for (WatchEvent<?> event : key.pollEvents()) {
                System.out.println("Event: " + event.kind() + " on file: " + event.context());
            }
            if (!key.reset()) break; // Continue watching
        }
    }
}
```
We started with creating a **`WatchService`**, which acts as a dedicated background listener for file system activity. To make this listener active, we register a specific **`Path`** in this case, and provide to it  specific flags or event kinds. 
- **`ENTRY_CREATE`** Tell the system to notify our program only when a new file is added
- **`ENTRY_DELETE`**: Tell the system to notify our program only when a existing file is removed.
 
To keep the monitoring alive, we use infinite while loop. Inside this loop, the method is **`watcher.take()`**. make our program goes to sleep, and wait the operating system to send a hardware-level signal that matches our registered flags at which point the thread "wakes up" and returns a `WatchKey`.   

Once the program receives a signal, we handle the data associated with it. Since multiple changes can happen at the exact same time , we use for-each loop to iterate through all pending events. For every event, we extract the **`kind()`**, which describes the action that took place, and the **`context()`**, which represents the name of the file or directory that triggered the change.
## Error Handling and Annotations
## Errors Handeling
As humans, we are prone to mistakes. When writing code, it is easy to misspell a class name, use the wrong data type for a parameter, or forget a semicolon (`;`). These slips cause our programs to fail, but thankfully, the Java Compiler catches these compile-time errors immediately, preventing us from running a broken program.   
However, not all errors are related to syntax. Sometimes the code is written correctly according to the rules of the language, but the logic or implementation is flawed. These are known as runtime errors.   
To help catch these logic-based issues early, Java provides Annotations. These act as metadata that enforce specific rules in our code. If we break those rules, the annotation triggers the compiler to throw an error before the program ever runs.
### Annotations
Annotations are a powerful form of metadata that we can add to our Java code. They don't change the execution of the logic directly, but they provide critical information to the compiler or the runtime environment.     
Before annotations were introduced, developers often relied on heavy XML configuration files. Now, we can bake those rules directly into the source code, making it much easier to read and maintain.
#### Common Built-in Annotations
Java provides several standard annotations that help developers avoid common pitfalls. Here are the most frequently used ones:

- **`@Override`**: Perhaps the most common annotation. It tells the compiler that the method is intended to override a method in its superclass. If we misspell the method name or get the parameters wrong, the compiler will alert us immediately rather than treating it as a new, separate method.
- **`@Deprecated`**: This marks a method, field, or class as "old" or "obsolete." It warns other developers that while the code still works, it might be removed in future versions and they should find an alternative.
- **`@SuppressWarnings`**: Sometimes the compiler gives us warnings that we know are safe to ignore. This annotation tells the compiler to "hush" and stop showing specific warnings for that block of code.
- **`@FunctionalInterface`**: Used on interfaces that are intended to have exactly one abstract method. This ensures the interface can be used safely with Lambda expressions.

#### Creating Costume Annotations
Java built-in annotations do not cover all of our possible use cases and problems. To address this, Java allows us to create our own custom annotations.   
We can create a custom annotation using the `@interface` keyword. Each annotation typically includes two important metadata annotations: `@Target` and `@Retention`.  
`@Target` specifies where the annotation can be applied. It restricts the usage of the annotation to certain elements in the code.

It can have the following common values from the `ElementType` enum:
- `ElementType.TYPE` Class, interface, enum, or record
- `ElementType.FIELD` Fields (instance variables)
- `ElementType.METHOD` Methods 
- `ElementType.PARAMETER` Method parameters
- `ElementType.CONSTRUCTOR` Constructors
- `ElementType.LOCAL_VARIABLE` Local variables
- `ElementType.ANNOTATION_TYPE` Another annotation
- `ElementType.PACKAGE` Package declarations

`@Retention` defines how long the annotation is retained in the program lifecycle. It uses values from the `RetentionPolicy` enum:  
- `RetentionPolicy.SOURCE`  The annotation is available only in the source code and discarded during compilation.  
- `RetentionPolicy.CLASS` The annotation is stored in the compiled `.class` file but not available at runtime (default behavior).
- `RetentionPolicy.RUNTIME`  The annotation is available at runtime through reflection.

```java
import java.lang.annotation.*;

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
    // body
}
```
Here the annotation can only be applied to classes (TYPE) and it is available at runtime.  
The body of an annotation contains elements, which look like methods but are not regular methods, they don't have body and can have default value.
```java
import java.lang.annotation.*;

@Target(ElementType.TYPE)

@Retention(RetentionPolicy.RUNTIME)
public @interface AppConfig {
    String appName();
    int version() default 1;
}
```
Now, we can apply this annotation to a class:
```java
@AppConfig(appName = "MyApplication", version = 2)
public class Main {
    public static void main(String[] args) {
        System.out.println("Application running...");
    }
}
```
Finally we can access and read out annotation from other classes and program
```java
import java.lang.annotation.Annotation;

public class AnnotationReader {
    public static void main(String[] args) {

        // Get the Class object of Main
        Class<Main> clazz = Main.class;

        // Check if the class has the AppConfig annotation
        if (clazz.isAnnotationPresent(AppConfig.class)) {

            // Get the annotation instance
            AppConfig config = clazz.getAnnotation(AppConfig.class);

            // Read values from the annotation
            System.out.println("App Name: " + config.appName());
            System.out.println("Version: " + config.version());
        } else {
            System.out.println("No AppConfig annotation found.");
        }
    }
}
```
This allows us to set configurations, build larger projects more efficiently, and even throw errors if required elements or settings are missing.  
Similarly, we can create annotations for methods and access them at runtime.  
```java
import java.lang.annotation.*;

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface RunMe {
    String description() default "No description";
}
```
Using it in method
```java
public class MyClass {

    @RunMe(description = "This method runs important logic")
    public void importantMethod() {
        System.out.println("Important method executed!");
    }
}
```
Finally we can read it as following
```java
import java.lang.reflect.Method;

public class MethodAnnotationReader {
    public static void main(String[] args) throws Exception {
        Class<MyClass> clazz = MyClass.class;

        // Iterate over all methods of the class
        for (Method method : clazz.getDeclaredMethods()) {

            // Check if the method has @RunMe annotation
            if (method.isAnnotationPresent(RunMe.class)) {
                RunMe annotation = method.getAnnotation(RunMe.class);
                // Print annotation info
                System.out.println("Method: " + method.getName());
                System.out.println("Description: " + annotation.description());
                // Optionally, invoke the method
                method.invoke(clazz.getDeclaredConstructor().newInstance());
            }
        }
    }
}
```
### Catching Runtime Error
Even when we use annotations and debugging in our code, we can still encounter errors. Some errors are beyond our control. For example, when we take input from a user, we cannot always be sure that the user entered valid data. These types of errors are called runtime errors because they occur while the program is running and can cause it to crash.    
Fortunately, Java provides a mechanism to catch and handle exceptions when they occur, using the `try-catch` block.
#### try-catch in Java
In Java, a `try-catch` block allows us to handle exceptions:
1. **try block** We place the code that might cause an error inside the `try` block.
2. **catch block** The `catch` block captures the exception and executes instructions to handle it, preventing the program from crashing.
```java
try {
    // Code that might throw an exception
    int result = 10 / 0; // This will cause an ArithmeticException
} catch (Exception e) {
    System.out.println("An error occurred: " + e.getMessage());
}
```
Catch block is used to handle a specific type of exception or any of its subclasses. If we use the general `Exception` type, it will catch all exceptions, but we can handle a specific exception, by specifying its type explicitly.
```java
public class ExceptionExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;
            String text = null;
            System.out.println(text.length());
            
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero.");
        } catch (NullPointerException e) {
            System.out.println("Error: Tried to access a null object.");
        } catch (Exception e) {
            System.out.println("An unexpected error occurred: " + e.getMessage());
        }  
        System.out.println("Program continues running...");
    }
}
```
We can also catch multiple exceptions using single catch block by separating them with `|`
```java
public class MultiCatchExample {
    public static void main(String[] args) {
        try {
            int[] numbers = {1, 2, 3};
            System.out.println(numbers[5]); // ArrayIndexOutOfBoundsException
            int result = 10 / 0; // ArithmeticException
        } catch (ArithmeticException | ArrayIndexOutOfBoundsException e) {
            System.out.println("An error occurred: " + e.getMessage());
        }

        System.out.println("Program continues...");
    }
}
```
Sometimes, we still want to run a block of code regardless of whether an exception occurred or not. To do this, we use the `finally` block.    
The `finally` block is always executed after the `try` and `catch` blocks, even if an exception is thrown or a return statement is executed. It is typically used for clean-up operations, such as closing files, releasing resources, or clearing memory.
```java
public class FinallyExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // This will throw ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Caught exception: " + e.getMessage());
        } finally {
            System.out.println("This block always runs, cleaning up resources...");
        }

        System.out.println("Program continues running...");
    }
}
```
#### try with Resources
The modern versions of Java (7 and above) introduced the **`try-with-resources`** feature, which automatically closes resources that implement the `AutoCloseable` interface. This allows us to write cleaner and safer code without the need for verbose `finally` blocks.  
We open the resouce before the try block 
```java
try (ResourceType resource = new ResourceType()) {
    // Use the resource
} catch (ExceptionType e) {
    // Handle exceptions
}
```
Example reading from file.
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class TryWithResourcesExample {
    public static void main(String[] args) {
        // Automatically closes BufferedReader
        try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
            String line = reader.readLine();
            System.out.println(line);
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }

        System.out.println("Program continues...");
    }
}
```
#### Throwing Errors
Java allows us to do more than just catching runtime errors, we can also throw exceptions ourselves. This is useful when working on large projects where we want to prevent others from accidentally misusing our code or to enforce certain rules in our program.   
To throw an exception, use the `throw` keyword followed by an instance of `Exception`
```java
public class ThrowExample {
    static void checkAge(int age) {
        if (age < 18) {
            // Throw an exception if the user is under 18
            throw new IllegalArgumentException("Age must be 18 or older.");
        } else {
            System.out.println("Access granted.");
        }
    }

    public static void main(String[] args) {
        try {
            checkAge(15); // This will cause an exception
        } catch (IllegalArgumentException e) {
            System.out.println("Caught an exception: " + e.getMessage());
        }

        System.out.println("Program continues running...");
    }
}
```
#### The `throws` Keyword
We can’t anticipate all possible scenarios that might occur inside our methods, but we can often predict the types of errors that are likely to happen. Java allows us to declare that a method might throw specific types of exceptions by using the `throws` keyword. This helps notify anyone using the method that they need to handle these potential errors.
```java
import java.io.IOException;

public class ThrowsExample {
    // This method declares that it might throw an IOException
    static void readFile(String filename) throws IOException {
        if (filename == null) {
            throw new IOException("Filename cannot be null.");
        }
        System.out.println("Reading file: " + filename);
    }

    public static void main(String[] args) {
        try {
            readFile(null); // This will throw an IOException
        } catch (IOException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
        
        System.out.println("Program continues running...");
    }
}
```
We can declare that the method could throws more than one exception by separating the exception types with a comma.
```java
import java.io.IOException;

public class MultiThrowExample {
    static void riskyMethod(boolean ioProblem, boolean arithmeticProblem) throws IOException, ArithmeticException {
        if (ioProblem) {
            throw new IOException("IO problem occurred!");
        }
        if (arithmeticProblem) {
            throw new ArithmeticException("Division by zero!");
        }
    }

    public static void main(String[] args) {
        try {
            riskyMethod(true, false); // Throws IOException
        } catch (IOException | ArithmeticException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }

        System.out.println("Program continues...");
    }
}
```
#### Creating Custom Exceptions
Finally, Java allows us to create our own custom exceptions. This is useful when the standard Java exceptions do not clearly describe a specific error in our program.   
To create a custom exception we extend the `Exception` class for a checked exception or `RuntimeException` class for an unchecked exception, and provide constructors to pass error messages or other information.
```java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public class CustomExceptionExample {
    static void checkAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be 18 or older.");
        } else {
            System.out.println("Access granted.");
        }
    }

    public static void main(String[] args) {
        try {
            checkAge(15); // This will trigger the custom exception
        } catch (InvalidAgeException e) {
            System.out.println("Caught custom exception: " + e.getMessage());
        }

        System.out.println("Program continues running...");
    }
}
```