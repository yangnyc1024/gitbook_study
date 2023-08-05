# Shuffle Algorithm

### What is the shuffle algorithm?

A shuffle algorithm is a method used to&#x20;

* rearrange the elements of a list or array into a random order.&#x20;
* The goal is to ensure that each permutation is equally likely.



### What does it look like?

Data Structure

* <mark style="color:red;">already shuffled</mark> || <mark style="color:blue;">not shuffle yet</mark>
* <mark style="color:blue;">index: \[index... n -1] are not shuffled yet, \[0, ... index - 1] are already shuffled</mark>

Algorithm

* Initialization: index = 0
* For each step:
  * Uniformly and randomly choose one card from the non-shuffled cards
  * Swap this chosen card with the card at the index
  * More the index one step to the right

```java
public void shuffle(int[] array) {
    // assume array not null and not empty
    if (array.length <= 1) {
        return;
    }
    for(int i = array.length; i >= 1; i--) {
        int index = (int)(Math.random() * i);
        swap(array, index, i -1);
    }
}
private void swap(int[] array, int left, int right) {
    int temp = array[left];
    array[left] = array[right];
    array[right] = temp;
}


```
