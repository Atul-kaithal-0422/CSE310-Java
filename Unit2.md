# Unit 2: Arrays, Classes & Control Flow

## 1. Arrays

Arrays store multiple values of the same type in a single variable.

### Single-Dimensional Arrays

```java
// Declaration and initialization
int[] numbers = new int[5];  // Creates array of size 5
int[] scores = {85, 90, 78, 92, 88};  // Initialize with values

// Accessing elements
System.out.println(scores[0]);  // 85 (index starts at 0)
scores[2] = 95;  // Modify element

// Array length
System.out.println(scores.length);  // 5
```

### Multi-Dimensional Arrays

```java
// 2D Array
int[][] matrix = new int[3][4];  // 3 rows, 4 columns
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Accessing 2D array
System.out.println(grid[1][2]);  // 6

// Jagged arrays (different column sizes)
int[][] jagged = new int[3][];
jagged[0] = new int[2];
jagged[1] = new int[4];
jagged[2] = new int[3];
```

### Enhanced For Loop with Arrays

```java
int[] numbers = {10, 20, 30, 40, 50};

for (int num : numbers) {
    System.out.println(num);
}
```

### Common Array Operations

```java
import java.util.Arrays;

int[] arr = {5, 2, 8, 1, 9};

// Sort
Arrays.sort(arr);  // [1, 2, 5, 8, 9]

// Binary search (requires sorted array)
int index = Arrays.binarySearch(arr, 5);  // Returns index

// Fill
Arrays.fill(arr, 0);  // All elements become 0

// Copy
int[] copy = Arrays.copyOf(arr, arr.length);

// Compare
boolean equal = Arrays.equals(arr, copy);
```

---

## 2. Enums

Enums represent a fixed set of constants.

```java
// Basic enum
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

public class EnumExample {
    public static void main(String[] args) {
        Day today = Day.MONDAY;
        System.out.println(today);  // MONDAY
        
        // Using in switch
        switch (today) {
            case MONDAY:
                System.out.println("Start of work week");
                break;
            case FRIDAY:
                System.out.println("TGIF!");
                break;
            default:
                System.out.println("Midweek");
        }
    }
}
```

### Enum with Fields and Methods

```java
enum Planet {
    MERCURY(3.303e+23, 2.4397e6),
    VENUS(4.869e+24, 6.0518e6),
    EARTH(5.976e+24, 6.37814e6);
    
    private final double mass;
    private final double radius;
    
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }
    
    public double getMass() {
        return mass;
    }
    
    public double surfaceGravity() {
        return 6.67300E-11 * mass / (radius * radius);
    }
}

// Usage
Planet earth = Planet.EARTH;
System.out.println(earth.surfaceGravity());
```

### Enum Methods

```java
// values() - returns all enum constants
for (Day d : Day.values()) {
    System.out.println(d);
}

// valueOf() - converts string to enum
Day day = Day.valueOf("MONDAY");

// ordinal() - returns position
System.out.println(Day.FRIDAY.ordinal());  // 4
```

---

## 3. Classes and Objects

### Class Definition

```java
class Student {
    // Instance variables (fields)
    String name;
    int age;
    double gpa;
    
    // Method
    void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("GPA: " + gpa);
    }
}
```

### Creating Objects

```java
public class Main {
    public static void main(String[] args) {
        // Create object
        Student s1 = new Student();
        
        // Set values
        s1.name = "Alice";
        s1.age = 20;
        s1.gpa = 3.8;
        
        // Call method
        s1.displayInfo();
        
        // Multiple objects
        Student s2 = new Student();
        s2.name = "Bob";
        s2.age = 21;
        s2.gpa = 3.5;
    }
}
```

### Constructors

```java
class Car {
    String brand;
    String model;
    int year;
    
    // Default constructor
    Car() {
        brand = "Unknown";
        model = "Unknown";
        year = 2020;
    }
    
    // Parameterized constructor
    Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }
    
    void displayInfo() {
        System.out.println(brand + " " + model + " (" + year + ")");
    }
}

// Usage
Car car1 = new Car();  // Uses default constructor
Car car2 = new Car("Toyota", "Camry", 2023);  // Uses parameterized
```

### Access Modifiers

```java
class BankAccount {
    private double balance;  // Only accessible within class
    public String accountNumber;  // Accessible everywhere
    
    // Getter
    public double getBalance() {
        return balance;
    }
    
    // Setter
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
}
```

---

## 4. Method Overloading

Same method name with different parameters.

