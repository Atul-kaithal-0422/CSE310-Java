# Unit 4: Nested Classes, Lambda & Exception Handling

## 1. Nested Classes

Classes defined within another class.

### Inner Class (Non-static Nested Class)

```java
class Outer {
    private int outerData = 10;
    
    // Inner class
    class Inner {
        void display() {
            // Can access outer class members (including private)
            System.out.println("Outer data: " + outerData);
        }
    }
    
    void createInner() {
        Inner inner = new Inner();
        inner.display();
    }
}

// Usage
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();  // Need outer instance
inner.display();
```

### Static Nested Class

```java
class Outer {
    private static int staticData = 100;
    private int instanceData = 50;
    
    // Static nested class
    static class StaticNested {
        void display() {
            // Can access only static members of outer class
            System.out.println("Static data: " + staticData);
            // System.out.println(instanceData);  // ERROR!
        }
    }
}

// Usage (no outer instance needed)
Outer.StaticNested nested = new Outer.StaticNested();
nested.display();
```

### Practical Example: LinkedList Node

```java
class LinkedList {
    // Static nested class for Node
    private static class Node {
        int data;
        Node next;
        
        Node(int data) {
            this.data = data;
        }
    }
    
    private Node head;
    
    void add(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }
}
```

---

## 2. Local vs Anonymous Classes

### Local Class (Inside Method)

```java
class Demo {
    void methodWithLocalClass() {
        final int localVar = 100;
        
        // Local class
        class LocalClass {
            void display() {
                System.out.println("Local variable: " + localVar);
            }
        }
        
        LocalClass local = new LocalClass();
        local.display();
    }
}

// Local classes have access to final/effectively final local variables
```

### Anonymous Class

Anonymous classes are classes without a name, defined and instantiated in one expression.

```java
// Anonymous class extending a class
abstract class Animal {
    abstract void makeSound();
}

Animal dog = new Animal() {
    @Override
    void makeSound() {
        System.out.println("Bark!");
    }
};
dog.makeSound();

// Anonymous class implementing an interface
interface Greeting {
    void greet(String name);
}

Greeting greeting = new Greeting() {
    @Override
    public void greet(String name) {
        System.out.println("Hello, " + name);
    }
};
greeting.greet("Alice");
```

### Anonymous Class with Constructor Arguments

```java
abstract class Vehicle {
    String brand;
    
    Vehicle(String brand) {
        this.brand = brand;
    }
    
    abstract void start();
}

Vehicle car = new Vehicle("Toyota") {
    @Override
    void start() {
        System.out.println(brand + " car started");
    }
};
car.start();
```

### Practical Example: Event Handling

```java
interface ClickListener {
    void onClick();
}

class Button {
    private ClickListener listener;
    
    void setOnClickListener(ClickListener listener) {
        this.listener = listener;
    }
    
    void click() {
        if (listener != null) {
            listener.onClick();
        }
    }
}

// Usage with anonymous class
Button button = new Button();
button.setOnClickListener(new ClickListener() {
    @Override
    public void onClick() {
        System.out.println("Button clicked!");
    }
});
button.click();
```

---

## 3. Functional Interface

Interface with exactly one abstract method (can have default/static methods).

### Basic Functional Interface

```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

// Implementation using anonymous class
Calculator add = new Calculator() {
    @Override
    public int calculate(int a, int b) {
        return a + b;
    }
};

System.out.println(add.calculate(5, 3));  // 8
```

### Built-in Functional Interfaces

```java
import java.util.function.*;

// Predicate<T> - takes T, returns boolean
Predicate<Integer> isEven = n -> n % 2 == 0;
System.out.println(isEven.test(4));  // true

// Function<T, R> - takes T, returns R
Function<String, Integer> stringLength = s -> s.length();
System.out.println(stringLength.apply("Hello"));  // 5

// Consumer<T> - takes T, returns nothing
Consumer<String> print = s -> System.out.println(s);
print.accept("Hello World");

// Supplier<T> - takes nothing, returns T
Supplier<Double> random = () -> Math.random();
System.out.println(random.get());

// BiFunction<T, U, R> - takes T and U, returns R
BiFunction<Integer, Integer, Integer> multiply = (a, b) -> a * b;
System.out.println(multiply.apply(5, 3));  // 15

// UnaryOperator<T> - takes T, returns T
UnaryOperator<Integer> square = n -> n * n;
System.out.println(square.apply(5));  // 25

// BinaryOperator<T> - takes two T, returns T
BinaryOperator<Integer> max = (a, b) -> a > b ? a : b;
System.out.println(max.apply(10, 20));  // 20
```

