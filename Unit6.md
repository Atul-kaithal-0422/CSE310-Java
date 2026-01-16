# Unit 6: Collections, JDBC & Non-Conventional Devices

## 1. ArrayList

Dynamic array that can grow or shrink in size.

### Basic Operations

```java
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        // Create ArrayList
        ArrayList<String> list = new ArrayList<>();
        
        // Add elements
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        
        // Add at specific position
        list.add(1, "Orange");
        
        // Get element
        String fruit = list.get(0);
        System.out.println(fruit);  // Apple
        
        // Size
        System.out.println("Size: " + list.size());  // 4
        
        // Remove element
        list.remove("Banana");
        list.remove(0);  // Remove by index
        
        // Check if exists
        boolean has = list.contains("Cherry");
        System.out.println(has);  // true
        
        // Print all elements
        for (String s : list) {
            System.out.println(s);
        }
    }
}
```

### ArrayList Methods

```java
ArrayList<Integer> numbers = new ArrayList<>();

// Add multiple elements
numbers.add(10);
numbers.add(20);
numbers.add(30);

// Set (replace) element
numbers.set(1, 25);  // Replace 20 with 25

// Check if empty
boolean empty = numbers.isEmpty();

// Clear all elements
numbers.clear();

// Create from array
Integer[] arr = {1, 2, 3, 4, 5};
ArrayList<Integer> list = new ArrayList<>(Arrays.asList(arr));
```

### Sorting and Searching

```java
import java.util.*;

ArrayList<Integer> nums = new ArrayList<>();
nums.add(5);
nums.add(2);
nums.add(8);
nums.add(1);

// Sort
Collections.sort(nums);
System.out.println(nums);  // [1, 2, 5, 8]

// Reverse
Collections.reverse(nums);
System.out.println(nums);  // [8, 5, 2, 1]

// Find max/min
int max = Collections.max(nums);
int min = Collections.min(nums);
```

---

## 2. TreeSet

Sorted set (no duplicates, maintains order).

### Basic Operations

```java
import java.util.TreeSet;

public class TreeSetDemo {
    public static void main(String[] args) {
        // Create TreeSet
        TreeSet<Integer> set = new TreeSet<>();
        
        // Add elements (automatically sorted)
        set.add(50);
        set.add(20);
        set.add(80);
        set.add(10);
        set.add(20);  // Duplicate - ignored
        
        // Print (sorted order)
        System.out.println(set);  // [10, 20, 50, 80]
        
        // First and last
        System.out.println("First: " + set.first());  // 10
        System.out.println("Last: " + set.last());    // 80
        
        // Remove element
        set.remove(20);
        
        // Check if exists
        boolean has = set.contains(50);
        
        // Size
        System.out.println("Size: " + set.size());
    }
}
```

### TreeSet Methods

```java
TreeSet<String> names = new TreeSet<>();
names.add("Charlie");
names.add("Alice");
names.add("Bob");

// Higher and Lower
String higher = names.higher("Alice");  // Bob
String lower = names.lower("Charlie");  // Bob

// Ceiling and Floor
String ceiling = names.ceiling("B");    // Bob
String floor = names.floor("D");        // Charlie

// Head and Tail sets
TreeSet<String> headSet = (TreeSet<String>) names.headSet("Charlie");
// Elements less than Charlie

TreeSet<String> tailSet = (TreeSet<String>) names.tailSet("Bob");
// Elements >= Bob

// Poll (remove and return)
String first = names.pollFirst();   // Removes Alice
String last = names.pollLast();     // Removes Charlie
```

### TreeSet with Custom Objects

```java
import java.util.*;

class Student implements Comparable<Student> {
    int id;
    String name;
    
    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
    
    public int compareTo(Student s) {
        return this.id - s.id;  // Sort by id
    }
    
    public String toString() {
        return id + ":" + name;
    }
}

TreeSet<Student> students = new TreeSet<>();
students.add(new Student(3, "Charlie"));
students.add(new Student(1, "Alice"));
students.add(new Student(2, "Bob"));

System.out.println(students);  // Sorted by id
```

---

## 3. HashMap

Key-value pairs (unordered, no duplicate keys).

### Basic Operations

