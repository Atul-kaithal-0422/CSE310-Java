# Java Installation and First Program Guide

## Installing Java on Windows

### Step 1: Download Java Development Kit (JDK)
Visit the official Oracle website or adopt OpenJDK and download the latest JDK version for Windows. Choose the Windows x64 Installer.

### Step 2: Run the Installer
Double-click the downloaded `.exe` file and follow the installation wizard. Note the installation path (typically `C:\Program Files\Java\jdk-<version>`).

### Step 3: Set Environment Variables
1. Right-click on "This PC" or "My Computer" and select "Properties"
2. Click on "Advanced system settings"
3. Click on "Environment Variables"
4. Under "System variables", click "New" and add:
   - Variable name: `JAVA_HOME`
   - Variable value: Your JDK installation path (e.g., `C:\Program Files\Java\jdk-21`)
5. Find the "Path" variable under "System variables", select it, and click "Edit"
6. Click "New" and add `%JAVA_HOME%\bin`
7. Click "OK" to save all changes

### Step 4: Verify Installation
Open Command Prompt and type:
```
java -version
javac -version
```
Both commands should display the Java version information.

## Installing Java on macOS

### Step 1: Download Java Development Kit (JDK)
Visit the official Oracle website or use Homebrew. For Homebrew installation, open Terminal and run:
```
brew install openjdk
```

For manual installation, download the macOS installer from Oracle's website.

### Step 2: Install JDK
If using the downloaded installer, double-click the `.dmg` file and follow the installation instructions.

If using Homebrew, the installation completes automatically.

### Step 3: Set Up Environment (for Homebrew installation)
For Homebrew installation, you need to create a symlink and set up your environment:

1. First, create a symlink (required for Homebrew OpenJDK):
```
sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
```

For Intel Macs, use:
```
sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
```

2. Create the `.zshrc` file if it doesn't exist:
```
touch ~/.zshrc
```

3. Add to your shell profile using this command:
```
echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc
```

For Intel Macs:
```
echo 'export PATH="/usr/local/opt/openjdk/bin:$PATH"' >> ~/.zshrc
```

4. Reload your profile:
```
source ~/.zshrc
```

Alternatively, you can simply close and reopen your Terminal window for the changes to take effect.

### Step 4: Verify Installation
Open Terminal and type:
```
java -version
javac -version
```
Both commands should display the Java version information.

## Writing and Running Your First Java Program

### Step 1: Create a Java File

#### On Windows:
1. Open Notepad or any text editor
2. Create a new file and save it as `HelloWorld.java`

#### On macOS:
1. Open TextEdit or any text editor
2. Create a new file and save it as `HelloWorld.java`

### Step 2: Write the Program
Type the following code into your file:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Important: The class name (`HelloWorld`) must match the filename (`HelloWorld.java`).

### Step 3: Compile the Program

#### On Windows:
1. Open Command Prompt
2. Navigate to the directory where you saved `HelloWorld.java` using the `cd` command
3. Compile the program:
```
javac HelloWorld.java
```

#### On macOS:
1. Open Terminal
2. Navigate to the directory where you saved `HelloWorld.java` using the `cd` command
3. Compile the program:
```
javac HelloWorld.java
```

If successful, this creates a `HelloWorld.class` file in the same directory.

### Step 4: Run the Program

#### On Windows (Command Prompt):
```
java HelloWorld
```

#### On macOS (Terminal):
```
java HelloWorld
```

### Expected Output
You should see:
```
Hello, World!
```

## Common Issues and Solutions

**Problem**: `javac` is not recognized as a command
- **Solution**: Check that your PATH environment variable includes the JDK bin directory. On Windows, restart Command Prompt after setting environment variables. On macOS, restart Terminal or run `source ~/.zshrc`

**Problem**: "Could not find or load main class"
- **Solution**: Ensure you're in the correct directory and the class name matches the filename exactly (case-sensitive)

**Problem**: Compilation errors
- **Solution**: Check for typos, ensure class name matches filename, and verify all syntax is correct

**Problem** (macOS): `source: no such file or directory: .zshrc`
- **Solution**: The file doesn't exist yet. Run `touch ~/.zshrc` to create it first

**Problem** (macOS): Permission denied when creating symlink
- **Solution**: Make sure you're using `sudo` before the `ln` command and enter your password when prompted

## Tips for Success

- Always save Java files with the `.java` extension
- The public class name must exactly match the filename
- Java is case-sensitive
- Make sure you're in the correct directory when compiling and running programs
- Use `dir` (Windows) or `ls` (macOS) to verify files are in the current directory
- On Windows, you may need to restart Command Prompt after setting environment variables
- On macOS, restart Terminal or run `source ~/.zshrc` after modifying shell configuration
