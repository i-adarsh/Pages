What is Map-Reduce ?

1. Map-Reduce is a functional programming model it serves our 2 purpose

Мар ----> Transforming data
Reduce ----> Aggregating data
(combine elements of a stream and produces a single value)

2. Ex: Stream: [2,4,6,9,1,3,7] Sum of numbers present in stream?

3. Map ----> Transform Stream<Object> to Stream of int
4. Reduce() ----> combine stream of int and produce the sum result

### Reduce method

T reduce(T identity, BinaryOperator<T> accumulator);

1. identity is initial value of type T
2. accumulator is a function for combining two values.

``` Integer sumResult = Stream.of(2, 4, 6, 9, 1, 3, 7).reduce (0, (a, b) -> a + b); ```

Identity: 0 which is nothing initial value
Accumulator: (a, b) -> a+b function

___

```sh
package Java8;

import stream.DataBase;
import stream.Employee;

import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class MapReduceExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(3,7,8,1,5,9);
        List<String> courses = Arrays.asList("Java", "Python", "Spring Boot", "Angular", "Hibernate");
        int sum = 0;
        for (int i : numbers){
            sum += i;
        }
        System.out.println(sum);

        // Using map
        int sum1 = numbers.stream().mapToInt(i -> i).sum();
        System.out.println("Map: " + sum1);
        // Using reduce
        int reduceSum = numbers.stream().reduce(0, (a,b)->a+b);
        System.out.println("Reduce: " + reduceSum);
        // Using stream
        Optional<Integer> reduceSumWithMethodReference = numbers.stream().reduce(Integer::sum);
        System.out.println("Method Reference: " + reduceSumWithMethodReference.get());
        // Multiplication
        Integer multiplication = numbers.stream().reduce(1,(a,b)->a*b);
        System.out.println("Multiplication: " + multiplication);
        // Maximum
        Integer maximum = numbers.stream().reduce(0, (a,b)->a > b ? a : b);
        System.out.println("Maximum: " + maximum);
        // Maximum using method reference
        Integer maximumUsingMethodReference = numbers.stream().reduce(0, Integer::max);
        System.out.println("Maximum Method Reference: " + maximumUsingMethodReference);

        // On String
        String longestString = courses.stream().reduce((c1, c2)->c1.length() > c2.length() ? c1 : c2).get();
        System.out.println("Longest String: " + longestString);

        // Custom Objects
        double averageSalary = DataBase.getEmployees().stream()
                .filter(employee -> employee.getDepartment().equalsIgnoreCase("Core"))
                .map(Employee::getSalary)
                .mapToDouble(i->i)
                .average().getAsDouble();
        System.out.println("Average Salary: " + averageSalary);

        double sumSalary = DataBase.getEmployees().stream()
                .filter(employee -> employee.getDepartment().equalsIgnoreCase("IT"))
                .map(Employee::getSalary)
                .mapToDouble(i->i)
                .sum();
        System.out.println("Salary sum: " + sumSalary);
    }
}

```