```java
import java.util.HashMap;

public class HashMapDemo {
    public static void main(String[] args) {
        // Create HashMap
        HashMap<String, Integer> map = new HashMap<>();
        
        // Add key-value pairs
        map.put("Apple", 10);
        map.put("Banana", 20);
        map.put("Cherry", 15);
        
        // Get value by key
        int value = map.get("Apple");
        System.out.println(value);  // 10
        
        // Update value
        map.put("Apple", 25);  // Replaces 10 with 25
        
        // Remove key
        map.remove("Banana");
        
        // Check if key exists
        boolean hasKey = map.containsKey("Cherry");
        
        // Check if value exists
        boolean hasValue = map.containsValue(15);
        
        // Size
        System.out.println("Size: " + map.size());
    }
}
```

### Iterating HashMap

```java
HashMap<String, Integer> scores = new HashMap<>();
scores.put("Math", 85);
scores.put("Science", 90);
scores.put("English", 88);

// Method 1: Using keySet
for (String key : scores.keySet()) {
    System.out.println(key + " : " + scores.get(key));
}

// Method 2: Using entrySet (better performance)
for (Map.Entry<String, Integer> entry : scores.entrySet()) {
    System.out.println(entry.getKey() + " : " + entry.getValue());
}

// Method 3: Using values
for (Integer value : scores.values()) {
    System.out.println(value);
}
```

### HashMap Methods

```java
HashMap<Integer, String> map = new HashMap<>();
map.put(1, "One");
map.put(2, "Two");
map.put(3, "Three");

// Get or default
String val = map.getOrDefault(4, "Not Found");

// Put if absent (only if key doesn't exist)
map.putIfAbsent(4, "Four");

// Replace
map.replace(1, "ONE");

// Get all keys
Set<Integer> keys = map.keySet();

// Get all values
Collection<String> values = map.values();

// Clear all
map.clear();

// Check if empty
boolean empty = map.isEmpty();
```

---

## 4. Deque (Double-Ended Queue)

Can add/remove from both ends.

### Deque using ArrayDeque

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class DequeDemo {
    public static void main(String[] args) {
        Deque<Integer> deque = new ArrayDeque<>();
        
        // Add at front
        deque.addFirst(10);
        deque.addFirst(20);
        
        // Add at rear
        deque.addLast(30);
        deque.addLast(40);
        
        System.out.println(deque);  // [20, 10, 30, 40]
        
        // Remove from front
        int first = deque.removeFirst();
        System.out.println(first);  // 20
        
        // Remove from rear
        int last = deque.removeLast();
        System.out.println(last);   // 40
        
        // Peek (view without removing)
        int peekFirst = deque.peekFirst();
        int peekLast = deque.peekLast();
    }
}
```

### Deque as Stack

```java
Deque<String> stack = new ArrayDeque<>();

// Push (add to top)
stack.push("First");
stack.push("Second");
stack.push("Third");

// Pop (remove from top)
String top = stack.pop();
System.out.println(top);  // Third

// Peek (view top)
String peek = stack.peek();
System.out.println(peek); // Second
```

### Deque as Queue

```java
Deque<String> queue = new ArrayDeque<>();

// Offer (add to rear)
queue.offer("A");
queue.offer("B");
queue.offer("C");

// Poll (remove from front)
String front = queue.poll();
System.out.println(front);  // A

// Peek (view front)
String peek = queue.peek();
System.out.println(peek);   // B
```

---

## 5. JDBC (Java Database Connectivity)

JDBC connects Java applications to databases.

### JDBC Components Explained

#### 1. **DriverManager**
Manages database drivers and establishes connections.

```java
// Load driver (optional in modern JDBC)
Class.forName("com.mysql.cj.jdbc.Driver");

// Get connection
Connection conn = DriverManager.getConnection(url, username, password);
```

**What it does:**
- Loads the JDBC driver
- Establishes connection to database
- Returns Connection object

#### 2. **Connection**
Represents a connection to the database.

```java
String url = "jdbc:mysql://localhost:3306/mydb";
String user = "root";
String password = "password";

Connection conn = DriverManager.getConnection(url, user, password);
```

**What it does:**
- Creates Statement objects
- Manages transactions
- Provides database metadata
- Must be closed after use

#### 3. **Statement**
Executes SQL queries.

```java
Statement stmt = conn.createStatement();

// Execute query
ResultSet rs = stmt.executeQuery("SELECT * FROM students");

