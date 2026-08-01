#java #javaCollections 

## **Java Collection Framework (JCF)**

The **Java Collection Framework (JCF)** is a set of classes and interfaces in Java that provide data structures and algorithms to store, manipulate, and retrieve data efficiently. It is part of the `java.util` package and provides implementations of various commonly used data structures like **lists, sets, queues, and maps**.

## **What Does JCF (Java Collection framework) consist of ?**

- Collection Interfaces : ex List , Set, Queue (Root Interface)
- Implementation of Collection Interfaces

- Map Interfaces
- Implementation of Map Interfaces

- Deprecated Collections
- Synchronized Collections

- Algorithms
- Wrappers
---
### **🔶Collection V/S Arrays**

|                              | **Collection **                                                                                          | **Arrays**                                                                                                         |
| ---------------------------- | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Definition**               | A dynamic data structurethat is part of `java.util` package.                                             | A fixed-size data structure that holds elements of the same type.                                                  |
| **Size**                     | **Dynamic** – Can grow or shrink as needed.                                                              | **Fixed** – Size is defined at the time of creation and cannot be changed.                                         |
| **Performance**              | Generally slower than arrays due to overhead                                                             | Faster as it provides direct memory access.                                                                        |
| **Data Type Support**        | Supports **both objects and generic types** (e.g., `ArrayList<Integer>`).                                | Supports **both primitives and objects** (e.g., `int[]`, `String[]`).                                              |
| **Memory Usage**             | Higher due to additional functionalities (e.g., resizing, extra metadata).                               | Lower as it directly stores values in contiguous memory.                                                           |
| **Flexibility**              | Provides built-in methods (e.g., `add()`, `remove()`, `contains()`, `sort()`).                           | Requires manual implementation for operations like resizing, searching, and sorting.                               |
| **Performance in Iteration** | Iteration is slower due to additional overhead. Uses **Iterator** or **for-each loop**.                  | Faster iteration with **for-loop** or **enhanced for-loop**.                                                       |
| **Sorting**                  | Uses `Collections.sort()` for sorting.                                                                   | Uses `Arrays.sort()` for sorting.                                                                                  |
| **Thread Safety**            | Some classes like `Vector` and `Collections.synchronizedList()` are thread-safe.                         | Not thread-safe unless explicitly synchronized.                                                                    |
| **Implementation**           | Implemented using **abstract data structures** like linked lists, hash tables, trees, etc.               | Implemented as a **contiguous memory block** (array elements stored in adjacent memory locations).                 |
| **Usage Scenario**           | Preferred when **dynamic resizing, insertion, or deletion** is needed (e.g., `ArrayList`, `LinkedList`). | Preferred when **memory efficiency and fast access** are required (e.g., numerical computations, fixed data sets). |

---
### **🔶Collection Interface**

![ 700](Drawing%202025-03-05%2013.05.35.excalidraw%20)

In Java, the **`Iterable` interface** is the **root interface** for all collection classes. It is **on top of `Collection` and other interfaces** because it provides the fundamental **iteration capability** for any data structure.

Hierarchy: `Iterable` → `Collection` → `List`, `Set`, `Queue`

The `Collection` interface **extends** `Iterable`, meaning all its subclasses **must implement the `iterator()` method** to support iteration.

### **Collection Interface Methods**

The `Collection<E>` interface is the root interface in Java's Collection Framework, providing fundamental methods for handling groups of objects.

## **1️⃣ Basic Methods**

|Method|Return Type|Description|
|---|---|---|
|`size()`|`int`|Returns the number of elements in the collection.|
|`isEmpty()`|`boolean`|Returns `true` if the collection has no elements, otherwise `false`.|
|`contains(Object o)`|`boolean`|Checks if the specified element exists in the collection.|

---

## **2️⃣ Conversion Methods**

|Method|Return Type|Description|
|---|---|---|
|`toArray()`|`Object[]`|Converts the collection into an array of objects.|

---

## **3️⃣ Modification Methods**

|Method|Return Type|Description|
|---|---|---|
|`add(E e)`|`boolean`|Adds an element to the collection and returns `true` if added successfully.|
|`remove(Object o)`|`boolean`|Removes the specified element from the collection if it exists.|

---

## **4️⃣ Bulk Operations**

|Method|Return Type|Description|
|---|---|---|
|`containsAll(Collection<?> c)`|`boolean`|Checks if the collection contains all elements of the specified collection.|
|`addAll(Collection<? extends E> c)`|`boolean`|Adds all elements from the specified collection to the current collection.|
|`removeAll(Collection<?> c)`|`boolean`|Removes all elements present in the specified collection from the current collection.|
|`retainAll(Collection<?> c)`|`boolean`|Retains only the elements that exist in the specified collection, removing others.|

---

## **5️⃣ Utility Methods**

|Method|Return Type|Description|
|---|---|---|
|`clear()`|`void`|Removes all elements from the collection.|
|`equals(Object o)`|`boolean`|Compares the current collection with another object for equality.|
|`hashCode()`|`int`|Returns the hash code of the collection.|

---

## **💡 Notes**

✅ `Collection` is the base interface for all Java collections (`List`, `Set`, `Queue`).  
✅ `size()`, `isEmpty()`, and `contains()` are commonly used for checking collection state.  
✅ `add()`, `remove()`, `clear()`, and `addAll()` modify the collection.  
✅ `equals()` and `hashCode()` help in object comparison and hashing.