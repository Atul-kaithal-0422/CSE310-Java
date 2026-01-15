# Unit 1: Java Fundamentals

## 1. Java Introduction

Java is a high-level, object-oriented programming language developed by Sun Microsystems (now Oracle) in 1995. It's designed to be platform-independent, secure, and robust.

**Key Features:**
- Platform Independent (WORA - Write Once, Run Anywhere)
- Object-Oriented
- Strongly Typed
- Automatic Memory Management (Garbage Collection)
- Multi-threaded
- Secure

---

## 2. Simple Program Structure

Every Java program follows a basic structure:

```java
// Class declaration
public class MyFirstProgram {
    // Main method - entry point of the program
    public static void main(String[] args) {
        // Statements
        System.out.println("Hello, Java!");
    }
}
```

**Key Components:**
- **Class**: Container for code (must match filename)
- **main method**: Program execution starts here
- **Statements**: Instructions ending with semicolon (;)
- **Comments**: `//` single line, `/* */` multi-line

**Example: Simple Calculator**
```java
public class Calculator {
    public static void main(String[] args) {
        int a = 10;
        int b = 5;
        int sum = a + b;
        System.out.println("Sum: " + sum);
    }
}
```

---

## 3. JDK, JRE, JVM

### JVM (Java Virtual Machine)
- Executes Java bytecode
- Platform-specific (different for Windows, Mac, Linux)
- Provides runtime environment

### JRE (Java Runtime Environment)
- JVM + Libraries + Other components
- Needed to **run** Java applications
- JRE = JVM + Standard Libraries

### JDK (Java Development Kit)
- JRE + Development Tools (compiler, debugger)
- Needed to **develop** Java applications
- JDK = JRE + Development Tools (javac, java, javadoc)

**Relationship:**
```
JDK > JRE > JVM
```

**Compilation and Execution Flow:**
```
Source Code (.java) → Compiler (javac) → Bytecode (.class) → JVM → Machine Code
```

---

## 4. Primitive Data Types

Java has 8 primitive data types:

| Type | Size | Range | Default | Example |
|------|------|-------|---------|---------|
| byte | 8-bit | -128 to 127 | 0 | `byte b = 100;` |
| short | 16-bit | -32,768 to 32,767 | 0 | `short s = 1000;` |
| int | 32-bit | -2³¹ to 2³¹-1 | 0 | `int i = 50000;` |
| long | 64-bit | -2⁶³ to 2⁶³-1 | 0L | `long l = 100000L;` |
| float | 32-bit | ~±3.4E38 | 0.0f | `float f = 3.14f;` |
| double | 64-bit | ~±1.7E308 | 0.0d | `double d = 3.14159;` |
| char | 16-bit | 0 to 65,535 | '\u0000' | `char c = 'A';` |
| boolean | 1-bit | true/false | false | `boolean flag = true;` |

```java
public class DataTypeExample {
    public static void main(String[] args) {
        int age = 25;
        double salary = 55000.50;
        char grade = 'A';
        boolean isStudent = true;
        
        System.out.println("Age: " + age);
        System.out.println("Salary: " + salary);
        System.out.println("Grade: " + grade);
        System.out.println("Is Student: " + isStudent);
    }
}
```

---

## 5. Type Conversion

### Implicit Conversion (Widening)
Automatic conversion from smaller to larger type.

```java
int i = 100;
long l = i;        // int to long
double d = l;      // long to double
System.out.println(d); // 100.0
```

**Widening hierarchy:**
```
byte → short → int → long → float → double
         ↓
        char
```

### Explicit Conversion (Narrowing)
Manual conversion from larger to smaller type using casting.

```java
double d = 9.78;
int i = (int) d;   // explicit cast
System.out.println(i); // 9 (loses decimal part)

// Loss of data example
int large = 130;
byte small = (byte) large; // May cause data loss
System.out.println(small); // -126 (overflow)
```

---

## 6. Wrapper Classes

Wrapper classes convert primitives to objects.

| Primitive | Wrapper Class |
|-----------|---------------|
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
| char | Character |
| boolean | Boolean |