// Execute update
int rows = stmt.executeUpdate("INSERT INTO students VALUES (1, 'Alice')");
```

**What it does:**
- Executes static SQL queries
- Returns ResultSet for SELECT queries
- Returns affected row count for INSERT/UPDATE/DELETE

#### 4. **PreparedStatement**
Precompiled SQL statements (prevents SQL injection).

```java
String sql = "INSERT INTO students VALUES (?, ?)";
PreparedStatement pstmt = conn.prepareStatement(sql);

pstmt.setInt(1, 101);
pstmt.setString(2, "Alice");
pstmt.executeUpdate();
```

**What it does:**
- Precompiles SQL for better performance
- Prevents SQL injection with parameters
- Reusable with different parameter values

#### 5. **ResultSet**
Contains results from SELECT query.

```java
ResultSet rs = stmt.executeQuery("SELECT * FROM students");

while (rs.next()) {
    int id = rs.getInt("id");
    String name = rs.getString("name");
    System.out.println(id + " : " + name);
}
```

**What it does:**
- Holds query results
- Provides methods to retrieve data
- Cursor moves through rows with next()

#### 6. **SQLException**
Handles database errors.

```java
try {
    Connection conn = DriverManager.getConnection(url, user, password);
} catch (SQLException e) {
    System.out.println("Error: " + e.getMessage());
    e.printStackTrace();
}
```

**What it does:**
- Reports database access errors
- Provides error codes and messages
- Must be caught or declared

---

## 6. JDBC Setup and Connection

### Step-by-Step: Setting Up JDBC

**Step 1:** Download MySQL Connector JAR
- Download from: https://dev.mysql.com/downloads/connector/j/
- Add JAR to project classpath

**Step 2:** Create Database

```sql
CREATE DATABASE studentdb;
USE studentdb;

CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT
);
```

**Step 3:** Write Java Code

```java
import java.sql.*;

public class JDBCDemo {
    public static void main(String[] args) {
        // Database credentials
        String url = "jdbc:mysql://localhost:3306/studentdb";
        String user = "root";
        String password = "yourpassword";
        
        try {
            // 1. Load driver (optional in JDBC 4.0+)
            Class.forName("com.mysql.cj.jdbc.Driver");
            
            // 2. Create connection
            Connection conn = DriverManager.getConnection(url, user, password);
            System.out.println("Connected!");
            
            // 3. Create statement
            Statement stmt = conn.createStatement();
            
            // 4. Execute query
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");
            
            // 5. Process results
            while (rs.next()) {
                System.out.println(rs.getInt("id") + " " + rs.getString("name"));
            }
            
            // 6. Close connections
            rs.close();
            stmt.close();
            conn.close();
            
        } catch (ClassNotFoundException e) {
            System.out.println("Driver not found");
        } catch (SQLException e) {
            System.out.println("Connection failed");
            e.printStackTrace();
        }
    }
}
```

---

## 7. CRUD Operations using JDBC

CRUD = Create, Read, Update, Delete

### CREATE (Insert)

```java
public class InsertData {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/studentdb";
        String user = "root";
        String password = "yourpassword";
        
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            
            // Method 1: Using Statement
            Statement stmt = conn.createStatement();
            String sql = "INSERT INTO students VALUES (1, 'Alice', 20)";
            int rows = stmt.executeUpdate(sql);
            System.out.println(rows + " row inserted");
            
            // Method 2: Using PreparedStatement (recommended)
            String query = "INSERT INTO students VALUES (?, ?, ?)";
            PreparedStatement pstmt = conn.prepareStatement(query);
            
            pstmt.setInt(1, 2);
            pstmt.setString(2, "Bob");
            pstmt.setInt(3, 21);
            
            int result = pstmt.executeUpdate();
            System.out.println(result + " row inserted");
            
