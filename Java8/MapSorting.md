
### Java 8 - Sorting Map

```sh
package stream.sort;

import stream.Employee;
import java.util.*;

public class SortMap {
    // For primitive data types
    public static void conventionalWay(){
        Map<String, Integer> map = new HashMap<>();
        map.put("eight", 8);
        map.put("four", 4);
        map.put("six", 6);
        map.put("seven", 7);
        map.put("two", 2);

        List<Map.Entry<String, Integer>> entries = new ArrayList<>(map.entrySet());
        Collections.sort(entries, new Comparator<Map.Entry<String, Integer>>() {
            @Override
            public int compare(Map.Entry<String, Integer> o1, Map.Entry<String, Integer> o2) {
                return o1.getKey().compareTo(o2.getKey());
            }
        });
        for (Map.Entry<String, Integer> entry : entries){
            System.out.println(entry.getKey() + " " + entry.getValue());
        }
    }
    public static void usingLambdaExpression(){
        Map<String, Integer> map = new HashMap<>();
        map.put("four", 4);
        map.put("six", 6);
        map.put("seven", 7);
        map.put("eight", 8);
        map.put("two", 2);

        List<Map.Entry<String, Integer>> entries = new ArrayList<>(map.entrySet());
        Collections.sort(entries, (o1, o2)->(o1.getKey().compareTo(o2.getKey())));
        for (Map.Entry<String, Integer> entry : entries){
            System.out.println(entry.getKey() + " " + entry.getValue());
        }
    }
    public static void usingStreamApi(){
        Map<String, Integer> map = new HashMap<>();
        map.put("four", 4);
        map.put("six", 6);
        map.put("seven", 7);
        map.put("eight", 8);
        map.put("two", 2);
        map.entrySet().stream().sorted(Map.Entry.comparingByKey()).forEach(System.out::println);
        System.out.println("---------");
        map.entrySet().stream().sorted(Map.Entry.comparingByValue()).forEach(System.out::println);
    }

    // For custom classes
    public static void customConventionalWay(){
        Map<Employee, Integer> map = new TreeMap<>(new Comparator<Employee>() {
            @Override
            public int compare(Employee o1, Employee o2) {
                return (int) (o1.getSalary() - o2.getSalary());
            }
        });
        map.put(new Employee(176, "Roshan", "IT", 760000), 60);
        map.put(new Employee(388, "Bikash", "Civil", 860000), 90);
        map.put(new Employee(325, "Bimal", "Defence", 960000), 50);
        map.put(new Employee(547, "Sourav", "Core", 360000), 40);
        map.put(new Employee(326, "Prakash", "Social", 560000), 20);
        map.entrySet().forEach(System.out::println);
    }
    public static void customUsingLambdaExpression(){
        Map<Employee, Integer> map = new TreeMap<>((a,b) -> (int)(b.getSalary() - a.getSalary()));
        map.put(new Employee(176, "Roshan", "IT", 760000), 60);
        map.put(new Employee(388, "Bikash", "Civil", 860000), 90);
        map.put(new Employee(325, "Bimal", "Defence", 960000), 50);
        map.put(new Employee(547, "Sourav", "Core", 360000), 40);
        map.put(new Employee(326, "Prakash", "Social", 560000), 20);
        map.entrySet().forEach(System.out::println);
    }
    public static void customUsingStreamApi(){
        Map<Employee, Integer> map = new HashMap<>();
        map.put(new Employee(176, "Roshan", "IT", 760000), 60);
        map.put(new Employee(388, "Bikash", "Civil", 860000), 90);
        map.put(new Employee(325, "Bimal", "Defence", 960000), 50);
        map.put(new Employee(547, "Sourav", "Core", 360000), 40);
        map.put(new Employee(326, "Prakash", "Social", 560000), 20);
        // Sorting in increasing order
        map.entrySet().stream()
                .sorted(Map.Entry.comparingByKey(Comparator.comparing(Employee::getSalary)))
                .forEach(System.out::println);
        System.out.println("----------");
        // Sorting in decreasing order
        map.entrySet().stream()
                .sorted(Map.Entry.comparingByKey(Comparator.comparing(Employee::getSalary).reversed()))
                .forEach(System.out::println);
    }
    public static void main(String[] args) {
        // conventionalWay();
        // usingLambdaExpression();
//        usingStreamApi();
//        customConventionalWay();
//        customUsingLambdaExpression();
        customUsingStreamApi();
    }
}

```

### Map() & flatMap()


1. Java 8 stream API provides map() and flatMap() method. Both these methods are intermediate methods and returns another stream as part of the output.
2. map() method used for transformation
3. flatMap() used for transformation & flattering
4. flatMap() → map() + flattering

___

map() method > Data Transformation

• map() takes Stream<T> as input and return Stream<R>
Stream<R> map(Stream<T> input){}

```‹R› Stream<R› map(Function‹? super T, ? extends R› mapper);```

It's mapper function produces single value for each input value,
hence it is also called One-To-One mapping.

___

flatMap() method > map() + Flattering

• flatMap() takes Stream<Stream<T>> as input and return Stream<R>
Stream<R> map(Stream<Stream<T input)}

```<R> Stream<R> flatMap(Function‹? super T, ? extends Stream<? extends R>> mapper);```

It's mapper function produces multiple value for each input value,
hence it is also called One-To-Many mapping.

___

#### Data Transformation and Flattering

Data Transformation: Transform data from lowercase to uppercase

stream.of("a", "b", "c", "d");      -->     [A, B, C, D]


Data Flattering: Convert stream of stream into single stream

[[1, 2], [3, 4], [5, 6], [7, 8]]    -->     [1, 2, 3, 4, 5, 6, 7, 8]

| map() | flatMap()|
|-------|----------|
| It processes stream of values. | It processes stream of stream of values. |
| It does only mapping. | It performs mapping as well as flattening. |
| It's mapper function produces single value for each input value. | It's mapper function produces mutiple values for each input value. |
| It is a One-To-One mapping. | It is a One-To-Many mapping.|
| Data Transformation : From Stream to Stream | Data Transformation : From Stream<Stream>to Stream |
| Use this method when the mapper function is producing a single value for each input value. | Use this method when the mapper function is producing multiple values for each input value. |

___

```sh
package stream.sort;

import java.util.List;

public class MapVsFlatMap {
    public static void main(String[] args) {
        List<Customer> customers = EkartDatabase.getAll();

        // List<Customer> convert List<String> -> Data Transformation
        // mapping : customer -> customer.getEmail()
        // customer -> customer.getEmail() : one to one mapping
        // conventional
        // List<String> emails = customers.stream().map(customer -> customer.getEmail()).collect(Collectors.toList());
        // using lambda
        List<String> emails = customers.stream().map(Customer::getEmail).toList();
        emails.forEach(System.out::println);

        // conventional
        // List<List<String>> phoneNumbers = customers.stream().map(customer -> customer.getPhoneNumbers()).collect(Collectors.toList());
        // lambda
        List<List<String>> phoneNumbers = customers.stream().map(Customer::getPhoneNumbers).toList();
        System.out.println(phoneNumbers);

        // flatmap()
        // List<Customer> convert List<String> -> Data Transformation
        // mapping : customer -> phone numbers
        // customer -> customer.getPhoneNumbers() : one to many mapping
        List<String> phone = customers.stream().flatMap(customer -> customer.getPhoneNumbers().stream()).toList();
        System.out.println(phone);
    }
}
```




 