```java
class Calculator {
    // Overloaded methods
    int add(int a, int b) {
        return a + b;
    }
    
    int add(int a, int b, int c) {
        return a + b + c;
    }
    
    double add(double a, double b) {
        return a + b;
    }
    
    String add(String a, String b) {
        return a + b;
    }
}

// Usage
Calculator calc = new Calculator();
System.out.println(calc.add(5, 10));           // 15
System.out.println(calc.add(5, 10, 15));       // 30
System.out.println(calc.add(5.5, 10.5));       // 16.0
System.out.println(calc.add("Hello", "World")); // HelloWorld
```

### Constructor Overloading

```java
class Rectangle {
    int length;
    int width;
    
    // No parameters
    Rectangle() {
        length = 1;
        width = 1;
    }
    
    // One parameter (square)
    Rectangle(int side) {
        length = side;
        width = side;
    }
    
    // Two parameters
    Rectangle(int l, int w) {
        length = l;
        width = w;
    }
    
    int area() {
        return length * width;
    }
}
```

---

## 5. The `this` Keyword

`this` refers to the current object.

### Using `this` to Resolve Name Conflicts

```java
class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;  // this.name is instance variable
        this.age = age;    // name and age are parameters
    }
}
```

### Using `this` to Call Another Constructor

```java
class Employee {
    String name;
    int id;
    double salary;
    
    Employee() {
        this("Unknown", 0, 0.0);  // Calls parameterized constructor
    }
    
    Employee(String name, int id) {
        this(name, id, 50000.0);  // Calls three-parameter constructor
    }
    
    Employee(String name, int id, double salary) {
        this.name = name;
        this.id = id;
        this.salary = salary;
    }
}
```

### Using `this` to Return Current Object

```java
class Builder {
    String name;
    int value;
    
    Builder setName(String name) {
        this.name = name;
        return this;  // Returns current object
    }
    
    Builder setValue(int value) {
        this.value = value;
        return this;
    }
    
    void display() {
        System.out.println(name + ": " + value);
    }
}

// Method chaining
Builder b = new Builder();
b.setName("Test").setValue(100).display();
```

---

## 6. Initializer Blocks

Code blocks that execute before constructors.

### Instance Initializer Block

```java
class Demo {
    int x;
    
    // Instance initializer block
    {
        x = 10;
        System.out.println("Instance block executed");
    }
    
    Demo() {
        System.out.println("Constructor executed");
    }
}

// Output when object is created:
// Instance block executed
// Constructor executed
```

---

## 7. Loops

### for Loop

```java
// Basic for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// Multiple variables
for (int i = 0, j = 10; i < j; i++, j--) {
    System.out.println(i + " " + j);
}

// Infinite loop
for (;;) {
    // runs forever (until break)
}
```

### Enhanced for Loop (for-each)

```java
int[] numbers = {1, 2, 3, 4, 5};

for (int num : numbers) {
    System.out.println(num);
}

String[] names = {"Alice", "Bob", "Charlie"};
for (String name : names) {
    System.out.println(name);
}
```

### while Loop

```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}

// User input validation
Scanner sc = new Scanner(System.in);
int num = -1;
while (num < 0) {
    System.out.println("Enter positive number:");
    num = sc.nextInt();
}
```

### do-while Loop

```java
int count = 0;
do {
    System.out.println(count);
    count++;
} while (count < 5);

// Executes at least once even if condition is false
int x = 10;
do {
    System.out.println("Executed");
} while (x < 5);  // Still prints "Executed" once
```

### Loop Control Statements

```java
// break - exits the loop
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // Loop stops at i=5
    }
    System.out.println(i);
}

// continue - skips current iteration
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // Skip even numbers
    }
    System.out.println(i);  // Only prints odd numbers
}

// Labeled break
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer;  // Breaks out of outer loop
        }
        System.out.println(i + "," + j);
    }
}
```

---

## 8. String Class

Strings are immutable objects in Java.

### Creating Strings

```java
// String literal (preferred)
String str1 = "Hello";

// Using new keyword
String str2 = new String("Hello");

// From char array
char[] chars = {'J', 'a', 'v', 'a'};
String str3 = new String(chars);
```

### String Methods

```java
String text = "Hello World";

// Length
System.out.println(text.length());  // 11

// Character at index
System.out.println(text.charAt(0));  // H

// Substring
System.out.println(text.substring(0, 5));  // Hello
System.out.println(text.substring(6));     // World

// Case conversion
System.out.println(text.toLowerCase());  // hello world
System.out.println(text.toUpperCase());  // HELLO WORLD

// Trim whitespace
String padded = "  Java  ";
System.out.println(padded.trim());  // "Java"

// Replace
System.out.println(text.replace('l', 'L'));  // HeLLo WorLd

// Split
String csv = "apple,banana,orange";
String[] fruits = csv.split(",");

// Contains
System.out.println(text.contains("World"));  // true

// Starts/Ends with
System.out.println(text.startsWith("Hello"));  // true
System.out.println(text.endsWith("World"));    // true

// Index of
System.out.println(text.indexOf('o'));      // 4
System.out.println(text.lastIndexOf('o'));  // 7

// Equals
String s1 = "Java";
String s2 = "Java";
System.out.println(s1.equals(s2));           // true
System.out.println(s1.equalsIgnoreCase("java"));  // true

// Compare
System.out.println("abc".compareTo("def"));  // negative
```

