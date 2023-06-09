﻿# Java-8-Lambda
# Why Lambda?

- Enables functional programming
- Readable and concise code
- Easier-to-use API’s and libraries
- Enables support for parallel processing

---

# Code in OOP

- Everything is an object.
- All code blocks are “associated” with class and ojects.

---

# Functions as Values

## Inline values

```java
String name = "JSK";
```

## Funcations as value

```java
aBlockOfCode = ~~public void perform~~(){
		System.out.println("JSK!");
}
```

```java
aBlockOfCode = () -> System.out.println("JSK!");
```

```java
aBlockOfCode = () -> {
		System.out.println("JSK!");
		System.out.println("JSK!");
}
```

---

# Example

```java
greet(() -> System.out.println("JSK!"));
```

```java
doubleNumberFunction = (int a) -> a*2;
```

```java
addFunction = (int a, int b) -> a + b;
```

```java
safeDivideFuncation = (int a, int b) -> {
		if(b == 0) return 0;
		return a/b;
}
```

---

# Lambda as interface type

```java
class Greater{
	public static void main(String[] args){
		MyLambda myLambdaFuncation = () => System.ot.println("JSK!");
		MyAdd addFuncation = (int a, int b) -> a+b;
	}
}

interface MyLambda{
	void foo(); // Method name doesn't matter.
	// We cannot write 2 methods if we want to use it for lambda expression.
}
interface MyAdd{
	int add(int x, int y);
}
```

---

# Lambdas vs Interface Implementaions

```java
public interface Greeting{
	public void perform();
}

class JskGreeting implements Greating{
	public void perform(){
		System.out.println("JSK!");
	}
}

public class Greater{

	public void greet(Greeting greeting){
		greeting.perform();
	}

	public static void main(String[] args){
		Greeter jskGreeting = new Greeting();
		Greeter lambdaGreeting = () -> System.out.println("JSK!");

		//anonymous inner class 
		Greeting innerClassGreeting = new Greeting(){
			public void perform(){
				System.out.println("JSK!");
			}
		};
	
		jskGreeting.perform();                 // OUTPUT: JSK!
		lambdaGreeting.perform();              // OUTPUT: JSK!
		innerClassGreeting.perform();          // OUTPUT: JSK!

		greeter.greet(lambdaGreeting);         // OUTPUT: JSK!
		greeter.greet(innerClassGreeting);     // OUTPUT: JSK!
	}
}
```

<aside>
💡 Labda Expressiona and inner class both looks same but they are not.

</aside>

---

# Type Inference

```java
public class TypeInferenceExample {
    public static void main(String[] args) {
        StringLengthLambda myLambda = s -> s.length();
        System.out.println(myLambda.getLength("JSK!"));
    }

    interface StringLengthLambda{
        int getLength(String s);
    }
}
```

**Output:**

4

```java
public class TypeInferenceExample {
    public static void main(String[] args) {
//        StringLengthLambda myLambda = s -> s.length();
//        System.out.println(myLambda.getLength("JSK!"));

        printLambda(s->s.length());
    }

    public static void printLambda(StringLengthLambda l){
        System.out.println(l.getLength("JSK!!!"));
    }

    interface StringLengthLambda{
        int getLength(String s);
    }
}
```

**Output:**

6

---

# Runnable using Lambda

**Plain old method:**

```java
public class RunnableExample {
    public static void main(String[] args) {
        Thread myThread = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("Printed inside Runnable!");
            }
        });
        myThread.run();
    }
}
```

**Output:**

Printed inside Runnable!

```java
public class RunnableExample {
    public static void main(String[] args) {
        Thread myThread = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("Printed inside Runnable!");
            }
        });
        myThread.run();

        Thread myLambdaThread = new Thread(()-> System.out.println("Printed inside lambda Runnable"));
        myLambdaThread.run();
    }
}
```

**Output:**

Printed inside Runnable!
Printed inside lambda Runnable

<aside>
💡 remember this works because Runnable has a single method. If it had more than one method, you could not have written a lambda function of that type.

</aside>

<aside>
💡 These interfaces are called as “Funcational Interface”.

</aside>

---

# Funcational Interface

The interface which has one abstact method only is called funcational interface.

- Its a property of Interface.

```java
@FunctionalInterface
public interface Greeting {
    public void perform();
}
```

<aside>
💡 The @FuncationalInterface annotation is completely optional. The java compiler does not require it for your lambda types. But it is goof practice to add it.

</aside>

---

# Exercise

