---
tags:
  - java
  - stream
---


Interfaces are ==Center focus== on how functional programming works in java

HOW TO:
1. Create a Interface
2. Tell compiler that please imagine that there will be 2 inputs
3. and you are supposed to give me an integer back
4. DID NOT tell compiler what that operation will be

>  - With the interface Programmer can describe general signature of function
> - but not describe the whole function itself
> - thus giving me flexibility
> - operation could be any operation that takes 2 integer input and return 1 integer as output
> - ex : addition, subtraction, multiplication, division 

---
## **Functional Interface**

```java
@FunctionalInterface
interface MathOperation {
    int operation(int a, int b);
}
```

- **`@FunctionalInterface`** annotation in Java is used to indicate that an interface is a **functional interface**
- The `@FunctionalInterface` annotation ensures that the interface follows the functional interface contract. If you mistakenly add another abstract method, the compiler will throw an error.
- Here, `MathOperation` is a functional interface because it has only **one** abstract method: `operation(int a, int b)`.
- The `@FunctionalInterface` annotation **is not mandatory**, but it helps catch errors at compile time if someone accidentally adds more abstract methods.

-  An **interface with only one abstract method**.
- It can have **default and static methods**.
- Used to create **concise implementations** using **lambdas**.
- Example: `Runnable`, `Callable`, `Comparator`, `Function`, etc.

#### **How to Use a Functional Interface?**

Since Java 8, functional interfaces can be implemented using **lambda expressions**, making the code more concise.
```java
public class FunctionalInterfaceExample {
    public static void main(String[] args) {
	// Using Lambda Expression
MathOperation addition = (a, b) -> a + b;
MathOperation multiplication = (a, b) -> a * b;

System.out.println("Sum: " + addition.operation(5,3));
System.out.print("Product:"+multiplication.operation(5, 3));
    }
}
```

- Instead of creating a separate class, we can implement the interface using **lambda expressions**.

- ## **Breakdown of Key Concepts**

|**Concept**|**Explanation**|**Example**|
|---|---|---|
|`@FunctionalInterface`|Ensures the interface has only **one** abstract method|`@FunctionalInterface interface MathOperation { int operation(int a, int b); }`|
|**Lambda Expression**|Provides an **inline** implementation of the interface|`(a, b) -> a + b`|
|**Method Call**|Calls the lambda function like a normal method|`addition.operation(10, 5)`|


Here :
```java
MathOperation addition = (a, b) -> a + b;
```

- When declaring `MathOperation` object as `addition`
- it has to satisfy  `(int a, int b)` this condition of what an operation is.
- So i have to define what an `addition` is : 
	- by saying  `(a, b)` is the input 
	- and `-> a + b` is the output.
- Then we can call the `Operation Method` that was defined in the interface
- by calling `addition.operation(5,3)`

### **How does `(a, b) -> a + b;` work?**

This is a **Lambda Expression**, which is a shorthand way of implementing an interface with a single method.
```java
MathOperation addition = (a, b) -> a + b;
```

- `(a, b)`: These are the **parameters** of the method `operation(int a, int b)`.
- `->`: This **arrow operator** separates parameters from the method body.
- `a + b`: This is the **method body** that returns the sum of `a` and `b`.
Without Lambda expression it can be written as:
```java
MathOperation addition = new MathOperation() {
    @Override
    public int operation(int a, int b) {
        return a + b;
    }
};
```

---
---
---

# **Rules of Java**
1. We can create "Objects" of a type
2. A type can be "class" or "Interface" or primitive data type
3. To Make "Function" type object :
	a) I need a type that explains "what" function is
	b) I need to use "this format" as my data type for the lambda

- Functional programming treats functions as **first-class citizens**, meaning functions can be **passed as arguments, stored in variables, and returned from other functions**. Java achieves this using **Functional Interfaces** and **Lambda Expressions**.

### **🔹Rule 1: We Can Create "Objects" of a Type**

**Object-Oriented Programming (OOP)** in Java is based on the idea that we create **objects** of a **class or interface**.  
💡 But in **Functional Programming**, we want to create objects that represent **functions**!
```java
class Car {
    void drive() {
        System.out.println("Driving...");
    }
}
Car myCar = new Car(); // Creating an object of Car
myCar.drive();  // Calling the method
```

### **🔹 Rule 2: A Type Can Be a Class, Interface, or Primitive Data Type**

