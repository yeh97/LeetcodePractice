

### Leetcode 146
#### [LRU Cache](https://leetcode.com/problems/lru-cache)

  

##### ***Problem:***

    Design and implement a data structure for Least Recently Used (LRU) cache. 
    It should support the following operations: 
    get and put.

    get(key) - 
    Get the value (will always be positive) of the key 
    if the key exists in the cache, otherwise return -1.

    put(key, value) - 
    Set or insert the value if the key is not already present. 
    When the cache reached its capacity, 
    it should invalidate the least recently used item before inserting a new item.


    
##### ***Example:***

    Input: ["LRUCache","put","put","get","put","get","put","get","get","get"]
            [[2],[1,1],[2,2],[1],[3,3],[2],[4,4],[1],[3],[4]]
        Output: [null,null,null,1,null,-1,null,-1,3,4]

##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2017_08_27
 *Language: Java
 *
 */

import java.util.Map.Entry;

class LRUCache {
    
    // LinkedHashMap : Deque + HashMap
    private CacheLinkedHashMap<Integer, Integer> cache;
    public LRUCache(int capacity) {
        this.cache = new CacheLinkedHashMap<Integer, Integer>(capacity);
    }
    
    public int get(int key) {
        int val = -1;
        if (cache.containsKey(key)) {
            val = cache.get(key);
            cache.keySet().remove(key);
            cache.put(key, val);
        }
        return val;
    }
    
    public void put(int key, int value) {
        if (cache.containsKey(key)) {
            cache.keySet().remove(key);
        }
        cache.put(key, value);
    }
}

class CacheLinkedHashMap<K, V> extends LinkedHashMap<K, V> {
    private int capacity;
    public CacheLinkedHashMap(int capacity) {
        super();
        this.capacity = Math.max(capacity, 0);
    }
    protected boolean removeEldestEntry(Entry<K, V> eldest) {
        return this.size() > capacity;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
 
```