            pstmt.close();
            stmt.close();
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### READ (Select)

```java
public class ReadData {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/studentdb";
        String user = "root";
        String password = "yourpassword";
        
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            
            // Select all
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");
            
            System.out.println("ID\tName\tAge");
            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                int age = rs.getInt("age");
                
                System.out.println(id + "\t" + name + "\t" + age);
            }
            
            rs.close();
            
            // Select with condition
            String query = "SELECT * FROM students WHERE age > ?";
            PreparedStatement pstmt = conn.prepareStatement(query);
            pstmt.setInt(1, 20);
            
            ResultSet rs2 = pstmt.executeQuery();
            while (rs2.next()) {
                System.out.println(rs2.getString("name"));
            }
            
            rs2.close();
            pstmt.close();
            stmt.close();
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### UPDATE (Modify)

```java
public class UpdateData {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/studentdb";
        String user = "root";
        String password = "yourpassword";
        
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            
            // Update using PreparedStatement
            String query = "UPDATE students SET age = ? WHERE id = ?";
            PreparedStatement pstmt = conn.prepareStatement(query);
            
            pstmt.setInt(1, 22);  // New age
            pstmt.setInt(2, 1);   // Student id
            
            int rows = pstmt.executeUpdate();
            System.out.println(rows + " row updated");
            
            pstmt.close();
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### DELETE (Remove)

```java
public class DeleteData {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/studentdb";
        String user = "root";
        String password = "yourpassword";
        
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            
            // Delete using PreparedStatement
            String query = "DELETE FROM students WHERE id = ?";
            PreparedStatement pstmt = conn.prepareStatement(query);
            
            pstmt.setInt(1, 2);  // Student id to delete
            
            int rows = pstmt.executeUpdate();
            System.out.println(rows + " row deleted");
            
            pstmt.close();
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 8. Complete CRUD Application

```java
import java.sql.*;
import java.util.Scanner;

public class StudentManagement {
    static String url = "jdbc:mysql://localhost:3306/studentdb";
    static String user = "root";
    static String password = "yourpassword";
    
