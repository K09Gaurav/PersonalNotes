#### - To quickly get `setter and getters` / `constructors` for some data members:
  1. `ctrl` + `shift` + `p`
  2. `source action`
  3. `select option` -> `getter|setter` / `constructors`
  4. `arrow key` to navigate
  5. `space` to select

#### - To view what all arguments can be passed inside we can do 
- `ctrl + space`
- for Trigger Parameter Hints : `ctrl + shift + space`
---
---
#### - USE `@Override public String toString()` because:
1. `toString()` is a method in the `Object` class that returns a string representation of an object.
2. By default, if not overridden, it returns a string containing the class name and the object's hash code.
3. Overriding `toString()` allows you to define a meaningful string representation of the object.
```java
	@Override
	public String toString() {
	return "Person{name='" + name + "', age=" + age + "}";			
	} 
```
---
---
#### - Quickly fix Indentations on VS Code
- Alt + Shift + F
---
---

## ⚙️ Lombok — Reducing Boilerplate in Java

### 📌 What is Lombok?

**Lombok** is a compile-time Java library that auto-generates boilerplate code like:
- Getters/Setters
- Constructors
- `toString()`, `equals()`, `hashCode()`

You write less code, but compiled classes have everything needed.
### 🔧 Common Lombok Annotations

#### 1. `@Getter` / `@Setter`
Generates getter/setter methods for all fields (or per field if applied individually).
#### 2. `@Data`
Shortcut for:
- `@Getter` + `@Setter`
- `@ToString`
- `@EqualsAndHashCode`
- `@RequiredArgsConstructor`

Best used for **POJOs / DTOs** like config classes, models, etc.
#### 3. `@NoArgsConstructor`
Generates a **no-argument constructor**.

#### 4. `@AllArgsConstructor`
Generates a constructor with **all fields as parameters**.

#### 5. `@ToString`
Overrides `toString()` with a clean representation of fields.

### ✅ Example

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class PizzaConfig {
    private String sauce;
    private String topping;
    private String crust;
}
```

---
---
---




#java #vscode