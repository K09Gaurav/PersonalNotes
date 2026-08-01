---
tags:
  - java
  - spring
---

# What is a Bean in Spring?

Think of a **bean** as just a **normal Java object** —  
But it’s **created, managed, and injected by Spring**.

Since we code interfaces instead of concrete classes and we leave it up to framework where to supply the concrete classes via dependency injection 
we will use term beans for those concrete class

---

## Why Do We Care?

- You **don’t** create beans manually using `new`.
- Spring does it **for you** when the app starts.
- It **stores them**, **reuses them**, and **injects them** wherever needed.

This is part of **Inversion of Control (IoC)**.

---

### How Do We Make a Bean?

Spring turns a class into a bean if:
- It’s marked with annotations like:
  - `@Component`
  - `@Service`
  - `@Repository`
  - `@Controller`
- Or it’s created manually in a config class using `@Bean`.

```
@Component
public class MyHelper {
// This is now a Spring Bean
}
```

---

# THE PROJECT TO UNDERSTAND BEANS

Starting what i am doing: 

```java
@SpringBootApplication
@Log
public class ColorsApplication implements CommandLineRunner{  

	public static void main(String[] args) {
	SpringApplication.run(ColorsApplication.class, args);
	}
	  
	@Override
	public void run(final String... args) throws Exception {
		final ColorPrinter colorPrinter = new ColorPrinterImpl();
		log.info()
	}
}

```
her ewe are implementing `CommandLineRunner` for making this spring app in a sommand line app. and using logger to print in the logs.

ColorPrinterImpl :

```java

public class ColorPrinterImpl implements ColorPrinter {
  private RedPrinter redPrinter;
  private BluePrinter bluePrinter;
  private GreenPrinter greenPrinter;

  public ColorPrinterImpl() {
    this.redPrinter = new EnglishRedPrinter();
    this.bluePrinter = new EnglishBluePrinter();
    this.greenPrinter = new EnglishGreenPrinter();
  }

  @Override
  public String print() {
    return String.join(", ", redPrinter.print(), bluePrinter.print(), greenPrinter.print());
  }
}
```

Here the Color Printer Implementation class has :

3 dependencies: 
```
  -  private RedPrinter redPrinter;
  -  private BluePrinter bluePrinter;
  -  private GreenPrinter greenPrinter;
```
- each interface being same : 

```java
public interface BluePrinter {
    String print();
}
```
and their implementation : 

```java
public class EnglishGreenPrinter implements GreenPrinter {

  @Override
  public String print() {
    return "green";
  }
}

```

After running the main spring application file the output comes as 
`red, blue, green`

NOW what if we wanted to swap out the implementation of them in another way.

how to do that we would need to changes to the classes specifically the `ColorPrinterImpl` class from english to spanish where the `new` keyword is used and objects are being created.

That means changing the hard codded stuff even though we just wanted to swap out the dependencies we were using.
OBVIOUS WAY TO FIX THIS and change easily is touise beans.

what should become beans are : 
```
	 ColorPrinter colorPrinter = new ColorPrinterImpl();

    this.redPrinter = new EnglishRedPrinter();
    this.bluePrinter = new EnglishBluePrinter();
    this.greenPrinter = new EnglishGreenPrinter();
```

One way of doing is via a configuration file
create a new package called config : called printer config 

We add configuration annotation : `@Configuration`
this tell spring to look in this class for bean declaration.

we start adding the classes which should bne bean with `@Bean` annotation as a method.
it should return implementation of blue printor :

```java
    @Bean
    public BluePrinter bluePrinter(){
        return new EnglishBluePrinter();
    }

    @Bean
    public RedPrinter redPrinter() {
        return new EnglishRedPrinter();
    }

    @Bean
    public GreenPrinter greenPrinter() {
        return new EnglishGreenPrinter();
    }

```

now we have 3 beans availaible,
can now be injected.
we need to change the place that they are actually used rather than create them.

inside constructor we cna declare them because spring will be using constructor to assign the dependencies 

