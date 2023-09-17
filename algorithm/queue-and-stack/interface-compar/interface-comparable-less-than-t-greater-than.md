# Interface Comparable\<T>

## API 1: compareTo(T o)

* 负数，表示优先

```java
// Some code
public class ClassName implements Comparable<ClassName> {
    @Override
    public int compareTo(ClassName, otherClassName) {
        return Integer.compare(this.filedName, otherClassName.fieldName);
    }
}
```

### example

```java
// Some code

class Node implements Comparable<Node> {
    int id;
    String name;
    char character;
    @Override
    public int compareTo(Node that) {
        return Integer.compare(this.scores, that.scores);
    }
}

class Node implements Comparable<Node> {
    @Override
    public int compareTo(Node other) {
        if (Integer.compare(this.id, other.id) < 0) {
            return -1;
        }
        else if (Integer.compare(this.id, other.id) > 0) {
            return 1;
        }
        else { // this.id == other.id
            if (this.character < other.character) {
                return -1;
            }
            else if (this.character > other.character) {
                return 1;
            }
            else {
                return 0;
            }
        }
    }
}
```
