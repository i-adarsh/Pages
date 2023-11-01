# Use of Java 8
1. Concise and Minimal Code
2. Benefits of functional programming but still Java is OOP language not Functional Programing language
3. To enable parallel programming, more compatible code for multi core processors

# Features of Java 8

###### 1. Lambda Expressions:
Anonymous functions w/o any name and no need to define
```(x,y) -> x+y;```

###### 2. Stream API
Stream API for bulk data operations on collections. like list and arrat

###### 3. Date and Time API
Under the package java.time Java 8 offers a new date-time API

###### 4. Base64 Encode Decode
For Base64 encoding, Java8 has built-in encode and decode functions. -> java.util.Base64.

###### 5. Method and Constructor reference
```:: operator```

###### 6. default and static methods came inside interface

###### 7. Functional Interface @FunctionalInterface
```SAM -> Single Abstract Method```

###### 8. Optional Class, Java I/O operations and Collections API Improvements


# Q. What is lambda expression?

###### Lambda expression is an anonymous function, i.e. 
- not having any name
- not having any return type 
- and not having modifiers (public, private, default)

###### Steps to make any function lambda expression
1. remove modifier
2. remove return type
3. remove method name
4. place arrow

```sh
Example1:
private int getDtringLength(String str) {
    return str.length();
}
(String str) -> {return str.length();}
(str) -> str.length();

Example2:
private void add(int a, int b) {
    System.out.println(a+b);
}
(int a, int b) -> {System.out.println(a+b);}
(a,b) -> System.out.println(a+b);
```

# Benefits of Lambda Expression:

1. To enable functional programming in Java
2. To make code more readable, maintainable and Concise
3. To enable parallel programming
4. JAR file size reduction
5. Elimination of shadow variables

### Functional Interface:
public abstract methods are only allowed in interface. but after jaav 8 default and static somes inside interface

##### @FunctionalInterface
The interface which contains only one abstract method but can have multiple default and static method is called functional interface;

```
ex: 
    Runnable    => run()
    Callable    => call()
    Comparable  => compareTo()
    Comparator  => compare()
```

##### What is the advantage of this annotation?

It restrict the interface to be a Functional Interface.
So if people have already used some lambda expression and some new team member added another abstract method in the Interface
all lambda expression will have errors.

##### Inheritance in Functional Interface:

```sh
public interface Parent {
    public void sayHello();
}
```
If its empty, then also its an FI.
If we only define the Parent abstract method then also it is FI.

```sh
public interface Child extends Parent {
    public void sayHello();
    default void sayBye() {}
    static void sayTest() {}
}
```

```sh
@FunctionalInterface
public interface MyFunctionalInterface {
    void m1();
    default void m2() {
        System.out.println("Default Method - 2");
    }
    default void m3() {
        System.out.println("Default Method - 3");
    }
    default void m4() {
        System.out.println("Default Method - 4");
    }
}
```

Traditional Approach, first we have to override the abstract method and then only we can call that method:

```sh
interface Calculator {
    void switchOn();
}
public class CalculatorImpl implements Calculator {
    @Override
    public void switchOn() {
        System.out.println("Switch On");
    }
    public static void main(String[] args) {
        Calculator calculator = new CalculatorImpl();
        calculator.switchOn();
    }
}
```

```Syntax of Lambda Functions: () -> {}```

###### Now how we're using it, even if it's a single line of statement we don't have to give the curly braces as well:

```sh
@FunctionalInterface
interface Calculator {
    void switchOn();
}
public class CalculatorImpl {
    public static void main(String[] args) {
        Calculator calculator = () -> {
            System.out.println("Switch On");
        };
        calculator.switchOn();
    }
}
```

###### Without braces:

```sh
@FunctionalInterface
interface Calculator {
    void switchOn();
}
public class CalculatorImpl {
    public static void main(String[] args) {
        Calculator calculator = () -> System.out.println("Switch On");
        calculator.switchOn();
    }
}
```

###### Single Parameter/Arguments:

```sh
@FunctionalInterface
interface Calculator {
    void add(int num1);
}
public class CalculatorImpl {
    public static void main(String[] args) {
        Calculator calculator = (input) -> System.out.println("Sum: " + input);
        calculator.add(24);
    }
}
```

###### Multiple Parameter/Arguments

```sh
@FunctionalInterface
interface Calculator {
    void subtract(int num1, int num2);
}
public class CalculatorImpl {
    public static void main(String[] args) {
        Calculator calculator = (num1 , num2) -> System.out.println("Subtract: " + (num1 - num2));
        calculator.subtract(46, 38);
    }
}
```

###### With some custom logic

```sh
@FunctionalInterface
interface Calculator {
    int subtract(int num1, int num2);
}
public class CalculatorImpl {
    public static void main(String[] args) {
        Calculator calculator = (num1 , num2) ->  {
            if (num1 > num2) {
                return num1 - num2;
            } else {
                throw new RuntimeException("Please make num1 greater");
            }
        };
        System.out.println("Subtract: " + calculator.subtract(46, 38));
    }
}
```

##### Realworld examples:

```Runnable```

