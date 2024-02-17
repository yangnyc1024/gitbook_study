# Practice 1 HashMap Design



```java
// Some code
// Some code
public static class MyHashMap<String, Integer> {
    public static class Entry<String, Integer>{ //本质上是个ListNode
        private final String key;
        private Entry<String, Integer> next;
        public Entry(String key, int value) {
            this.key = key
            this.value = value
        }
    }
    private static final int DEFAULT_CAPACITY = 16;
    private static final float DEFAULT_LOAD_FACTOR = 0.75f;
    private Entry<String, Integer>[] buckets; // array of ListList ==> array of listnode(entry)
    private int capacity;
    private int size;   // size(你现在拉了多少) vs capacity（最多拉多少）
    private float loadFactor;
    
    
    //用户提供capacity和loadFactor版本
    public MyHashMap(int capacity, float loadFactor) {
        this.capacity = capacity;
        this.loadFactor = loadFactor;
        this.size = 0;
        this.buckets = new Entry[capacity];
    }
    //用户不提供capacity和loadFactor版本
    public MyHashMap(int capacity, float loadFactor) {
        this.capacity = DEFAULT_CAPACITY;
        this.loadFactor = DEFAULT_LOAD_FACTOR;
        this.size = 0;
        this.buckets = new Entry[capacity];
    }
    /* OOD:
    public MyHashMap() {
        this(DEFAULT_CAPACITY, DEFAULT_LOAD_FACTOR);
    }
    */
    public int size(){
        return this.size;
    }
    public boolean isEmpty(){
        return this.size == 0;
    }
    private boolean equalsKey(String key1, String key2) {
        return key1.equals(key2);
    }
    //给我一个key, 我就还给你一个hashCode，保证这个hashCode不会超界，也不会是负数
    private int hash(String key) {
        if (key == null) {
            return 0;
        }
        return key.hashCode() & 0X7FFFFFFFF
    }
    // 16, 1,2,3,4,5,6,7,8,9,A,B,C,D,E,F
    // OX7FFFFFFFF => 0111 1111 1111 1111 1111 1111 1111 1111.
    // 1 & anynumber = any number, 0 & anynumber = 0
    
    // 既然说我只要有个key就有hashcode了，我怎么知道这个key应该在我的map的array里的哪个index bucket
    // 你给我一个key，我能告诉你这个key在哪个bucket里
    
    private int getIndex(String key) {
        int hashCode = hash(key)
        return hashCode % this.capacity;
    }
    
    // rehashing: 扩容 这个方法能告诉我们现在的hashmap的状况，需不需要rehash
    // 如果当前的map里的entry的总数/capacity =》 你设置的load factor了，那么我们就应该，否不不应该
    private boolean needRehashing() {
        float ratio = (size  + 0.0f/ capacity);
        return ratio >= this.loadFactor;
    }
    
    private void clear() {
        Arrays.fill(this.buckets, null);
        size = 0;
    }
    
    
    
    private Integer put(String key, int value){
        
    
    }
    
    private void rehashing(){
        this.capacity *= 2;
        
        Entry<String, Integer>[] newBuckets = new Entry[this.capacity];
        for (Entry<String, Integer> eachHead: buckets) {
        }
    }
    private Integer remove(String key){
        
    }
}
```
