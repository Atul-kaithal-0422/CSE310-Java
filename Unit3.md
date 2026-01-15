# Unit 3: Inheritance, Polymorphism & Abstraction

## 1. Inheritance

Inheritance allows a class to inherit properties and methods from another class.

### Basic Inheritance

```java
// Parent class (Superclass)
class Animal {
    String name;
    
    void eat() {
        System.out.println(name + " is eating");
    }
    
    void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Child class (Subclass)
class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking");
    }
}

// Usage
Dog dog = new Dog();
dog.name = "Buddy";
dog.eat();    // Inherited from Animal
dog.sleep();  // Inherited from Animal
dog.bark();   // Own method
```

### Types of Inheritance

```java
// Single Inheritance
class Vehicle {
    void start() {
        System.out.println("Vehicle started");
    }
}

class Car extends Vehicle {
    void drive() {
        System.out.println("Car is driving");
    }
}

// Multilevel Inheritance
class SportsCar extends Car {
    void turboBoost() {
        System.out.println("Turbo activated!");
    }
}

// Hierarchical Inheritance
class Bird extends Animal { }
class Fish extends Animal { }
class Mammal extends Animal { }

// Note: Multiple inheritance NOT supported (use interfaces instead)
```

### Constructor in Inheritance

```java
class Parent {
    Parent() {
        System.out.println("Parent constructor");
    }
    
    Parent(String msg) {
        System.out.println("Parent: " + msg);
    }
}

class Child extends Parent {
    Child() {
        super();  // Calls Parent's no-arg constructor
        System.out.println("Child constructor");
    }
    
    Child(String msg) {
        super(msg);  // Calls Parent's parameterized constructor
        System.out.println("Child: " + msg);
    }
}

// Output when creating Child():
// Parent constructor
// Child constructor
```

### The `super` Keyword

```java
class Employee {
    String name;
    double salary;
    
    Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }
    
    void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Salary: " + salary);
    }
}

class Manager extends Employee {
    String department;
    
    Manager(String name, double salary, String department) {
        super(name, salary);  // Call parent constructor
        this.department = department;
    }
    
    @Override
    void displayInfo() {
        super.displayInfo();  // Call parent method
        System.out.println("Department: " + department);
    }
}
```

---

## 2. Polymorphism

Polymorphism means "many forms" - same method behaves differently in different contexts.

### Compile-Time Polymorphism (Method Overloading)

```java
class Calculator {
    // Same method name, different parameters
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
    
    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

### Runtime Polymorphism (Method Overriding)

```java
class Shape {
    void draw() {
        System.out.println("Drawing a shape");
    }
    
    double area() {
        return 0;
    }
}

class Circle extends Shape {
    double radius;
    
    Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    void draw() {
        System.out.println("Drawing a circle");
    }
    
    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    double length, width;
    
    Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }
    
    @Override
    void draw() {
        System.out.println("Drawing a rectangle");
    }
    
    @Override
    double area() {
        return length * width;
    }
}

// Polymorphic behavior
Shape s1 = new Circle(5);
Shape s2 = new Rectangle(4, 6);

s1.draw();  // Drawing a circle
s2.draw();  // Drawing a rectangle

System.out.println(s1.area());  // Circle area
System.out.println(s2.area());  // Rectangle area
```

### Dynamic Method Dispatch

```java
class Bank {
    double getInterestRate() {
        return 0;
    }
}

class SBI extends Bank {
    @Override
    double getInterestRate() {
        return 7.5;
    }
}

class HDFC extends Bank {
    @Override
    double getInterestRate() {
        return 8.0;
    }
}

// Dynamic method dispatch
Bank bank;

bank = new SBI();
System.out.println(bank.getInterestRate());  // 7.5

bank = new HDFC();
System.out.println(bank.getInterestRate());  // 8.0
```

---

## 3. Object Class

`Object` is the root class of all Java classes. Every class implicitly extends `Object`.

### Common Object Class Methods

```java
class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

Person p = new Person("Alice", 25);

