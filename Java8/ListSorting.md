### Java 8 Stream - How to Sort a List using lambda

```sh
package stream.sort;

import stream.DataBase;
import stream.Employee;

import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class SortList {
    public static void main(String[] args) {
        // Primitive Data Types
        List<Integer> list = Arrays.asList(2,5,6,4,7,4,6,3,5,8,4,9);
        //Using Collections
        Collections.sort(list);
        Collections.reverse(list);

        // Using lambda functions
        list.sort((a, b) -> b - a); // sort the list in descending order
        list.forEach(System.out::print);

        // Using streams
        // Increasing Order
        list.stream().sorted().forEach(System.out::println);
        // Decreasing Order
        list.stream().sorted(Comparator.reverseOrder()).forEach(System.out::println);

        // Custom created class
        List<Employee> employees = DataBase.getEmployees();
        employees.sort((a, b) -> (int) (b.getSalary() - a.getSalary()));
        System.out.println(employees);

        // by using method reference
        employees.stream().sorted(Comparator.comparing(Employee::getName)).forEach(System.out::println);
    }
}

```
___

#### Database

```sh
public static List<Employee> getEmployees() {
    List<Employee> list = new ArrayList<>();
    list.add(new Employee(176, "Roshan", "IT", 760000));
    list.add(new Employee(388, "Bikash", "Civil", 860000));
    list.add(new Employee(325, "Bimal", "Defence", 960000));
    list.add(new Employee(547, "Sourav", "Core", 360000));
    list.add(new Employee(326, "Prakash", "Social", 560000));
    return list;
}
```