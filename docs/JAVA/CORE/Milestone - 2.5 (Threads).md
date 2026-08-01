#java #thread


### **1️⃣ What is a Thread?**

- A **thread** is the smallest unit of execution within a process.
- Java supports **multithreading**, meaning multiple tasks can run simultaneously.
- Threads **share memory** within the same process but execute independently.
---
### **2️⃣ Why Use Threads?**

✅ Perform multiple tasks at the same time (e.g., UI updates, background tasks).  
✅ Improve program efficiency by utilizing CPU cores effectively.  
✅ Keep applications responsive (e.g., downloading while showing progress).

---
### **3️⃣ Creating a Thread in Java**

#### 🔹 **Method 1: Extending `Thread` Class**  
1️⃣ Create a class that extends `Thread`.  
2️⃣ Override the `run()` method.  
3️⃣ Start the thread using `start()`.

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running...");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread(); // Create thread
        t1.start(); // Start execution
    }
}
```

>  We can call the `run()` method but it will not run the code in a separate thread.
>  We have to use `start()` method 
>  When called `start()` Java will branch off this brand new thread and start running this `run()` method.


- **Purpose of that is to run two different threads sat same time**
```java
	MyThread t1 = new MyThread(); // Create thread
	MyThread t2 = new MyThread();
	
	t1.start(); // Start execution
	t2.start();
```


##### 🔹 **We can Use multiple threads at a same time by just using a for loop**

```java
for (int i = 0; i < 5; i++) {
	Ops o1 = new Ops();
	o1.start();
}
```

- By this 5 different threads will be created at the same time
- And all 5 of them will be running at the same time.

##### 🔹 **We can Assign a number to the threads sand we can look which thread is doing the current task:**

- To do that we have to create a new public constructor
- That takes a parameter of int that will be the thread number

```java
private int threadnumber;
public Ops (int threadnumber){
	this.threadnumber = threadnumber;
}
```
- Now we can use/ Print the Thread Number if required.


---
---
#### 🔹 **Method 2: Implementing `Runnable` Interface**
1️⃣ Create a class that implements `Runnable`.  
2️⃣ Define the `run()` method.  
3️⃣ Pass an instance of `Runnable` to `Thread`.

```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Runnable Thread is running...");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyTask()); // Create thread
        t1.start(); // Start execution
    }
}
```

✅ **Why Use `Runnable` Over `Thread`?**

- More **flexible** (Java doesn’t support multiple inheritance, so you can still extend another class).
- Allows **sharing the same task** across multiple threads.

- If you extend thread you cannot extend any other class and you are stuck
- since Java doesn’t support multiple inheritance
- but java doesn't limit no of interface to implement. 

---

### **4️⃣ Thread Lifecycle**

A thread in Java goes through the following states:

1️⃣ **New** → Created but not started (`Thread t = new Thread();`).  
2️⃣ **Runnable** → Ready to run (`t.start();`).  
3️⃣ **Running** → Actively executing `run()`.  
4️⃣ **Blocked/Waiting** → Paused (e.g., waiting for a resource).  
5️⃣ **Terminated** → Execution finished or stopped.

---

### **5️⃣ Controlling Threads**

🔹 **`sleep(ms)`** → Pause thread for `ms` milliseconds.
	`Thread.sleep(1000); // 1-second pause`

🔹 **`join()`** → Wait for a thread to finish before continuing.
	`t1.join(); // Ensures t1 completes before moving ahead`

🔹 **`isAlive()`** → Check if a thread is still running.
	`if (t1.isAlive()) { System.out.println("Thread is running"); }`

---
### **6️⃣ Thread Pooling (`ExecutorService`)**

Instead of creating new threads manually, use **`ExecutorService`** to manage them.

```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        executor.submit(() -> System.out.println("Task 1 running"));
        executor.submit(() -> System.out.println("Task 2 running"));
        executor.shutdown();
    }
}
```

- `ExecutorService` is a high-level **thread management framework** in Java 
- used to **efficiently manage and control threads**. 
- Instead of creating new threads manually, it provides a **thread pool** that reuses existing threads, reducing overhead.

#### **✅ Why Use `ExecutorService` Instead of `new Thread()`?**

|Feature|`new Thread()`|`ExecutorService`|
|---|---|---|
|**Thread Reuse**|❌ Creates a new thread every time|✅ Reuses existing threads|
|**Performance**|❌ Higher memory and CPU overhead|✅ Optimized resource usage|
|**Thread Control**|❌ Hard to manage multiple threads|✅ Handles multiple tasks efficiently|
|**Scalability**|❌ Not suitable for large tasks|✅ Ideal for high-performance applications|

#### **✅ Creating a Thread Pool Using `ExecutorService`**

## **🔹 Summary: Best Thread Pool for Different Use Cases**