    // CREATE
    public static void addStudent(int id, String name, int age) {
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            String query = "INSERT INTO students VALUES (?, ?, ?)";
            PreparedStatement pstmt = conn.prepareStatement(query);
            pstmt.setInt(1, id);
            pstmt.setString(2, name);
            pstmt.setInt(3, age);
            pstmt.executeUpdate();
            System.out.println("Student added successfully");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    // READ
    public static void viewAllStudents() {
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");
            
            System.out.println("\nID\tName\tAge");
            System.out.println("-------------------");
            while (rs.next()) {
                System.out.println(rs.getInt("id") + "\t" + 
                                 rs.getString("name") + "\t" + 
                                 rs.getInt("age"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    // UPDATE
    public static void updateStudent(int id, int newAge) {
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            String query = "UPDATE students SET age = ? WHERE id = ?";
            PreparedStatement pstmt = conn.prepareStatement(query);
            pstmt.setInt(1, newAge);
            pstmt.setInt(2, id);
            int rows = pstmt.executeUpdate();
            if (rows > 0) {
                System.out.println("Student updated successfully");
            } else {
                System.out.println("Student not found");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    // DELETE
    public static void deleteStudent(int id) {
        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            String query = "DELETE FROM students WHERE id = ?";
            PreparedStatement pstmt = conn.prepareStatement(query);
            pstmt.setInt(1, id);
            int rows = pstmt.executeUpdate();
            if (rows > 0) {
                System.out.println("Student deleted successfully");
            } else {
                System.out.println("Student not found");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        while (true) {
            System.out.println("\n1. Add Student");
            System.out.println("2. View All Students");
            System.out.println("3. Update Student");
            System.out.println("4. Delete Student");
            System.out.println("5. Exit");
            System.out.print("Choice: ");
            
            int choice = sc.nextInt();
            
            switch (choice) {
                case 1:
                    System.out.print("Enter ID: ");
                    int id = sc.nextInt();
                    System.out.print("Enter Name: ");
                    sc.nextLine();
                    String name = sc.nextLine();
                    System.out.print("Enter Age: ");
                    int age = sc.nextInt();
                    addStudent(id, name, age);
                    break;
                    
                case 2:
                    viewAllStudents();
                    break;
                    
                case 3:
                    System.out.print("Enter Student ID: ");
                    int updateId = sc.nextInt();
                    System.out.print("Enter New Age: ");
                    int newAge = sc.nextInt();
                    updateStudent(updateId, newAge);
                    break;
                    
                case 4:
                    System.out.print("Enter Student ID: ");
                    int deleteId = sc.nextInt();
                    deleteStudent(deleteId);
                    break;
                    
                case 5:
                    System.out.println("Goodbye!");
                    sc.close();
                    System.exit(0);
                    
                default:
                    System.out.println("Invalid choice");
            }
        }
    }
}
```

---

## 9. Non-Conventional Devices

Java programs can run on various devices beyond computers.

### 1. **Mobile Devices (Android)**

```java
// Android uses Java/Kotlin
// Example: Simple Android Button Click
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        Button btn = findViewById(R.id.button);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this, 
                             "Button Clicked", 
                             Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

**Devices:** Smartphones, Tablets
**Examples:** WhatsApp, Instagram, Spotify apps

### 2. **Embedded Systems (IoT)**

```java
// Java ME (Micro Edition) for embedded devices
// Example: Temperature Sensor Reader
public class TemperatureSensor {
    public void readTemperature() {
        // Read from sensor
        double temp = getSensorData();
        
        if (temp > 30) {
            activateCooling();
        }
    }
}
```

**Devices:** Smart thermostats, Industrial sensors
**Examples:** Nest Thermostat, Smart home devices

### 3. **Smart Cards**

```java
// Java Card for smart cards
public class CreditCardApplet extends Applet {
    private short balance;
    
    public void debit(short amount) {
        if (balance >= amount) {
            balance -= amount;
        }
    }
}
```

**Devices:** Credit/Debit cards, SIM cards
**Examples:** Contactless payment cards

### 4. **Set-Top Boxes**

```java
// Java TV API
public class TVApplication {
    public void changeChannel(int channel) {
        tuner.setChannel(channel);
        display.show();
    }
}
```

**Devices:** Cable boxes, Streaming devices
**Examples:** Blu-ray players, Digital TV boxes

### 5. **Automotive Systems**

```java
// Example: Car Dashboard
public class Dashboard {
    public void updateSpeed(int speed) {
        if (speed > 120) {
            showSpeedWarning();
        }
        display.setSpeed(speed);
    }
}
```

**Devices:** Car infotainment systems
**Examples:** Tesla dashboard, BMW iDrive

### 6. **Wearables**

```java
// Smartwatch Application
public class FitnessTracker {
    public void trackSteps(int steps) {
        if (steps >= 10000) {
            sendNotification("Goal reached!");
        }
    }
}
```

**Devices:** Smartwatches, Fitness bands
**Examples:** Android Wear devices

---

## Practice Problems (LeetCode)

### ArrayList
1. **LeetCode #1 - Two Sum** (Using ArrayList)
2. **LeetCode #169 - Majority Element**
3. **LeetCode #283 - Move Zeroes**
4. **LeetCode #448 - Find All Numbers Disappeared**

### TreeSet
5. **LeetCode #349 - Intersection of Two Arrays**
6. **LeetCode #220 - Contains Duplicate III**
7. **LeetCode #1122 - Relative Sort Array**

### HashMap
8. **LeetCode #1 - Two Sum** (HashMap solution)
9. **LeetCode #242 - Valid Anagram**
10. **LeetCode #383 - Ransom Note**
11. **LeetCode #387 - First Unique Character**
12. **LeetCode #771 - Jewels and Stones**

### Deque
13. **LeetCode #232 - Implement Queue using Stacks**
14. **LeetCode #225 - Implement Stack using Queues**
15. **LeetCode #239 - Sliding Window Maximum**

### Database Design
16. **LeetCode #175 - Combine Two Tables** (SQL)
17. **LeetCode #176 - Second Highest Salary** (SQL)
18. **LeetCode #181 - Employees Earning More Than Managers** (SQL)

---

## Real-Life Applications

### 1. **Contact Manager (ArrayList)**

```java
import java.util.*;

class Contact {
    String name;
    String phone;
    
    Contact(String name, String phone) {
        this.name = name;
        this.phone = phone;
    }
}

class ContactManager {
    ArrayList<Contact> contacts = new ArrayList<>();
    
    void addContact(String name, String phone) {
        contacts.add(new Contact(name, phone));
    }
    
    void displayAll() {
        for (Contact c : contacts) {
            System.out.println(c.name + " : " + c.phone);
        }
    }
}

// Used in: Phone apps, CRM systems
```

### 2. **Leaderboard (TreeSet)**

```java
class Player implements Comparable<Player> {
    String name;
    int score;
    
    Player(String name, int score) {
        this.name = name;
        this.score = score;
    }
    
    public int compareTo(Player p) {
        return p.score - this.score;  // Descending order
    }
    
    public String toString() {
        return name + ": " + score;
    }
}

TreeSet<Player> leaderboard = new TreeSet<>();
leaderboard.add(new Player("Alice", 100));
leaderboard.add(new Player("Bob", 150));

// Used in: Gaming apps, Competition platforms
```

### 3. **Shopping Cart (HashMap)**

```java
HashMap<String, Integer> cart = new HashMap<>();

// Add items
cart.put("Apple", 5);
cart.put("Banana", 3);

// Update quantity
cart.put("Apple", cart.get("Apple") + 2);

// Calculate total items
int total = 0;
for (int quantity : cart.values()) {
    total += quantity;
}

// Used in: E-commerce, Online shopping
```

### 4. **Browser History (Deque)**

```java
Deque<String> history = new ArrayDeque<>();

void visit(String url) {
    history.addLast(url);
}

String back() {
    if (history.size() > 1) {
        history.removeLast();
    }
    return history.peekLast();
}

// Used in: Web browsers, Navigation systems
```

### 5. **Library System (JDBC)**

```java
class LibraryManager {
    void issueBook(int bookId, int studentId) {
        try (Connection conn = DriverManager.getConnection(url, user, pwd)) {
            String query = "INSERT INTO issued_books VALUES (?, ?, CURDATE())";
            PreparedStatement pstmt = conn.prepareStatement(query);
            pstmt.setInt(1, bookId);
            pstmt.setInt(2, studentId);
            pstmt.executeUpdate();
            System.out.println("Book issued");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

// Used in: Library management, Book tracking
```

### 6. **Attendance System (JDBC + ArrayList)**

```java
class AttendanceSystem {
    ArrayList<String> presentStudents = new ArrayList<>();
    
    void markAttendance(String name) {
        presentStudents.add(name);
    }
    
    void saveToDatabase() {
        try (Connection conn = DriverManager.getConnection(url, user, pwd)) {
            String query = "INSERT INTO attendance VALUES (?, CURDATE())";
            PreparedStatement pstmt = conn.prepareStatement(query);
            
            for (String student : presentStudents) {
                pstmt.setString(1, student);
                pstmt.executeUpdate();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

// Used in: Schools, Offices, Events
```

---

## Key Takeaways

- **ArrayList** - Dynamic array, allows duplicates, maintains insertion order
- **TreeSet** - Sorted set, no duplicates, O(log n) operations
- **HashMap** - Key-value pairs, O(1) average access time
- **Deque** - Double-ended queue, can act as stack or queue
- **JDBC** - Bridge between Java and databases
- **DriverManager** - Manages drivers and creates connections
- **Connection** - Represents database connection
- **Statement** - Executes static SQL
- **PreparedStatement** - Precompiled SQL, prevents SQL injection
- **ResultSet** - Holds query results
- Always close database resources (use try-with-resources)
- Use PreparedStatement to prevent SQL injection
- Java runs on non-conventional devices through Java ME, Java Card, Android

---

## Quick Reference

**ArrayList:** `ArrayList<Type> list = new ArrayList<>();`  
**Add:** `list.add(element);`  
**Get:** `list.get(index);`  
**Remove:** `list.remove(index);`  

**TreeSet:** `TreeSet<Type> set = new TreeSet<>();`  
**Add:** `set.add(element);`  
**First/Last:** `set.first();` `set.last();`  

**HashMap:** `HashMap<K, V> map = new HashMap<>();`  
**Put:** `map.put(key, value);`  
**Get:** `map.get(key);`  
**Iterate:** `for (Map.Entry<K,V> e : map.entrySet()) { }`  

**Deque:** `Deque<Type> deque = new ArrayDeque<>();`  
**Add front/rear:** `deque.addFirst();` `deque.addLast();`  
**Remove front/rear:** `deque.removeFirst();` `deque.removeLast();`  

**JDBC Connection:** `Connection conn = DriverManager.getConnection(url, user, pwd);`  
**Create Statement:** `Statement stmt = conn.createStatement();`  
**PreparedStatement:** `PreparedStatement pstmt = conn.prepareStatement(sql);`  
**Execute Query:** `ResultSet rs = stmt.executeQuery(sql);`  
**Execute Update:** `int rows = stmt.executeUpdate(sql);`  
**Close:** `conn.close(); stmt.close(); rs.close();`
