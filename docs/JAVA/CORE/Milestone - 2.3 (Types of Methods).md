#java #Interface 



> There are 9 Major Types of functions or Methods you can create in Java
> Depending on use case one can use them

## **Final Summary Table**

|      ==***Method Type***==       |             ==***Description***==             |                     ==***Use Case***==                     |
| :------------------------------: | :-------------------------------------------: | :--------------------------------------------------------: |
|       **Instance Methods**       |           Methods tied to an object           |             When instance variables are needed             |
|        **Static Methods**        |           Methods tied to the class           |           When instance variables are not needed           |
|       **Abstract Methods**       |         Methods in an abstract class          |              Enforce subclass implementation               |
|        **Final Methods**         |       Methods that cannot be overridden       |             Prevent modification in subclasses             |
|     **Synchronized Methods**     |   Prevent race conditions in multithreading   |          When multiple threads modify shared data          |
|        **Native Methods**        |           Calls external C/C++ code           |              For system-dependent operations               |
|       **Varargs Methods**        |    Accepts a variable number of arguments     |               When argument count is unknown               |
|       **Default Methods**        | Methods with implementation inside interfaces | When modifying an interface without breaking existing code |
| **Functional Interface Methods** |         Used with lambda expressions          |             When using functional programming              |

---

## **1️⃣ Instance Methods (Non-Static Methods)**

- **Belong to an object** (not the class).  
- Need an **object to call them**.

```java
class Calculator {
    int add(int a, int b) {  // Instance method
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();  // Create object
        System.out.println(calc.add(5, 3));  // Call method -> Output: 8
    }
}
```

- 👉 **When to use?** When the method **depends on instance variables**.

---
## **2️⃣ Static Methods**

- **Belong to the class** (not the object).  
- Called **without creating an object**.

```java
class MathUtil {
    static int square(int x) {  // Static method
        return x * x;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(MathUtil.square(5));  // Output: 25
    }
}
```

- 👉 **When to use?** When the method **does not depend on instance variables**.

---
## **3️⃣ Abstract Methods**

- **Declared in an abstract class** but **must be implemented in a subclass**.  
- **No method body** in the abstract class.

```java
abstract class Animal {
    abstract void makeSound();  // Abstract method (no body)
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Bark! Bark!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();
        dog.makeSound();  // Output: Bark! Bark!
    }
}
```

- 👉 **When to use?** When you **force subclasses to implement** a method.

---
## **4️⃣ Final Methods**

- **Cannot be overridden** by subclasses.  
- Useful when **you want to prevent modifications**.

```java
class Parent {
    final void show() {  // Final method
        System.out.println("This cannot be overridden");
    }
}

class Child extends Parent {
    // void show() { } ❌ ERROR: Cannot override final method
}
```

- 👉 **When to use?** When you want to **prevent modification of behavior**.

---
## **5️⃣ Synchronized Methods**

- Used in **multithreading** to **prevent race conditions**.  
- Ensures **only one thread accesses the method at a time**.

```java
class SharedResource {
    synchronized void display(String msg) {  // Synchronized method
        System.out.print("[ " + msg);
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
        System.out.println(" ]");
    }
}

class MyThread extends Thread {
    SharedResource obj;
    String message;

    MyThread(SharedResource obj, String msg) {
        this.obj = obj;
        this.message = msg;
    }

    public void run() {
        obj.display(message);
    }
}

public class Main {
    public static void main(String[] args) {
        SharedResource res = new SharedResource();
        MyThread t1 = new MyThread(res, "Hello");
        MyThread t2 = new MyThread(res, "World");
        t1.start();
        t2.start();
    }
}
```

- 👉 **When to use?** When multiple threads **modify shared data**.

---
## **6️⃣ Native Methods**

- Methods that **call code written in C/C++**.  
- Used for **interfacing with system-level operations**.

```java
class NativeExample {
    native void printMessage();  // Native method declaration

    static {
        System.loadLibrary("myNativeLib");  // Load native library
    }
}
```

- 👉 **When to use?** When calling **platform-dependent code** (e.g., C/C++ code in Java).

---
## **7️⃣ Varargs (Variable Arguments) Methods**

- Allows passing **multiple arguments of the same type**.  
- Internally treated as an **array**.

```java
class Utility {
    static void printNumbers(int... numbers) {  // Varargs method
        for (int num : numbers) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
}

public class Main {
    public static void main(String[] args) {
        Utility.printNumbers(1, 2, 3);  // Output: 1 2 3
        Utility.printNumbers(10, 20, 30, 40, 50);  // Output: 10 20 30 40 50
    }
}
```

- 👉 **When to use?** When **number of parameters is unknown**.

---
## **8️⃣ Default Methods (Java 8)**

- **Methods inside an interface** that have a **default implementation**.  
- Used to **add functionality to interfaces without breaking existing code**.

```java
interface Vehicle {
    default void start() {  // Default method
        System.out.println("Vehicle is starting...");
    }
}

class Car implements Vehicle {}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.start();  // Output: Vehicle is starting...
    }
}
```

- 👉 **When to use?** When adding new functionality to **existing interfaces**.

---
## **9️⃣ Functional Interface Methods (Java 8)**

- Used in **lambda expressions**.  
- Functional interfaces have **only one abstract method**.

```java
@FunctionalInterface
interface Greeting {
    void sayHello();  // Functional interface method
}

public class Main {
    public static void main(String[] args) {
        Greeting greet = () -> System.out.println("Hello, world!");
        greet.sayHello();  // Output: Hello, world!
    }
}
```

- 👉 **When to use?** When working with **functional programming & lambda expressions**.