// toString() - returns string representation
System.out.println(p.toString());  
// Output: Person@15db9742 (default implementation)

// hashCode() - returns hash code
System.out.println(p.hashCode());  // Some integer value

// getClass() - returns runtime class
System.out.println(p.getClass());  // class Person

// equals() - compares objects
Person p2 = new Person("Alice", 25);
System.out.println(p.equals(p2));  // false (default compares references)
```

---

## 4. Overriding toString() and equals()

### Overriding toString()

```java
class Book {
    String title;
    String author;
    double price;
    
    Book(String title, String author, double price) {
        this.title = title;
        this.author = author;
        this.price = price;
    }
    
    @Override
    public String toString() {
        return "Book{title='" + title + "', author='" + author + 
               "', price=" + price + "}";
    }
}

Book book = new Book("1984", "George Orwell", 15.99);
System.out.println(book);  
// Output: Book{title='1984', author='George Orwell', price=15.99}
```

### Overriding equals()

```java
class Student {
    int id;
    String name;
    
    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
    
    @Override
    public boolean equals(Object obj) {
        // Check if same reference
        if (this == obj) return true;
        
        // Check if null or different class
        if (obj == null || getClass() != obj.getClass()) {
            return false;
        }
        
        // Cast and compare fields
        Student student = (Student) obj;
        return id == student.id && name.equals(student.name);
    }
    
    @Override
    public int hashCode() {
        // Important: override hashCode when overriding equals
        return Objects.hash(id, name);
    }
}

Student s1 = new Student(101, "Alice");
Student s2 = new Student(101, "Alice");
Student s3 = new Student(102, "Bob");

System.out.println(s1.equals(s2));  // true (same content)
System.out.println(s1.equals(s3));  // false (different content)
System.out.println(s1 == s2);       // false (different references)
```

### equals() Contract

```java
// Properties of equals():
// 1. Reflexive: x.equals(x) == true
// 2. Symmetric: x.equals(y) == y.equals(x)
// 3. Transitive: if x.equals(y) and y.equals(z), then x.equals(z)
// 4. Consistent: multiple calls return same result
// 5. x.equals(null) == false

import java.util.Objects;

class Point {
    int x, y;
    
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Point point = (Point) o;
        return x == point.x && y == point.y;
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(x, y);
    }
    
    @Override
    public String toString() {
        return "Point(" + x + ", " + y + ")";
    }
}
```

---

## 5. instanceof Operator

Checks if an object is an instance of a class or interface.

### Basic Usage

```java
class Animal { }
class Dog extends Animal { }
class Cat extends Animal { }

Animal a = new Dog();

System.out.println(a instanceof Dog);     // true
System.out.println(a instanceof Animal);  // true
System.out.println(a instanceof Cat);     // false

// Avoid ClassCastException
if (a instanceof Dog) {
    Dog d = (Dog) a;  // Safe casting
    // Use d...
}
```

### Pattern Matching (Java 16+)

```java
Object obj = "Hello";

// Traditional approach
if (obj instanceof String) {
    String s = (String) obj;
    System.out.println(s.toUpperCase());
}

// Pattern matching (Java 16+)
if (obj instanceof String s) {
    System.out.println(s.toUpperCase());
}
```

### Practical Example

```java
class PaymentProcessor {
    void processPayment(Object payment) {
        if (payment instanceof CreditCard) {
            CreditCard cc = (CreditCard) payment;
            System.out.println("Processing credit card: " + cc.number);
        } else if (payment instanceof PayPal) {
            PayPal pp = (PayPal) payment;
            System.out.println("Processing PayPal: " + pp.email);
        } else if (payment instanceof Cash) {
            System.out.println("Processing cash payment");
        } else {
            System.out.println("Unknown payment method");
        }
    }
}
```

### instanceof with null

```java
String str = null;
System.out.println(str instanceof String);  // false
// instanceof returns false for null, never throws NullPointerException
```

---

## 6. Abstract Classes and Methods

Abstract classes cannot be instantiated and can contain abstract methods (without implementation).

### Basic Abstract Class

```java
abstract class Vehicle {
    String brand;
    