### String Immutability

```java
String original = "Hello";
String modified = original.concat(" World");

System.out.println(original);   // Hello (unchanged)
System.out.println(modified);   // Hello World (new object)
```

### String Pool

```java
String s1 = "Java";      // Created in string pool
String s2 = "Java";      // Points to same object in pool
String s3 = new String("Java");  // Creates new object in heap

System.out.println(s1 == s2);   // true (same reference)
System.out.println(s1 == s3);   // false (different references)
System.out.println(s1.equals(s3));  // true (same content)
```

---

## 9. StringBuilder Class

Mutable alternative to String for efficient string manipulation.

### Creating StringBuilder

```java
// Empty StringBuilder
StringBuilder sb1 = new StringBuilder();

// With initial capacity
StringBuilder sb2 = new StringBuilder(50);

// From String
StringBuilder sb3 = new StringBuilder("Hello");
```

### StringBuilder Methods

```java
StringBuilder sb = new StringBuilder("Hello");

// Append
sb.append(" World");
sb.append(123);
System.out.println(sb);  // Hello World123

// Insert
sb.insert(5, ",");
System.out.println(sb);  // Hello, World123

// Delete
sb.delete(5, 7);  // Removes ", "
System.out.println(sb);  // HelloWorld123

// Delete character at index
sb.deleteCharAt(5);
System.out.println(sb);  // Helloorld123

// Reverse
StringBuilder rev = new StringBuilder("Java");
rev.reverse();
System.out.println(rev);  // avaJ

// Replace
sb.replace(0, 5, "Hi");
System.out.println(sb);  // Hiorld123

// Capacity and length
System.out.println(sb.length());    // Current length
System.out.println(sb.capacity());  // Current capacity

// Convert to String
String result = sb.toString();
```

### String vs StringBuilder

```java
// Inefficient (creates multiple String objects)
String str = "";
for (int i = 0; i < 1000; i++) {
    str += i;  // Creates new String object each time
}

// Efficient (modifies same StringBuilder object)
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);  // Modifies existing object
}
String result = sb.toString();
```

### StringBuffer vs StringBuilder

```java
// StringBuilder - Fast, not thread-safe
StringBuilder sb = new StringBuilder();

// StringBuffer - Slower, thread-safe (synchronized)
StringBuffer sbuf = new StringBuffer();

// Use StringBuilder unless you need thread safety
```

---

## Practice Problems (LeetCode)

### Arrays
1. **LeetCode #26 - Remove Duplicates from Sorted Array**
2. **LeetCode #27 - Remove Element**
3. **LeetCode #88 - Merge Sorted Array**
4. **LeetCode #121 - Best Time to Buy and Sell Stock**
5. **LeetCode #217 - Contains Duplicate**
6. **LeetCode #283 - Move Zeroes**
7. **LeetCode #1089 - Duplicate Zeros**

### Loops
8. **LeetCode #1672 - Richest Customer Wealth** (Nested loops)
9. **LeetCode #1470 - Shuffle the Array**
10. **LeetCode #1431 - Kids With Greatest Number of Candies**

### Strings
11. **LeetCode #14 - Longest Common Prefix**
12. **LeetCode #28 - Find the Index of First Occurrence**
13. **LeetCode #58 - Length of Last Word**
14. **LeetCode #125 - Valid Palindrome**
15. **LeetCode #344 - Reverse String**
16. **LeetCode #387 - First Unique Character**
17. **LeetCode #392 - Is Subsequence**
18. **LeetCode #242 - Valid Anagram**

### Classes and Objects
19. **LeetCode #705 - Design HashSet** (Class design)
20. **LeetCode #706 - Design HashMap** (Class design)
21. **LeetCode #1603 - Design Parking System** (Class design)

### StringBuilder
22. **LeetCode #151 - Reverse Words in a String**
23. **LeetCode #443 - String Compression**

---

## Real-Life Applications

### 1. **Student Management System (Arrays & Classes)**

```java
class Student {
    String name;
    int rollNumber;
    double[] marks;  // Array for subject marks
    
    Student(String name, int rollNumber, int subjects) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.marks = new double[subjects];
    }
    
    double calculateAverage() {
        double sum = 0;
        for (double mark : marks) {
            sum += mark;
        }
        return sum / marks.length;
    }
}

// University management systems like Blackboard, Canvas
```

### 2. **E-Commerce Order Status (Enums)**