```sh
public class Main {
    static class MyClass implements Runnable { // This is a thread
        @Override
        public void run() { // This is thread job
            for (int i = 1; i <= 10; i++) {
                System.out.println("Hello: " + i);
            }
        }
    }
    public static void main(String[] args) {
        MyClass myClass = new MyClass();
        Thread thread = new Thread(myClass);
        thread.start(); // starts new thread
    }
}
```

##### Using Lambda expression

```sh
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            for (int i = 1; i <= 10; i++) {
                System.out.println("Hello: " + i);
            }
        });
        thread.start(); // starts new thread
    }
}
```

```Comparator```

```sh

```

```Book.java```

```sh
package lambda.bookExample;

public class Book {
    private int id;

    public Book(int id, String name, int pages) {
        this.id = id;
        this.name = name;
        this.pages = pages;
    }

    private String name;

    @Override
    public String toString() {
        return "Book{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", pages=" + pages +
                '}';
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getPages() {
        return pages;
    }

    public void setPages(int pages) {
        this.pages = pages;
    }

    private int pages;
}
```

```BookDAO.java```

```sh
package lambda.bookExample;

import java.util.ArrayList;
import java.util.List;

public class BookDAO {
    public List<Book> getBooks() {
        List<Book> books = new ArrayList<>();
        books.add(new Book(101, "Core Java", 400));
        books.add(new Book(102, "Hibernate", 131));
        books.add(new Book(103, "Spring", 124));
        books.add(new Book(104, "Spring Boot", 242));
        books.add(new Book(105, "Docker", 532));
        return books;
    }
}
```

```sh
package lambda.bookExample;

import java.util.Comparator;
import java.util.List;

public class BookService {
    public List<Book> getBooksInSortedOrder(){
        List<Book> books = new BookDAO().getBooks();
        books.sort(new MyComparator());
        return books;
    }

    public static void main(String[] args) {
        System.out.println(new BookService().getBooksInSortedOrder());
    }
}

class MyComparator implements Comparator<Book>{
    @Override
    public int compare(Book o1, Book o2) {
        return o2.getName().compareTo(o1.getName());
    }
}
```

```sh
import java.util.Comparator;
import java.util.List;

public class BookService {
    public List<Book> getBooksInSortedOrder(){
        List<Book> books = new BookDAO().getBooks();
        books.sort(new Comparator<Book>() {
            @Override
            public int compare(Book o1, Book o2) {
                return o2.getName().compareTo(o1.getName());
            }
        });
        return books;
    }

    public static void main(String[] args) {
        System.out.println(new BookService().getBooksInSortedOrder());
    }
}
```

```sh
public class BookService {
    public List<Book> getBooksInSortedOrder(){
        List<Book> books = new BookDAO().getBooks();
        books.sort((book1, book2) -> book1.getName().compareTo(book2.getName()));
        return books;
    }

    public static void main(String[] args) {
        System.out.println(new BookService().getBooksInSortedOrder());
    }
}
```

```sh
public class BookService {
    public List<Book> getBooksInSortedOrder(){
        List<Book> books = new BookDAO().getBooks();
        books.sort(Comparator.comparing(Book::getName));
        return books;
    }

    public static void main(String[] args) {
        System.out.println(new BookService().getBooksInSortedOrder());
    }
}
```

### default Methods

```sh
interface Parent {
    default void sayHello() {
        System.out.println("Hello");
    }
}

class Child implements Parent{
    @Override
    public void sayHello() {
        System.out.println("Hello from child");
    }
}
public class MyClass {
    public static void main(String[] args) {
        Parent p = new Child();
        p.sayHello();
    }
}
```

#### Interview Question

```sh
interface A {
    default void sayHello() {
        System.out.println("A says Hello");
    }
}
interface B {
    default void sayHello(){
        System.out.println("B says Hello");
    }
}
public class MyClass implements A, B{
    public static void main(String[] args) {
        MyClass myClass = new MyClass();
        myClass.sayHello();
    }
}

NOTE: Hmlog A aur B ko ek sath implement nhi kar skte hai jab tak dono mai same function with same signature hai, ye compile time error dega. 
Agar hame dono ko implement krna hai toh:
1. Ya to hm dono methods ka signature change krde
2. Ya phir, hame main class mai methods ko override krna hoga

public class MyClass implements A, B{
    public static void main(String[] args) {
        MyClass myClass = new MyClass();
        myClass.sayHello();
    }

    @Override
    public void sayHello() {
        A.super.sayHello();
        // B.super.sayHello();
        // Ya phir hmlog yha pe apna kuch define kar skte hai
        // System.out.println("Hello");
    }
}
```

___

#### Static Method in interface

- Static Methods in Interface are those methods, which are defined in the interface with the keyword static.

- static methods contain the complete definition of the function

- cannot be overridden or changed in the implementation class

- interface mai agar static method hai toh hmlog usko sirf uske name se hi call kar skte hai

- but agar hamare pas koi default method hai toh hmlog class ka obj bna ke usko call kar skte hai

