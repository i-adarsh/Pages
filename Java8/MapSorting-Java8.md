
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