### Custom Functional Interface

```java
@FunctionalInterface
interface StringProcessor {
    String process(String input);
    
    // Default methods allowed
    default String processUpperCase(String input) {
        return process(input).toUpperCase();
    }
    
    // Static methods allowed
    static String reverse(String s) {
        return new StringBuilder(s).reverse().toString();
    }
}

StringProcessor removeSpaces = s -> s.replace(" ", "");
System.out.println(removeSpaces.process("Hello World"));  // HelloWorld
```

---

## 4. Lambda Expressions

Concise way to represent anonymous functions.

### Basic Syntax

```java
// Traditional anonymous class
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running");
    }
};

// Lambda expression
Runnable r2 = () -> System.out.println("Running");

// With parameters
interface MathOperation {
    int operate(int a, int b);
}

MathOperation add = (a, b) -> a + b;
MathOperation subtract = (a, b) -> a - b;
MathOperation multiply = (a, b) -> a * b;

System.out.println(add.operate(5, 3));       // 8
System.out.println(subtract.operate(5, 3));  // 2
System.out.println(multiply.operate(5, 3));  // 15
```

### Lambda Syntax Variations

```java
// No parameters
Runnable r = () -> System.out.println("Hello");

// One parameter (parentheses optional)
Consumer<String> print1 = s -> System.out.println(s);
Consumer<String> print2 = (s) -> System.out.println(s);

// Multiple parameters
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;

// Multiple statements (need curly braces)
BiFunction<Integer, Integer, Integer> max = (a, b) -> {
    if (a > b) {
        return a;
    } else {
        return b;
    }
};

// Type inference (types optional)
BiFunction<Integer, Integer, Integer> multiply = (Integer a, Integer b) -> a * b;
```

### Method References

```java
import java.util.Arrays;
import java.util.List;

List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

// Lambda expression
names.forEach(name -> System.out.println(name));

// Method reference (equivalent)
names.forEach(System.out::println);

// Static method reference
Function<String, Integer> parser1 = s -> Integer.parseInt(s);
Function<String, Integer> parser2 = Integer::parseInt;

// Instance method reference
String str = "Hello";
Supplier<Integer> length1 = () -> str.length();
Supplier<Integer> length2 = str::length;

// Constructor reference
Supplier<StringBuilder> sb1 = () -> new StringBuilder();
Supplier<StringBuilder> sb2 = StringBuilder::new;
```

### Lambda with Collections

```java
import java.util.*;
import java.util.stream.*;

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Filter
List<Integer> evens = numbers.stream()
                             .filter(n -> n % 2 == 0)
                             .collect(Collectors.toList());
System.out.println(evens);  // [2, 4, 6, 8, 10]

// Map
List<Integer> squares = numbers.stream()
                               .map(n -> n * n)
                               .collect(Collectors.toList());

// Reduce
int sum = numbers.stream()
                 .reduce(0, (a, b) -> a + b);
System.out.println(sum);  // 55

// Sort
List<String> words = Arrays.asList("apple", "pie", "banana", "cherry");
words.sort((s1, s2) -> s1.compareTo(s2));
// or
words.sort(String::compareTo);
```

### Capturing Variables

```java
int multiplier = 10;  // Must be final or effectively final

Function<Integer, Integer> multiply = n -> n * multiplier;
System.out.println(multiply.apply(5));  // 50

// multiplier = 20;  // ERROR! Can't modify captured variable
```

---

## 5. Utility Classes

Classes with only static methods, cannot be instantiated.

### Math Class Example