```java
  public ColorPrinterImpl(RedPrinter redPrinter, BluePrinter bluePrinter, GreenPrinter greenPrinter) {
    this.bluePrinter = bluePrinter;
    this.redPrinter = redPrinter;
    this.greenPrinter = greenPrinter;
  }
```
DO the same in main application class by replacing `	 ColorPrinter colorPrinter = new ColorPrinterImpl();`

we add this in main application:
```java
	private ColorPrinter colorPrinter;
	
	public ColorsApplication(ColorPrinter colorPrinter) {
		this.colorPrinter = colorPrinter;
	}
```

and this in config file
```java
    @Bean
    public ColorPrinter colorPrinter(BluePrinter bluePrinter,RedPrinter redPrinter,GreenPrinter greenPrinter){ // inputing them as beans
        return new ColorPrinterImpl(bluePrinter, greenPrinter, redPrinter);
    }
```

NOW WHEN WE START OUR APPLICATION
it will look for config,
find it, will loook at red blue green printer breans,
when it will reach the color Printer it will look for red blue and green printer which it already has so it will inject them into color printer

then the colorPrinter bean will be injected into the main application. and it will run with it as a bean

#### **What Happens Internally (In Depth)**
Spring Boot:

- Initializes the Spring ApplicationContext (the container).
- Scans the application for:
	- @SpringBootApplication
	- @Configuration, @Component, etc.
- Starts managing beans and dependencies.
- Spring Finds @Configuration Class
-  Spring Creates Basic Printer Beans beacause Spring sees methods annotated with @Bean
- For each method like this:
    - Spring calls the method once
    - Registers the return value as a singleton bean in the container.
    - Associates the method name (redPrinter) with that bean.
- Same goes for BluePrinter and GreenPrinter.
	- Result: Spring now owns and manages 3 printer beans.
- Spring Creates ColorPrinter Bean
- Here’s what Spring does:
	- Notices that colorPrinter() needs 3 beans.
	- Looks up those beans (already created in previous step).
	- Calls this method with the existing beans as arguments.
	- Registers the returned ColorPrinterImpl as a new bean.


    Spring wires the dependencies automatically by matching the parameter types.

- Spring Injects ColorPrinter into ColorsApplication

- Spring sees the constructor in your main class:
- At this point, Spring knows:
	- You’ve declared a need for a ColorPrinter.
	- It already has a ColorPrinterImpl bean.
	- It calls this constructor with the correct bean.
	- Result: ColorsApplication is now also a bean — and fully wired.

```
@SpringBootApplication starts →
  Spring scans beans →
    Finds PrinterConfig →
      Builds Red/Blue/Green Printer beans →
        Injects them into ColorPrinterImpl →
          Injects ColorPrinter into main class →
            Calls run() →
              Logs output

```

**NOW WHAT IF WE WANT TO DO CHANGES LIKE IN PREVIOUS ONE:** 

If we now want to switch to Spanish output ("rojo" instead of "red"), we would have to:

    Create a new class SpanishRedPrinter.

    Go inside ColorPrinterImpl and manually change EnglishRedPrinter to SpanishRedPrinter.

This breaks modularity and violates Open/Closed Principle —
our class has to change for a small config-level decision.

**BUT With Spring Beans, Swapping Is Easy**

	Step 1: Create Spanish Implementations

	Step 2: Modify the Config Class

All you do is change the return values in your @Configuration class.

```java
@Bean
public RedPrinter redPrinter() {
    return new SpanishRedPrinter();  // Swapped from EnglishRedPrinter
}

@Bean
public BluePrinter bluePrinter() {
    return new SpanishBluePrinter();
}

@Bean
public GreenPrinter greenPrinter() {
    return new SpanishGreenPrinter();
}

```

What You Didn’t Have to Touch

- ColorPrinterImpl stays the same

- Main application class stays the same

- Service wiring, constructor injection, run method — untouched

You only updated the configuration.

- That’s the power of using beans + dependency injection:
- change what you use, not how your code behaves.


