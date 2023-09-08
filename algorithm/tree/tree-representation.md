# Tree Representation



## Case 1

index represent ID: id from the range \[0,... number of node -1]

```java
Map<Node, List<Node>> tree = new HashMap<>();
integer RootID = null;

for (int id = 0; id < input.length; id++) {
    if (input[id] == -1) {
        RootID = id;
    }
    int parentID = input[id];
    tree.putIfAbsent(parentID, new ArrayList<>());
    tree.get(parentID).add(id);
}
```

### Case 2 General Nary Tree

```java
// Some code
for (int i = 0; id < referenceConnection.length; i++) {
    int from = referenceConnection[i][0];
    int to = referenceConnection[i][1];
    
    tree.putIfAbsent(from, new ArrayList<>());
    tree.get(from).add(to);
}
```