```java
// Math is a utility class
double result1 = Math.sqrt(25);           // 5.0
double result2 = Math.pow(2, 3);          // 8.0
int result3 = Math.max(10, 20);           // 20
double result4 = Math.abs(-5.5);          // 5.5
double result5 = Math.random();           // 0.0 to 1.0
double result6 = Math.floor(4.7);         // 4.0
double result7 = Math.ceil(4.2);          // 5.0
double result8 = Math.round(4.6);         // 5
```

### Creating Custom Utility Class

```java
public final class StringUtils {
    
    // Private constructor prevents instantiation
    private StringUtils() {
        throw new AssertionError("Cannot instantiate utility class");
    }
    
    public static boolean isEmpty(String str) {
        return str == null || str.trim().isEmpty();
    }
    
    public static String reverse(String str) {
        if (isEmpty(str)) return str;
        return new StringBuilder(str).reverse().toString();
    }
    
    public static int countWords(String str) {
        if (isEmpty(str)) return 0;
        return str.trim().split("\\s+").length;
    }
    
    public static String capitalize(String str) {
        if (isEmpty(str)) return str;
        return str.substring(0, 1).toUpperCase() + str.substring(1);
    }
}

// Usage
String reversed = StringUtils.reverse("hello");
int words = StringUtils.countWords("Hello World");
```

### Arrays Utility Class

```java
import java.util.Arrays;

int[] arr = {5, 2, 8, 1, 9};

// Sort
Arrays.sort(arr);

// Binary search (requires sorted array)
int index = Arrays.binarySearch(arr, 8);

// Fill
Arrays.fill(arr, 0);

// Copy
int[] copy = Arrays.copyOf(arr, arr.length);

// Compare
boolean equal = Arrays.equals(arr, copy);

// Convert to string
String str = Arrays.toString(arr);

// Stream
int sum = Arrays.stream(arr).sum();
```

### Collections Utility Class

```java
import java.util.*;

List<Integer> list = new ArrayList<>(Arrays.asList(5, 2, 8, 1, 9));

// Sort
Collections.sort(list);

// Reverse
Collections.reverse(list);

// Shuffle
Collections.shuffle(list);

// Binary search
int index = Collections.binarySearch(list, 5);

// Max/Min
int max = Collections.max(list);
int min = Collections.min(list);

// Frequency
int count = Collections.frequency(list, 5);

// Unmodifiable collection
List<Integer> unmodifiable = Collections.unmodifiableList(list);
```

---

## 6. Exceptions and Assertions

### Exception Hierarchy

```
Throwable
├── Error (e.g., OutOfMemoryError)
└── Exception
    ├── RuntimeException (Unchecked)
    │   ├── NullPointerException
    │   ├── ArrayIndexOutOfBoundsException
    │   ├── ArithmeticException
    │   └── IllegalArgumentException
    └── Checked Exceptions
        ├── IOException
        ├── SQLException
        └── ClassNotFoundException
```

### Common Exceptions

```java
// ArithmeticException
int result = 10 / 0;  // Division by zero

// NullPointerException
String str = null;
str.length();  // NPE

// ArrayIndexOutOfBoundsException
int[] arr = new int[5];
int x = arr[10];  // Index out of bounds

// NumberFormatException
int num = Integer.parseInt("abc");  // Invalid number

// IllegalArgumentException
void setAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
}
```

### Assertions

```java
// Enable assertions: java -ea ClassName
// Disable assertions: java -da ClassName

public class AssertionDemo {
    public static void main(String[] args) {
        int age = -5;
        
        // Simple assertion
        assert age >= 0;  // Throws AssertionError if false
        
        // Assertion with message
        assert age >= 0 : "Age cannot be negative";
        
        // Assertions should be used for:
        // 1. Internal invariants
        // 2. Control flow invariants
        // 3. Preconditions, postconditions
        
        // DON'T use assertions for:
        // 1. Public method argument checking
        // 2. Side effects (they can be disabled)
    }
    
    private double squareRoot(double x) {
        assert x >= 0 : "Cannot compute square root of negative";
        return Math.sqrt(x);
    }
}
```

---

## 7. Try-Catch

### Basic Try-Catch

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
}