```java
// Boxing: primitive to object
int num = 10;
Integer obj = Integer.valueOf(num);  // explicit
Integer obj2 = num;                   // autoboxing

// Unboxing: object to primitive
Integer obj3 = 50;
int num2 = obj3.intValue();          // explicit
int num3 = obj3;                      // auto-unboxing

// Useful methods
String str = "123";
int parsed = Integer.parseInt(str);
System.out.println(parsed + 10);     // 133

System.out.println(Integer.MAX_VALUE); // 2147483647
System.out.println(Double.isNaN(0.0/0.0)); // true
```

---

## 7. Operators

### Arithmetic Operators
```java
int a = 10, b = 3;
System.out.println(a + b);  // 13 (Addition)
System.out.println(a - b);  // 7  (Subtraction)
System.out.println(a * b);  // 30 (Multiplication)
System.out.println(a / b);  // 3  (Division)
System.out.println(a % b);  // 1  (Modulus)
```

### Relational Operators
```java
int x = 5, y = 10;
System.out.println(x == y);  // false (Equal to)
System.out.println(x != y);  // true  (Not equal)
System.out.println(x > y);   // false (Greater than)
System.out.println(x < y);   // true  (Less than)
System.out.println(x >= y);  // false (Greater or equal)
System.out.println(x <= y);  // true  (Less or equal)
```

### Logical Operators
```java
boolean p = true, q = false;
System.out.println(p && q);  // false (AND)
System.out.println(p || q);  // true  (OR)
System.out.println(!p);      // false (NOT)
```

### Assignment Operators
```java
int n = 10;
n += 5;  // n = n + 5  → 15
n -= 3;  // n = n - 3  → 12
n *= 2;  // n = n * 2  → 24
n /= 4;  // n = n / 4  → 6
n %= 4;  // n = n % 4  → 2
```

### Unary Operators
```java
int i = 5;
System.out.println(++i);  // 6 (pre-increment)
System.out.println(i++);  // 6 (post-increment, then i=7)
System.out.println(--i);  // 6 (pre-decrement)
System.out.println(i--);  // 6 (post-decrement, then i=5)
```

### Ternary Operator
```java
int age = 18;
String result = (age >= 18) ? "Adult" : "Minor";
System.out.println(result);  // Adult
```

---

## 8. Conditional Statements

### if Statement
```java
int marks = 75;

if (marks >= 60) {
    System.out.println("Pass");
}
```

### if-else Statement
```java
int number = 7;

if (number % 2 == 0) {
    System.out.println("Even");
} else {
    System.out.println("Odd");
}
```

### if-else-if Ladder
```java
int score = 85;

if (score >= 90) {
    System.out.println("Grade: A");
} else if (score >= 80) {
    System.out.println("Grade: B");
} else if (score >= 70) {
    System.out.println("Grade: C");
} else if (score >= 60) {
    System.out.println("Grade: D");
} else {
    System.out.println("Grade: F");
}
```

### Nested if
```java
int age = 25;
boolean hasLicense = true;

if (age >= 18) {
    if (hasLicense) {
        System.out.println("Can drive");
    } else {
        System.out.println("Get a license first");
    }
} else {
    System.out.println("Too young to drive");
}
```

### switch Statement
```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    case 4:
        System.out.println("Thursday");
        break;
    case 5:
        System.out.println("Friday");
        break;
    default:
        System.out.println("Weekend");
}
```

**Enhanced Switch (Java 14+):**
```java
String day = switch (dayNum) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Invalid day";
};
```

---

## Practice Problems (LeetCode)

### Basic Problems
1. **LeetCode #1344 - Angle Between Hands of a Clock** (Operators, Type conversion)
2. **LeetCode #191 - Number of 1 Bits** (Bitwise operators)
3. **LeetCode #7 - Reverse Integer** (Operators, Type handling)
4. **LeetCode #9 - Palindrome Number** (Conditional statements, Operators)
5. **LeetCode #1281 - Subtract Product and Sum of Digits** (Operators, Loops)

