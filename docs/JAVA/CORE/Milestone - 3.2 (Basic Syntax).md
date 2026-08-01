#java #javaCollections 

## **1. List (Ordered, allows duplicates)**

A `List` is an ordered collection that allows duplicate elements.

### **Implementation Classes:** `ArrayList`, `LinkedList`, `Vector`

### **Commonly Used Methods:**

|Method|Description|
|---|---|
|`add(E e)`|Adds an element to the list|
|`add(int index, E e)`|Adds an element at a specific index|
|`get(int index)`|Retrieves element at given index|
|`set(int index, E e)`|Replaces element at given index|
|`remove(int index)`|Removes element at index|
|`remove(Object o)`|Removes first occurrence of the element|
|`contains(Object o)`|Returns `true` if element exists|
|`size()`|Returns the number of elements|
|`isEmpty()`|Returns `true` if list is empty|
|`indexOf(Object o)`|Returns first index of element, or -1 if not found|
|`clear()`|Removes all elements|
|`sort(Comparator c)`|Sorts the list using a comparator|

### **Example:**
```java
import java.util.*;

public class ListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(); // Can use LinkedList, Vector

        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        list.add(1, "Mango"); // Insert at index 1

        System.out.println(list.get(2)); // Cherry
        list.set(2, "Grapes"); // Replace Cherry with Grapes

        list.remove("Mango");
        System.out.println(list.contains("Apple")); // true

        Collections.sort(list); // Sort list
        System.out.println(list); // [Apple, Banana, Grapes]

		// Printing using for-each loop
        System.out.println("List elements:");
        for (String item : list) {
            System.out.println(item);
        }

        list.clear(); // Remove all elements
    }
}
```

---
## **2. Set (Unordered, unique elements)**

A `Set` does not allow duplicate elements.

### **Implementation Classes:** `HashSet`, `LinkedHashSet`, `TreeSet`

### **Commonly Used Methods:**

|Method|Description|
|---|---|
|`add(E e)`|Adds an element (ignores duplicates)|
|`remove(Object o)`|Removes an element if present|
|`contains(Object o)`|Returns `true` if present|
|`size()`|Returns the number of elements|
|`isEmpty()`|Returns `true` if empty|
|`clear()`|Removes all elements|
|`iterator()`|Returns an iterator for traversal|

### **Example:**
```java
import java.util.*;

public class SetExample {
    public static void main(String[] args) {
        Set<Integer> set = new HashSet<>(); // Can use LinkedHashSet, TreeSet

        set.add(10);
        set.add(20);
        set.add(10); // Duplicate ignored
        set.remove(20);

        System.out.println(set.contains(10)); // true
        System.out.println(set); // [10]
		
		for (int num : set) {
            System.out.println(num);
        }
        set.clear(); // Remove all elements
    }
}
```

---
## **3. Queue (FIFO - First In First Out)**

A `Queue` follows the **FIFO** principle, where elements are added at the end and removed from the front.

### **Implementation Classes:** `LinkedList`, `PriorityQueue`

### **Commonly Used Methods:**

|Method|Description|
|---|---|
|`add(E e)`|Inserts an element (throws exception if full)|
|`offer(E e)`|Inserts an element (returns `false` if full)|
|`poll()`|Retrieves and removes head (returns `null` if empty)|
|`remove()`|Retrieves and removes head (throws exception if empty)|
|`peek()`|Retrieves head without removing (returns `null` if empty)|
|`element()`|Retrieves head without removing (throws exception if empty)|

### **Example:**
```java
import java.util.*;

public class QueueExample {
    public static void main(String[] args) {
        Queue<String> queue = new LinkedList<>(); // Can use PriorityQueue

        queue.offer("Task1");
        queue.offer("Task2");
        queue.offer("Task3");

        System.out.println(queue.poll()); // Removes Task1
        System.out.println(queue.peek()); // Shows Task2 without removing
        for (String task : queue) {
            System.out.println(task);
        }
    }
}
```

---
## **4. Deque (Double-ended queue)**

A `Deque` supports insertion and removal from both ends.

### **Implementation Classes:** `ArrayDeque`, `LinkedList`

### **Commonly Used Methods:**

|Method|Description|
|---|---|
|`addFirst(E e)`, `addLast(E e)`|Adds an element at front/back|
|`offerFirst(E e)`, `offerLast(E e)`|Adds element (returns `false` if full)|
|`pollFirst()`, `pollLast()`|Retrieves and removes from front/back|
|`peekFirst()`, `peekLast()`|Retrieves from front/back without removing|

### **Example:**
```java
import java.util.*;

public class DequeExample {
    public static void main(String[] args) {
        Deque<Integer> deque = new ArrayDeque<>();

        deque.addFirst(10);
        deque.addLast(20);
        System.out.println(deque.pollFirst()); // 10
        System.out.println(deque.pollLast());  // 20
         for (int num : deque) {
            System.out.println(num);
        }
    }
}
```

---
## **5. Map (Key-Value pairs, unique keys)**

A `Map` stores data as key-value pairs.

### **Implementation Classes:** `HashMap`, `LinkedHashMap`, `TreeMap`

### **Commonly Used Methods:**

|Method|Description|
|---|---|
|`put(K key, V value)`|Inserts key-value pair|
|`get(K key)`|Retrieves value for key|
|`remove(K key)`|Removes key-value pair|
|`containsKey(K key)`, `containsValue(V value)`|Checks existence|
|`keySet()`|Returns set of keys|
|`values()`|Returns collection of values|
|`entrySet()`|Returns set of key-value pairs|

### **Example:**
```java
import java.util.*;

public class MapExample {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();

        map.put(1, "One");
        map.put(2, "Two");
        map.put(3, "Three");

        System.out.println(map.get(2)); // Two
        map.remove(1);
        System.out.println(map.keySet()); // [2, 3]
        System.out.println(map.values()); // [Two, Three]

		for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```

---
## **6. Stack (LIFO - Last In First Out)**

A `Stack` follows the **LIFO** principle.

### **Commonly Used Methods:**

|Method|Description|
|---|---|
|`push(E e)`|Pushes an element onto the stack|
|`pop()`|Removes and returns top element|
|`peek()`|Returns top element without removing|
|`isEmpty()`|Checks if stack is empty|
|`search(Object o)`|Returns position of element (1-based)|

### **Example:**
```java
import java.util.*;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();

        stack.push(100);
        stack.push(200);
        System.out.println(stack.pop());  // 200
        System.out.println(stack.peek()); // 100
         for (int num : stack) {
            System.out.println(num);
        }
    }
}
```