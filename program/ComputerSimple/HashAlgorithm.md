# Hash算法

[toc]



## 参考资料

[Hash算法总结]( https://www.jianshu.com/p/bf1d7eee28d0 )

一个优秀的hash算法，将能实现：

- 正向快速：给定明文和hash算法，在有限的时间和有限的资源内能计算出hash值
- 逆向困难：给定若干hash值，在有限的时间内很难（基本不可能）逆推出明文
- 输入敏感：原始输入信息修改一点信息，产生的hash值看起来应该有很大的不同
- 冲突避免：很难找到两端内容不同的明文，使得他们的hash值一致（产生冲突）。对于两个不同的数据块，其hash值相同的可能性很小；对于一个给定的数据块，找到和他hash值相同的数据块极为困难



## java中没有重写hashCode方法的类

没有重写hashCode方法的类，默认继承的是Object的native int hashCode()方法源码如下：

```java
/**
     * Returns a hash code value for the object. This method is
     * supported for the benefit of hash tables such as those provided by
     * {@link java.util.HashMap}.
     * <p>
     * The general contract of {@code hashCode} is:
     * <ul>
     * <li>Whenever it is invoked on the same object more than once during
     *     an execution of a Java application, the {@code hashCode} method
     *     must consistently return the same integer, provided no information
     *     used in {@code equals} comparisons on the object is modified.
     *     This integer need not remain consistent from one execution of an
     *     application to another execution of the same application.
     * <li>If two objects are equal according to the {@code equals(Object)}
     *     method, then calling the {@code hashCode} method on each of
     *     the two objects must produce the same integer result.
     * <li>It is <em>not</em> required that if two objects are unequal
     *     according to the {@link java.lang.Object#equals(java.lang.Object)}
     *     method, then calling the {@code hashCode} method on each of the
     *     two objects must produce distinct integer results.  However, the
     *     programmer should be aware that producing distinct integer results
     *     for unequal objects may improve the performance of hash tables.
     * </ul>
     * <p>
     * As much as is reasonably practical, the hashCode method defined by
     * class {@code Object} does return distinct integers for distinct
     * objects. (This is typically implemented by converting the internal
     * address of the object into an integer, but this implementation
     * technique is not required by the
     * Java&trade; programming language.)
     *
     * @return  a hash code value for this object.
     * @see     java.lang.Object#equals(java.lang.Object)
     * @see     java.lang.System#identityHashCode
     */
    public native int hashCode();
```



==默认情况下，hashCode方法是将对象的存储地址进行映射==



查看hashmap的源码：

```java
public V put(K key, V value) {
        return putVal(hash(key), key, value, false, true);
    }

final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e; K k;
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            else if (p instanceof TreeNode)
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
        if (++size > threshold)
            resize();
        afterNodeInsertion(evict);
        return null;
    }
```



## Hash在管理数据结构中的应用

在用到hash进行管理的数据结构中，就对速度比较重视，对抗碰撞不太看中，只要保证hash均匀分布就可以。比如hashmap，hash值（key）存在的目的是加速键值对的查找，key的作用是为了将元素适当地放在各个桶里，对于抗碰撞的要求没有那么高。换句话说，hash出来的key，只要保证value大致均匀的放在不同的桶里就可以了。但整个算法的set性能，直接与hash值产生的速度有关，所以这时候的hash值的产生速度就尤为重要，以JDK中的String.hashCode()方法为例：

 ![img](HashAlgorithm.assets/Hash_table.png) 



## Hash有哪些流行的算法

目前流行的 Hash 算法包括 MD5、SHA-1 和 SHA-2。

- MD4（RFC 1320）是 MIT 的 Ronald L. Rivest 在 1990 年设计的，MD 是 Message Digest 的缩写。其输出为 128 位。MD4 已证明不够安全。
- MD5（RFC 1321）是 Rivest 于1991年对 MD4 的改进版本。它对输入仍以 512 位分组，其输出是 128 位。MD5 比 MD4 复杂，并且计算速度要慢一点，更安全一些。MD5 已被证明不具备"强抗碰撞性"。
- SHA （Secure Hash Algorithm）是一个 Hash 函数族，由 NIST（National Institute of Standards and Technology）于 1993 年发布第一个算法。目前知名的 SHA-1 在 1995 年面世，它的输出为长度 160 位的 hash 值，因此抗穷举性更好。SHA-1 设计时基于和 MD4 相同原理，并且模仿了该算法。SHA-1 已被证明不具"强抗碰撞性"。
- 为了提高安全性，NIST 还设计出了 SHA-224、SHA-256、SHA-384，和 SHA-512 算法（统称为 SHA-2），跟 SHA-1 算法原理类似。SHA-3 相关算法也已被提出。

可以看出，上面这几种流行的算法，它们最重要的一点区别就是"强抗碰撞性"

## Hash算法的==碰撞==

对于不同的



## Hash在Java中的应用

### HashMap的复杂度

在介绍HashMap的实现之前，先考虑一下，HashMap与ArrayList和LinkedList在数据复杂度上有什么区别。下图是他们的性能对比图：

| 获取       | 查找             | 添加/删除        | 空间             |      |
| ---------- | ---------------- | ---------------- | ---------------- | ---- |
| ArrayList  | O(1)             | O(1)             | O(N)             | O(N) |
| LinkedList | O(N)             | O(N)             | O(1)             | O(N) |
| HashMap    | O(N/Bucket_size) | O(N/Bucket_size) | O(N/Bucket_size) | O(N) |

可以看出HashMap整体上性能都非常不错，但是不稳定，为O(N/Buckets)，N就是以数组中没有发生碰撞的元素，==Buckets是因碰撞产生的链表==。

HashMap是对Array与Link的折衷处理，Array与Link可以说是两个速度方向的极端，Array注重于数据的获取，而处理修改（添加/删除）的效率非常低；Link由于是每个对象都保持着下一个对象的指针，查找某个数据需要遍历之前所有的数据，所以效率比较低，而在修改操作中比较快。