    // Abstract method (no body)
    abstract void start();
    
    // Concrete method
    void stop() {
        System.out.println("Vehicle stopped");
    }
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car started with key");
    }
}

class Motorcycle extends Vehicle {
    @Override
    void start() {
        System.out.println("Motorcycle started with button");
    }
}

// Vehicle v = new Vehicle();  // ERROR: Cannot instantiate
Car car = new Car();
car.start();  // Car started with key
car.stop();   // Vehicle stopped
```

### Abstract Class with Constructor

```java
abstract class Employee {
    String name;
    double baseSalary;
    
    Employee(String name, double baseSalary) {
        this.name = name;
        this.baseSalary = baseSalary;
    }
    
    abstract double calculateSalary();
    
    void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Salary: " + calculateSalary());
    }
}

class FullTimeEmployee extends Employee {
    double bonus;
    
    FullTimeEmployee(String name, double baseSalary, double bonus) {
        super(name, baseSalary);
        this.bonus = bonus;
    }
    
    @Override
    double calculateSalary() {
        return baseSalary + bonus;
    }
}

class ContractEmployee extends Employee {
    int hoursWorked;
    double hourlyRate;
    
    ContractEmployee(String name, int hours, double rate) {
        super(name, 0);
        this.hoursWorked = hours;
        this.hourlyRate = rate;
    }
    
    @Override
    double calculateSalary() {
        return hoursWorked * hourlyRate;
    }
}
```

### When to Use Abstract Classes

```java
// Template for common behavior
abstract class GameCharacter {
    int health;
    int level;
    
    abstract void attack();
    abstract void defend();
    
    // Common behavior
    void levelUp() {
        level++;
        health += 10;
    }
    
    boolean isAlive() {
        return health > 0;
    }
}

class Warrior extends GameCharacter {
    @Override
    void attack() {
        System.out.println("Sword slash!");
    }
    
    @Override
    void defend() {
        System.out.println("Shield block!");
    }
}

class Mage extends GameCharacter {
    @Override
    void attack() {
        System.out.println("Fireball!");
    }
    
    @Override
    void defend() {
        System.out.println("Magic barrier!");
    }
}
```

---

## 7. Interfaces

Interfaces define a contract that classes must implement. All methods are abstract by default (until Java 8).

### Basic Interface

```java
interface Drawable {
    void draw();  // public abstract by default
}

class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing circle");
    }
}

class Square implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing square");
    }
}

// Usage
Drawable shape = new Circle();
shape.draw();  // Drawing circle
```

### Multiple Interfaces

```java
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

// Class can implement multiple interfaces
class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck is flying");
    }
    
    @Override
    public void swim() {
        System.out.println("Duck is swimming");
    }
}
```

### Interface with Constants

```java
interface Constants {
    // Variables are public, static, final by default
    int MAX_USERS = 100;
    String APP_NAME = "MyApp";
    double PI = 3.14159;
}

class App implements Constants {
    void checkLimit(int users) {
        if (users > MAX_USERS) {
            System.out.println("Limit exceeded");
        }
    }
}
```

### Default Methods (Java 8+)

```java
interface Vehicle {
    void start();
    
    // Default method with implementation
    default void horn() {
        System.out.println("Beep beep!");
    }
}

class Bike implements Vehicle {
    @Override
    public void start() {
        System.out.println("Bike started");
    }
    
    // Can override default method or use as-is
}

Bike bike = new Bike();
bike.start();  // Bike started
bike.horn();   // Beep beep! (default implementation)
```

### Static Methods in Interface (Java 8+)

```java
interface MathOperations {
    static int add(int a, int b) {
        return a + b;
    }
    
    static int multiply(int a, int b) {
        return a * b;
    }
}

// Call using interface name
int sum = MathOperations.add(5, 3);
int product = MathOperations.multiply(4, 2);
```

### Functional Interface

```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);  // Single abstract method
}

