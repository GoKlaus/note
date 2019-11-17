# Collection学习

[toc]

## List

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