// With exception details
try {
    int[] arr = new int[5];
    arr[10] = 50;
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Error: " + e.getMessage());
    e.printStackTrace();
}
```

### Multiple Catch Blocks

```java
try {
    String str = null;
    System.out.println(str.length());
} catch (NullPointerException e) {
    System.out.println("Null pointer error");
} catch (Exception e) {
    System.out.println("General error");
}

// Order matters: specific to general
try {
    // code
} catch (FileNotFoundException e) {
    // Handle specific exception
} catch (IOException e) {
    // Handle more general exception
} catch (Exception e) {
    // Handle all other exceptions
}
```

### Finally Block

```java
try {
    int result = 10 / 2;
    System.out.println(result);
} catch (ArithmeticException e) {
    System.out.println("Error");
} finally {
    // Always executes (even if exception or return)
    System.out.println("Cleanup code");
}

// Practical example
FileReader reader = null;
try {
    reader = new FileReader("file.txt");
    // Read file
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try {
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Throw and Throws

```java
// throw - to throw an exception
void validateAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Must be 18 or older");
    }
}

// throws - declares that method might throw exception
void readFile(String filename) throws IOException {
    FileReader reader = new FileReader(filename);
    // Read file
}

// Caller must handle
void caller() {
    try {
        readFile("data.txt");
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

---

## 8. Multi-Catch

Catching multiple exception types in one catch block (Java 7+).

### Basic Multi-Catch

```java
try {
    String str = args[0];
    int num = Integer.parseInt(str);
    int result = 100 / num;
} catch (ArrayIndexOutOfBoundsException | NumberFormatException e) {
    System.out.println("Invalid input");
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
}
```

### Multi-Catch with Common Handler

```java
try {
    // Code that might throw multiple exceptions
    performOperation();
} catch (IOException | SQLException | ClassNotFoundException e) {
    // Handle all three exceptions the same way
    System.out.println("Operation failed: " + e.getMessage());
    logError(e);
}

// Note: Exception variable is implicitly final
```

### Before Java 7 vs After

```java
// Before Java 7 - verbose
try {
    // code
} catch (IOException e) {
    System.out.println("Error: " + e);
} catch (SQLException e) {
    System.out.println("Error: " + e);
}

// Java 7+ - concise
try {
    // code
} catch (IOException | SQLException e) {
    System.out.println("Error: " + e);
}
```

---

## 9. Try-With-Resources (Auto-Close)

Automatically closes resources that implement AutoCloseable (Java 7+).

### Basic Try-With-Resources

```java
// Old way - manual close
BufferedReader reader = null;
try {
    reader = new BufferedReader(new FileReader("file.txt"));
    String line = reader.readLine();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try {
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// New way - automatic close
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String line = reader.readLine();
} catch (IOException e) {
    e.printStackTrace();
}
// reader.close() called automatically
```

### Multiple Resources

```java
try (
    FileInputStream input = new FileInputStream("input.txt");
    FileOutputStream output = new FileOutputStream("output.txt")
) {
    int data = input.read();
    while (data != -1) {
        output.write(data);
        data = input.read();
    }
} catch (IOException e) {
    e.printStackTrace();
}
// Both input and output closed automatically
```

### Custom AutoCloseable Resource

```java
class DatabaseConnection implements AutoCloseable {
    public DatabaseConnection() {
        System.out.println("Connection opened");
    }
    
    public void executeQuery(String query) {
        System.out.println("Executing: " + query);
    }
    
    @Override
    public void close() {
        System.out.println("Connection closed");
    }
}

// Usage
try (DatabaseConnection conn = new DatabaseConnection()) {
    conn.executeQuery("SELECT * FROM users");
}
// Output:
// Connection opened
// Executing: SELECT * FROM users
// Connection closed
```

### Try-With-Resources with Catch and Finally

```java
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String line = reader.readLine();
    System.out.println(line);
} catch (FileNotFoundException e) {
    System.out.println("File not found");
} catch (IOException e) {
    System.out.println("Read error");
} finally {
    System.out.println("Done");
}
// Order of execution:
// 1. Try block
// 2. Resource close (automatic)
// 3. Catch block (if exception)
// 4. Finally block
```

---

## 10. Custom Exceptions

Creating your own exception classes.

### Creating Custom Checked Exception

```java
// Custom checked exception
class InsufficientFundsException extends Exception {
    private double amount;
    
    public InsufficientFundsException(double amount) {
        super("Insufficient funds. Need: " + amount);
        this.amount = amount;
    }
    
    public double getAmount() {
        return amount;
    }
}

class BankAccount {
    private double balance;
    
    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException(amount - balance);
        }
        balance -= amount;
    }
}