```java
enum OrderStatus {
    PENDING, CONFIRMED, SHIPPED, DELIVERED, CANCELLED
}

class Order {
    String orderId;
    OrderStatus status;
    
    void updateStatus(OrderStatus newStatus) {
        this.status = newStatus;
        notifyCustomer();
    }
}

// Used in: Amazon, Flipkart, Shopify
```

### 3. **Game Character System (Classes & Overloading)**

```java
class GameCharacter {
    String name;
    int health;
    int level;
    
    // Overloaded attack methods
    void attack(GameCharacter enemy) {
        enemy.health -= 10;
    }
    
    void attack(GameCharacter enemy, String weapon) {
        enemy.health -= 20;
    }
    
    void attack(GameCharacter enemy, String weapon, int powerUp) {
        enemy.health -= (20 + powerUp);
    }
}

// Used in: Mobile games, RPG games
```

### 4. **Search Engine (String & StringBuilder)**

```java
class SearchEngine {
    StringBuilder buildQuery(String[] keywords) {
        StringBuilder query = new StringBuilder();
        for (int i = 0; i < keywords.length; i++) {
            query.append(keywords[i]);
            if (i < keywords.length - 1) {
                query.append(" AND ");
            }
        }
        return query;
    }
}

// Used in: Google Search, Elasticsearch
```

### 5. **Social Media Feed (Loops & Arrays)**

```java
class Post {
    String author;
    String content;
    int likes;
}

class Feed {
    Post[] posts;
    
    void displayFeed() {
        for (Post post : posts) {
            if (post != null) {
                System.out.println(post.author + ": " + post.content);
                System.out.println("Likes: " + post.likes);
            }
        }
    }
}

// Used in: Instagram, Twitter, Facebook
```

### 6. **Banking Transaction Log (StringBuilder Performance)**

```java
class TransactionLogger {
    StringBuilder log = new StringBuilder();
    
    void logTransaction(String type, double amount) {
        log.append(System.currentTimeMillis())
           .append(": ")
           .append(type)
           .append(" - $")
           .append(amount)
           .append("\n");
    }
    
    String generateReport() {
        return log.toString();
    }
}

// Used in: Banking apps, PayPal, Stripe
```

### 7. **Hotel Booking System (2D Arrays)**

```java
class Hotel {
    boolean[][] rooms;  // [floor][room number]
    
    Hotel(int floors, int roomsPerFloor) {
        rooms = new boolean[floors][roomsPerFloor];
    }
    
    boolean bookRoom(int floor, int roomNum) {
        if (!rooms[floor][roomNum]) {
            rooms[floor][roomNum] = true;
            return true;
        }
        return false;
    }
}

// Used in: Booking.com, Airbnb, OYO
```

### 9. **Text Editor (StringBuilder)**

```java
class TextEditor {
    StringBuilder content = new StringBuilder();
    
    void type(String text) {
        content.append(text);
    }
    
    void delete(int count) {
        if (content.length() >= count) {
            content.delete(content.length() - count, content.length());
        }
    }
    
    void insert(int position, String text) {
        content.insert(position, text);
    }
}

// Used in: Notepad++, VSCode, Google Docs
```

### 10. **Fitness Tracker (Enums & Arrays)**

```java
enum WorkoutType {
    CARDIO, STRENGTH, YOGA, RUNNING
}

class WorkoutSession {
    WorkoutType type;
    int duration;  // minutes
    int caloriesBurned;
}

class FitnessTracker {
    WorkoutSession[] weeklyWorkouts = new WorkoutSession[7];
    
    int getTotalCalories() {
        int total = 0;
        for (WorkoutSession session : weeklyWorkouts) {
            if (session != null) {
                total += session.caloriesBurned;
            }
        }
        return total;
    }
}

// Used in: Fitbit, Apple Health, Google Fit
```

---

## Key Takeaways

- Arrays store multiple values efficiently; use enhanced for-loop for traversal
- Enums provide type-safe constants with additional functionality
- Classes are blueprints; objects are instances
- Overloading allows same method name with different parameters
- `this` refers to current object and resolves naming conflicts
- Static blocks run once when class loads; instance blocks run before constructor
- Choose appropriate loop based on use case (for, while, do-while)
- String is immutable; StringBuilder is mutable and efficient for concatenation
- Use `==` for reference comparison, `.equals()` for content comparison

---

## Quick Reference

**Array declaration:** `int[] arr = new int[5];`  
**Enhanced for:** `for (Type item : collection)`  
**Enum:** `enum Name { CONSTANT1, CONSTANT2 }`  
**Constructor:** Same name as class, no return type  
**StringBuilder:** `sb.append()`, `sb.insert()`, `sb.delete()`  
**String methods:** `charAt()`, `substring()`, `split()`, `trim()`