|Use Case|Best `ExecutorService`|
|---|---|
|**Fixed number of tasks**|`newFixedThreadPool(n)`|
|**Many short tasks**|`newCachedThreadPool()`|
|**One task at a time**|`newSingleThreadExecutor()`|
|**Scheduled tasks**|`newScheduledThreadPool(n)`|

### **1️⃣ Fixed Thread Pool**

Creates a **fixed number** of threads that execute tasks.
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2); // 2 threads

        Runnable task1 = () -> System.out.println("Task 1 running in: " + Thread.currentThread().getName());
        Runnable task2 = () -> System.out.println("Task 2 running in: " + Thread.currentThread().getName());
        Runnable task3 = () -> System.out.println("Task 3 running in: " + Thread.currentThread().getName());

        executor.submit(task1);
        executor.submit(task2);
        executor.submit(task3);

        executor.shutdown(); // Must call shutdown to stop accepting new tasks
    }
}
```

✅ **Explanation:**

- `Executors.newFixedThreadPool(2)` → Creates **2 reusable threads**.
- **Tasks share the same threads**, reducing overhead.
- **`shutdown()`** → Prevents new tasks but allows existing ones to finish.


### **2️⃣ Cached Thread Pool (Unlimited Threads)**

✅ Creates new threads **as needed** but reuses idle ones.

	`ExecutorService executor = Executors.newCachedThreadPool();`

- **Ideal for** short-lived tasks with unpredictable workloads.
- Threads are **reused** if they become available.

### **3️⃣ Single-Threaded Executor (Sequential Execution)**

✅ Ensures **one thread at a time** (FIFO order).

	`ExecutorService executor = Executors.newSingleThreadExecutor();`

- **Ideal for** tasks that must run in a strict **order**.


### **4️⃣ Scheduled Thread Pool (Delayed & Repeated Execution)**

✅ Used for **delayed** or **periodic tasks**.

```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) {
        ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);

        Runnable task = () -> System.out.println("Task executed at: " + System.currentTimeMillis());

        scheduler.scheduleAtFixedRate(task, 1, 3, TimeUnit.SECONDS); // Runs every 3 sec after 1 sec delay
    }
}
```

- `scheduleAtFixedRate(task, 1, 3, TimeUnit.SECONDS)` → Starts **after 1 sec**, then runs **every 3 sec**.

### **5️⃣ Shutting Down `ExecutorService`**

🚨 **Always shut down the executor to release resources.**

	`executor.shutdown(); // Initiates shutdown (no new tasks)`
	`executor.shutdownNow(); // Forces shutdown (interrupts running tasks)`

---
---

##  Best Approach to Thread !?

**💡 Summary of Thread Creation Methods**

|Method|Code Length|Efficiency|Best Use Case|
|---|---|---|---|
|`Thread` class|❌ Long|❌ Low|Not recommended|
|`Runnable`|✅ Short|🆗 Medium|Simple cases|
|`Lambda with Thread`|✅✅ Very Short|🆗 Medium|Quick execution|
|`ExecutorService + Lambda`|✅✅ Very Short|✅✅ High|Best for real-world apps|

### **🔹 Creating a Thread Using Lambda (Best Modern Approach)**

Using **lambda expressions** makes code cleaner and avoids unnecessary class definitions. Since `Runnable` is a **functional interface** (having only one abstract method), we can use **lambda expressions** to create a thread efficiently.

```java
public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> { System.out.println("Thread running via Lambda!"); } );
        t1.start();
    }
}
```
🔹 **Explanation:**

- `Runnable` has a single method `run()`, so we use **lambda**: `() -> System.out.println("Thread running...")`
- No need to create a separate class for `Runnable`.


### **✅  Using Lambda with `ExecutorService` (Best Practice)**

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);

        executor.submit(() -> System.out.println("Task 1 running in: " + Thread.currentThread().getName()));
        executor.submit(() -> System.out.println("Task 2 running in: " + Thread.currentThread().getName()));

        executor.shutdown();
    }
}
```

🔹 **Why is this the Best Approach?**  
✔ **Short & Clean** – No need for extra classes.  
✔ **Better Performance** – Uses a **thread pool** for efficient execution.  
✔ **Scalable** – Ideal for handling multiple tasks in parallel.


### **💡 Summary of Thread Creation Methods**

|Method|Code Length|Efficiency|Best Use Case|
|---|---|---|---|
|`Thread` class|❌ Long|❌ Low|Not recommended|
|`Runnable`|✅ Short|🆗 Medium|Simple cases|
|`Lambda with Thread`|✅✅ Very Short|🆗 Medium|Quick execution|
|`ExecutorService + Lambda`|✅✅ Very Short|✅✅ High|Best for real-world apps|