### Intermediate Problems
6. **LeetCode #412 - Fizz Buzz** (Conditional statements)
7. **LeetCode #1232 - Check If It Is a Straight Line** (Arithmetic operators)
8. **LeetCode #258 - Add Digits** (Operators, Type conversion)
9. **LeetCode #263 - Ugly Number** (Conditional statements, Operators)
10. **LeetCode #326 - Power of Three** (Operators, Conditionals)

### Challenge Problems
11. **LeetCode #231 - Power of Two** (Bitwise operators)
12. **LeetCode #50 - Pow(x, n)** (Operators, Type conversion)
13. **LeetCode #29 - Divide Two Integers** (Operators without using *, /, %)

---

## Real-Life Applications

### 1. **E-Commerce Price Calculation**
```java
// Discount calculation using operators
double originalPrice = 1999.99;
double discountPercent = 15;
double discount = originalPrice * (discountPercent / 100);
double finalPrice = originalPrice - discount;

if (finalPrice < 1500) {
    System.out.println("Great deal!");
}
```
**Used in**: Amazon, Flipkart pricing engines

### 2. **Banking ATM System**
```java
// Type safety prevents financial errors
double balance = 5000.50;
double withdrawal = 1000.00;

if (withdrawal <= balance) {
    balance -= withdrawal;
    System.out.println("Remaining: " + balance);
} else {
    System.out.println("Insufficient funds");
}
```
**Used in**: ATM software, mobile banking apps

### 3. **Grade Management System**
```java
// Educational institutions use conditional statements
int marks = 78;
char grade;

if (marks >= 90) grade = 'A';
else if (marks >= 80) grade = 'B';
else if (marks >= 70) grade = 'C';
else if (marks >= 60) grade = 'D';
else grade = 'F';
```
**Used in**: School management systems, LMS platforms

### 4. **Temperature Converter (IoT Sensors)**
```java
// Type conversion in sensor data
double celsius = 25.5;
double fahrenheit = (celsius * 9/5) + 32;
int roundedTemp = (int) Math.round(fahrenheit);
```
**Used in**: Smart thermostats, weather stations

### 5. **Traffic Light Control System**
```java
// Switch statements in embedded systems
int signalState = 2;

switch (signalState) {
    case 1:
        System.out.println("RED - Stop");
        break;
    case 2:
        System.out.println("YELLOW - Slow down");
        break;
    case 3:
        System.out.println("GREEN - Go");
        break;
}
```
**Used in**: Traffic management systems worldwide

### 6. **Gaming Score Calculator**
```java
// Wrapper classes for storing high scores
Integer playerScore = 15000;
Integer highScore = 12000;

if (playerScore > highScore) {
    highScore = playerScore;
    System.out.println("New high score: " + highScore);
}
```
**Used in**: Mobile games, online gaming platforms

### 7. **Tax Calculation Software**
```java
// Precise calculations using appropriate types
double income = 550000.0;
double tax = 0.0;

if (income <= 250000) {
    tax = 0;
} else if (income <= 500000) {
    tax = (income - 250000) * 0.05;
} else {
    tax = 12500 + (income - 500000) * 0.20;
}
```
**Used in**: TurboTax, H&R Block tax software

### 8. **Date Validator in Forms**
```java
// Type conversion and validation
String dayStr = "15";
int day = Integer.parseInt(dayStr);
int month = 2;

if (month == 2 && day > 28) {
    System.out.println("Invalid date for February");
} else if (day > 31) {
    System.out.println("Invalid day");
}
```
**Used in**: Online forms, booking systems

---

## Key Takeaways

- Java programs must have a `main` method as the entry point
- JDK contains JRE, which contains JVM
- Choose appropriate data types to optimize memory
- Understand implicit vs explicit type conversion to avoid data loss
- Wrapper classes enable primitives to work with collections
- Master operators for efficient calculations
- Conditional statements control program flow based on logic

---

## Quick Reference

**Compile:** `javac FileName.java`  
**Run:** `java FileName`  
**JDK Download:** oracle.com/java/technologies/downloads/