// Usage
BankAccount account = new BankAccount();
try {
    account.withdraw(5000);
} catch (InsufficientFundsException e) {
    System.out.println(e.getMessage());
    System.out.println("Short by: " + e.getAmount());
}
```

### Creating Custom Unchecked Exception

```java
// Custom unchecked exception
class InvalidAgeException extends RuntimeException {
    public InvalidAgeException(int age) {
        super("Invalid age: " + age + ". Must be between 0 and 150");
    }
}

class Person {
    private int age;
    
    public void setAge(int age) {
        if (age < 0 || age > 150) {
            throw new InvalidAgeException(age);
        }
        this.age = age;
    }
}

// Usage (no need to declare throws)
Person person = new Person();
try {
    person.setAge(-5);
} catch (InvalidAgeException e) {
    System.out.println(e.getMessage());
}
```

### Exception Best Practices

```java
// 1. Use meaningful names
class OrderNotFoundException extends Exception { }
class PaymentFailedException extends Exception { }

// 2. Provide multiple constructors
class ValidationException extends Exception {
    public ValidationException() {
        super();
    }
    
    public ValidationException(String message) {
        super(message);
    }
    
    public ValidationException(String message, Throwable cause) {
        super(message, cause);
    }
    
    public ValidationException(Throwable cause) {
        super(cause);
    }
}

// 3. Include context information
class DatabaseException extends Exception {
    private String query;
    private String tableName;
    
    public DatabaseException(String message, String query, String tableName) {
        super(message);
        this.query = query;
        this.tableName = tableName;
    }
    
    public String getQuery() {
        return query;
    }
    
    public String getTableName() {
        return tableName;
    }
}

// 4. Don't suppress exceptions
try {
    riskyOperation();
} catch (Exception e) {
    // DON'T do this (swallowing exception)
    // Do nothing
    
    // DO this instead
    throw new CustomException("Operation failed", e);
}
```

### Chaining Exceptions

```java
class ServiceException extends Exception {
    public ServiceException(String message, Throwable cause) {
        super(message, cause);
    }
}

void businessLogic() throws ServiceException {
    try {
        // Database operation
        databaseCall();
    } catch (SQLException e) {
        throw new ServiceException("Business logic failed", e);
    }
}

// Access original exception
try {
    businessLogic();
} catch (ServiceException e) {
    System.out.println("Service error: " + e.getMessage());
    Throwable cause = e.getCause();
    System.out.println("Root cause: " + cause);
}
```

---

## Practice Problems (LeetCode)

### Nested Classes & Lambda
1. **LeetCode #341 - Flatten Nested List Iterator** (Nested classes)
2. **LeetCode #1603 - Design Parking System** (Inner classes)
3. **LeetCode #146 - LRU Cache** (Nested class design)

### Functional Interface & Lambda
4. **LeetCode #1672 - Richest Customer Wealth** (Use streams)
5. **LeetCode #1678 - Goal Parser Interpretation** (String processing with lambda)
6. **LeetCode #2011 - Final Value of Variable After Performing Operations** (Functional approach)
7. **LeetCode #1431 - Kids With Greatest Number of Candies** (Streams & filter)
8. **LeetCode #1470 - Shuffle the Array** (Functional operations)

### Exception Handling
9. **LeetCode #1 - Two Sum** (Handle edge cases with exceptions)
10. **LeetCode #7 - Reverse Integer** (Handle overflow exceptions)
11. **LeetCode #8 - String to Integer (atoi)** (Exception handling for parsing)
12. **LeetCode #13 - Roman to Integer** (Validation exceptions)

### Utility Classes Usage
13. **LeetCode #268 - Missing Number** (Arrays utility)
14. **LeetCode #189 - Rotate Array** (Arrays.copyOfRange)
15. **LeetCode #350 - Intersection of Two Arrays II** (Arrays.sort)
16. **LeetCode #912 - Sort an Array** (Implement using Arrays utility)

### Collections with Lambda
17. **LeetCode #1528 - Shuffle String** (Streams)
18. **LeetCode #2089 - Find Target Indices After Sorting Array** (Filter & map)
19. **LeetCode #1365 - How Many Numbers Are Smaller Than Current** (Streams)
20. **LeetCode #1920 - Build Array from Permutation** (Functional approach)

---

## Real-Life Applications

### 1. **GUI Event Handling (Anonymous Classes)**

```java
import javax.swing.*;
import java.awt.event.*;