- **Java-7 Implementation:**
    
    ```java
    import java.util.Arrays;
    import java.util.Collections;
    import java.util.Comparator;
    import java.util.List;
    
    public class Unit1Exercise {
        public static void main(String[] args) {
            List<Person> people = Arrays.asList(
                    new Person("Charles","Dickens",60),
                    new Person("Lewis","Carrol",20),
                    new Person("Uday","Bhaskar",21),
                    new Person("Anna","Carlyle",55)
            );
    
            //Step-1: Sort List by Last name
            Collections.sort(people, new Comparator<Person>() {
                @Override
                public int compare(Person o1, Person o2) {
                    return o1.getLastName().compareTo(o2.getLastName());
                }
            });
    
            //Step-2: Create a method that prints all elements in the List
            System.out.println("Print all persons");
            printAll(people);
    
            //Step-3: Create a method that prints all people that have last name beginning withC
            System.out.println("Print all persons whose last name begins with 'C'");
            printConditionally(people, new Condition() {
                @Override
                public boolean test(Person p) {
                    return p.getLastName().startsWith("C");
                }
            });
    
            System.out.println("Print all persons whose first name begins with 'U'");
            printConditionally(people, new Condition() {
                @Override
                public boolean test(Person p) {
                    return p.getFirestName().startsWith("U");
                }
            });
        }
    
        private static void printConditionally(List<Person> people, Condition condition) {
            for(Person p: people){
                if(condition.test(p))
                    System.out.println(p);
            }
        }
    
        private static void printAll(List<Person> people) {
            for(Person p: people){
                System.out.println(p);
            }
        }
    }
    interface Condition{
        boolean test(Person p);
    }
    ```
    
- **Java-8** **Implementation**:
    
    ```java
    import java.util.Arrays;
    import java.util.Collections;
    import java.util.Comparator;
    import java.util.List;
    
    public class Unit1ExerciseSolutionJava8 {
        public static void main(String[] args) {
            List<Person> people = Arrays.asList(
                    new Person("Charles","Dickens",60),
                    new Person("Lewis","Carrol",20),
                    new Person("Uday","Bhaskar",21),
                    new Person("Anna","Carlyle",55)
            );
    
            //Step-1: Sort List by Last name
            Collections.sort(people, (p1, p2) -> p1.getLastName().compareTo(p2.getLastName()));
    
            //Step-2: Create a method that prints all elements in the List
            System.out.println("Print all persons");
            printConditionally(people, p -> true);
    
            //Step-3: Create a method that prints all people that have last name beginning withC
            System.out.println("Print all persons whose last name begins with 'C'");
            printConditionally(people,p -> p.getLastName().startsWith("C"));
    
            System.out.println("Print all persons whose first name begins with 'U'");
            printConditionally(people, p -> p.getFirestName().startsWith("U"));
        }
    
        private static void printConditionally(List<Person> people, Condition condition) {
            for(Person p: people){
                if(condition.test(p))
                    System.out.println(p);
            }
        }
    
    }
    interface Condition{
        boolean test(Person p);
    }
    ```
    
- **Output**
    
    ```
    Print all persons
    Person{firestName='Uday', lastName='Bhaskar', age=21}
    Person{firestName='Anna', lastName='Carlyle', age=55}
    Person{firestName='Lewis', lastName='Carrol', age=20}
    Person{firestName='Charles', lastName='Dickens', age=60}
    Print all persons whose last name begins with 'C'
    Person{firestName='Anna', lastName='Carlyle', age=55}
    Person{firestName='Lewis', lastName='Carrol', age=20}
    Print all persons whose first name begins with 'U'
    Person{firestName='Uday', lastName='Bhaskar', age=21}
    ```
    

---

# Using Funcation Interfaces

**Package java.util.function**

<aside>
💡 Funcational interfaces provided to target types for lambda expressions and method references.

</aside>

[java.util.function (Java Platform SE 8 )](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)

```java
private static void printConditionally(List<Person> people, Predicate<Person> predicate) {
   for(Person p: people){
       if(predicate.test(p))
          System.out.println(p);
   }
}
```

- As we know we need to create an interface to use lambda expression.
- But if you find an interface that you need in java.util.funcation then no need to create an interface, you can use it directly from that package.

---

# More Functional Interfaces

```java
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Predicate;

public class Unit1ExerciseSolutionJava8 {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
                new Person("Charles","Dickens",60),
                new Person("Lewis","Carrol",20),
                new Person("Uday","Bhaskar",21),
                new Person("Anna","Carlyle",55)
        );

        //Step-1: Sort List by Last name
        Collections.sort(people, (p1, p2) -> p1.getLastName().compareTo(p2.getLastName()));

        //Step-2: Create a method that prints all elements in the List
        System.out.println("Print all persons");
        performConditionally(people, p -> true, p -> System.out.println(p));

        //Step-3: Create a method that prints all people that have last name beginning withC
        System.out.println("Print all persons whose last name begins with 'C'");
        performConditionally(people,p -> p.getLastName().startsWith("C"), p -> System.out.println(p));

        System.out.println("Print fist name of all persons whose first name begins with 'U'");
        performConditionally(people, p -> p.getFirestName().startsWith("U"), p -> System.out.println(p.getFirestName()));
    }

    private static void performConditionally(List<Person> people, Predicate<Person> predicate, Consumer<Person> consumer) {
        for(Person p: people){
            if(predicate.test(p))
                consumer.accept(p);
        }
    }

}
```