> Bonus: Environment-Specific Switching
> You can even make Spring choose the implementation based on profile:


```java
@Profile("english")
@Bean
public RedPrinter englishRedPrinter() {
    return new EnglishRedPrinter();
}

@Profile("spanish")
@Bean
public RedPrinter spanishRedPrinter() {
    return new SpanishRedPrinter();
}

```

> Then you run your app like this:
> 
> `-Dspring.profiles.active=spanish`
> 
> Now you’ve got full environment-level modularity — without touching core logic.

## Easier Way of Making Beans: `@Component`

Instead of creating beans via `@Configuration` + `@Bean` methods,  
Spring also lets you define beans more easily using **annotations directly on classes**.

---

### ✅ Use `@Component` on Class

You can annotate the class itself:

```java
@Component
public class EnglishRedPrinter implements RedPrinter {
    public String print() {
        return "red";
    }
}
```

This tells Spring:
    “Scan this class, create a bean, and manage it.”

---

✅ How to Inject

Spring will automatically inject the bean wherever it's needed, using:
Constructor Injection (Preferred)

⚠️ Common Mistake to Avoid

    ❌ @Component goes on the class, not the method.


---


## Summary: Two Ways to Register Beans
| Method                     | Use Case                                                         |
| -------------------------- | ---------------------------------------------------------------- |
| `@Component`               | Quick, automatic scanning                                        |
| `@Bean` + `@Configuration` | Full control, multiple implementations, profiles, complex wiring |


## Friends of `@Components`

#### Are `@Service`, `@Controller`, `@Repository` the Same as `@Component`?

##### Short Answer: ✅ Yes, Technically

All of them — `@Service`, `@Controller`, `@Repository` — are **stereotype annotations** and are **meta-annotated with `@Component`**.

That means:
> Spring treats them the same in terms of component scanning and bean registration.

So yes:
```java
@Component
public class MyService { ... }
```
is functionally identical to:
```java
@Service
public class MyService { ... }

```

---

### Then Why Use Different Annotations?

Because each one:

- Conveys intent and role of the class in your architecture.
- Enables specific Spring features depending on the stereotype.

✅ @Component

- Generic stereotype.
- Use when no specific role applies.
- Most flexible and neutral.

✅ @Service

- Indicates a business logic class.
- Helps IDEs and tools understand it's a service layer.
- Spring may add AOP (Aspect-Oriented Programming) features like transaction handling or logging around methods.
- Preferred for classes in the Service Layer.

✅ @Repository

- Indicates a data access class (e.g., DAO).
- Adds exception translation — converts low-level persistence exceptions (like SQLException) into Spring’s DataAccessException.
- Preferred for Persistence Layer (e.g., using JpaRepository, JdbcTemplate, etc.).

✅ @Controller

- Indicates a web controller.
- Enables Spring MVC request mapping.
- Classes annotated with @Controller can use:

	@RequestMapping, @GetMapping, etc.
	Automatic binding of HTTP requests to method arguments.

> Use only for Presentation Layer (REST endpoints, web UI).

### Can You Swap Them?
| Swap Case                    | Will It Work? | Should You Do It?  | Why?                                   |
| ---------------------------- | ------------- | ------------------ | -------------------------------------- |
| `@Service` → `@Component`    | ✅ Yes         | ⚠️ Not Recommended | Loses semantic meaning                 |
| `@Repository` → `@Component` | ✅ Yes         | ❌ No               | Loses exception translation            |
| `@Controller` → `@Component` | ❌ No          | ❌ No               | Won’t register HTTP routes             |
| `@Component` → `@Controller` | ❌ No          | ❌ No               | Will fail unless it's a web controller |


Conclusion

- All are technically components.
- But each has extra behaviour and clear purpose.
- Use the correct one for the role of your class — it makes your code:

	Easier to read
	Easier to maintain
	Less prone to subtle bugs

Stick to:
`@Controller` → for REST/web
`@Service `→ for business logic
`@Repository` → for database interaction
`@Component` → for anything else that doesn't fit