// Lambda expression
Calculator add = (a, b) -> a + b;
Calculator multiply = (a, b) -> a * b;

System.out.println(add.calculate(5, 3));       // 8
System.out.println(multiply.calculate(5, 3));  // 15
```

### Interface Inheritance

```java
interface Animal {
    void eat();
}

interface Mammal extends Animal {
    void breathe();
}

interface Carnivore extends Animal {
    void hunt();
}

class Lion implements Mammal, Carnivore {
    @Override
    public void eat() {
        System.out.println("Lion eating");
    }
    
    @Override
    public void breathe() {
        System.out.println("Lion breathing");
    }
    
    @Override
    public void hunt() {
        System.out.println("Lion hunting");
    }
}
```

### Abstract Class vs Interface

```java
// Use ABSTRACT CLASS when:
// - You want to share code among related classes
// - Classes have common fields
// - You need constructors

abstract class AbstractAnimal {
    String name;  // Common field
    
    AbstractAnimal(String name) {  // Constructor
        this.name = name;
    }
    
    abstract void makeSound();
    
    void sleep() {  // Common method
        System.out.println(name + " is sleeping");
    }
}

// Use INTERFACE when:
// - Unrelated classes should implement same methods
// - You want multiple inheritance
// - You're defining a contract/capability

interface Playable {
    void play();  // Just a capability
}

interface Recordable {
    void record();
}

class VideoPlayer implements Playable, Recordable {
    public void play() { }
    public void record() { }
}
```

---

## Practice Problems (LeetCode)

### Inheritance & Polymorphism
1. **LeetCode #232 - Implement Queue using Stacks** (Class design)
2. **LeetCode #225 - Implement Stack using Queues** (Class design)
3. **LeetCode #146 - LRU Cache** (OOP design)
4. **LeetCode #155 - Min Stack** (Inheritance concepts)
5. **LeetCode #622 - Design Circular Queue** (Class design)

### Object Class Methods
6. **LeetCode #383 - Ransom Note** (String equals)
7. **LeetCode #205 - Isomorphic Strings** (equals implementation)
8. **LeetCode #290 - Word Pattern** (equals and hashCode)

### Abstract Classes & Interfaces
9. **LeetCode #1603 - Design Parking System** (Interface/Abstract)
10. **LeetCode #1396 - Design Underground System** (OOP design)
11. **LeetCode #1244 - Design A Leaderboard** (Interface design)
12. **LeetCode #588 - Design In-Memory File System** (Complex OOP)

### instanceof & Type Checking
13. **LeetCode #173 - Binary Search Tree Iterator** (Type handling)
14. **LeetCode #1274 - Number of Ships in Rectangle** (Object type handling)

### Comprehensive OOP
15. **LeetCode #355 - Design Twitter** (Complete OOP)
16. **LeetCode #380 - Insert Delete GetRandom O(1)** (Data structure design)
17. **LeetCode #208 - Implement Trie** (Tree structure with OOP)
18. **LeetCode #211 - Design Add and Search Words Data Structure**
19. **LeetCode #705 - Design HashSet** (Custom implementation)
20. **LeetCode #706 - Design HashMap** (Custom implementation)

---

## Real-Life Applications

### 1. **Payment Gateway System (Polymorphism)**

```java
abstract class Payment {
    double amount;
    
    Payment(double amount) {
        this.amount = amount;
    }
    
    abstract boolean processPayment();
    abstract String getReceipt();
}

class CreditCardPayment extends Payment {
    String cardNumber;
    
    CreditCardPayment(double amount, String cardNumber) {
        super(amount);
        this.cardNumber = cardNumber;
    }
    
    @Override
    boolean processPayment() {
        // Process credit card
        return true;
    }
    
    @Override
    String getReceipt() {
        return "Credit card ending in " + 
               cardNumber.substring(cardNumber.length() - 4);
    }
}

class UPIPayment extends Payment {
    String upiId;
    
