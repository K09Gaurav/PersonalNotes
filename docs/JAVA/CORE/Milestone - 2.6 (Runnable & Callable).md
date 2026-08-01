#java #thread 



### **Runnable vs Callable in Java**

Both `Runnable` and `Callable` are functional interfaces used in Java to represent tasks that can be executed by a thread. However, they have key differences in their implementation and return values.

| Feature                | Runnable                               | Callable                                                |
| ---------------------- | -------------------------------------- | ------------------------------------------------------- |
| **Method**             | `run()`                                | `call()`                                                |
| **Return Type**        | `void` (no return)                     | `V` (generic return type)                               |
| **Exception Handling** | Cannot throw checked exceptions        | Can throw checked exceptions                            |
| **Usage**              | Simple tasks, often used with `Thread` | Tasks that return a result, used with `ExecutorService` |


---

# **🔹 Runnable Interface** (No Return Value, No Exception)

- **Functional Interface** with a single `run()` method.
- **Does not return a result** (`void` return type).
- **Cannot throw checked exceptions**.
- Used in multithreading when we just want to execute a task without needing a result.

### **Syntax:**

```java
@FunctionalInterface
public interface Runnable {
    void run(); // No return value
}
```

### **Example using Lambda Expression:**
```java
public class Main {
    public static void main(String[] args) {
        Runnable task = () -> System.out.println("Task is running!");
        Thread thread = new Thread(task);
        thread.start();
    }
}
```

### **Key Points:**

✅ Simple and lightweight for tasks that don't return values.  
✅ Commonly used in `Thread` class for multithreading.  
✅ Cannot throw checked exceptions.

---
---
# **🔹 Callable Interface** (Has Return Value, Can Throw Exception)

- **Functional Interface** with a single `call()` method.
- **Returns a result** (`Generics` used for return type).
- **Can throw checked exceptions**.
- Used when a thread needs to return a result after execution.

### **Syntax:**

```java
@FunctionalInterface
public interface Callable<V> {
    V call() throws Exception; // Returns a value of type V
}
```

### **Example using Lambda Expression:**
```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class Main {
    public static void main(String[] args) throws Exception {
        Callable<Integer> task = () -> {
            Thread.sleep(1000);
            return 10 * 2;
        };

        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<Integer> result = executor.submit(task);
        
        System.out.println("Processing...");
        System.out.println("Result: " + result.get()); // Waits and gets the result

        executor.shutdown();
    }
}

OUTPUT: Processing...
		Result: 20

```

### **Key Points:**

✅ Useful for tasks that return a result.  
✅ Supports **checked exceptions** (unlike `Runnable`).  
✅ Works with `ExecutorService` and `Future` to retrieve the result asynchronously.

#java 