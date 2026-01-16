# Unit 5: I/O, Serialization & Generics

## 1. Input and Output from Console

### Reading Input using Scanner

**Step 1:** Import Scanner class
```java
import java.util.Scanner;
```

**Step 2:** Create Scanner object
```java
Scanner sc = new Scanner(System.in);
```

**Step 3:** Read different data types
```java
// Read integer
System.out.print("Enter age: ");
int age = sc.nextInt();

// Read double
System.out.print("Enter salary: ");
double salary = sc.nextDouble();

// Read string (single word)
System.out.print("Enter name: ");
String name = sc.next();

// Read string (full line)
System.out.print("Enter address: ");
sc.nextLine();  // Clear buffer
String address = sc.nextLine();

// Close scanner
sc.close();
```

**Complete Example:**
```java
import java.util.Scanner;

public class InputDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Enter name: ");
        String name = sc.nextLine();
        
        System.out.print("Enter age: ");
        int age = sc.nextInt();
        
        System.out.println("Hello " + name + ", age " + age);
        
        sc.close();
    }
}
```

### Output to Console

```java
// Simple print
System.out.print("Hello");  // No new line

// Print with new line
System.out.println("Hello");

// Formatted output
int marks = 85;
System.out.printf("Marks: %d%%\n", marks);  // Marks: 85%

String name = "Alice";
double gpa = 3.75;
System.out.printf("Name: %s, GPA: %.2f\n", name, gpa);
// Name: Alice, GPA: 3.75
```

---

## 2. Reading and Writing Data from Console

### Reading Multiple Values

**Step-by-step:**

```java
import java.util.Scanner;

public class StudentInput {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Step 1: Read student details
        System.out.print("Enter roll number: ");
        int rollNo = sc.nextInt();
        
        System.out.print("Enter name: ");
        sc.nextLine();  // Clear buffer
        String name = sc.nextLine();
        
        System.out.print("Enter marks: ");
        double marks = sc.nextDouble();
        
        // Step 2: Display output
        System.out.println("\n--- Student Details ---");
        System.out.println("Roll: " + rollNo);
        System.out.println("Name: " + name);
        System.out.println("Marks: " + marks);
        
        sc.close();
    }
}
```

### Using BufferedReader

```java
import java.io.*;

public class BufferedReaderDemo {
    public static void main(String[] args) throws IOException {
        // Create BufferedReader
        BufferedReader br = new BufferedReader(
            new InputStreamReader(System.in));
        
        System.out.print("Enter name: ");
        String name = br.readLine();
        
        System.out.print("Enter age: ");
        int age = Integer.parseInt(br.readLine());
        
        System.out.println("Name: " + name + ", Age: " + age);
    }
}
```

---

## 3. Using Streams to Read and Write Files

### Writing to a File

**Step-by-step using FileWriter:**

```java
import java.io.*;

public class WriteFile {
    public static void main(String[] args) {
        try {
            // Step 1: Create FileWriter
            FileWriter writer = new FileWriter("output.txt");
            
            // Step 2: Write data
            writer.write("Hello World\n");
            writer.write("Java File Writing\n");
            
            // Step 3: Close file
            writer.close();
            
            System.out.println("File written successfully");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Using BufferedWriter (Better Performance):**

```java
import java.io.*;

