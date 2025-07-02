# Comparable  vs Comparator 

### 🔷 1. Comparable Interface

#### ✅ Purpose:

Defines a **natural ordering** for objects of a class.  
Implemented by the class itself.

#### ✅ Signature:

```java
public interface Comparable<T> {
    int compareTo(T o);
}

```

#### ✅ Sorting Rule:

-   Returns **0** → objects are equal
-   Returns **< 0** → current object is _less than_ the argument
-   Returns **> 0** → current object is _greater than_ the argument

----------

#### 📌 Example: Sorting Students by Name Using `Comparable`

```java
class Student implements Comparable<Student> {
    private String name;
    private int marks;

    public Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    public String getName() { return name; }
    public int getMarks() { return marks; }

    @Override
    public int compareTo(Student other) {
        return this.name.compareTo(other.name); // Sort by name alphabetically
    }

    @Override
    public String toString() {
        return name + " (" + marks + ")";
    }
}

```

#### 🔽 Usage:

```java
import java.util.*;

public class ComparableExample {
    public static void main(String[] args) {
        List<Student> list = Arrays.asList(
            new Student("Alice", 85),
            new Student("Bob", 75),
            new Student("Charlie", 90)
        );

        Collections.sort(list); // Uses compareTo()
        System.out.println(list);
    }
}

```

----------

### 🔷 2. Comparator Interface

#### ✅ Purpose:

Provides **custom ordering** for objects outside the class.  
Used when natural ordering isn't sufficient or multiple sort criteria are needed.

#### ✅ Signature:

```java
public interface Comparator<T> {
    int compare(T o1, T o2);
}

```

----------

#### 📌 Example: Sorting Students by Marks Using `Comparator`

```java
import java.util.*;

class MarksComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return Integer.compare(s1.getMarks(), s2.getMarks()); // Ascending
    }
}

```

#### 🔽 Usage:

```java
public class ComparatorExample {
    public static void main(String[] args) {
        List<Student> list = Arrays.asList(
            new Student("Alice", 85),
            new Student("Bob", 75),
            new Student("Charlie", 90)
        );

        Collections.sort(list, new MarksComparator()); // Uses compare()
        System.out.println(list);
    }
}

```

----------

#### 🔥 Bonus: Comparator Using Lambda (Java 8+)

```java
Collections.sort(list, (s1, s2) -> Integer.compare(s2.getMarks(), s1.getMarks())); // Descending

```

OR using method references:

```java
list.sort(Comparator.comparing(Student::getMarks)); // Ascending

```

----------

### 📌 Summary: Comparable vs Comparator

| Feature|Comparable | Comparator|
|--|--|--|
| Located in Class | Yes (`compareTo()` inside class) |No (defined externally)|
|Interface Used|`Comparable<T>`|`Comparator<T>`|
|Method Name|`compareTo(T o)`|`compare(T o1, T o2)`|
|Single / Multi|Allows only one sorting logic|Can define multiple sorting rules|
|Example Use Case|Default sort (e.g., by name)|Custom sort (e.g., by marks, age)
|

----------

Let’s explore how to **use both `Comparable` and `Comparator` together**, including **multi-level sorting** (e.g., by name, then by marks) in Java.

----------

### 🔷 Scenario: Sort Students First by Name, Then by Marks (If Names Match)

#### ✅ Student Class with `Comparable` for Natural Sorting (by Name)

```java
class Student implements Comparable<Student> {
    private String name;
    private int marks;

    public Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    public String getName() { return name; }
    public int getMarks() { return marks; }

    @Override
    public int compareTo(Student other) {
        return this.name.compareTo(other.name); // Natural order: by name
    }

    @Override
    public String toString() {
        return name + " (" + marks + ")";
    }
}

```

----------

#### ✅ Custom Comparator for Multi-Level Sorting (Name + Marks)

```java
import java.util.*;

class NameThenMarksComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        int nameComparison = s1.getName().compareTo(s2.getName());
        if (nameComparison == 0) {
            return Integer.compare(s2.getMarks(), s1.getMarks()); // Descending by marks
        }
        return nameComparison;
    }
}

```

----------

#### 🔽 Usage

```java
public class CombinedSortExample {
    public static void main(String[] args) {
        List<Student> students = Arrays.asList(
            new Student("Alice", 85),
            new Student("Bob", 75),
            new Student("Alice", 92),
            new Student("Charlie", 78),
            new Student("Bob", 90)
        );

        System.out.println("Sorted by name (natural order):");
        Collections.sort(students); // Uses Comparable
        students.forEach(System.out::println);

        System.out.println("\nSorted by name, then marks (custom order):");
        Collections.sort(students, new NameThenMarksComparator()); // Uses Comparator
        students.forEach(System.out::println);
    }
}

```

----------

#### 🧠 Output

```
Sorted by name (natural order):
Alice (85)
Alice (92)
Bob (75)
Bob (90)
Charlie (78)

Sorted by name, then marks (custom order):
Alice (92)
Alice (85)
Bob (90)
Bob (75)
Charlie (78)

```

----------

#### 🔥 Pro Tip: Lambda Style Comparator (Java 8+)

```java
students.sort(
    Comparator.comparing(Student::getName)
              .thenComparing(Comparator.comparingInt(Student::getMarks).reversed())
);

```

----------