    UPIPayment(double amount, String upiId) {
        super(amount);
        this.upiId = upiId;
    }
    
    @Override
    boolean processPayment() {
        // Process UPI
        return true;
    }
    
    @Override
    String getReceipt() {
        return "UPI transaction from " + upiId;
    }
}

// Used in: PayTM, PhonePe, Google Pay, Stripe
```

### 2. **Media Player (Interface & Polymorphism)**

```java
interface MediaPlayer {
    void play();
    void pause();
    void stop();
}

interface Downloadable {
    void download(String url);
}

class AudioPlayer implements MediaPlayer, Downloadable {
    @Override
    public void play() {
        System.out.println("Playing audio");
    }
    
    @Override
    public void pause() {
        System.out.println("Audio paused");
    }
    
    @Override
    public void stop() {
        System.out.println("Audio stopped");
    }
    
    @Override
    public void download(String url) {
        System.out.println("Downloading audio from " + url);
    }
}

class VideoPlayer implements MediaPlayer, Downloadable {
    @Override
    public void play() {
        System.out.println("Playing video");
    }
    
    @Override
    public void pause() {
        System.out.println("Video paused");
    }
    
    @Override
    public void stop() {
        System.out.println("Video stopped");
    }
    
    @Override
    public void download(String url) {
        System.out.println("Downloading video from " + url);
    }
}

// Used in: VLC, Spotify, YouTube, Netflix
```

### 3. **Employee Management System (Inheritance)**

```java
class Employee {
    protected String name;
    protected int id;
    protected double baseSalary;
    
    Employee(String name, int id, double baseSalary) {
        this.name = name;
        this.id = id;
        this.baseSalary = baseSalary;
    }
    
    double calculateSalary() {
        return baseSalary;
    }
    
    @Override
    public String toString() {
        return "Employee{name='" + name + "', id=" + id + 
               ", salary=" + calculateSalary() + "}";
    }
}

class Manager extends Employee {
    private double bonus;
    
    Manager(String name, int id, double baseSalary, double bonus) {
        super(name, id, baseSalary);
        this.bonus = bonus;
    }
    
    @Override
    double calculateSalary() {
        return baseSalary + bonus;
    }
}

class Developer extends Employee {
    private int projectsCompleted;
    private double projectBonus;
    
    Developer(String name, int id, double baseSalary) {
        super(name, id, baseSalary);
    }
    
    void completeProject() {
        projectsCompleted++;
    }
    
    @Override
    double calculateSalary() {
        return baseSalary + (projectsCompleted * projectBonus);
    }
}

// Used in: SAP, Workday, BambooHR
```

### 4. **Vehicle Rental System (Abstract Class)**

```java
abstract class Vehicle {
    String licensePlate;
    String brand;
    double pricePerDay;
    
    Vehicle(String licensePlate, String brand, double pricePerDay) {
        this.licensePlate = licensePlate;
        this.brand = brand;
        this.pricePerDay = pricePerDay;
    }
    
    abstract double calculateRentalCost(int days);
    
    abstract String getVehicleType();
    
    void displayInfo() {
        System.out.println(getVehicleType() + ": " + brand);
        System.out.println("License: " + licensePlate);
    }
}

class Car extends Vehicle {
    boolean hasAC;
    
    Car(String license, String brand, double price, boolean hasAC) {
        super(license, brand, price);
        this.hasAC = hasAC;
    }
    
    @Override
    double calculateRentalCost(int days) {
        double cost = pricePerDay * days;
        if (hasAC) cost += 200 * days;
        return cost;
    }
    
    @Override
    String getVehicleType() {
        return "Car";
    }
}

class Bike extends Vehicle {
    int engineCC;
    
    Bike(String license, String brand, double price, int cc) {
        super(license, brand, price);
        this.engineCC = cc;
    }
    
    @Override
    double calculateRentalCost(int days) {
        return pricePerDay * days * 0.8;  // 20% discount for bikes
    }
    
