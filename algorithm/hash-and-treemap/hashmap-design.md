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
    
    // 你给我一个key， 我看看这个key在map里面有没有，如果有我就get出来返回这个key对应的value
    // 如果没有， 返回一个特殊值 null
    /* 逻辑：
        step 1: 先知道这个key在哪个bucket
        step 2: 对这个bucket里有的这个linkedlist进行遍历，逐一判断到底有没有我要找的key
        
        index      0
        Entry array: Entry(key, value), Entry(key2, value2), ...
                        |
                    Entry(key3, value3)     Entry(key4, value4)
    
    */
    public Integer get(String key) {
        int index = getIndex(key);
        Entry<String, Integer> head = buckets[index];
        Entry<String, Integer> cur = head;
        while (cur != null) {
            if (equalsKey(cur.key, key)) {
                return cur.value;
            }
            cur = cur.next;
        }
        return null;
    }
    
    // 你给我一个key，我看看这个key在map里面有没有，如果有我就返回true， 没有我就返回false
    public boolean containsKey(String key) {
        int index = getIndex(key);
        Entry<String, Integer> head = buckets[index];
        Entry<String, Integer> cur = head;
        while (cur != null) {
            if (equalsKey(cur.key, key)) {
                return true;
            }
            cur = cur.next;
        }
        return false;
    }
    // key 是null，不代表value是null，map允许key和value是null
    // value pair: <null, 3>
    
    
    /* 逻辑
        我们尝试往hashmap里放入<key, value>这个entry
        case1:以前map里没有这个entry
            insert this entry to the head of the linkedlist in the bucktes
            (get the linkedlist and insert head)
            
        case2: 以前map里有这个entry
            update oldkey's value to newValue
            
        returnType:
            如果你抹掉了旧的value <3,5> --> <3,3> 你一定把抹掉的value return出来
            如果你没有抹掉任何值，return null就ok了
            关系: entry -- Node 包含了key value field
            put这个方法有没有可能触发rehash？注意有可能
    */
    
    private Integer put(String key, int value){
        // step 1： 先拿到key应该在的index
        int index = getIndex(key);
        Entry<String, Integer> head = buckets[index];
        Entry<String, Integer> cur = head;
            
        // step 2: 得看看以前map里面有可以这个key
        while (cur != null) {
            if (equalsKey(cur.key, key)) {
                // update value
                int oldValue = cur.value;
                cur.value = value;
                return oldValue;
            }    
            cur = cur.next;
        }
        //代码执行到这里的时候说明map里面没有这个key-value pair需要insert at head
        Entry<String, Integer> newEntry = new Entry<>(key, value);
        // insert head
        newEntry.next = head;
        buckets[index] = newEntry;
        this.size++;
        
        //已经成功插入一个新的entry，有可能你的ratio要rehash
        if (needRehahsing()) {
            rehashing();
        }
        return null;
    }
    
    /*
        rehash的逻辑不是说把以前旧的每个bucket里的linkedlist超过去就可以了
        把以前的map里的每个entry都重新计算bucket重新放一遍
    */
    
    private void rehashing(){
        this.capacity *= 2;
        /*
            如果你自己定义扩容成几倍，scale_factor
            private static final int SCALE_FACTOR = 4;
            ==> this.capacity *= SCALE_FACTOR;
        */
        Entry<String, Integer>[] newBuckets = new Entry[this.capacity];
        for (Entry<String, Integer> eachHead: buckets) {
            Entry<String, Integer> eachCur = eachHead;
            while (eachCur != null) {
                Entry<String, Integer> next = eachCur.next;
                eachCur.next = null;
                // 把eachCur放进新的map
                // 算一下这个eachCur在新的map里放在哪里
                int index = getIndex(eachCur.key);
                if (newBuckets[index] == null) {
                    newBucktes[index] = eachCur;
                } else {
                    // insert head
                    eachCur.next = newBucks[index];
                    newBucks[index] = eachCur;
                }
                eachCur = next;
            }
        }
        this.buckets = newBuckets;
    }
    
    
    /* function能做什么
        你给我一个key，如果这个map里存在这个key，请你把它remove掉，并且返回你remove的key的value
        如果不存在return null
        
        逻辑：
        还是得看看有没有这个key
        step 1: 先找到index
        step 2: 遍历一遍这个bucktets里的linkedlist看看有没有这个可以
            如果有就remove掉
            否则return null
    */
    private Integer remove(String key){
        int index = getIndex(key);
        Entry<String, Integer> head = buckets[index];
        Entry<String, Integer> cur = head;
        Entry<String, Integer> prev = null;
        
        while (cur != null) {
            if (equalsKey(cur.key, key)) {
                //如果正好是head
                if (prev == null) {
                    buckets[index] = head.next;
                } else {
                    prev.next = cur.next;
                }
                this.size--;
                return cur.value;
            }
            prev = cur;
            cur = cur.next;
        }
        return null;
    }
}
```