class LoginForm {
    void createUI() {
        JButton loginButton = new JButton("Login");
        
        // Anonymous class for event listener
        loginButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("Login button clicked");
                validateCredentials();
            }
        });
        
        // Modern approach with lambda
        loginButton.addActionListener(e -> {
            System.out.println("Login button clicked");
            validateCredentials();
        });
    }
    
    void validateCredentials() {
        // Validation logic
    }
}

// Used in: Desktop applications, Swing, JavaFX
```

### 2. **Data Processing Pipeline (Lambda & Streams)**

```java
import java.util.*;
import java.util.stream.*;

class Transaction {
    String type;
    double amount;
    String status;
    
    Transaction(String type, double amount, String status) {
        this.type = type;
        this.amount = amount;
        this.status = status;
    }
    
    double getAmount() { return amount; }
    String getStatus() { return status; }
    String getType() { return type; }
}

class TransactionProcessor {
    List<Transaction> transactions;
    
    // Find total amount of successful transactions
    double getTotalSuccessfulAmount() {
        return transactions.stream()
            .filter(t -> t.getStatus().equals("SUCCESS"))
            .mapToDouble(Transaction::getAmount)
            .sum();
    }
    
    // Get unique transaction types
    List<String> getUniqueTypes() {
        return transactions.stream()
            .map(Transaction::getType)
            .distinct()
            .collect(Collectors.toList());
    }
    
    // Find high-value transactions
    List<Transaction> getHighValueTransactions(double threshold) {
        return transactions.stream()
            .filter(t -> t.getAmount() > threshold)
            .sorted((t1, t2) -> Double.compare(t2.getAmount(), t1.getAmount()))
            .collect(Collectors.toList());
    }
}

// Used in: Banking apps, Payment gateways, Analytics platforms
```

### 3. **Configuration Manager (Utility Class)**

```java
public final class ConfigManager {
    private static final Properties properties = new Properties();
    
    private ConfigManager() {
        throw new AssertionError("Cannot instantiate");
    }
    