    @Override
    String getVehicleType() {
        return "Bike";
    }
}

// Used in: Zoomcar, Drivezy, Revv
```

### 5. **Notification System (Interface)**

```java
interface Notifiable {
    void sendNotification(String message);
}

class EmailNotification implements Notifiable {
    String email;
    
    EmailNotification(String email) {
        this.email = email;
    }
    
    @Override
    public void sendNotification(String message) {
        System.out.println("Email to " + email + ": " + message);
    }
}

class SMSNotification implements Notifiable {
    String phoneNumber;
    
    SMSNotification(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
    
    @Override
    public void sendNotification(String message) {
        System.out.println("SMS to " + phoneNumber + ": " + message);
    }
}

class PushNotification implements Notifiable {
    String deviceId;
    
    PushNotification(String deviceId) {
        this.deviceId = deviceId;
    }
    
    @Override
    public void sendNotification(String message) {
        System.out.println("Push to device " + deviceId + ": " + message);
    }
}

class NotificationService {
    void notify(Notifiable[] channels, String message) {
        for (Notifiable channel : channels) {
            channel.sendNotification(message);
        }
    }
}

// Used in: WhatsApp, Slack, Firebase Cloud Messaging
```

### 6. **E-commerce Product System (toString & equals)**

```java
class Product {
    String id;
    String name;
    double price;
    String category;
    
    Product(String id, String name, double price, String category) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.category = category;
    }
    
    @Override
    public String toString() {
        return String.format("Product{id='%s', name='%s', price=%.2f, category='%s'}", 
                           id, name, price, category);
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Product product = (Product) obj;
        return id.equals(product.id);
    }
    
    @Override
    public int hashCode() {
        return id.hashCode();
    }
}

// Used in: Amazon, Flipkart, Shopify product catalogs
```

### 7. **Game Character System (instanceof)**

```java
class Character {
    String name;
    int health;
}

class Warrior extends Character {
    void heavyAttack() {
        System.out.println("Heavy sword attack!");
    }
}

class Mage extends Character {
    void castSpell() {
        System.out.println("Casting fireball!");
    }
}

class GameEngine {
    void handleAction(Character c, String action) {
        if (c instanceof Warrior) {
            Warrior w = (Warrior) c;
            if (action.equals("attack")) {
                w.heavyAttack();
            }
        } else if (c instanceof Mage) {
            Mage m = (Mage) c;
            if (action.equals("spell")) {
                m.castSpell();
            }
        }
    }
}

// Used in: RPG games, MMORPG systems
```

### 8. **Banking System (Comprehensive OOP)**

```java
abstract class Account {
    protected String accountNumber;
    protected String holderName;
    protected double balance;
    
    Account(String accountNumber, String holderName, double balance) {
        this.accountNumber = accountNumber;
        this.holderName = holderName;
        this.balance = balance;
    }
    
    abstract void calculateInterest();
    
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
    
    boolean withdraw(double amount) {
        if (amount > 0 && balance >= amount) {
            balance -= amount;
            return true;
        }
        return false;
    }
    
    @Override
    public String toString() {
        return accountNumber + " - " + holderName + " - Balance: " + balance;
    }
}

class SavingsAccount extends Account {
    double interestRate = 4.5;
    
    SavingsAccount(String accNum, String name, double balance) {
        super(accNum, name, balance);
    }
    
    @Override
    void calculateInterest() {
        double interest = balance * interestRate / 100;
        balance += interest;
    }
}

class CurrentAccount extends Account {
    double overdraftLimit;
    
    CurrentAccount(String accNum, String name, double balance, double limit) {
        super(accNum, name, balance);
        this.overdraftLimit = limit;
    }
    
    @Override
    void calculateInterest() {
        // No interest for current accounts
    }
    
    @Override
    boolean withdraw(double amount) {
        if (amount > 0 && (balance + overdraftLimit) >= amount) {
            balance -= amount;
            return true;
        }
        return false;
    }
}

// Used in: Core banking systems, ICICI, HDFC
