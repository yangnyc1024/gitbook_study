# Array/ List API

| Method API                                                                             | Description                                                                                                            | TC |
| -------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | -- |
| asList(T... a)                                                                         | Return a fixed-size list backed by specified array                                                                     |    |
| binarySearch(int\[] a, int key)                                                        | Search the specified array of ints for the specified value using the binary search algorithm                           |    |
| copyOf(int\[] original, int newLength)                                                 | Copies the psecified arrya, truncating or padding with zeros(if necessary) so the copy has the psecified length.       |    |
| copyOfRange(int\[] original, int from, int to)                                         | Copies the specified range of the specified array into a new array                                                     |    |
| equals(int\[] a1, int\[] a2)                                                           |                                                                                                                        |    |
| equals(int\[] a, int aFromIndex, int aToIndex, int\[] b, int bFromIndex, int bToIndex) | Return true if two specified arrays of ints, over the specified ranges, are equal to one another                       |    |
| deepEquals(Object\[] a1, Object\[] a2)                                                 | Returns true if the two specified arrays are deeply equal to one another                                               |    |
| fill(int\[] a, int val)                                                                | Assigns the specified int value to each elemetn fothe specified array of ints                                          |    |
| sort(int\[] a)                                                                         | Sorts the speicifed array into ascending numerical order                                                               |    |
| sort(int\[] a, int fromIndex, int toIndex)                                             | Sorts the speicifed range of the array into a ascending order.                                                         |    |
| sort(T\[] a, Comparrator\<? super T> c)                                                | Sorts the speicifed array of objects according to the order induced by the speicifed comparator                        |    |
| sort(T\[] a, int fromIndex, int toIndex, Comparator\<? super T> c)                     | Sorts the specified range of the specified array of objects according to the order induced by the specifed comparator. |    |
| toString(int\[] a)                                                                     | REturns a string representation of the contens of the pseicifed array.                                                 |    |
| deepToString(Obejct\[] a)                                                              | Return a string representation of the 'dep contents' of the specified array.                                           |    |
