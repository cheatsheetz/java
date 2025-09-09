# Java Cheat Sheet

Comprehensive reference for Java programming language covering syntax, OOP concepts, collections, streams, and essential features for modern Java development.

---

## Table of Contents
- [Basic Syntax](#basic-syntax)
- [Data Types](#data-types)
- [Object-Oriented Programming](#object-oriented-programming)
- [Collections Framework](#collections-framework)
- [Streams API](#streams-api)
- [Exception Handling](#exception-handling)
- [Concurrency](#concurrency)
- [Lambda Expressions](#lambda-expressions)
- [Annotations](#annotations)
- [File I/O](#file-io)

---

## Basic Syntax

| Feature | Syntax | Example |
|---------|--------|---------|
| Class Declaration | `public class ClassName` | `public class MyClass {}` |
| Method Declaration | `public returnType methodName(parameters)` | `public int add(int a, int b)` |
| Variable Declaration | `dataType variableName` | `int count = 0;` |
| Constants | `final dataType NAME` | `final int MAX_SIZE = 100;` |
| Comments | `// single line` or `/* multi-line */` | `// This is a comment` |

### Basic Program Structure
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

## Data Types

### Primitive Types
| Type | Size | Range | Default |
|------|------|-------|---------|
| `byte` | 8 bits | -128 to 127 | 0 |
| `short` | 16 bits | -32,768 to 32,767 | 0 |
| `int` | 32 bits | -2^31 to 2^31-1 | 0 |
| `long` | 64 bits | -2^63 to 2^63-1 | 0L |
| `float` | 32 bits | IEEE 754 | 0.0f |
| `double` | 64 bits | IEEE 754 | 0.0d |
| `char` | 16 bits | '\u0000' to '\uffff' | '\u0000' |
| `boolean` | 1 bit | true, false | false |

### String Operations
```java
String str = "Hello";
String str2 = new String("World");

// Common operations
str.length()                    // Length
str.charAt(0)                   // Character at index
str.substring(0, 3)             // Substring
str.toUpperCase()               // Convert to uppercase
str.toLowerCase()               // Convert to lowercase
str.trim()                      // Remove whitespace
str.equals("Hello")             // Compare strings
str.contains("ell")             // Check if contains
String.join(",", "a", "b", "c") // Join strings
```

## Object-Oriented Programming

### Classes and Objects
```java
public class Car {
    // Fields
    private String brand;
    private int year;
    
    // Constructor
    public Car(String brand, int year) {
        this.brand = brand;
        this.year = year;
    }
    
    // Getter
    public String getBrand() {
        return brand;
    }
    
    // Setter
    public void setBrand(String brand) {
        this.brand = brand;
    }
    
    // Method
    public void start() {
        System.out.println("Car is starting...");
    }
}

// Usage
Car car = new Car("Toyota", 2023);
car.start();
```

### Inheritance
```java
public class Animal {
    protected String name;
    
    public void eat() {
        System.out.println(name + " is eating");
    }
}

public class Dog extends Animal {
    public Dog(String name) {
        this.name = name;
    }
    
    @Override
    public void eat() {
        System.out.println(name + " is eating dog food");
    }
    
    public void bark() {
        System.out.println(name + " is barking");
    }
}
```

### Interfaces
```java
public interface Drawable {
    void draw();
    default void print() {
        System.out.println("Printing...");
    }
}

public class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
```

### Abstract Classes
```java
public abstract class Shape {
    protected String color;
    
    public Shape(String color) {
        this.color = color;
    }
    
    public abstract double getArea();
    
    public void displayColor() {
        System.out.println("Color: " + color);
    }
}

public class Rectangle extends Shape {
    private double width, height;
    
    public Rectangle(String color, double width, double height) {
        super(color);
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double getArea() {
        return width * height;
    }
}
```

## Collections Framework

### List Interface
```java
// ArrayList
List<String> list = new ArrayList<>();
list.add("item1");
list.add("item2");
list.get(0);                    // Get element
list.set(0, "newItem");         // Set element
list.remove(0);                 // Remove by index
list.size();                    // Size
list.contains("item1");         // Contains check

// LinkedList
List<String> linkedList = new LinkedList<>();
((LinkedList<String>) linkedList).addFirst("first");
((LinkedList<String>) linkedList).addLast("last");
```

### Set Interface
```java
// HashSet
Set<String> hashSet = new HashSet<>();
hashSet.add("item1");
hashSet.add("item2");
hashSet.contains("item1");      // Check if contains

// TreeSet (sorted)
Set<String> treeSet = new TreeSet<>();
treeSet.add("c");
treeSet.add("a");
treeSet.add("b");
// Automatically sorted: [a, b, c]
```

### Map Interface
```java
// HashMap
Map<String, Integer> map = new HashMap<>();
map.put("key1", 10);
map.put("key2", 20);
map.get("key1");                // Get value
map.containsKey("key1");        // Check if key exists
map.keySet();                   // Get all keys
map.values();                   // Get all values
map.entrySet();                 // Get key-value pairs

// Iteration
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```

### Queue Interface
```java
// LinkedList as Queue
Queue<String> queue = new LinkedList<>();
queue.offer("item1");           // Add to rear
queue.poll();                   // Remove from front
queue.peek();                   // Look at front without removing

// PriorityQueue
Queue<Integer> pq = new PriorityQueue<>();
pq.offer(3);
pq.offer(1);
pq.offer(2);
pq.poll();                      // Returns 1 (smallest)
```

## Streams API

### Basic Stream Operations
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Filter and collect
List<Integer> evenNumbers = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());

// Map and reduce
int sum = numbers.stream()
    .map(n -> n * 2)
    .reduce(0, Integer::sum);

// Find operations
Optional<Integer> first = numbers.stream()
    .filter(n -> n > 5)
    .findFirst();

boolean anyMatch = numbers.stream()
    .anyMatch(n -> n > 5);
```

### Advanced Stream Operations
```java
List<String> words = Arrays.asList("hello", "world", "java", "stream");

// Group by length
Map<Integer, List<String>> grouped = words.stream()
    .collect(Collectors.groupingBy(String::length));

// Parallel streams
long count = words.parallelStream()
    .filter(word -> word.length() > 4)
    .count();

// FlatMap
List<List<String>> listOfLists = Arrays.asList(
    Arrays.asList("a", "b"),
    Arrays.asList("c", "d")
);

List<String> flattened = listOfLists.stream()
    .flatMap(List::stream)
    .collect(Collectors.toList());
```

## Exception Handling

### Try-Catch-Finally
```java
try {
    // Code that might throw an exception
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Division by zero: " + e.getMessage());
} catch (Exception e) {
    System.out.println("General exception: " + e.getMessage());
} finally {
    System.out.println("This always executes");
}
```

### Try-with-Resources
```java
try (FileInputStream fis = new FileInputStream("file.txt");
     BufferedReader reader = new BufferedReader(new InputStreamReader(fis))) {
    
    String line = reader.readLine();
    System.out.println(line);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Custom Exceptions
```java
public class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}

public void validateAge(int age) throws CustomException {
    if (age < 0) {
        throw new CustomException("Age cannot be negative");
    }
}
```

## Concurrency

### Thread Creation
```java
// Extending Thread
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

// Implementing Runnable
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable is running");
    }
}

// Usage
MyThread thread1 = new MyThread();
thread1.start();

Thread thread2 = new Thread(new MyRunnable());
thread2.start();

// Lambda
Thread thread3 = new Thread(() -> System.out.println("Lambda thread"));
thread3.start();
```

### Synchronization
```java
public class Counter {
    private int count = 0;
    
    public synchronized void increment() {
        count++;
    }
    
    public synchronized int getCount() {
        return count;
    }
}

// Synchronized block
public void method() {
    synchronized(this) {
        // Critical section
    }
}
```

### ExecutorService
```java
ExecutorService executor = Executors.newFixedThreadPool(3);

// Submit tasks
Future<Integer> future = executor.submit(() -> {
    Thread.sleep(1000);
    return 42;
});

try {
    Integer result = future.get(); // Blocks until result is available
} catch (Exception e) {
    e.printStackTrace();
}

executor.shutdown();
```

## Lambda Expressions

### Basic Syntax
```java
// Basic lambda
(parameters) -> expression
(parameters) -> { statements; }

// Examples
Runnable r = () -> System.out.println("Hello Lambda");

Function<Integer, Integer> square = x -> x * x;

BiFunction<Integer, Integer, Integer> add = (x, y) -> x + y;

Predicate<String> isEmpty = s -> s.isEmpty();

Consumer<String> printer = System.out::println; // Method reference
```

### Method References
```java
// Static method reference
Function<String, Integer> parser = Integer::parseInt;

// Instance method reference
String str = "Hello";
Supplier<Integer> lengthSupplier = str::length;

// Constructor reference
Supplier<ArrayList<String>> listSupplier = ArrayList::new;
```

## Annotations

### Built-in Annotations
```java
@Override
public void method() {} // Indicates method overrides parent

@Deprecated
public void oldMethod() {} // Marks as deprecated

@SuppressWarnings("unchecked")
public void method() {} // Suppresses compiler warnings

@FunctionalInterface
public interface MyInterface {
    void method();
} // Ensures interface has only one abstract method
```

### Custom Annotations
```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
    String value() default "default";
    int count() default 1;
}

@MyAnnotation(value = "test", count = 5)
public void annotatedMethod() {}
```

## File I/O

### Reading Files
```java
// Using Files class (Java 8+)
try {
    List<String> lines = Files.readAllLines(Paths.get("file.txt"));
    String content = Files.readString(Paths.get("file.txt"));
} catch (IOException e) {
    e.printStackTrace();
}

// Using BufferedReader
try (BufferedReader reader = Files.newBufferedReader(Paths.get("file.txt"))) {
    String line;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### Writing Files
```java
// Using Files class
try {
    Files.write(Paths.get("output.txt"), "Hello World".getBytes());
    Files.write(Paths.get("output.txt"), Arrays.asList("Line 1", "Line 2"));
} catch (IOException e) {
    e.printStackTrace();
}

// Using BufferedWriter
try (BufferedWriter writer = Files.newBufferedWriter(Paths.get("output.txt"))) {
    writer.write("Hello World");
    writer.newLine();
    writer.write("Second line");
} catch (IOException e) {
    e.printStackTrace();
}
```

---

## Resources
- [Oracle Java Documentation](https://docs.oracle.com/javase/)
- [Java SE API Documentation](https://docs.oracle.com/en/java/javase/17/docs/api/)
- [Java Tutorials](https://docs.oracle.com/javase/tutorial/)
- [OpenJDK](https://openjdk.org/)

---
*Originally compiled from various sources. Contributions welcome!*