**************Output:**************

```
Print all persons
Person{firestName='Uday', lastName='Bhaskar', age=21}
Person{firestName='Anna', lastName='Carlyle', age=55}
Person{firestName='Lewis', lastName='Carrol', age=20}
Person{firestName='Charles', lastName='Dickens', age=60}
Print all persons whose last name begins with 'C'
Person{firestName='Anna', lastName='Carlyle', age=55}
Person{firestName='Lewis', lastName='Carrol', age=20}
Print fist name of all persons whose first name begins with 'U'
Uday
```

---

# Execption Handling in Lambdas

```java
import java.util.function.BiConsumer;

public class ExceptionalHandlingExample {
    public static void main(String[] args) {
        int[] someNumber = {1,2,3,4};
        int key =0;
        process(someNumber, key, (v,k)-> {
            try {
                System.out.println(v / k);
            }
            catch (ArithmeticException e){
                System.out.println("An Arithmetic Exception occurred");
            }
        });

    }
    private static void process(int[] someNumbers, int key, BiConsumer<Integer,Integer> consumer){
        for(int i: someNumbers){
            consumer.accept(i, key);
        }
    }
}
```

Look up → This is a mess.

Lets make it clean and clear.

---

# An Exceptional Handling Approach

```java
import java.util.function.BiConsumer;

public class ExceptionalHandlingExample {
    public static void main(String[] args) {
        int[] someNumber = {1,2,3,4};
        int key =0;
        process(someNumber, key, wrapperLambda((v,k)-> System.out.println(v/k)));

    }
    private static void process(int[] someNumbers, int key, BiConsumer<Integer,Integer> consumer){
        for(int i: someNumbers){
            System.out.println("Executing from process");
            consumer.accept(i, key);
        }
    }

    private static BiConsumer<Integer, Integer> wrapperLambda(BiConsumer<Integer,Integer> consumer){
        return (v,k)-> {
            System.out.println("Executing from wrapper");
            try{
                consumer.accept(v,k);
            }
            catch (ArithmeticException e){
                System.out.println("Exception caught in wrapper lambda");
                System.out.println();
            }
        };
    }
}
```

**************Output:**************

```
Executing from process
Executing from wrapper
Exception caught in wrapper lambda

Executing from process
Executing from wrapper
Exception caught in wrapper lambda

Executing from process
Executing from wrapper
Exception caught in wrapper lambda

Executing from process
Executing from wrapper
Exception caught in wrapper lambda
```

---

# Closures in Lambda Expressions

```java
public class ClosuresExample {
    public static void main(String[] args) {
        int a=10;
        int b=20;                                // Java assumes that this is final and we will not change it in future.
        doProcess(a, new Process() {
            @Override
            public void process(int i) {
                b=40;                             //Error: Variable 'b' is accessed from within inner class, needs to be final or effectively final
                System.out.println(i+b);
            }
        });
    }
    public static void doProcess(int i, Process p){
        p.process(i);
    }
}
interface Process{
    void process(int i);
}
```

This is almost similar to closure

```java
public class ClosuresExample {
    public static void main(String[] args) {
        int a=10;
        int b=20;
        doProcess(a, (i) -> System.out.println(i+b));
    }
    public static void doProcess(int i, Process p){
        p.process(i);
    }
}
interface Process{
    void process(int i);
}
```

- Value of b is frozen.
- The compiler says, you don’t have to put a final there (final b =20;) as long as you can garenty that its final I am good. (Thats effextively final).

---

# The this reference in lambdas

```java
public class ThisReferenceExample {
    public void doProcess(int i, Process p){
        p.process(i);
    }

    public void execute(){
        doProcess(10, (i)->{
            System.out.println("Value of i in execute is: "+i);
            System.out.println(this);
        });
    }

    public static void main(String[] args) {
        ThisReferenceExample thisReferenceExample = new ThisReferenceExample();
        thisReferenceExample.doProcess(10, (i)->{
            System.out.println("Value of i in main is: "+i);
//            System.out.println(this); This will not work
        });

        thisReferenceExample.execute();
    }
    public String toString(){
        return "This is a main ThisReferenceExample class instance";
    }
}
```

**************Output:**************

```
Value of i in main is: 10
Value of i in execute is: 10
This is a main ThisReferenceExample class instance
```

---

# Method References

******************Example-1:******************

