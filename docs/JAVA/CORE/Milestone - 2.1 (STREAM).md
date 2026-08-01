#java #stream

The **Stream API** in Java (introduced in **Java 8**) allows for functional-style operations on collections, arrays, and data structures. It provides a clean and **efficient way** to process data without modifying the original collection.

---
## **🔹 What is a Stream?**

- A **Stream** is a sequence of elements that supports **functional operations** like filtering, mapping, and reducing.
- It does **not store data** but processes it **on demand**.
- **Streams do not modify the original data;** they generate new results.

---
## **🔹 Stream API Operations**

### **1️⃣ Creating a Stream**

Streams can be created from arrays, lists, or other data sources:
```java
int[] numbers = {1, 2, 3, 4, 5, 6};
Arrays.stream(numbers); // Creates a stream from an array
```
### **2️⃣ Intermediate Operations** (Transform Data)

These operations return a **new stream** and are applied **one after another**:

| **Method**               | **Description**                         | **Example**                  |
| ------------------------ | --------------------------------------- | ---------------------------- |
| `.filter(Predicate<T>)`  | Keeps elements that satisfy a condition | `filter(n -> n % 2 == 0)`    |
| `.map(Function<T, R>)`   | Transforms elements                     | `map(n -> n * 2)`            |
| `.peek(Consumer<T>)`     | Debugging (prints intermediate values)  | `peek(System.out: :println)` |
| `.sorted(Comparator<T>)` | Sorts elements                          | `sorted()`                   |

Example: Filtering Even Numbers & Doubling Values
```java
int[] even = Arrays.stream(numbers)
        .filter(n -> n % 2 == 0) // Keep even numbers
        .map(n -> n * 2)         // Double them
        .toArray();              // Convert back to array
```

### **3️⃣ Terminal Operations** (End the Stream)

These operations **consume the stream** and return a result:

|**Method**|**Description**|**Example**|
|---|---|---|
|`.toArray()`|Converts stream to an array|`toArray()`|
|`.collect(Collectors.toList())`|Converts stream to a List|`collect(Collectors.toList())`|
|`.forEach(Consumer<T>)`|Iterates over each element|`forEach(System.out::println)`|
|`.count()`|Counts elements in the stream|`count()`|

 **Example: Printing the Final Array**
```java
Arrays.stream(even).forEach(System.out::println);
```

## **🔹 Benefits of Stream API**

✅ **Concise & Readable** – Reduces boilerplate loops  
✅ **Functional Programming** – Uses **Lambda Expressions**  
✅ **Parallel Processing** – Improves performance on large datasets  
✅ **Immutability** – Does not modify the original collection







#java