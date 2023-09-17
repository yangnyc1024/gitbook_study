---
description: Interface Comparator
---

# Interface Comparator\<T>

## API 1: compare(T o1, T o2)

```java
// Some code
class MyComparator implements Comparator<classname> {
    @Override
    public int compare(className name1, className name2) {
    
    }

}
```



Example

```java
// Some code


class Student{
    String name;
    int age;
    int scores;
    public Student(String name, int age, int scores) {
        this.name = name;
        this.age = age;
        this.scores = scores;
    }
}

class MyComparator implements Comparetor<Student> {
    @Override
    public int compare(Student student1, Student student2) {
        return Integer.compare(student2.scores, student1.scores)
    }
}

public static void main(String[] args) {
    List<Student> vipClass = newArrayList<>();
    Student student1 = new Student("Harry", 18, 95);
    Student student2 = new Student("Bob", 20, 90);
    Student student3 = new Student("Jane", 26, 60);
    Student student4 = new Student("Alice", 19 65);
    vipClass.add(student1);
    vipClass.add(student2);
    vipClass.add(student3);
    vipClass.add(student4);
    for (int i = 0; i < vipClass.size(); i++) {
        System.out.println("Before Sorting: " + vipClass.get(i).name);
    }
    Collections.sort(vipClas, new MyComparator());
    for (int i = 0; i <vipClss.size(); i++) {
        System.out.println("After Sorting: " + vipClass.get(i).name);
    }
}

class MyComparator implements Comparator<Student> {
    @Override
    public compare(Student student1, Student student2) {
        if (student1.scores > student2.scores) {
            return -1; 
        }
        else if (student1.scores < student2.scores) {
            return 1;
        }
        else {
            if (student1.age > student2.age) {
                return 1;
            }
            else if (student1.age < student2.age) {
                return -1;
            }
            else {
                return 0;
            }
        }
    }

}
```

## API 2: equals(Object obj)

## API 3: naturalOrder()

## API 4: reverseOrder()
