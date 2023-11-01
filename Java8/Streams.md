### Streams in Java

- Stream API is used to process collections of objects.
A stream is a sequence of objects that supports various methods which can be pipelined to produce the desired result.
- A stream is not a data structure instead it takes input from the Collections, Arrays or I/O channels.
- Streams don't change the original data structure, they only provide the result as per the pipelined methods.

#### Why we need stream?

- Functional Programming: Means If I have a functional interface then I can represent that with lambda expression.
- Code Reduce: Helps to write less code
- Bulk Operation: Stream will give better performance

#### Methods:

- filter - for conditional check
- forEach - for iteration

```forEach```

```sh
public class ForEachDemo {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("John", "Peter", "Ben", "Sarah", "Luci", "Alice");
        list.forEach(s -> System.out.println("Name: " + s));

        Map<Integer, String > map = new HashMap<>();
        map.put(1, "a");
        map.put(2, "b");
        map.put(3, "c");
        map.put(4, "d");

        map.forEach((key, value) -> System.out.println(key + " : " + value));
        map.entrySet().forEach(obj -> System.out.println(obj + " "));
    }
}
```

```filter```

```sh
public class ForEachDemo {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("John", "Peter", "Ben", "Sarah", "Luci", "Alice");

        Map<Integer, String > map = new HashMap<>();
        map.put(1, "a");
        map.put(2, "b");
        map.put(3, "c");
        map.put(4, "d");
        list.stream().filter(s -> s.startsWith("A")).forEach(s -> System.out.println("Hello: " + s));
        map.entrySet().stream()
                .filter(k -> k.getKey() % 2 == 0)
                .forEach(obj-> System.out.println(obj.getKey() + " : " + obj.getValue()));
    }
}
```

```Real world example```

```sh
package stream;

public class Employee {
    private int id;
    private String name;
    private String department;
    private long salary ;

    public Employee(int id, String name, String department, long salary) {
        this.id = id;
        this.name = name;
        this.department = department;
        this.salary = salary;
    }
}
```


```sh
public class DataBase {
    // DAO Layer
    public static List<Employee> getEmployees() {
        List<Employee> list = new ArrayList<>();
        list.add(new Employee(176, "Roshan", "IT", 760000));
        list.add(new Employee(388, "Bikash", "Civil", 860000));
        list.add(new Employee(325, "Bimal", "Defence", 960000));
        list.add(new Employee(547, "Sourav", "Core", 360000));
        list.add(new Employee(326, "Prakash", "Social", 560000));
        return list;
    }
}
```

```sh
public class TaxService {
    public static List<Employee> evaluateTaxUser(String input){
        return (input.equalsIgnoreCase("Taxpayer"))
                ? DataBase.getEmployees().stream()
                .filter(employee -> employee.getSalary() > 500000).collect(Collectors.toList())
                : DataBase.getEmployees().stream()
                .filter(employee -> employee.getSalary() <= 500000).collect(Collectors.toList());
    }

    public static void main(String[] args) {
        System.out.println(evaluateTaxUser(""));
        System.out.println(evaluateTaxUser("Taxpayer"));
    }
}
```