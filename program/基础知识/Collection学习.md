# Collection学习

[toc]

# List

### ArrayList<T>

父类

AbstractList<T>

implement

```java
List<E>,RandomAccess,Cloneable,java.io.serializable
    
/**RandomAccess 
*Marker interface used by <tt>List</tt> implementations to indicate that
* they support fast (generally constant time) random access.  The primary
 * purpose of this interface is to allow generic algorithms to alter their
 * behavior to provide good performance when applied to either random or
 * sequential access lists.
 */
```



properties

```java
/**
* Default initial capacity.
*/
private static final int DEFAULT_CAPACITY = 10;

```

the array into which the element of the arraylist are stored

```java
/**
     * The array buffer into which the elements of the ArrayList are stored.
     * The capacity of the ArrayList is the length of this array buffer. Any
     * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
     * will be expanded to DEFAULT_CAPACITY when the first element is added.
     */
    transient Object[] elementData; // non-private to simplify nested class access
```

# Map

## HashMap

Entry<K,V> tab

int size;

int capacity;

int threshold;

threshold = capacity * 0.75f;

DEFAULT_INITILAL_CAPACITY = 0.75f;



treeify = 8 

链表化  6;

[红黑树参考笔记](../ComputerSimple/DataStructure.md)

```java

```

## LinkedHashMap

```java
LinkedHashMap extends HashMap implements Map
```



accessOrder属性

- true  顺序会根据获取而改动
- false 默认的，插入顺序



```java
/**
 * HashMap.Node subclass for normal LinkedHashMap entries.
 */
static class Entry<K,V> extends HashMap.Node<K,V> {
    Entry<K,V> before, after;
    Entry(int hash, K key, V value, Node<K,V> next) {
        super(hash, key, value, next);
    }
}

/**
     * The head (eldest) of the doubly linked list.
     */
    transient LinkedHashMap.Entry<K,V> head;

    /**
     * The tail (youngest) of the doubly linked list.
     */
    transient LinkedHashMap.Entry<K,V> tail;
```



收尾引用，内部存储结构仍然是数组 + 链表 + 红黑树结构





实现LRU算法：

```java
void afterNodeAccess(Node<K,V> e) { // move node to last
    LinkedHashMap.Entry<K,V> last;
    if (accessOrder && (last = tail) != e) {
        LinkedHashMap.Entry<K,V> p =
            (LinkedHashMap.Entry<K,V>)e, b = p.before, a = p.after;
        p.after = null;
        if (b == null)
            head = a;
        else
            b.after = a;
        if (a != null)
            a.before = b;
        else
            last = b;
        if (last == null)
            head = p;
        else {
            p.before = last;
            last.after = p;
        }
        tail = p;
        ++modCount;
    }
}
```







# Set

## HashSet

底层用的是HashMap来存储

对象hashcode 作为key 存储在HashMap中