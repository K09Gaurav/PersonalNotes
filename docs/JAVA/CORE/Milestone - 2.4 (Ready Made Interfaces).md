---
tags:
  - java
  - interface
---

### **Ready-Made Functional Interfaces in Java (Java 8+) 🚀**

> Java provides **predefined functional interfaces** inside the `java.util.function` package. 
> These interfaces help in functional programming and **eliminate the need for defining custom interfaces**.
---
# **📌 Summary Table of Ready-Made Functional Interfaces**

| **Interface**                                                                                                                     | **Inputs** | **Returns** | **Use Case**                     |
| --------------------------------------------------------------------------------------------------------------------------------- | ---------- | ----------- | -------------------------------- |
| [](.md#**1️⃣`Function<T,%20R>`%20→%20Takes%20Input,%20Returns%20Output**%20%5C|%20Function<T,%20R>)               | 1          | 1           | Data transformation              |
| [](.md#**2️⃣%20`Consumer<T>`%20→%20Takes%20Input,%20Returns%20Nothing**%20%5C|%20Consumer<T>)                   | 1          | None        | Performing actions               |
| [](.md#**3️⃣%20`Supplier<T>`%20→%20Takes%20Nothing,%20Returns%20Output**%20%5C|%20Supplier<T>)                  | None       | 1           | Generating values                |
| [](.md#**4️⃣%20`Predicate<T>`%20→%20Takes%20Input,%20Returns%20Boolean**%20%5C|%20Predicate<T>)                 | 1          | Boolean     | Filtering data                   |
| [](.md#**5️⃣%20`BiFunction<T,%20U,%20R>`%20→%20Takes%202%20Inputs,%20Returns%20Output**%20%5C|%20BiFunction<T,%20U,%20R>) | 2          | 1           | Processing two inputs            |
| [](.md#**6️⃣%20`BiConsumer<T,%20U>`%20→%20Takes%202%20Inputs,%20Returns%20Nothing**%20%5C|%20BiConsumer<T,%20U>)      | 2          | None        | Performing actions on two inputs |
| [](.md#**7️⃣%20`BiPredicate<T,%20U>`%20→%20Takes%202%20Inputs,%20Returns%20Boolean**%20%5C|%20BiPredicate<T,%20U>)    | 2          | Boolean     | Filtering two inputs             |
| [](.md#**8️⃣%20`IntFunction<R>`%20→%20Takes%20`int`,%20Returns%20Output**%20%5C|%20IntFunction<R>)              | `int`      | 1           | Optimized data transformation    |
| [](.md#**9️⃣%20`IntConsumer`%20→%20Takes%20`int`,%20Returns%20Nothing**%20%5C|%20IntConsumer)                   | `int`      | None        | Optimized action on int          |


> - These **predefined functional interfaces** save time and reduce code complexity.
> - Use **`Function<T, R>`** for **data transformation**.
> - Use **`Consumer<T>`** for **side effects (logging, printing, saving)**.
> - Use **`Predicate<T>`** for **boolean conditions**.
> - Use **primitive versions (`IntFunction`, `IntConsumer`) for performance**.

---
## **1️⃣`Function<T, R>` → Takes Input, Returns Output**

```java
Function<Integer, Integer> square = x -> x * x;
int result = square.apply(5);
```

- **`Function<T, R>`** is a **functional interface** from `java.util.function` package.
- It represents a function that **takes ==one input== (`T`) and ==returns an output== (`R`)**.
- Used for **data transformation** (e.g., converting one type to another).
####  **Breaking Down the Code**
|        **Component**         |                                                         **Explanation**                                                         |
| :--------------------------: | :-----------------------------------------------------------------------------------------------------------------------------: |
| `Function<Integer, Integer>` | This is the **`type`** of square. It means the function **takes an `Integer` as input** and **returns an `Integer` as output**. |
|           `square`           |                                   This is the **variable name** where the function is stored.                                   |
|         `x -> x * x`         |      This is the **lambda expression**, defining how the function works. It takes `x`, squares it, and returns the result.      |
🔹 **Use Case:** When **transforming** data from one type to another.

#### **For Custom Function Edit This:**
```java
@FunctionalInterface
interface MyFunction<T, R> {
    R apply(T t);
}
```

In Java, `T`, `U`, and `R` are **generic type parameters** used to define flexible and reusable functional interfaces.

#### **🔹 What do `T`, `U`, and `R` represent?**

| **Placeholder** | **Meaning**                       |
| --------------- | --------------------------------- |
| `T`             | The first input type              |
| `U`             | The second input type (if needed) |
| `R`             | The return type                   |

These **generic placeholders** allow a functional interface to work with **any data type**, making it **type-safe and reusable**.

---
## **2️⃣ `Consumer<T>` → Takes Input, Returns Nothing**

✔ **T** → Input type  
✔ **Performs an action but does not return a value.**

 **Example: Printing a message**
```java
import java.util.function.Consumer;

public class Main {
    public static void main(String[] args) {
        Consumer<String> printMessage = message -> System.out.println("Hello, " + message);
        printMessage.accept("Alice");  // Output: Hello, Alice
    }
}
```

🔹 **When to Use?**

- When we want to **perform an action** but don’t need a return value.
- Example: **Logging, saving to a database, sending emails.**

#### **For Custom Consumer edit this :**

```java
@FunctionalInterface
interface MyBiConsumer<T, U> {
    void accept(T t, U u);
}
```
---
## **3️⃣ `Supplier<T>` → Takes Nothing, Returns Output**

✔ **T** → Return type  
✔ **Generates a value** without taking any arguments.

 **Example: Generating a random number**
```java
import java.util.function.Supplier;
import java.util.Random;

public class Main {
    public static void main(String[] args) {
        Supplier<Integer> getRandomNumber = () -> new Random().nextInt(100);
        System.out.println(getRandomNumber.get());  // Output: Random number (0-99)
    }
}
```

🔹 **When to Use?**

- When we need **lazy evaluation** (the value is computed only when needed).
- Example: Fetching system time, **UUID generation, caching values.**

##### **For Custom no of outputs from supplier edit like this :**

```java
@FunctionalInterface
interface TriSupplier<T, U, V> {
    T getFirst();
    U getSecond();
    V getThird();
}

public class Main {
    public static void main(String[] args) {
        TriSupplier<String, Integer, String> personDetails = new TriSupplier<>() {
            @Override
            public String getFirst() {
                return "Alice";
            }

            @Override
            public Integer getSecond() {
                return 25;
            }

            @Override
            public String getThird() {
                return "New York";
            }
        };

        System.out.println(personDetails.getFirst());  // Output: Alice
        System.out.println(personDetails.getSecond()); // Output: 25
        System.out.println(personDetails.getThird());  // Output: New York
    }
}
```
---
## **4️⃣ `Predicate<T>` → Takes Input, Returns Boolean**

✔ **T** → Input type  
✔ **Returns `true` or `false`** based on a condition.

 **Example: Checking if a number is even**
```java
import java.util.function.Predicate;

public class Main {
    public static void main(String[] args) {
        Predicate<Integer> isEven = num -> num % 2 == 0;
        System.out.println(isEven.test(8));  // Output: true
        System.out.println(isEven.test(7));  // Output: false
    }
}
```

🔹 **When to Use?**

- When filtering data (e.g., in **Streams, Collections**).
- Example: **Checking login conditions, filtering even numbers from a list.**



### **🔹Custom Predicate with Different Parameters**

##### 🔹1 Parameter (Similar to Java's `Predicate<T>`).

```java
@FunctionalInterface
interface MyPredicate<T> {
    boolean test(T t);
}

public class Main {
    public static void main(String[] args) {
        MyPredicate<Integer> isEven = n -> n % 2 == 0;
        
        System.out.println(isEven.test(10)); // true
        System.out.println(isEven.test(11)); // false
    }
}
```

##### 🔹1+ Parameter (Similar to Java's `BiPredicate<T, U>`).

```java
@FunctionalInterface
interface MyBiPredicate<T, U> {
    boolean test(T t, U u);
}
public class Main {
    public static void main(String[] args) {
        MyBiPredicate<Integer, Integer> isSumEven = (a, b) -> (a + b) % 2 == 0;
        
        System.out.println(isSumEven.test(10, 20)); // true
        System.out.println(isSumEven.test(10, 21)); // false
    }
}
```


---
---
# **🔹 Extended Functional Interfaces (More Than One Argument)**

Java also provides interfaces that work with **two inputs** or **primitive types** to optimize performance.

## **5️⃣ `BiFunction<T, U, R>` → Takes 2 Inputs, Returns Output**

✔ **T, U** → Two input types  
✔ **R** → Return type

#### **Example: Adding two numbers**
```java
import java.util.function.BiFunction;

public class Main {
    public static void main(String[] args) {
        BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
        System.out.println(add.apply(5, 3));  // Output: 8
    }
}
```
🔹 **When to Use?**

- When processing two inputs together (e.g., merging values).
- Example: **Calculating salary (base salary + bonus).**

---
## **6️⃣ `BiConsumer<T, U>` → Takes 2 Inputs, Returns Nothing**

✔ **T, U** → Two input types  
✔ **Performs an action without returning anything.**

#### **Example: Printing a name with age**
```java
import java.util.function.BiConsumer;

public class Main {
    public static void main(String[] args) {
        BiConsumer<String, Integer> printInfo = (name, age) ->
                System.out.println(name + " is " + age + " years old");
        printInfo.accept("Alice", 25);  // Output: Alice is 25 years old
    }
}
```

🔹 **When to Use?**

- When performing operations on two values **without returning anything**.
- Example: **Logging username and action, saving key-value pairs.**
---
## **7️⃣ `BiPredicate<T, U>` → Takes 2 Inputs, Returns Boolean**

✔ **T, U** → Two input types  
✔ **Returns `true` or `false` based on a condition.**

#### **Example: Checking if a string starts with a given character**
```java
import java.util.function.BiPredicate;

public class Main {
    public static void main(String[] args) {
        BiPredicate<String, String> startsWith = (word, prefix) -> word.startsWith(prefix);
        System.out.println(startsWith.test("Java", "J"));  // Output: true
    }
}
```

🔹 **When to Use?**

- When filtering **two inputs** together.
- Example: **Checking user permissions, validating credentials.**


## **8️⃣: Extending `Predicate<T>` for Additional Features**

If you want to **extend Java’s `Predicate<T>`** (for chaining multiple conditions), you can **add extra methods**.

```java
@FunctionalInterface
interface AdvancedPredicate<T> extends Predicate<T> {
    default AdvancedPredicate<T> xor(Predicate<T> other) {
        return t -> this.test(t) ^ other.test(t);
    }
}
public class Main {
    public static void main(String[] args) {
        AdvancedPredicate<Integer> isEven = n -> n % 2 == 0;
        AdvancedPredicate<Integer> isGreaterThan10 = n -> n > 10;

        System.out.println(isEven.xor(isGreaterThan10).test(12)); // false
        System.out.println(isEven.xor(isGreaterThan10).test(9));  // true
    }
}
```

---
---
# **🔹 Optimized Primitive Functional Interfaces**

Java provides **primitive versions** of Function, Consumer, and Predicate to avoid **autoboxing overhead** (improving performance).

### **8️⃣ `IntFunction<R>` → Takes `int`, Returns Output**

```java
import java.util.function.IntFunction;

public class Main {
    public static void main(String[] args) {
        IntFunction<String> intToString = num -> "Number: " + num;
        System.out.println(intToString.apply(10));  // Output: Number: 10
    }
}
```

### **9️⃣ `IntConsumer` → Takes `int`, Returns Nothing**

```java
import java.util.function.IntConsumer;

public class Main {
    public static void main(String[] args) {
        IntConsumer printDouble = num -> System.out.println(num * 2);
        printDouble.accept(10);  // Output: 20
    }
}
```






#java