public class BufferedWriteDemo {
    public static void main(String[] args) {
        try (BufferedWriter writer = new BufferedWriter(
                new FileWriter("data.txt"))) {
            
            writer.write("Line 1");
            writer.newLine();
            writer.write("Line 2");
            writer.newLine();
            
            System.out.println("Done");
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Reading from a File

**Step-by-step using FileReader:**

```java
import java.io.*;

public class ReadFile {
    public static void main(String[] args) {
        try {
            // Step 1: Create FileReader
            FileReader reader = new FileReader("output.txt");
            
            // Step 2: Read character by character
            int ch;
            while ((ch = reader.read()) != -1) {
                System.out.print((char) ch);
            }
            
            // Step 3: Close file
            reader.close();
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Using BufferedReader (Read Lines):**

```java
import java.io.*;

public class BufferedReadDemo {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(
                new FileReader("data.txt"))) {
            
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Byte Streams (Binary Files)

**Writing bytes:**
```java
import java.io.*;

public class ByteWrite {
    public static void main(String[] args) {
        try (FileOutputStream out = new FileOutputStream("bytes.dat")) {
            out.write(65);  // Writes 'A'
            out.write(66);  // Writes 'B'
            out.write(67);  // Writes 'C'
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**Reading bytes:**
```java
import java.io.*;

public class ByteRead {
    public static void main(String[] args) {
        try (FileInputStream in = new FileInputStream("bytes.dat")) {
            int data;
            while ((data = in.read()) != -1) {
                System.out.print((char) data);  // ABC
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 4. Writing and Reading Objects using Serialization

Serialization converts object to byte stream for storage or transmission.

### Step-by-Step Guide to Serialization

**Step 1:** Create a class that implements Serializable

```java
import java.io.Serializable;

class Student implements Serializable {
    int rollNo;
    String name;
    double marks;
    
    Student(int rollNo, String name, double marks) {
        this.rollNo = rollNo;
        this.name = name;
        this.marks = marks;
    }
}
```

**Step 2:** Write object to file

```java
import java.io.*;

public class WriteObject {
    public static void main(String[] args) {
        try {
            // Create object
            Student s = new Student(101, "Alice", 85.5);
            
            // Create ObjectOutputStream
            FileOutputStream file = new FileOutputStream("student.dat");
            ObjectOutputStream out = new ObjectOutputStream(file);
            
            // Write object
            out.writeObject(s);
            
            // Close streams
            out.close();
            file.close();
            
            System.out.println("Object saved");
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**Step 3:** Read object from file

```java
import java.io.*;

public class ReadObject {
    public static void main(String[] args) {
        try {
            // Create ObjectInputStream
            FileInputStream file = new FileInputStream("student.dat");
            ObjectInputStream in = new ObjectInputStream(file);
            
            // Read object
            Student s = (Student) in.readObject();
            
            // Display data
            System.out.println("Roll: " + s.rollNo);
            System.out.println("Name: " + s.name);
            System.out.println("Marks: " + s.marks);
            
            // Close streams
            in.close();
            file.close();
            
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### Complete Serialization Example

```java
import java.io.*;

class Employee implements Serializable {
    int id;
    String name;
    double salary;
    
    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }
    
    void display() {
        System.out.println("ID: " + id);
        System.out.println("Name: " + name);
        System.out.println("Salary: " + salary);
    }
}

public class SerializationDemo {
    public static void main(String[] args) {
        // Write
        try (ObjectOutputStream out = new ObjectOutputStream(
                new FileOutputStream("emp.dat"))) {
            Employee emp = new Employee(1, "John", 50000);
            out.writeObject(emp);
            System.out.println("Saved");
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Read
        try (ObjectInputStream in = new ObjectInputStream(
                new FileInputStream("emp.dat"))) {
            Employee emp = (Employee) in.readObject();
            emp.display();
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### transient Keyword

```java
class User implements Serializable {
    String username;
    transient String password;  // Won't be serialized
    
    User(String username, String password) {
        this.username = username;
        this.password = password;
    }
}
```

---

## 5. Creating a Custom Generic Class

Generics allow type parameters for classes, interfaces, and methods.

### Step-by-Step: Create Generic Class

**Step 1:** Define generic class with type parameter

```java
class Box<T> {
    T value;
    
    void set(T value) {
        this.value = value;
    }
    
    T get() {
        return value;
    }
}
```

**Step 2:** Use the generic class

```java
public class GenericDemo {
    public static void main(String[] args) {
        // Box for Integer
        Box<Integer> intBox = new Box<>();
        intBox.set(100);
        System.out.println(intBox.get());  // 100
        
        // Box for String
        Box<String> strBox = new Box<>();
        strBox.set("Hello");
        System.out.println(strBox.get());  // Hello
        
        // Box for Double
        Box<Double> doubleBox = new Box<>();
        doubleBox.set(3.14);
        System.out.println(doubleBox.get());  // 3.14
    }
}
```

### Generic Class with Multiple Type Parameters

```java
class Pair<K, V> {
    K key;
    V value;
    
    Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }
    
    void display() {
        System.out.println(key + " : " + value);
    }
}

// Usage
Pair<String, Integer> pair = new Pair<>("Age", 25);
pair.display();  // Age : 25
```

### Generic Method

```java
class Printer {
    // Generic method
    <T> void print(T item) {
        System.out.println(item);
    }
    
    // Generic method with array
    <T> void printArray(T[] arr) {
        for (T item : arr) {
            System.out.print(item + " ");
        }
        System.out.println();
    }
}

// Usage
Printer p = new Printer();
p.print(100);           // Integer
p.print("Hello");       // String
p.print(3.14);          // Double

Integer[] nums = {1, 2, 3};
p.printArray(nums);     // 1 2 3
```

---

## 6. Using Type Inference Diamond to Create Object

Diamond operator `<>` for automatic type inference (Java 7+).

### Before Java 7

```java
// Had to specify type twice
List<String> list = new ArrayList<String>();
Map<String, Integer> map = new HashMap<String, Integer>();
```

### After Java 7 (Diamond Operator)

```java
// Type inferred from left side
List<String> list = new ArrayList<>();
Map<String, Integer> map = new HashMap<>();
```

### Step-by-Step with Custom Generic Class

**Step 1:** Define generic class
```java
class Container<T> {
    T item;
    
    Container(T item) {
        this.item = item;
    }
    
    T getItem() {
        return item;
    }
}
```

**Step 2:** Use diamond operator
```java
public class DiamondDemo {
    public static void main(String[] args) {
        // Without diamond (old way)
        Container<String> c1 = new Container<String>("Hello");
        
        // With diamond (new way) - type inferred
        Container<String> c2 = new Container<>("World");
        Container<Integer> c3 = new Container<>(100);
        
        System.out.println(c2.getItem());  // World
        System.out.println(c3.getItem());  // 100
    }
}
```

### Diamond with Collections

```java
// Lists
List<Integer> numbers = new ArrayList<>();
numbers.add(1);
numbers.add(2);

// Sets
Set<String> names = new HashSet<>();
names.add("Alice");
names.add("Bob");

// Maps
Map<String, Double> scores = new HashMap<>();
scores.put("Math", 85.5);
scores.put("Science", 90.0);
```

---

## 7. Using Bounded Types and Wildcards

### Bounded Types

Restrict type parameters to specific types.

**Upper Bound (extends):**

**Step 1:** Create bounded generic class
```java
// T must be Number or its subclass
class Calculator<T extends Number> {
    T num;
    
    Calculator(T num) {
        this.num = num;
    }
    
    double square() {
        return num.doubleValue() * num.doubleValue();
    }
}
```

**Step 2:** Use with different number types
```java
public class BoundedDemo {
    public static void main(String[] args) {
        Calculator<Integer> c1 = new Calculator<>(5);
        System.out.println(c1.square());  // 25.0
        
        Calculator<Double> c2 = new Calculator<>(3.5);
        System.out.println(c2.square());  // 12.25
        
        // Calculator<String> c3 = new Calculator<>("Hi");  // ERROR!
    }
}
```

**Multiple Bounds:**

```java
// T must extend both Number and Comparable
class MinMax<T extends Number & Comparable<T>> {
    T[] values;
    
    MinMax(T[] values) {
        this.values = values;
    }
    
    T min() {
        T min = values[0];
        for (T val : values) {
            if (val.compareTo(min) < 0) {
                min = val;
            }
        }
        return min;
    }
}

// Usage
Integer[] nums = {5, 2, 8, 1, 9};
MinMax<Integer> mm = new MinMax<>(nums);
System.out.println(mm.min());  // 1
```

### Wildcards

**Upper Bounded Wildcard (`? extends Type`):**

```java
// Step-by-step example
class Animal { }
class Dog extends Animal { }
class Cat extends Animal { }

class AnimalProcessor {
    // Accepts List of Animal or its subclasses
    void processList(List<? extends Animal> list) {
        for (Animal a : list) {
            System.out.println(a);
        }
    }
}

// Usage
List<Dog> dogs = new ArrayList<>();
List<Cat> cats = new ArrayList<>();
List<Animal> animals = new ArrayList<>();

AnimalProcessor p = new AnimalProcessor();
p.processList(dogs);     // OK
p.processList(cats);     // OK
p.processList(animals);  // OK
```

**Lower Bounded Wildcard (`? super Type`):**

```java
class NumberProcessor {
    // Accepts List of Integer or its superclass
    void addNumbers(List<? super Integer> list) {
        list.add(10);
        list.add(20);
        list.add(30);
    }
}

// Usage
List<Integer> intList = new ArrayList<>();
List<Number> numList = new ArrayList<>();
List<Object> objList = new ArrayList<>();

NumberProcessor np = new NumberProcessor();
np.addNumbers(intList);  // OK
np.addNumbers(numList);  // OK
np.addNumbers(objList);  // OK
```

**Unbounded Wildcard (`?`):**

```java
class Util {
    void printList(List<?> list) {
        for (Object obj : list) {
            System.out.println(obj);
        }
    }
}

// Accepts any type of List
List<Integer> nums = Arrays.asList(1, 2, 3);
List<String> words = Arrays.asList("a", "b", "c");

Util u = new Util();
u.printList(nums);   // OK
u.printList(words);  // OK
```

---

## 8. Complete Examples

### Example 1: Generic Stack Implementation

```java
class Stack<T> {
    private T[] items;
    private int top = -1;
    
    @SuppressWarnings("unchecked")
    Stack(int size) {
        items = (T[]) new Object[size];
    }
    
    void push(T item) {
        if (top == items.length - 1) {
            System.out.println("Stack full");
            return;
        }
        items[++top] = item;
    }
    
    T pop() {
        if (top == -1) {
            System.out.println("Stack empty");
            return null;
        }
        return items[top--];
    }
    
    boolean isEmpty() {
        return top == -1;
    }
}

// Usage
Stack<Integer> stack = new Stack<>(5);
stack.push(10);
stack.push(20);
stack.push(30);

System.out.println(stack.pop());  // 30
System.out.println(stack.pop());  // 20
```

### Example 2: Generic Method with Bounds

```java
class ArrayUtils {
    // Find max in array - works only with Comparable types
    static <T extends Comparable<T>> T findMax(T[] array) {
        T max = array[0];
        for (T item : array) {
            if (item.compareTo(max) > 0) {
                max = item;
            }
        }
        return max;
    }
}

// Usage
Integer[] nums = {5, 2, 8, 1, 9};
System.out.println(ArrayUtils.findMax(nums));  // 9

String[] words = {"apple", "zebra", "cat"};
System.out.println(ArrayUtils.findMax(words)); // zebra
```

### Example 3: File and Serialization Combined

```java
import java.io.*;
import java.util.*;

class Student implements Serializable {
    int id;
    String name;
    
    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
    
    public String toString() {
        return "ID: " + id + ", Name: " + name;
    }
}

public class StudentManager {
    // Save list of students
    static void saveStudents(List<Student> students, String filename) {
        try (ObjectOutputStream out = new ObjectOutputStream(
                new FileOutputStream(filename))) {
            out.writeObject(students);
            System.out.println("Saved " + students.size() + " students");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    // Load list of students
    @SuppressWarnings("unchecked")
    static List<Student> loadStudents(String filename) {
        try (ObjectInputStream in = new ObjectInputStream(
                new FileInputStream(filename))) {
            return (List<Student>) in.readObject();
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
            return new ArrayList<>();
        }
    }
    
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(101, "Alice"));
        students.add(new Student(102, "Bob"));
        
        // Save
        saveStudents(students, "students.dat");
        
        // Load
        List<Student> loaded = loadStudents("students.dat");
        for (Student s : loaded) {
            System.out.println(s);
        }
    }
}
```

---

## Practice Problems (LeetCode)

### I/O and File Operations
1. **LeetCode #1528 - Shuffle String** (String manipulation for I/O)
2. **LeetCode #1221 - Split a String in Balanced Strings** (String processing)

### Generics
3. **LeetCode #155 - Min Stack** (Generic stack implementation)
4. **LeetCode #232 - Implement Queue using Stacks** (Generic queue)
5. **LeetCode #225 - Implement Stack using Queues** (Generic stack)
6. **LeetCode #622 - Design Circular Queue** (Generic circular queue)
7. **LeetCode #1472 - Design Browser History** (Generic data structure)

### Collections with Generics
8. **LeetCode #1 - Two Sum** (Using generic HashMap)
9. **LeetCode #217 - Contains Duplicate** (Using generic HashSet)
10. **LeetCode #242 - Valid Anagram** (Generic collections)
11. **LeetCode #349 - Intersection of Two Arrays** (Generic sets)

### Bounded Generics
12. **LeetCode #88 - Merge Sorted Array** (Comparable interface)
13. **LeetCode #21 - Merge Two Sorted Lists** (Generic merge)
14. **LeetCode #23 - Merge k Sorted Lists** (Generic comparison)

### Wildcard Usage
15. **LeetCode #706 - Design HashMap** (Wildcard in implementation)
16. **LeetCode #705 - Design HashSet** (Generic implementation)

---

## Real-Life Applications

### 1. **User Registration (Console I/O)**

```java
import java.util.Scanner;

class Registration {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Enter username: ");
        String username = sc.nextLine();
        
        System.out.print("Enter email: ");
        String email = sc.nextLine();
        
        System.out.print("Enter age: ");
        int age = sc.nextInt();
        
        System.out.println("\nRegistration Successful!");
        System.out.println("Username: " + username);
        System.out.println("Email: " + email);
        System.out.println("Age: " + age);
        
        sc.close();
    }
}

// Used in: Registration forms, User input systems
```

### 2. **Log File Writer (File Writing)**

```java
import java.io.*;
import java.time.LocalDateTime;

class Logger {
    void log(String message) {
        try (BufferedWriter writer = new BufferedWriter(
                new FileWriter("app.log", true))) {  // append mode
            
            String timestamp = LocalDateTime.now().toString();
            writer.write(timestamp + " : " + message);
            writer.newLine();
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// Usage
Logger logger = new Logger();
logger.log("Application started");
logger.log("User logged in");

// Used in: Application logging, Error tracking
```

### 3. **Configuration Reader (File Reading)**

```java
import java.io.*;
import java.util.*;

class ConfigReader {
    Map<String, String> loadConfig(String filename) {
        Map<String, String> config = new HashMap<>();
        
        try (BufferedReader reader = new BufferedReader(
                new FileReader(filename))) {
            
            String line;
            while ((line = reader.readLine()) != null) {
                String[] parts = line.split("=");
                if (parts.length == 2) {
                    config.put(parts[0], parts[1]);
                }
            }
            
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        return config;
    }
}

// config.txt:
// host=localhost
// port=8080
// database=mydb

// Used in: Application configuration, Settings management
```

### 4. **Save Game State (Serialization)**

```java
import java.io.*;

class GameState implements Serializable {
    int level;
    int score;
    String playerName;
    
    GameState(String playerName, int level, int score) {
        this.playerName = playerName;
        this.level = level;
        this.score = score;
    }
}

class GameManager {
    void saveGame(GameState state) {
        try (ObjectOutputStream out = new ObjectOutputStream(
                new FileOutputStream("savegame.dat"))) {
            out.writeObject(state);
            System.out.println("Game saved");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    GameState loadGame() {
        try (ObjectInputStream in = new ObjectInputStream(
                new FileInputStream("savegame.dat"))) {
            return (GameState) in.readObject();
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
            return null;
        }
    }
}

// Used in: Video games, Mobile games
```

### 5. **Generic Container (Generics)**

```java
class Container<T> {
    private List<T> items = new ArrayList<>();
    
    void add(T item) {
        items.add(item);
    }
    
    T get(int index) {
        return items.get(index);
    }
    
    int size() {
        return items.size();
    }
}

// Usage - Shopping cart
Container<String> cart = new Container<>();
cart.add("Apple");
cart.add("Banana");

// Usage - Numbers
Container<Integer> numbers = new Container<>();
numbers.add(10);
numbers.add(20);

// Used in: Collections, Data containers
```

### 6. **Type-Safe Database (Bounded Generics)**

```java
class Database<T extends Serializable> {
    private List<T> records = new ArrayList<>();
    
    void insert(T record) {
        records.add(record);
    }
    
    List<T> findAll() {
        return new ArrayList<>(records);
    }
    
    void save(String filename) {
        try (ObjectOutputStream out = new ObjectOutputStream(
                new FileOutputStream(filename))) {
            out.writeObject(records);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// Used in: ORM systems, Data persistence
```

### 7. **Report Generator (File I/O)**

```java
import java.io.*;

class ReportGenerator {
    void generateReport(String filename, List<String> data) {
        try (PrintWriter writer = new PrintWriter(
                new FileWriter(filename))) {
            
            writer.println("===== REPORT =====");
            writer.println("Date: " + new Date());
            writer.println();
            
            for (String line : data) {
                writer.println(line);
            }
            
            writer.println("\nTotal entries: " + data.size());
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// Used in: Business reports, Analytics
```

### 8. **Generic Cache System (Wildcards)**

```java
class Cache<K, V> {
    private Map<K, V> map = new HashMap<>();
    
    void put(K key, V value) {
        map.put(key, value);
    }
    
    V get(K key) {
        return map.get(key);
    }
    
    // Works with any cache type
    void copyFrom(Cache<? extends K, ? extends V> other) {
        // Copy logic
    }
}

// Used in: Web applications, Performance optimization
```

---

## Key Takeaways

- **Scanner** reads console input; remember to close it
- **FileWriter/FileReader** for text files
- **ObjectOutputStream/ObjectInputStream** for serialization
- Classes must implement **Serializable** to serialize
- **transient** keyword prevents field serialization
- **Generics** provide type safety at compile time
- **Diamond operator `<>`** infers type automatically (Java 7+)
- **Bounded types** restrict generic types (extends, super)
- **Wildcards** make methods flexible with generic types
- Always use try-with-resources for file operations
- Generic types are erased at runtime (type erasure)

---

## Quick Reference

**Scanner:** `Scanner sc = new Scanner(System.in);`  
**Read line:** `String s = sc.nextLine();`  
**Write file:** `FileWriter fw = new FileWriter("file.txt");`  
**Read file:** `FileReader fr = new FileReader("file.txt");`  
**Serialize:** `ObjectOutputStream out = new ObjectOutputStream(...);`  
**Deserialize:** `ObjectInputStream in = new ObjectInputStream(...);`  
**Generic class:** `class Box<T> { T item; }`  
**Diamond:** `List<String> list = new ArrayList<>();`  
**Upper bound:** `<T extends Number>`  
**Lower bound:** `<T super Integer>`  
**Wildcard:** `List<?> list` or `List<? extends Type>`