    static {
        try (InputStream input = ConfigManager.class
                .getResourceAsStream("config.properties")) {
            properties.load(input);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    public static String get(String key) {
        return properties.getProperty(key);
    }
    
    public static int getInt(String key) {
        return Integer.parseInt(get(key));
    }
    
    public static boolean getBoolean(String key) {
        return Boolean.parseBoolean(get(key));
    }
}

// Usage
String dbUrl = ConfigManager.get("database.url");
int maxConnections = ConfigManager.getInt("database.maxConnections");

// Used in: Spring Boot, Hibernate, Enterprise applications
```

### 4. **File Processing with Exception Handling**

```java
class FileProcessor {
    void processFile(String filename) {
        try (BufferedReader reader = new BufferedReader(
                new FileReader(filename))) {
            
            String line;
            int lineNumber = 0;
            
            while ((line = reader.readLine()) != null) {
                try {
                    processLine(line, ++lineNumber);
                } catch (DataFormatException e) {
                    System.err.println("Error at line " + lineNumber + 
                                     ": " + e.getMessage());
                    // Continue processing other lines
                }
            }
            
        } catch (FileNotFoundException e) {
            System.err.println("File not found: " + filename);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }
    
    void processLine(String line, int lineNumber) 
            throws DataFormatException {
        if (line.trim().isEmpty()) {
            throw new DataFormatException("Empty line");
        }
        // Process line
    }
}

// Used in: Log analyzers, Data import tools, ETL pipelines
```

### 5. **RESTful API Error Handling (Custom Exceptions)**

```java
// Custom exceptions for different HTTP status codes
class ResourceNotFoundException extends Exception {
    public ResourceNotFoundException(String resource, String id) {
        super("Resource '" + resource + "' with id '" + id + "' not found");
    }
}

class UnauthorizedException extends Exception {
    public UnauthorizedException(String message) {
        super(message);
    }
}

class ValidationException extends Exception {
    private Map<String, String> errors = new HashMap<>();
    
    public ValidationException(Map<String, String> errors) {
        super("Validation failed");
        this.errors = errors;
    }
    
    public Map<String, String> getErrors() {
        return errors;
    }
}

class UserService {
    void getUserById(String userId) throws ResourceNotFoundException {
        User user = database.findUser(userId);
        if (user == null) {
            throw new ResourceNotFoundException("User", userId);
        }
        return user;
    }
    
    void createUser(UserDTO userData) throws ValidationException {
        Map<String, String> errors = new HashMap<>();
        
        if (userData.email == null || !isValidEmail(userData.email)) {
            errors.put("email", "Invalid email format");
        }
        
        if (userData.age < 18) {
            errors.put("age", "Must be 18 or older");
        }
        
        if (!errors.isEmpty()) {
            throw new ValidationException(errors);
        }
        
        // Create user
    }
}

// Used in: Spring Boot REST APIs, Microservices
```

### 6. **Shopping Cart (Nested Classes)**

```java
class ShoppingCart {
    private List<Item> items = new ArrayList<>();
    
    // Inner class representing cart item
    public class Item {
        private String productId;
        private String productName;
        private int quantity;
        private double price;
        
        public Item(String productId, String name, int quantity, double price) {
            this.productId = productId;
            this.productName = name;
            this.quantity = quantity;
            this.price = price;
        }
        
        public double getSubtotal() {
            return quantity * price;
        }
        
        public void updateQuantity(int newQuantity) {
            this.quantity = newQuantity;
            updateCartTotal();  // Access outer class method
        }
    }
    
    public Item addItem(String id, String name, int qty, double price) {
        Item item = new Item(id, name, qty, price);
        items.add(item);
        return item;
    }
    
    private void updateCartTotal() {
        // Recalculate total
    }
    
    public double getTotal() {
        return items.stream()
                   .mapToDouble(Item::getSubtotal)
                   .sum();
    }
}

// Used in: E-commerce platforms, Amazon, Flipkart
```

### 7. **Thread Pool with Lambda (Concurrency)**

```java
import java.util.concurrent.*;

class TaskExecutor {
    private ExecutorService executor = Executors.newFixedThreadPool(5);
    
    void executeTasks() {
        // Submit tasks using lambda expressions
        Future<Integer> future1 = executor.submit(() -> {
            Thread.sleep(1000);
            return 42;
        });
        
        executor.submit(() -> {
            System.out.println("Task 2 executing");
        });
        
        // Execute with method reference
        executor.submit(this::longRunningTask);
        
        // Shutdown
        executor.shutdown();
    }
    
    void longRunningTask() {
        // Task implementation
    }
}

// Used in: Web servers, Background job processors, Async operations
```

### 8. **Form Validation Framework (Functional Interface)**

```java
@FunctionalInterface
interface Validator<T> {
    boolean validate(T value);
}

class FormValidation {
    private Map<String, List<Validator<String>>> rules = new HashMap<>();
    
    void addRule(String field, Validator<String> validator) {
        rules.computeIfAbsent(field, k -> new ArrayList<>()).add(validator);
    }
    
    Map<String, String> validate(Map<String, String> formData) {
        Map<String, String> errors = new HashMap<>();
        
        for (Map.Entry<String, List<Validator<String>>> entry : rules.entrySet()) {
            String field = entry.getKey();
            String value = formData.get(field);
            
            for (Validator<String> validator : entry.getValue()) {
                if (!validator.validate(value)) {
                    errors.put(field, "Invalid " + field);
                    break;
                }
            }
        }
        
        return errors;
    }
}

// Usage
FormValidation validation = new FormValidation();
validation.addRule("email", s -> s != null && s.contains("@"));
validation.addRule("age", s -> Integer.parseInt(s) >= 18);
validation.addRule("phone", s -> s.matches("\\d{10}"));

Map<String, String> formData = new HashMap<>();
formData.put("email", "user@example.com");
formData.put("age", "25");
formData.put("phone", "1234567890");

Map<String, String> errors = validation.validate(formData);

// Used in: Web forms, Registration systems, Survey platforms
```

### 9. **Retry Logic with Exception Handling**

```java
class RetryableOperation {
    private static final int MAX_RETRIES = 3;
    
    <T> T executeWithRetry(Supplier<T> operation) throws Exception {
        int attempts = 0;
        Exception lastException = null;
        
        while (attempts < MAX_RETRIES) {
            try {
                return operation.get();
            } catch (Exception e) {
                lastException = e;
                attempts++;
                System.out.println("Attempt " + attempts + " failed: " + 
                                 e.getMessage());
                
                if (attempts < MAX_RETRIES) {
                    Thread.sleep(1000 * attempts);  // Exponential backoff
                }
            }
        }
        
        throw new Exception("Operation failed after " + MAX_RETRIES + 
                          " attempts", lastException);
    }
}

// Usage
RetryableOperation retry = new RetryableOperation();
try {
    String result = retry.executeWithRetry(() -> {
        return callExternalAPI();
    });
} catch (Exception e) {
    System.err.println("All retries failed: " + e.getMessage());
}

// Used in: API clients, Network operations, Microservices
```

### 10. **Database Transaction Manager (Try-With-Resources)**

```java
class DatabaseTransaction implements AutoCloseable {
    private Connection connection;
    private boolean committed = false;
    
    public DatabaseTransaction() throws SQLException {
        this.connection = DriverManager.getConnection(DB_URL);
        this.connection.setAutoCommit(false);
        System.out.println("Transaction started");
    }
    
    public void execute(String sql) throws SQLException {
        try (PreparedStatement stmt = connection.prepareStatement(sql)) {
            stmt.execute();
        }
    }
    
    public void commit() throws SQLException {
        connection.commit();
        committed = true;
        System.out.println("Transaction committed");
    }
    
    @Override
    public void close() throws SQLException {
        if (!committed) {
            connection.rollback();
            System.out.println("Transaction rolled back");
        }
        connection.close();
    }
}

// Usage
try (DatabaseTransaction transaction = new DatabaseTransaction()) {
    transaction.execute("INSERT INTO users VALUES (...)");
    transaction.execute("UPDATE accounts SET balance = ...");
    transaction.commit();
} catch (SQLException e) {
    // Transaction automatically rolled back
    System.err.println("Transaction failed: " + e.getMessage());
}

// Used in: Banking systems, E-commerce checkout, Data consistency
```

---

## Key Takeaways

- **Nested classes** provide logical grouping and encapsulation
- **Anonymous classes** are useful for one-time implementations
- **Functional interfaces** enable lambda expressions and functional programming
- **Lambda expressions** provide concise syntax for functional interfaces
- **Utility classes** contain static helper methods and prevent instantiation
- **Try-catch** handles exceptions gracefully
- **Multi-catch** reduces code duplication when handling multiple exceptions
- **Try-with-resources** automatically closes resources, prevents resource leaks
- **Custom exceptions** provide domain-specific error handling
- Always close resources (files, connections, streams) properly
- Use checked exceptions for recoverable errors, unchecked for programming errors

---

## Quick Reference

**Inner class:** `class Outer { class Inner { } }`  
**Static nested:** `class Outer { static class Nested { } }`  
**Anonymous class:** `new Interface() { @Override void method() { } }`  
**Lambda:** `(parameters) -> expression` or `(parameters) -> { statements; }`  
**Functional interface:** `@FunctionalInterface interface Name { void method(); }`  
**Try-catch:** `try { } catch (Exception e) { } finally { }`  
**Multi-catch:** `catch (Exception1 | Exception2 e) { }`  
**Try-with-resources:** `try (Resource r = new Resource()) { }`  
**Custom exception:** `class MyException extends Exception { }`  
**Throw:** `throw new Exception("message")`  
**Throws:** `void method() throws Exception { }`  
**Assert:** `assert condition : "message";`