```java
public class MethodReferenceExample1 {
    public static void main(String[] args) {
        Thread t = new Thread(()->printMessage());  //If both the parameters are same here then we use Method Reference
        t.start();
    }
    
    public static void printMessage(){
        System.out.println("JSK!");
    }
}
```

Using Method Reference, see below

```java
public class MethodReferenceExample1 {
    public static void main(String[] args) {
        Thread t = new Thread(MethodReferenceExample1::printMessage);
//        MethodReferenceExample1::printMessage === ()->printMessage()
        
        t.start();
    }

    public static void printMessage(){
        System.out.println("JSK!");
    }
}
```

******************Example-2:******************

```java
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Predicate;

public class MethodReferenceExample2 {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
                new Person("Charles","Dickens",60),
                new Person("Lewis","Carrol",20),
                new Person("Uday","Bhaskar",21),
                new Person("Anna","Carlyle",55)
        );

        System.out.println("Print all persons");
//        performConditionally(people, p -> true, p -> System.out.println(p));
        performConditionally(people, p -> true,System.out::println);
    }

    private static void performConditionally(List<Person> people, Predicate<Person> predicate, Consumer<Person> consumer) {
        for(Person p: people){
            if(predicate.test(p))
                consumer.accept(p);
        }
    }

}
```

**************Output:**************

```
Print all persons
Person{firestName='Charles', lastName='Dickens', age=60}
Person{firestName='Lewis', lastName='Carrol', age=20}
Person{firestName='Uday', lastName='Bhaskar', age=21}
Person{firestName='Anna', lastName='Carlyle', age=55}
```

---

# The foreach iterator

<aside>
💡 for and for-in are called “External Iterators”.

</aside>

<aside>
💡 forEach is an “Internal Iterator”.

</aside>

- forEach is helpful in multi threading while running in parallel

```java
import java.util.Arrays;
import java.util.List;

public class CollectionIteratorExample {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
                new Person("Charles","Dickens",60),
                new Person("Lewis","Carrol",20),
                new Person("Uday","Bhaskar",21),
                new Person("Anna","Carlyle",55)
        );
        System.out.println("Using for loop");
        for(int i=0;i<people.size();i++){
            System.out.println(people.get(i));
        }

        System.out.println("\nUsing for in loop");
        for(Person p: people){
            System.out.println(p);
        }

        //Above two iterators are called external iterators.

        //Internal iterator
        System.out.println("\nUsing lambda for each loop");
        people.forEach(System.out::println);

    }
}
```

**************Output:**************

```
Using for loop
Person{firestName='Charles', lastName='Dickens', age=60}
Person{firestName='Lewis', lastName='Carrol', age=20}
Person{firestName='Uday', lastName='Bhaskar', age=21}
Person{firestName='Anna', lastName='Carlyle', age=55}

Using for in loop
Person{firestName='Charles', lastName='Dickens', age=60}
Person{firestName='Lewis', lastName='Carrol', age=20}
Person{firestName='Uday', lastName='Bhaskar', age=21}
Person{firestName='Anna', lastName='Carlyle', age=55}

Using lambda for each loop
Person{firestName='Charles', lastName='Dickens', age=60}
Person{firestName='Lewis', lastName='Carrol', age=20}
Person{firestName='Uday', lastName='Bhaskar', age=21}
Person{firestName='Anna', lastName='Carlyle', age=55}
```

---

# Streams

> A sequence of elements supporting sequentail and parallel aggregates operations.
> 

Example: Cars → person1- color, person2- fix engine, person3- fix tires → conveyer belt.

```java
import java.util.Arrays;
import java.util.List;

public class StreamsExample1 {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
                new Person("Charles","Dickens",60),
                new Person("Lewis","Carrol",20),
                new Person("Uday","Bhaskar",21),
                new Person("Anna","Carlyle",55)
        );

        people.stream()
                .filter(p-> p.getLastName().startsWith("C"))
                .forEach(p-> System.out.println(p.getFirestName()));
    }
}
```

**************Output:**************

```
Lewis
Anna
```

---

# More about Stream

```java
import java.util.Arrays;
import java.util.List;

public class StreamsExample1 {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
                new Person("Charles","Dickens",60),
                new Person("Lewis","Carrol",20),
                new Person("Uday","Bhaskar",21),
                new Person("Anna","Carlyle",55)
        );

        people.stream()
                .filter(p-> p.getLastName().startsWith("C"))
                .forEach(p-> System.out.println(p.getFirestName()));

        long count = people.stream()
                .filter(p-> p.getLastName().startsWith("C"))
                .count();

        System.out.println(count);

        long count2  = people.parallelStream()
                .filter(p-> p.getLastName().startsWith("C"))
                .count();

        System.out.println(count2);
    }
}
```

**Output:**

```
Lewis
Anna
2
2
```

---
