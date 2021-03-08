# 容器
## HashMap
```
存放元素（jdk1.8为例）
putval的 方法的主要逻辑：
    1. 如果数组还没有初始化，则先初始化，
    2. 通过hash算法，计算key的hash值，进而计算应该放置到数组的位置
    3. 如果位置为空，则直接放置，
    4. 如果元素不为空，而且是红黑树，则将元素插入其中
    5. 如果是链表，则遍历链表，如果找到相等的元素则替换，否则插入到链表尾部
    6. 如果链表的长度大于或者等于8，则将链表转为红黑树
```
```java
hashmap.put("key","value")


public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}

/**
*
*对key进行hash运算：自己的高半区和低半区做异或，就是为了混合原始哈希码的高位和低位，以此来加大低位的随机*性。而且混合后的低位掺杂了高位的部分特征，这样高位的信息*也被变相保留下来。
*目的:是为了尽可能少的减少hash碰触
*/

static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }

 


    final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; //用来存放元素Node数组
         Node<K,V> p; //用来存放要存入的元素
         int n, i;
         //第一次put的时候table是空数组，初使容量是16 阈值：16*0.75 =12
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        //计算key在Node[]数组中的位置
        if ((p = tab[i = (n - 1) & hash]) == null)
        //如果这个位置没有值，则将这个数据放入Node[i]位置
        //备注：如果线程A 和线程B同时进行put操作，刚好两个不同的数据hash值一样，并且该位置的数据是null，则会出现数据覆盖的情况，这也是jdk 1.8hashmap的问题
            tab[i] = newNode(hash, key, value, null);
        else {
          //如果这个地方已经有元素 
            Node<K,V> e;
             K k;
             //判断发生碰撞的key hash值是否相同 ，key是否相等
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                //如果相等  则替换
                e = p;
            else if (p instanceof TreeNode)
             // 如果该元素是红黑树则插入到红黑树中  
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                
                for (int binCount = 0; ; ++binCount) {
                    //如果是链表，则遍历 找到则替换，否则插入到链表的尾部
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        //当长度大于 8时，则将这个链表转成红黑树
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
        // 容器内的元素的数量是否 超过 要调整大小的下一个大小值（容量*负载系数）。
        if (++size > threshold)
            //扩容，resize（）
            resize();
        afterNodeInsertion(evict);
        return null;

    }



      /**
     * 初始化或增加表大小。 如果为空，则根据字段阈值中保持的初始容量目标进行分配。 否则，因为我们使用的是2的幂，所以每个bin中的元素必须保持相同的索引，或者在新表中以2的幂偏移。
     *  以2倍的大小 扩容
     * @return the table
     */
    final Node<K,V>[] resize() {
        Node<K,V>[] oldTab = table;
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        int oldThr = threshold;
        int newCap, newThr = 0;
        if (oldCap > 0) {
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        else {               // zero initial threshold signifies using defaults
            newCap = DEFAULT_INITIAL_CAPACITY;
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        @SuppressWarnings({"rawtypes","unchecked"})
            Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
        table = newTab;
        if (oldTab != null) {
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e;
                    else if (e instanceof TreeNode)
                    //如果是一个红黑树，会判断红黑树的长度，小于6，则将红黑树转为链表
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    else { // preserve order
                    //如果扩容后元素的index 与原来一样 则使用loHead和loTail指针
                        Node<K,V> loHead = null, loTail = null;
                    //如果扩容后元素的index = index+oldCap 则使用hiHead 和hiHead指针
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                            // 这个地方直接通过
                            if ((e.hash & oldCap) == 0) {
                                if (loTail == null)
                                    loHead = e;
                                else
                                //新的节点放置末尾
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                //新的节点放置末尾
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            //还是原来的index
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                            // index 变为index + oldCap
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }

```

### 获取元素（jdk1.8为例）
```
    获取元素
    1.计算hash值，看第一个元素是不是要找的元素，是则返回，否则遍历
```
```java
 public V get(Object key) {
        Node<K,V> e;
        return (e = getNode(hash(key), key)) == null ? null : e.value;
    }

    /**
     * Implements Map.get and related methods
     *
     * @param hash hash for key
     * @param key the key
     * @return the node, or null if none
     */
    final Node<K,V> getNode(int hash, Object key) {
        Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
        if ((tab = table) != null && (n = tab.length) > 0 &&
            (first = tab[(n - 1) & hash]) != null) {
            if (first.hash == hash && // always check first node
                ((k = first.key) == key || (key != null && key.equals(k))))
                return first;
            if ((e = first.next) != null) {
                if (first instanceof TreeNode)
                    return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                do {
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        return e;
                } while ((e = e.next) != null);
            }
        }
        return null;
    }

```





## concurcentHashMap 是如何实现线程安全的