```sh
interface A {
    static void sayHello() {
        System.out.println("A says Hello");
    }
    default void sayBye() {
        System.out.println("Bye !");
    }
}

public class MyClass implements A{
    public static void main(String[] args) {
        MyClass myClass = new MyClass();
        myClass.sayBye();
        A.sayHello();
    }
}
```

Agar mere pas koi static method hai mere interface mai toh wo mwthods mere implemented class ko show hi nhi hoga, jiske wajah se hum static methods ko override hi nhi kar skte

From Java8 we can call main functions from an interfacce, because from java8 se static methods interface ke andar aana suru ho gye hai

```sh
public interface MyClass {
    public static void main(String[] args) {
        System.out.println("Hello from interface");
    }
}
```

___


### Java 8 - Consumer, Predicate, Supplier examples

```Consumer Functional Interface```

Consumer<T> is an in-built functional interface introduced in Java 8.
Consumer can be used in all contexts where an object needs to be consumed i.e. taken as inout, and some operations is to be performed on the object without returning any result

```void accept(T t);```
___
```Predicate Functional Interface```

This Functional Interface used for conditional check where you think, we can use these true/false returning functions in day to day programming we should choose Predicate

```boolean test(T t);```
___
```Supplier Functional Interface```

Supplier can be used in all contexts where there is no input but an output is expected.

```T get();```
___
```Consumer Functional Interface```

```sh
public class ConsumerDemo implements Consumer<Integer> {
    @Override
    public void accept(Integer integer) {
        System.out.println("Printing: " + integer);
    }

    public static void main(String[] args) {
        
    }
}
```

```sh
public class ConsumerDemo{
    public static void main(String[] args) {
       Consumer<Integer> consumer = (t) -> {
            System.out.println("Printing: " + t);
       };
       consumer.accept(10);
    }
}

public class ConsumerDemo{
    public static void main(String[] args) {
       Consumer<Integer> consumer = (t) -> {
            System.out.println("Printing: " + t);
       };
       consumer.accept(10);
        List<Integer> list = Arrays.asList(1,4,23,6,3,7,84,3);
        list.forEach(consumer);
        list.forEach(t -> System.out.println("Print: " + t));
    }
}
```
___

```Predicate```

```sh
public class PredicateDemo implements Predicate<Integer> {
    @Override
    public boolean test(Integer integer) {
        return integer % 2 == 0;
    }

    public static void main(String[] args) {
        Predicate<Integer> predicate = new PredicateDemo();
        System.out.println(predicate.test(4));
    }
}
```
___

#### lambda expression

```sh
public class PredicateDemo{

    public static void main(String[] args) {
        Predicate<Integer> predicate = (t) -> {
            return t % 2 == 0;
        };
        System.out.println(predicate.test(57));
    }
}
```

```sh
public class PredicateDemo{

    public static void main(String[] args) {
        Predicate<Integer> predicate = (t) -> t % 2 == 0;
        System.out.println(predicate.test(64));
    }
}
```

```sh
public class PredicateDemo{

    public static void main(String[] args) {
        Predicate<Integer> predicate = (t) -> t % 2 == 0;
        System.out.println(predicate.test(64));
        List<Integer> list = Arrays.asList(1,4,23,6,3,7,84,3);
        list.stream().filter(t -> t % 2 == 0).forEach(t -> System.out.println("Even Numbers: " + t));
        list.stream().filter(t -> t % 2 != 0).forEach(t -> System.out.println("Odd Numbers: " + t));
    }
}
```

___

```Supplier```

```sh
import java.util.Arrays;
import java.util.List;

public class SupplierDemo {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("a", "b");
        System.out.println(list.stream().findAny().orElseGet(() -> "Bounce Back"));
    }
}
```
___


#### lambda expression

```sh
package Java8;

import stream.sort.Customer;
import stream.sort.EkartDatabase;

import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class OptionalDemo {
    public static Customer getCustomerByEmailId(String email) throws Exception {
        List<Customer> customers = EkartDatabase.getAll();
        return customers.stream()
                .filter(customer -> customer.getEmail().equalsIgnoreCase(email))
                .findAny().orElseThrow(() -> new Exception("no customer with this email"));
    }
    public static void main(String[] args) throws Exception {
        Customer customer = new Customer(101, "abc", "abc@email.com", Arrays.asList("1323536", "4367348"));
        // empty
        // of
        // ofNullable

        Optional<Object> emptyOptional = Optional.empty();
        System.out.println(emptyOptional);

        Optional<String> emailOptional = Optional.of(customer.getEmail());
        System.out.println(emailOptional);

        Optional<String> emailOption = Optional.ofNullable(customer.getEmail());
        /*
        old method
        if(emailOption.isPresent()){
            System.out.println(emailOption.get());
        }
        */
        emailOption.ifPresent(System.out::println);
        System.out.println(emailOption.orElse("Email not present: default@email.com"));
        System.out.println(emailOption.orElseThrow(() -> new IllegalArgumentException("Email not present")));
        System.out.println(emailOption.map(String::toUpperCase).orElseGet(()->"default email ..."));
        getCustomerByEmailId("hello");
    }
}

```
