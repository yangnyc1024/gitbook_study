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

=class Node implements Comparable<Node> {
    int id;
    String name;
    char character;
    @Override
    public int compareTo(Node that) {
        return Integer.compare(this.id, that.ide)
    }

}
```