```
    jdk1.8 concurrentHashMap 文档提炼
    1. CoucurrentHashMap支持检索的完全并发和更新的高预期并发性，这里的说法很有意思，检索支持完全并发，更新则支持高预期并发性，因为检索操作是没有加锁，实际上检索操作也没有必要加锁
    2. 实际上ConcurrentHashMap和HashTable在不考虑实现细节上来说，这两者完全可以相互操作的，hashTable在get ，put ，remove等这些方法实现中全部加入了synchroized，这样的问题是能够实现线程安全，但是缺点是性能太差，几乎所有的操作都加锁，ConcurrentHashMap的检测操作却是没有加锁的
    3. ConcurrentHashMap检索操作（包括get）通常不会阻塞，因此可以与更新操作（put、remove）重叠。
    4. ConcurrentHashMap跟HashTable类似，但是不同于HashMap，它不可以存放空值


    其实ConcirrentHashMap保证线程安全主要有三个地方
    一. 使用volatile保证Node中的值变化时，对其他线程是可见的
    二. 使用table数组的头节点作为synchronize的锁来保证写操作是安全的
    三. 当头节点是null时，使用cas操作来保证数据能正确的写入
```
```java

    //可以看到，Node中饿val和next都被volatile修饰
    

   static class Node<K,V> implements Map.Entry<K,V> {
       
        final int hash;
        final K key;
        volatile V val;
        volatile Node<K,V> next;

        Node(int hash, K key, V val, Node<K,V> next) {
            this.hash = hash;
            this.key = key;
            this.val = val;
            this.next = next;
        }

        public final K getKey()       { return key; }
        public final V getValue()     { return val; }
        public final int hashCode()   { return key.hashCode() ^ val.hashCode(); }
        public final String toString(){ return key + "=" + val; }
        public final V setValue(V value) {
            throw new UnsupportedOperationException();
        }

        public final boolean equals(Object o) {
            Object k, v, u; Map.Entry<?,?> e;
            return ((o instanceof Map.Entry) &&
                    (k = (e = (Map.Entry<?,?>)o).getKey()) != null &&
                    (v = e.getValue()) != null &&
                    (k == key || k.equals(key)) &&
                    (v == (u = val) || v.equals(u)));
        }

        /**
         * Virtualized support for map.get(); overridden in subclasses.
         */
        Node<K,V> find(int h, Object k) {
            Node<K,V> e = this;
            if (k != null) {
                do {
                    K ek;
                    if (e.hash == h &&
                        ((ek = e.key) == k || (ek != null && k.equals(ek))))
                        return e;
                } while ((e = e.next) != null);
            }
            return null;
        }
    }

    public V put(K key, V value) {
        return putVal(key, value, false);
    }

    /** Implementation for put and putIfAbsent */
    final V putVal(K key, V value, boolean onlyIfAbsent) {
        if (key == null || value == null) throw new NullPointerException();
        int hash = spread(key.hashCode());
        int binCount = 0;
        for (Node<K,V>[] tab = table;;) {
            Node<K,V> f; int n, i, fh;
            if (tab == null || (n = tab.length) == 0)
                tab = initTable();
            else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) {
                if (casTabAt(tab, i, null,
                             new Node<K,V>(hash, key, value, null)))
                    break;                   // no lock when adding to empty bin
            }
            else if ((fh = f.hash) == MOVED)
                tab = helpTransfer(tab, f);
            else {
                V oldVal = null;
                synchronized (f) {
                    if (tabAt(tab, i) == f) {
                        if (fh >= 0) {
                            binCount = 1;
                            for (Node<K,V> e = f;; ++binCount) {
                                K ek;
                                if (e.hash == hash &&
                                    ((ek = e.key) == key ||
                                     (ek != null && key.equals(ek)))) {
                                    oldVal = e.val;
                                    if (!onlyIfAbsent)
                                        e.val = value;
                                    break;
                                }
                                Node<K,V> pred = e;
                                if ((e = e.next) == null) {
                                    pred.next = new Node<K,V>(hash, key,
                                                              value, null);
                                    break;
                                }
                            }
                        }
                        else if (f instanceof TreeBin) {
                            Node<K,V> p;
                            binCount = 2;
                            if ((p = ((TreeBin<K,V>)f).putTreeVal(hash, key,
                                                           value)) != null) {
                                oldVal = p.val;
                                if (!onlyIfAbsent)
                                    p.val = value;
                            }
                        }
                    }
                }
                if (binCount != 0) {
                    if (binCount >= TREEIFY_THRESHOLD)
                        treeifyBin(tab, i);
                    if (oldVal != null)
                        return oldVal;
                    break;
                }
            }
        }
        addCount(1L, binCount);
        return null;
    }
```

