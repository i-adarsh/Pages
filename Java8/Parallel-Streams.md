### What is Java Parallel Streams?

1. Java Parallel Streams is a feature of Java 8, It meant for utilizing multiple cores of the processor.

2. Normally any java code has one stream of processing, where it is executed sequentially. Whereas by using parallel streams, we can divide the code into multiple streams that are executed in parallel on separate cores and the final result is the combination of the individual
outcomes

3. The order of execution, however, is not under our control.

___

```sh
package Java8.parallelStream;

import stream.DataBase;
import stream.Employee;

import java.util.List;
import java.util.stream.IntStream;

public class ParallelStreamExample {
    public static void parallelStream(){
        long start = 0;
        long end = 0;

        start = System.currentTimeMillis();
        IntStream.range(1,100).forEach(System.out::println);
        end = System.currentTimeMillis();
        System.out.println("Plain stream took time: " + (end - start));

        start = System.currentTimeMillis();
        IntStream.range(1, 100).parallel().forEach(System.out::println);
        end = System.currentTimeMillis();
        System.out.println("Parallel stream took time: " + (end - start));
    }
    public static void parallelThread(){
        IntStream.range(1, 20).forEach(x->{
            System.out.println("Thread: " + Thread.currentThread().getName() + " : " + x);
        });
        IntStream.range(1, 20).parallel().forEach(x->{
            System.out.println("Thread: " + Thread.currentThread().getName() + " : " + x);
        });
    }
    public static void main(String[] args) {
        List<Employee> employees = DataBase.getAllEmployee();
        long start = 0;
        long end = 0;

        start = System.currentTimeMillis();
        double avgWithStream = employees.stream()
                .map(Employee::getSalary).mapToDouble(i -> i).average().getAsDouble();
        end = System.currentTimeMillis();
        System.out.println("Stream execution time: " + (end - start));
        System.out.println("Average Salary: " + avgWithStream);

        start = System.currentTimeMillis();
        double avgWithParallelStream = employees.stream()
                .map(Employee::getSalary).mapToDouble(i -> i).average().getAsDouble();
        end = System.currentTimeMillis();
        System.out.println("Parallel Stream execution time: " + (end - start));
        System.out.println("Average Salary: " + avgWithParallelStream);
    }
}

```