Java allows us to define **types** in different ways:

1. **Class Type** → `class Car {}`
2. **Interface Type** → `interface Vehicle {}`
3. **Primitive Type** → `int, double, char`

💡 **But how do we define a function as a type?**  
👉 **Answer:** Use a [](.md#**Functional%20Interface**%20|%20Functional%20Interface)

### **🔹 Rule 3: Making "Function" Type Objects**

💡 In **functional programming**, functions can be stored as variables and passed around like objects.
#### **Step 1: I Need a Type That Explains "What" a Function Is**

- **Solution:** Use a **Functional Interface** to describe the function's signature (parameters & return type).
- In **`MathOperation`**, we define a function type that **takes two integers** and **returns an integer**.
```java
@FunctionalInterface
interface MathOperation {
    int operation(int a, int b);
}
```

#### **Step 2: Use "This Format" as My Data Type for the Lambda**

💡 Now that we have a type (`MathOperation`), we can store **functions as objects** using **lambda expressions**.

`MathOperation addition = (a, b) -> a + b;`

👉 **How is this functional programming?**  
✅ `addition` is now a **function stored as an object**!  
✅ We can **pass it as an argument, store it, and return it from methods**—just like data!

🔹 **Calling the function (lambda expression behaves like a method)**:
	`int result = addition.operation(10, 5);`

# **🔹 Summary: How This Relates to Functional Programming**

| **Java Rule**                                         |        **Functional Programming Concept**         |                                   **Example**                                   |
|:----------------------------------------------------- |:-------------------------------------------------:|:-------------------------------------------------------------------------------:|
| **1. We can create "Objects" of a type**              |        Functions can be stored as objects         |                   `MathOperation addition = (a, b) -> a + b;`                   |
| **2. A type can be a class, interface, or primitive** |   Functions need a type (functional interface)    | `@FunctionalInterface interface MathOperation { int operation(int a, int b); }` |
| **3. To Make "Function" Type Objects:**               | Use lambda expressions to create function objects |                               `(a, b) -> a + b;`                                |

---
---
# Another example:

```java
@FunctionalInterface
interface printThat {
    void print();
}

printThat pr = () -> System.out.println("wow");
pr.print(); // Output: wow
```

- Line 1 - 4 **ensures** that the interface contains **exactly one abstract method**.
- Line 6 is creating a object of that interface using lambda expression.
- The lambda expression `() -> System.out.println("wow");` is a shorthand for :
```java
public void print() {
    System.out.println("wow");
}
```

- Since `printThat` has **only one abstract method (`print()`)**, we don’t need to explicitly use `implements` or define a class.

### **Alternative Ways to Execute It**

### 🔹 **1. Using an Anonymous Class**

Instead of a lambda, we can use an **anonymous class**:
```java
printThat pr = new printThat() {
    @Override
    public void print() {
        System.out.println("wow");
    }
};
pr.print(); // Output: wow
```

- This is how we implemented interfaces **before Java 8**.  
- Lambdas **reduce this boilerplate code**.

### 🔹 **2. Using a Separate Class**

We can also create a **concrete class** that implements `printThat`:
```java
class PrintImplementation implements printThat {
    @Override
    public void print() {
        System.out.println("wow");
    }
}

public class Main {
    public static void main(String[] args) {
        printThat pr = new PrintImplementation();
        pr.print();  // Output: wow
    }
}
```

### 🔹 **3. Using a Method Reference**

Instead of using a lambda, we can use a **method reference**:
```java
class Printer {
    static void printMessage() {
        System.out.println("wow");
    }
}

printThat pr = Printer::printMessage;
pr.print(); // Output: wow
```

- `Printer::printMessage` is a **method reference** that points to `printMessage()`.  
- This is useful when an existing method already does the work.


### **Summary**

|**Method**|**Syntax**|**Notes**|
|---|---|---|
|**Lambda Expression** ✅|`printThat pr = () -> System.out.println("wow");`|Most concise, recommended|
|**Anonymous Class** 🔷|`new printThat() { public void print() { ... } };`|Works without lambdas, but verbose|
|**Concrete Class** 🔷|`class PrintImplementation implements printThat { ... }`|Traditional method, not flexible|
|**Method Reference** ✅|`printThat pr = Printer::printMessage;`|Clean when using existing methods|





#java 