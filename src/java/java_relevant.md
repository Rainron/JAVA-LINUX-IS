# java_relevant
### 部分基于thinkinJava
### 部分基于清华大学许斌教授授课内容
### 部分基于深入了解java虚拟机
### 目录结构
### - [0. 面向对象概述](#0-面向对象概述)
### - [1.Static Final 关键字](#1-Static_Final关键字)
### - [2.Java常用数组](#2-Java常用数组)
### - [3.Java中的线程](#3-Java中的线程)
### - [4.Java虚拟机](#4-Java虚拟机)
### - [5.Java中的反射](#5-Java中的反射)

## 0-面向对象概述
- ### 一切都是对象</br>
  * 在java中一切都被视为对象，因此可采用单一固定的语法。尽管一切都看成对象，但操纵的标识符实际上是对象的一个"引用"。可以将此情形想象为"遥控器"(引用)与"电视机"(对象)，只要握住这个遥控器，就能保持与电视机连接.当想减少音量，实际操控的是"遥控器"(引用)，在由遥控器来控制"电视机"(对象)如果你想在房间里面到处走走，同时可以控制"电视机"，那么只需要携带"遥控器"(引用)，而不是电视机(对象)此外，即使没有电视机，遥控器也可以独立存在，也就是说，你拥有一个引用，并不一定需要有一个对象与它关联。像这样创建一个引用:String s;但这里创建非只是引用，并不是对象。如果这是向s发送一个消息，就会返回一个运行时的错误。因为这会s实际并没有与任何事物关联。

- **0.1 封装**</br>
  * **封装**是保证软件部件具有优良的模块性的基础，封装的目标就是要实现软件部件的“高内聚、低耦合”，防止程序相互依赖性而带来的变动影响。在面向对象的编程语言中，对象是封装的最基本单 位，面向对象的封装比传统语言的封装更为清晰、更为有力。面向对象的封装就是把描述一个对象的属性和行为的代码封装在一个“模块”中，也就是一个类中，属性用变量定义，行为用方法进行定义，方法可以直接访问同一个对象中的属性。把握一个原则：把对同一事物进行操作的方法和相关的方法放在同一个类中，把方法和它操作的数据放在同一个类中。 
- **0.2 继承**</br>
  * 在创建一个类之后，即使另一个新类与其具有相似的功能(但还是有一些不同的地方)，你还是等创建一个新类。如果能以现有的类为基础，复制它，然后通过添加和修改这个 副本 来创建新类就要好多了。通过继承就可以达到这种效果，不过也有例外，当源类(被称为基类，超类或父类)发生变动时，"被修改的副本"(被称为导出类，继承类或子类)也会变动。继承是子类自动共享父类数据和方法的机制，这是类之间的一种关系，提高了软件的可重用性和可扩展性。 

- **0.3 多态**</br>
  * **多态**是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时 并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量 发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才 确定具体的类，这样，不用修改源程序代码，就可以让引用变量绑定到各种不同的类实现上，从 而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具体代码，让程序可以选择多个运行状态，这就是多态性。

## 1-Static_Final关键字
- ### **1.1 Static**</br>
* 通过static关键字可以满足下面两个方面的需要:
  * (1).只想为某特定域分配单一的存储空间，而不去考虑要创建多少对象，甚至根本不需要创建任何的对象
  * (2).希望某个方法不与这个类型的任何对象相关联
```java
package cn.test;

class Demo{
    public static int i = 1;
}

public class staticDemo {
    private static Demo demo1 = new Demo();
    private static Demo demo2 = new Demo();
    public static void main(String[] args){
        System.out.println(Demo.i);     //1
        System.out.println(demo1.i);    //1
        System.out.println(demo2.i);    //1
        demo1.i++;
        System.out.println(Demo.i);     //2
        System.out.println(demo1.i);    //2
        System.out.println(demo2.i);    //2
        Demo.i++;
        System.out.println(Demo.i);     //3
        System.out.println(demo1.i);    //3
        System.out.println(demo2.i);    //3
    }
}
```

### **1.2 Final**</br>
* 一般来说final关键字主要以下三个方面:
  * (1).声明数据为常量，可以是编译时常量，也可以是在运行时被初始化后不能被改变的常量。
  * (2).声明方法不能被子类覆盖。
  * (3).声明类不允许被继承。

## 2-Java常用数组
- ### **2.1 集合框架关联图**</br>
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/Collections.jpg)
 * Java 集合框架主要包括两种类型的容器，一种是集合（Collection），存储一个元素集合，另一种是图（Map），存储键/值对映射。Collection 接口又有 3 种子类型，List、Set 和 Queue，再下面是一些抽象类，最后是具体实现类，常用的有 ArrayList、LinkedList、HashSet、LinkedHashSet、HashMap、TreeMap、LinkedHashMap 等等。

- **2.2 List列表**</br>
 * List的特征是其元素**以线性方式存储，列表中可以存放重复对象**。
 * List接口主要实现类包括ArrayList()-LinkedList()。
 * 次序是List最重要的特点：它保证维护元素特定的顺序。List为Collection添加了许多方法，使得能够向List中间插入与移除元素(这只推 荐LinkedList使用。)一个List可以生成ListIterator,使用它可以从两个方向遍历List,也可以从List中间插入和移除元素。 
   * **ArrayList**：由数组实现的List。允许对元素进行快速随机访问，但是向List中间插入与移除元素的速度很慢。
   * **LinkedList** ：对顺序访问进行了优化，向List中间插入与删除的开销并不大。随机访问则相对较慢。还具有下列方法：addFirst(),addLast(), getFirst(), getLast(), removeFirst() 和 removeLast(), 这些方法使得LinkedList可以当作堆栈、队列和双向队列使用。
 * 源码实现及对比(版本JDK1.8)
 ```java
 ArrayList
 插入
 private static final int DEFAULT_CAPACITY = 10; 默认大小
 
 public boolean add(E e) {
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        elementData[size++] = e;
        return true;
}
ensureCapacityInternal->ensureExplicitCapacity->grow
 private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
上述add方法，主要是将e赋值给数组，将数组长度加一，ensureCapacityInternal里面做一些逻辑判断。
添加元素时使用 ensureCapacityInternal() 方法来保证容量足够，如果不够时，需要使用 grow() 方法进行扩容，
新容量的大小为 oldCapacity + (oldCapacity >> 1)，也就是旧容量的 1.5 倍。
扩容操作需要调用 Arrays.copyOf() 把原数组整个复制到新数组中，这个操作代价很高，会消耗大量的资源，导致性能变的很差。
因此最好在创建 ArrayList 对象时就指定大概的容量大小，减少扩容操作的次数。


指定插入
public void add(int index, E element) {
        rangeCheckForAdd(index);
  
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index);
        elementData[index] = element;
        size++;
}
主要操作为将indez+1后的元素后移，然后设置当前index为插入的元素
大量copy导致大量的数组移动，导致性能底下。remove方法与add方法实现类似。
随机访问和遍历
public E get(int index) {
        rangeCheck(index);
        return elementData(index);
}
直接指向数组下标位置的元素返回。

public E remove(int index) {
    rangeCheck(index);
    modCount++;
    E oldValue = elementData(index);
    int numMoved = size - index - 1;
    if (numMoved > 0)
        System.arraycopy(elementData, index+1, elementData, index, numMoved);
    elementData[--size] = null; // clear to let GC do its work
    return oldValue;
}
调用 System.arraycopy() 将 index+1 后面的元素都复制到 index 位置上，
把最后的index元素设置为NULL
该操作的时间复杂度为 O(N)，可以看出 ArrayList 删除元素的代价是非常高的。

Vector

1.它的实现与 ArrayList 类似，但是使用了 synchronized 进行同步。
2.Vector 是同步的，因此开销就比 ArrayList 要大，访问速度更慢，
最好使用 ArrayList 而不是 Vector，因为同步操作完全可以由程序员自己来控制；
3.Vector 每次扩容请求其大小的 2 倍空间，而 ArrayList 是 1.5 倍。
4.可以使用 Collections.synchronizedList(); 得到一个线程安全的 ArrayList。
List<String> list = new CopyOnWriteArrayList<>();
写操作在一个复制的数组上进行，读操作还是在原始数组中进行，读写分离，互不影响。
写操作需要加锁，防止并发写入时导致写入数据丢失。
写操作结束之后需要把原始数组指向新的复制数组。
CopyOnWriteArrayList 在写操作的同时允许读操作，大大提高了读操作的性能，因此很适合读多写少的应用场景。




LinkedList
内部有两个Node对象，一个指向集合第一个，一个指向最后一个。
private static class Node<E> {
        E item;
        Node<E> next;
        Node<E> prev;
  
        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
}

public boolean add(E e) {
        linkLast(e);
        return true;
}
void linkLast(E e) {
        final Node<E> l = last;
        final Node<E> newNode = new Node<>(l, e, null);
        last = newNode;
        if (l == null)
            first = newNode;
        else
            l.next = newNode;
        size++;
        modCount++;
}
普通的add会调用linkLast,linkdLast方法内部会新建一个Node对象，将要存储的值放入node中，
同时把当前的node绑定到集合最末端，算法时间复杂度为O(n)，数量增大n倍所需要的时间增加n倍。
指定插入



 
public void add(int index, E element) {
        checkPositionIndex(index);
  
        if (index == size)
            linkLast(element);
        else
            linkBefore(element, node(index));
}
void linkBefore(E e, Node<E> succ) {
        // assert succ != null;
        final Node<E> pred = succ.prev;
        final Node<E> newNode = new Node<>(pred, e, succ);
        succ.prev = newNode;
        if (pred == null)
            first = newNode;
        else
            pred.next = newNode;
        size++;
        modCount++;
}

Node<E> node(int index) {
        // assert isElementIndex(index);
        if (index < (size >> 1)) {
            Node<E> x = first;
            for (int i = 0; i < index; i++)
                x = x.next;
            return x;
        } else {
            Node<E> x = last;
            for (int i = size - 1; i > index; i--)
                x = x.prev;
            return x;
        }
 }
当需要插入的位置为集合大小时，可以直接插入集合尾部，
不是则检索出index的node节点，根据判断index是在size/2的左边还是右边来进行两端遍历，这样让遍历的查找时间降到最低。
拿到node节点后，如果当前节点的上节点为NULL则插入的节点为头节点
否则把node节点的上节点的下节点设置为插入的节点。
node的下节点的上节点设置为插入的节点，JDK1.7源码比较好分析。

get方法remove方法与add方法实现类似。
public E get(int index) {
        checkElementIndex(index);
        return node(index).item;
}
get()会检查索引是否大于等0并是否小于原Node数组大小  是则抛出IndexOutOfBoundsException

 ```


- ### **2.3 Set集合**</br>
 * Set是最简单的一种集合。集合中的对象**不按特定的方式排序，并且没有重复对象**。 Set接口主要实现了两个实现类。
   * **HashSet**类按照哈希算法来存取集合中的对象，存取速度比较快，基于hashMap,底层使用HashMap保存所有元素。
   * **TreeSet**类实现了SortedSet接口，能够对集合中的对象进行排序。 
 * 源码实现及对比
 ```java
private transient HashMap<E,Object> map;
//定义一个Object对象作为HashMap的value
private static final Object PRESENT = new Object();

相关方法
iterator() set 中元素进行迭代的迭代器。返回元素的顺序并不是特定的
size()set 中的元素的数量（set 的容量）
isEmpty()判断集合为空
contains()判断集合存在某个元素
clear()底层调用HashMap的clear方法清除所有的Entry
插入基于map的put方法
public boolean add(E e) {
        return map.put(e, PRESENT)==null;
}

public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}

map的put方法：1.7版本比1.8的版本比较好阅读理解
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
               boolean evict) {
    Node<K,V>[] tab; Node<K,V> p; int n, i;

    //初始化数组长度 table 的容量大小，默认为 16。需要注意的是 capacity 必须保证为 2 的 n 次方。
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length;

    //找到具体的数组下标，如果此位置没有值，那么直接初始化一下 Node 并放置在这个位置
    if ((p = tab[i = (n - 1) & hash]) == null)
        tab[i] = newNode(hash, key, value, null);
    else {
        Node<K,V> e; K k;
        //判断该位置的第一个数据和我们要插入的数据，key 是不是"相等"，如果是，取出这个节点
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))
            e = p;
        //判断是否是红黑树情况
        else if (p instanceof TreeNode)
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        else {
            //如果key不相等，则连成链表
            for (int binCount = 0; ; ++binCount) {
                if ((e = p.next) == null) {
                   //插入链表的最后面
                    p.next = newNode(hash, key, value, null);
                    if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                        treeifyBin(tab, hash);
                    break;
                }
                // 如果在该链表中找到了相等的 key(== 或 equals)
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    break;
                //那么e为链表中[与要插入的新值的key相等的node
                p = e;
            }
        }
        //如果插入的key值与Node中存在key值相同则进行值覆盖并返回
        if (e != null) { // existing mapping for key
            V oldValue = e.value;
            if (!onlyIfAbsent || oldValue == null)
                e.value = value;
            afterNodeAccess(e);
            return oldValue;
        }
    }
    //假如插入这个值导致 size 已经超过了阈值，需要进行扩容
    //resize() 方法用于初始化数组或数组扩容，每次扩容后，容量为原来的 2 倍，并进行数据迁移。
    //，需要注意的是，扩容操作同样需要把 oldTable 的所有键值对重新插入 newTable 中，因此这一步是很费时的。
    ++modCount;
    if (++size > threshold)
        resize();
    afterNodeInsertion(evict);
    return null;
}

hashset不允许重复的元素加入，但允许元素连成链表，因为只要key的equals方法判断为true时它们是相等的，
此时会发生value的替换，因为所有entry的value一样，所以和没有插入时一样的。

TreeSet
与HashSet是基于HashMap实现一样，TreeSet同样是基于TreeMap实现的。
TreeMap是一个有序的二叉树，那么同理TreeSet同样也是一个有序的，它的作用是提供有序的Set集合。
通过源码知道TreeSet基础AbstractSet，实现NavigableSet、Cloneable、Serializable接口。
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable
{
    private transient NavigableMap<E,Object> m;
    private static final Object PRESENT = new Object();

    TreeSet(NavigableMap<E,Object> m) {
        this.m = m;
    }

    public TreeSet() {
        this(new TreeMap<E,Object>());
    }
}
public boolean add(E e) {
        return m.put(e, PRESENT)==null;
 }

public V put(K key, V value) {
    Entry<K,V> t = root;
    if (t == null) {
    //空树时，判断节点是否为空
        compare(key, key); // type (and possibly null) check

        root = new Entry<>(key, value, null);
        size = 1;
        modCount++;
        return null;
    }
    int cmp;
    Entry<K,V> parent;
    // split comparator and comparable paths
    Comparator<? super K> cpr = comparator;
    //非空树，根据传入比较器进行节点的插入位置查找
    if (cpr != null) {
        do {
            parent = t;
            //节点比根节点小，则找左子树，否则找右子树
            cmp = cpr.compare(key, t.key);
            if (cmp < 0)
                t = t.left;
            else if (cmp > 0)
                t = t.right;
                //如果key的比较返回值相等，直接更新值（一般compareto相等时equals方法也相等）
            else
                return t.setValue(value);
        } while (t != null);
    }
    else {
    //如果没有传入比较器，则按照自然排序
        if (key == null)
            throw new NullPointerException();
        @SuppressWarnings("unchecked")
            Comparable<? super K> k = (Comparable<? super K>) key;
        do {
            parent = t;
            cmp = k.compareTo(t.key);
            if (cmp < 0)
                t = t.left;
            else if (cmp > 0)
                t = t.right;
            else
                return t.setValue(value);
        } while (t != null);
    }
    //查找的节点为空，直接插入，默认为红节点
    Entry<K,V> e = new Entry<>(key, value, parent);
    if (cmp < 0)
        parent.left = e;
    else
        parent.right = e;
        //插入后进行红黑树调整
    fixAfterInsertion(e);
    size++;
    modCount++;
    return null;
}    
```
## **2.4 Map映射**</br>
 * **Map 是一种把键对象和值对象映射的集合,它的每一个元素都包含一对键对象和值对象**。
 * 标准的Java类库中包含了几种不同的Map：HashMap, TreeMap, LinkedHashMap, WeakHashMap, IdentityHashMap。它们都有同样的基本接口Map，但是行为、效率、排序策略、保存对象的生命周期和判定“键”等价的策略等各不相同。
   * **HashMap**：就是使用对象的hashCode()进行快速查询的。此方法能够显著提高性能，同时基于散列表的实现。插入和查询“键值对”的开销是固定的。可以通过构造器设置容量capacity和负载因子load factor，以调整容器的性能。
   * **LinkedHashMap**：类似于HashMap，但是迭代遍历它时，取得“键值对”的顺序是其插入次序，或者是最近最少使用(LRU)的次序。只比HashMap慢一点。而在迭代访问时发而更快，因为它使用链表维护内部次序。
   * **TreeMap**：基于红黑树数据结构的实现。查看“键”或“键值对”时，它们会被排序(次序由Comparabel或Comparator决定)。TreeMap的特点在于，你得到的结果是经过排序的。TreeMap是唯一的带有subMap()方法的Map，它可以返回一个子树。
   * **WeakHashMao**：弱键(weak key)Map，Map中使用的对象也被允许释放: 这是为解决特殊问题设计的。如果没有map之外的引用指向某个“键”，则此“键”可以被垃圾收集器回收。 
   * **IdentifyHashMap**： 使用==代替equals()对“键”作比较的hashmap，专为解决特殊问题而设计。

### 这里选取HashMap TreeMap简单概述
 
- ### **2.4.1HashMap**：
* **以数组方式存储key/value，线程非安全，允许null作为key和value，key不可以重复，value允许重复，不保证元素迭代顺序是按照插入时的顺序，key的hash值是先计算key的hashcode值，然后再进行计算，每次容量扩容会重新计算所以key的hash值，会消耗资源，要求key必须重写equals和hashcode方法。**
* **哈希函数**：这个函数的设计好坏会直接影响到哈希表的优劣。
* **哈希冲突**：两个不同的元素，计算出来的实际存储地址一样。
* 哈希冲突的解决方案有多种:开放定址法（发生冲突，继续寻找下一块未被占用的存储地址），再散列函数法，链地址法，而HashMap即是采用了链地址法，也就是数组+链表的方式。

```java
HashMap的主干是一个Node数组。Node是HashMap的基本组成单元，每一个Node包含一个key-value键值对。
static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;//计算好的的元素hash（实际存储地址）
        final K key;
        V value;
        Node<K,V> next;//存储指向下一个Node的引用，单链表结构

        Node(int hash, K key, V value, Node<K,V> next) {
            this.hash = hash;
            this.key = key;
            this.value = value;
            this.next = next;
        }
 }
```
### hashMap大体上结构
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/hashMap.jpg)
* **HashMap**由数组+链表组成的，数组是HashMap的主体，链表则是主要为了解决哈希冲突而存在的，如果定位到的数组位置不含链表（当前entry的next指向null）,那么对于查找，添加等操作很快，仅需一次寻址即可；如果定位到的数组包含链表，对于添加操作，其时间复杂度为O(n)，首先遍历链表，存在即覆盖，否则新增；对于查找操作来讲，仍需遍历链表，然后通过key对象的equals方法逐一比对查找。所以，性能考虑，HashMap中的链表出现越少，性能才会越好。
* 插入元素put方法与上述hashSet一样，这里不再说明。
```java
* 计算 key 的 hash 值，根据 hash 值找到对应数组下标: hash & (length-1)
* 判断数组该位置处的元素是否刚好就是我们要找的，如果不是，走第三步
* 判断该元素类型是否是 TreeNode，如果是，用红黑树的方法取数据，如果不是，走第四步
* 遍历链表，直到找到相等的hash相等及等价的key
get()根据key获取value
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
* 简单了解了hashMap的实现原理及源码，就可以知道重写equals方法需同时重写hashCode方法。
  * 1.如果两个对象相同（即用equals比较返回true），那么它们的hashCode值一定要相同。
  * 2.如果两个对象的hashCode相同，它们并不一定相同(即用equals比较返回false)。
* 因此为了保证同一个对象，保证在equals相同的情况下hashcode值必定相同，如果重写了equals而未重写hashcode方法，可能就会出现两个没有关系的对象equals相同的（因为equal都是根据对象的特征进行重写的），但hashcode确实不相同的。
- ### 2.4.2TreeMap：
* **treeMap**在源码中实现NavigableMap接口并且也是基于红黑树的实现。
* **treeMap**可以对添加进来的元素进行排序，可以按照默认的排序方式，也可以自己指定排序方式,所以最重要的特点是可排序。
* 红黑树简单概述
  * 红黑树顾名思义就是节点是红色或者黑色的平衡二叉树，它通过颜色的约束来维持着二叉树的平衡。
  * 根节点是黑色，每个节点都只能是红色或者黑色。
  * 如果一个结点是红的，则它两个子节点都是黑的。也就是说在一条路径上不能出现相邻的两个红色结点。
  * 从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点。

```java
查看源码中的put()
public V put(K key, V value) {
        Entry<K,V> t = root;
        //根节点为空则设置为新节点
        if (t == null) {
            compare(key, key); // type (and possibly null) check
            root = new Entry<>(key, value, null);
            size = 1;集合为1
            modCount++;结构次数修改+1
            return null;
        }
        int cmp;
        Entry<K,V> parent;
        // split comparator and comparable paths
        Comparator<? super K> cpr = comparator;指定比较器
        if (cpr != null) {
             do {
                parent = t;
                cmp = cpr.compare(key, t.key);
                if (cmp < 0)//插入的key于当前的key比较小于则查询左子树
                    t = t.left;
                else if (cmp > 0)//插入的key于当前的key比较大于则查询右子树
                    t = t.right;
                else
                    return t.setValue(value);//等于则把当前的v设置为插入的v
            } while (t != null);
        }
        else {//默认比较器
            if (key == null)
                throw new NullPointerException();
            @SuppressWarnings("unchecked")
                Comparable<? super K> k = (Comparable<? super K>) key;
            do {
                parent = t;
                cmp = k.compareTo(t.key);
                if (cmp < 0)
                    t = t.left;
                else if (cmp > 0)
                    t = t.right;
                else
                    return t.setValue(value);
            } while (t != null);
        }
        Entry<K,V> e = new Entry<>(key, value, parent);//最后根据key找到父节点后新建一个节点
        if (cmp < 0)
            parent.left = e;//同理如上  根据比较的结果放在根节点的左子树或右子树
        else
            parent.right = e;
        fixAfterInsertion(e);
        size++;
        modCount++;
        return null;
}

```
## 3-Java中的线程
-  ### **3.1 进程线程简单概述**</br>
* **进程**
  * 进程是资源（CPU、内存等）分配的基本单位，它是程序执行时的一个实例。每个进程都有独立的代码和数据空间（进程上下文），进程间的切换会有较大的开销，一个进程包含1--n个线程。
* **线程**
  * 是一个进程中的顺序执行流，同一类线程共享代码和数据空间，每个线程有独立的运行栈和程序计数器(PC)，线程切换开销小。
* 多进程是指操作系统能同时运行多个任务（程序），多线程是指在同一程序中有多个线程在执行，线程和进程一样分为五个阶段：创建、就绪、运行、阻塞、终止。
-  ### **3.2 创建线程的方法**</br>
* 扩展java.lang.Thread类以及实现java.lang.Runnable接口及重写它们中的run方法。
* 大多数会使用实现Runnable接口来创建线程，原因在于，java单继承语法的限制，如果使用继承Thread类，则后期代码重构及解耦可能会遇到很多问题。并且Runnable与其相比有比较大的优势，多个线程可以共享及处理同一数据，代码可读性扩展性较高等。
* Executor 管理多个异步任务的执行，而无需程序员显式地管理线程的生命周期。这里的异步是指多个任务的执行互不干扰，不需要进行同步操作。
```java
public static void main(String[] args) {
	ExecutorService threadPool = Executors.newFixedThreadPool(2);

	for(int i=0;i<5;i++){
		Runnable runn = new Runnable(){
			public void run(){
				Thread t = Thread.currentThread();
				System.out.println(t+":正在执行任务");
				try{
					Thread.sleep(3000);
					System.out.println(t+":运行任务完毕");
				}catch(InterruptedException e){
					System.out.println("线程被中断了");
				}
			}
		};
		threadPool.execute(runn);
	}
	//shutdown()当线程池所有任务执行完毕后停止
	//shutdownNow()立即中断所有正在运行的线程并停止线程池

	threadPool.shutdownNow();
	System.out.println("停止线程池");
}
```
-  ### **3.3 线程常用方法**</br>
* start() ：线程调用该方法将启动线程，使之从新建状态进入就绪队列排队，一旦轮到它来享用CPU资源时，就可以脱离创建它的线程独立开始自己的生命周期了。
* run(): Thread类的run()方法与Runnable接口中的run()方法的功能和作用相同，都用来定义线程对象被调度之后所执行的操作，都是系统自动调用而用户程序不得引用的方法。
* sleep(int millsecond): 优先级高的线程可以在它的run()方法中调用sleep方法来使自己放弃CPU资源，休眠一段时间。
* isAlive(): 线程处于“新建”状态时，线程调用isAlive()方法返回false。在线程的run()方法结束之前，即没有进入死亡状态之前，线程调用isAlive()方法返回true.
* currentThread():该方法是Thread类中的类方法，可以用类名调用，该方法返回当前正在使用CPU资源的线程。
* interrupt() ：一个占有CPU资源的线程可以让休眠的线程调用interrupt()方法“吵醒”自己，即导致休眠的线程发生InterruptedException异常，从而结束休眠，重新排队等待CPU资源。

-  ### **3.4 线程同步与互斥**</br>
* 为什么要**线程同步**，因为在多线程环境下，多线程共享同一数据或资源的时候，如果不进行同步，则会引发很严重的问题，比如如果这些线程中既有读又有写操作时，就会导致变量值或对象的状态出现混乱，从而导致程序异常。同步就是协同步调，按预定的先后次序进行运行。线程同步是指多线程通过特定的设置来控制线程之间的执行顺序（即所谓的同步）也可以说是在线程之间通过同步建立起执行顺序的关系。
* **线程互斥**表示，在多线程下共享某一数据及资源时候，同一时刻只允许一个线程进行访问使用。
-  ### **3.5 线程同步方法**</br>
* #### 3.5.1 java中的原生语法
  * **synchronized**（对象）即有synchronized关键字修饰的语句块。被该关键字修饰的语句块会自动被加上内置锁，从而实现同步
  * synchronized synchronized关键字修饰的方法。 由于java的每个对象都有一个内置锁，当用此关键字修饰方法时，内置锁会保护整个方法。在调用该方法前，需要获得内置锁，否则就处于阻塞状态，该线程放置在jvm中的获取锁的线程池中。
  * 在使用synchronized时候，应尽可能减少synchronized范围，因为线程同步会降低系统的并发性能。
* #### 3.5.2 java中的wait()notify()方法（必须在synchronized同步块使用）
  * **wait()** 方法会把当前的锁释放，然后让出CPU，进入等待状态。
  * **notify()** 方法会唤醒一个处于等待该对象锁的线程，然后继续往下执行，直到执行完退出对象锁锁住的区域（synchronized修饰的代码块）后再释放锁。
  * 当使用synchronized来修饰某一个共享资源时候，如果线程1在执行synchronized代码，另外一个线程2也要同时执行同一对象的同一synchronized代码时，线程2将要等到线程1执行完毕后才能执行。因此可以使用wait方法和notify方法。在synchronized代码执行期间，线程可以调用对象的wait方法，释放对象锁，进入等待状态，并且可以调用notify方法或notifyAll方法通知正在等待的其他线程，notify方法 仅唤醒一个等待这个对象的线程，并允许它去获得锁，而notifyAll方法唤醒所有等待这个对象的线程，并允许他们去获得锁（并不是让所有唤醒的线程都获得锁，而是让他们去竞争）。
* #### 3.5.3 javaAPI层ReentrantLock(重入锁)方法
  * JDK1.5新曾的新增了Lock接口以及他的实现类**ReentrantLock(重入锁)**,它与使用synchronized方法和快具有相同的基本行为和语义，并且扩展了其能力。
  * ReentrantLock(): 创建一个ReentrantLock实例 lock(): 获得锁 unlock(): 释放锁 
  * synchronized能够简化代码，快速使用同步，但经过测试，单核及单线程下synchronized与ReentrantLock的数据吞吐量大致相同，而在多核多线程下ReentrantLock的数据吞吐量远远大于synchronized，因此当使用高级的功能或者复杂的业务中建议使用ReentrantLock。
```java
public class LockDemo implements Runnable {

    private Lock lock = new ReentrantLock();
    private int tickets = 1000;

    @Override
    public void run() {
        while (true) {
            lock.lock(); // 获取锁
            try {
                if (tickets > 0) {
                    Thread.sleep(100);
                    System.out.println(Thread.currentThread().getName() + " " + tickets--);
                } else {
                    break;
                }
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                lock.unlock(); // 释放锁
            }
        }
    }

    public static void main(String[] args) {
        LockDemo lk = new LockDemo();
        for (int i = 0; i < 10; i++) {
            Thread thread = new Thread(lk, "thread-" + i);
            thread.start();
        }
    }
}
模拟10个售票站进行售票，在这里10个线程不停阻塞获取Lock来进行售票释放Lock，但总是能够确保线程同步并且数据安全。
```   
* #### 3.5.4 线程本地存储ThreadLocal
* **ThreadLocal**用于保存某个线程共享变量：对于同一个static ThreadLocal，不同线程只能从中get，set，remove自己的变量，而不会影响其他线程的变量。
* 线程同步机制采取了时间换空间的方式，访问串行化，对象共享化；而ThreadLocal采取了空间换时间的方式，访问并行化，对象独享化。
* ThreadLocal.get: 获取ThreadLocal中当前线程共享变量的值。
* ThreadLocal.set: 设置ThreadLocal中当前线程共享变量的值。
* ThreadLocal.remove: 移除ThreadLocal中当前线程共享变量的值。
* ThreadLocal.initialValue: ThreadLocal没有被当前线程赋值时或当前线程刚调用remove方法后调用get方法，返回此方法值。
```java
public void set(T value) {
    Thread t = Thread.currentThread();
    ThreadLocalMap map = getMap(t);
    if (map != null)
        map.set(this, value);
    else
        createMap(t, value);
}

public T get() {
    Thread t = Thread.currentThread();
    ThreadLocalMap map = getMap(t);
    if (map != null) {
        ThreadLocalMap.Entry e = map.getEntry(this);
        if (e != null) {
            @SuppressWarnings("unchecked")
            T result = (T)e.value;
            return result;
        }
    }
    return setInitialValue();
}

ThreadLocalMap getMap(Thread t) {
    return t.threadLocals;
}
ThreadLocalMap getMap(Thread t) {
        return t.threadLocals;
 }
 /* ThreadLocal values pertaining to this thread. This map is maintained
     * by the ThreadLocal class. */
    ThreadLocal.ThreadLocalMap threadLocals = null;
    
 static class ThreadLocalMap {

        /**
         * The entries in this hash map extend WeakReference, using
         * its main ref field as the key (which is always a
         * ThreadLocal object).  Note that null keys (i.e. entry.get()
         * == null) mean that the key is no longer referenced, so the
         * entry can be expunged from table.  Such entries are referred to
         * as "stale entries" in the code that follows.
         */
        static class Entry extends WeakReference<ThreadLocal<?>> {
            /** The value associated with this ThreadLocal. */
            Object value;

            Entry(ThreadLocal<?> k, Object v) {
                super(k);
                value = v;
            }
}

可以发现，每个线程中都有一个ThreadLocalMap数据结构,当执行set方法时
其值是保存在当前线程的threadLocals变量中，当执行set方法中，是从当前线程的threadLocals变量获取。
同时在get方法中，get()→t.threadLocals→Entry，
在每个线程Thread内部有一个ThreadLocal.ThreadLocalMap类型的成员变量threadLocals，
这个threadLocals就是用来存储实际的变量副本的，键值为当前ThreadLocal变量，value为变量副本（即T类型的变量）。
因此在初始化时，当通过ThreadLocal变量调用get()方法或者set()方法，就会对Thread类中的threadLocals进行初始化，
并且以当前ThreadLocal变量为键值，以ThreadLocal要保存的副本变量为value，存到threadLocals。

private T setInitialValue() {
        T value = initialValue();
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null)
            map.set(this, value);
        else
            createMap(t, value);
        return value;
}

initialValue()方法会return null
如果想在get之前不需要调用set就能正常访问的话，必须重写initialValue()方法，
我们发现如果没有先set的话，即在map中查找不到对应的存储，则会通过调用setInitialValue方法返回i，
而在setInitialValue方法中，有一个语句是T value = initialValue()， 
而默认情况下，initialValue方法返回的是null。

使用ThreadLocal的典型场景正如上面的数据库连接管理，线程会话管理等场景，
只适用于独立变量副本的情况，如果变量为全局共享的，则不适用在高并发下使用。

```   
* #### 3.5.5 使用原子变量实现线程同步
* **原子操作**就是指将读取变量值、修改变量值、保存变量值看成一个整体来操作即-这几种行为要么同时完成，要么都不完成。在java的util.concurrent.atomic包中提供了创建了原子类型变量的工具类，使用该类可以简化线程同步。
其中AtomicInteger表示可以用原子方式更新int的值，可用在应用程序中(如以原子方式增加的计数器)，但不能用于替换Integer；可扩展Number，允许那些处理机遇数字类的工具和实用工具进行统一访问。
  * AtomicInteger类常用方法：
  * AtomicInteger(int initialValue) : 创建具有给定初始值的新的
  * AtomicIntegeraddAddGet(int dalta) : 以原子方式将给定值与当前值相加
  * get() : 获取当前值
* #### 3.5.6 使用特殊域变量volatile关键字
  * **volatile关键字为域变量的访问提供了一种免锁机制 
  * 使用volatile修饰域变量相当于告诉虚拟机可能会被其他线程更新，因此每次使用该域变量都要同步到内存，从内存中读取，而不是直接使用寄存器中的值。 
  * volatile不会提供原子操作，他不能用来修饰final类型的变量。 
  * volatile只对域变量起作用，并不能保证线程安全。 
-  ### **3.6 线程生命周期**</br>
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/threadStatus.png)
* **创建状态**
  * 当程序使用new关键字创建了一个线程之后，该线程就处于新建状态，此时它和其他Java对象一样，仅仅由Java虚拟机为其分配了内存，并初始化了其成员变量值。此时的线程对象没有表现出任何线程的动态特征，程序也不会执行线程的线程执行体。
* **就绪状态**
  * 当线程对象调用了start()方法之后，该线程处于就绪状态，Java虚拟机会为其创建方法调用栈和程序计数器，处于这个状态的线程并没有开始运行，它只是表示该线程可以运行了。至于该线程何时开始运行，取决于JVM里线程调度器的调度。
* **运行状态**
  * 如果处于就绪状态的线程获得了CPU的调度，开始执行run方法的线程执行体，则该线程处于运行状态。
* **阻塞状态**
  * 线程调用sleep方法主动放弃所占用的处理器资源。
  * 线程调用了一个阻塞式IO方法，在该方法返回之前，该线程被阻塞。
  * 线程试图获得一个同步监视器，但该同步监视器正被其他线程锁持有。关于同步监视器的知识将在后面有更深入的介绍。
  * 线程在等待某个通知(notify)。
  * 程序调用了线程的suspend方法将该线程挂起。不过这个方法容易导致死锁，所以程序应该尽量避免使用该方法。
  * 当前正在执行的线程被阻塞之后，其他线程就可以获得执行的机会了。被阻塞的线程会在合适时候重新进入就绪状态，注意是就绪状态而不是运行状态。也就是
说被阻塞线程的阻塞解除后，必须重新等待线程调度器再次调度它。
* 当发生如下特定的情况将可以解除上面的阻塞，让该线程重新进入就绪状态
  * 调用sleep方法的线程经过了指定时间。
  * 线程调用的阻塞式IO方法已经返回。
  * 线程成功地获得了试图取得同步监视器。
  * 线程正在等待某个通知时，其他线程发出了一个通知。
  * 处于挂起状态的线程被调用了resume恢复方法。
* **终止状态**
  * run()方法执行完成，线程正常结束。
  * 线程抛出一个未捕获的Exception或Error。
  * 直接调用该线程的stop()方法来结束该线程——该方法容易导致死锁，通常不推荐使用。
-  ### **3.7 线程的死锁与调度**</br>
* **死锁**
  * 当一个线程永远地持有一个锁，并且其他线程都尝试去获得这个锁时，那么它们将永远被阻塞。
  * 例如，线程A中持有了对象1中的锁，在里面执行功能需要获取线程B持有对象2的锁，线程B持有对象2的锁，中执行功能需要获取线程A持有对象1的锁，如此反复，所有线程都在阻塞，动弹不得。
```java 
public class Threadtest {
	
static int count = 0;
public static void main(String[] args) {

Object o1 = new Object();
Object o2 = new Object();

new Thread(new Runnable(){

	public void run(){
		Thread name = Thread.currentThread().getName();
		synchronized(o1){
			method();
			System.out.println(name+":method");
			try {
				Thread.sleep(300);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			System.out.println(name+":methoding");
			synchronized(o2){
				method();
				System.out.println(name+":methoded");
			}
		}

	}
}).start();

new Thread(new Runnable(){

	public void run(){
		Thread name = Thread.currentThread().getName();
		synchronized(o2){
			method();
			System.out.println(name+":method");
			try {
				Thread.sleep(300);
				System.out.println(name+":methoding");
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			synchronized(o1){
				method();
				System.out.println(name+":methoded");
			}
		}

	}
}).start();
}

public static void method(){
System.out.println("count:"+count);
++count;
}
}
```
  * 如果您已经持有一个资源，请避免锁定另一个资源。如果只使用一个对象锁，则几乎不可能出现死锁情况，比如以下代码对上边的循环嵌套部分进行修改，则避免了死锁的情况。
  * 明确锁定的部分代码而且避免嵌套锁。
  * 避免无限期等待，设置等待的最大时间来避免这种情况。
  * 使用死锁状态检测。
* **调度** 
  * 线程的调度是指按照特定的机制为多个线程分配CPU的使用权。其中有两种模型，分别为分时调度模型和抢占式调度模型。Java虚拟机采用抢占式调度模型，是指优先让可运行池中处于就绪态的线程中优先级高的占用CPU,如果可运行池中线程的优先级相同，那么就随机选择一个线程，使其占用CPU，处于运行状态的线程会一直执行，直至它不得不放弃CPU。
  * 线程的调度不是跨平台的，它不仅取决于Java虚拟机，还依赖于操作系统。在某些操作系统中，即使运行中的线程没有遇到阻塞，也会在运行一段时间后放弃CPU，给其他线程运行的机会。所有处于就绪状态的线程根据优先级存放在可运行池中，优先级低的线程获得较少的运行机会，优先级高的获得较多的运行机会。
* Thread类的setPriority(int)和getPriority()方法用于设置和读取优先级。优先级用整数表示，取值范围时1-10，Thread类有以下三个静态常量。
  * MAX_PRIORITY:取值是10，表示最高优先级
  * MIN_PRIORITY:取值是1，表示最低优先级
  * DEFAULT_PRIORITY:取值是5，表示默认优先级
* 线程阻塞Thread.sleep()方法，它就会放弃cpu，转到阻塞状态，但持有的锁不会放弃。
* 线程让步Thread.yield()方法，当线程在运行中执行了Thread类的yield()静态方法时，如果此时具有相同优先级的其他线程处于就绪状态，那么yield()方法将把当前运行的线程放到可运行池中并使另一个线程运行，同时放弃持有的锁。如果没有相同优先级的可运行进程，则yield()方法什么也不做。
* 线程等待结束Thread.join()方法， 当我们调用某个线程的这个方法时，这个方法会挂起调用线程，直到被调用线程结束执行，调用线程才会继续执行。也就是当前运行的线程可以调用另一个线程的join()方法,当前运行的线程将转到阻塞状态，直至另一个线程运行结束，它才会恢复运行(阻塞恢复到就绪)。
-  ### **3.8 线程的安全及实现**</br>
* 当多个线程访问一个对象时，如果不用考虑这些线程在运行时环境下的调度和交替执行，也不需要进行额外的同步，或者在调用方进行任何其他的协调操作，调用这个对象的行为都可以获得正确的结果，那这个对象是线程安全的”。
* 线程安全的概念限定于多个线程之间存在共享数据访问这个前提，因为如果一段代码根本不会与其他线程共享数据，那么从线程安全的角度来看，程序是串行执行还是多线程执行对它来说完全没有区别。
**线程安全的程度：不可变、绝对线程安全、相对线程安全、线程兼容和线程对立。**
* **不可变**
  * 不可变的对象一定是线程安全的，只要一个不可变对象被正确地构建出来（没有发生this引用逃逸情况），那其外部的可见状态永远也不会改变 ，永远也不会看到它在多个线程之中处于不一致的状态。Java API中符合不可变要求的类型，常用的有String字符串常量，枚举类型，以及java.lang.Number的部分子类，如Long和Double等数值包装类型，BigInteger和BigDecimal等大数据类型。
* **绝对线程安全**
  * 要达到不管运行的环境如何，调用者都不需要任何额外的同步措施。在Java API中标注自己是线程安全的类，大多数都不是绝对线程安全的。
* **相对线程安全**
  * 通常意义上的线程安全，需要保证对这个对象的单独操作是线程安全的，在调用的时候不需要做额外的保障措施，但对于一些特定顺序的连续调用，就可能需要在调用端使用额外的同步手段来保证调用的正确性。如Vector、HashTable、Collections的synchronizedCollection（）方法包装的集合。
* **兼容**
  * 指对象本身不是线程安全的，但是可以通过调用端正确地使用同步手段来保证对象在并发环境中可以安全地使用，Java API大部分类属于线程兼容，如ArrayList、HashMap。
* **对立**
  * 无论调用端是否采取了同步措施，都无法在多线程环境下并发使用的代码。有害的，应该尽量避免，如Thread类的suspend（）和resume（）方法，如果两个线程同时持有一个线程对象，一个尝试去中断线程，一个尝试去恢复线程，并且并发进行，无论调用时是否进行了同步，目标线程都存在死锁风险，所以这两个方法已经被声明废弃。
* **实现方式**
####  * 互斥同步
  * 同步指在多个线程并发访问共享数据时，保证共享数据在同一时刻只被一个（或者是一些，使用信号量的时候）线程使用，互斥是实现同步的一种手段，临界区、互斥量和信号量都是主要的互斥实现方式。
####  * 非阻塞同步
  * 互斥同步主要的问题是进行线程阻塞和唤醒所带来的性能问题，因此这种同步称为阻塞同步。互斥同步属于悲观并发策略，总认为只要不去做同步措施，那就肯定会出现问题，无论共享数据是否真的出现竞争，都要进行加锁。基于硬件指令集的发展，有了另外一种选择：基于冲突检测的乐观并发策略，就是先进行操作，如果没有其他线程争用共享数据，那操作就成功了，如果共享数据有争用，产生冲突，那就再采取其他补救措施（常见的补救措施是不断重试，直到成功为止），因为这种策略的许多实现不需要把线程挂起，因此称为非阻塞同步，但一般来说，使用乐观并发策略需要“硬件指令集的发展”才能进行。因为我们需要操作和冲突检测这两个步骤具备原子性。如果这里再使用互斥同步来保证就失去意义了，所以我们只能靠硬件来完成这件事情，硬件保证一个从语义上看起来需要多次操作的行为只通过一条处理器指令就能完成，处理器的常用指令有：
    * 测试并设置（Test-and-Set）。
    * 获取并增加（Fetch-and-Increment）。
    * 交换（Swap）。
    * 比较并交换（Compare-and-Swap，下文称CAS）。
    * 加载链接/条件存储（Load-Linked/Store-Conditional，下文称LL/SC）。
* 这些指令中就包括非常著名的CAS指令（Compare-And-Swap比较并交换）
* CAS指令需要有3个操作数，分别是内存位置（在Java中可以简单理解为变量的内存地址，用V表示）、旧的预期值（用A表示）和新值（用B表示）。CAS指令执行时，当且仅当V符合旧预期值A时，处理器用新值B更新V的值，否则它就不执行更新，但是无论是否更新了V的值，都会返回V的旧值，上述的处理过程是一个原子操作。
* 在上述线程同步中也介绍了使用原子操作来进行线程的同步-AtomicInteger类 
```java 
 public class test3 {
	public static volatile int num = 10;
	public static AtomicInteger ai = new AtomicInteger();
	public static void main(String[] args) {
		
		Thread[] threads = new Thread[10];
		
		for(int i=0;i<10;i++){
			threads[i] = new Thread(new Runnable(){
				@Override
				public void run() {
					for(int i=0;i<100;i++){
						++num;
						ai.incrementAndGet();
					}
				}
				
			});
			threads[i].start();
		}
		while(Thread.activeCount()>1) Thread.yield();
		System.out.println(num);
		System.out.println(ai.get());
	}
}
```
* 上述代码中，当我们在多线程下时候，自增变量，多次测试返回来的数据与我们预期的数据都不一样，并且小于期望数，这就是多线程引发的数据变动问题。
* 而我们使用带有原子操作的AtomicInteger类的incrementAndGet();方法，多次测试返回来的数据一致并无误。
* 在JDK1.8后此功能被被写到了Unsafe类里，AtomicInteger类只剩一行unsafe.getAndAddInt(this, valueOffset, 1) + 1;，但是实现的逻辑是没变的），incrementAndGet()方法在一个无限循环中，不断尝试将一个比当前值大1的新值赋给自己。如果失败了，那说明在执行“获取-设置”操作的时候值已经有了修改，于是再次循环进行下一次操作，直到设置成功为止。
####  * 无同步方案
  * **可重入代码（Reentrant Code）**：这种代码也叫做纯代码（Pure Code），可以在代码执行的任何时刻中断它，转而去执行另外一段代码（包括递归调用它本身），而在控制权返回后，原来的程序不会出现任何错误。相对线程安全来说，可重入性是更基本的特性，它可以保证线程安全，即所有的可重入的代码都是线程安全的，但是并非所有的线程安全的代码都是可重入的。
  * 可重入代码有一些共同的特征，例如不依赖存储在堆上的数据和公用的系统资源、用到的状态量都由参数中传入、不调用非可重入的方法等。我们可以通过一个简单的原则来判断代码是否具备可重入性：如果一个方法，它的返回结果是可以预测的，只要输入了相同的数据，就都能返回相同的结果，那它就满足可重入性的要求，当然也就是线程安全的。
-  ### **3.9 同步锁的优化**</br>
  * **自旋锁**-互斥同步对性能最大的影响是阻塞的实现，挂起线程和恢复线程的操作都需要转入内核态中完成，这些操作给系统的并发性能带来了很大的压力。同时，虚拟机的开发团队也注意到在许多应用上，共享数据的锁定状态只会持续很短的一段时间，为了这段时间去挂起和恢复线程并不值得。如果物理机器有一个以上的处理器，能让两个或以上的线程同时并行执行，我们就可以让后面请求锁的那个线程“稍等一下”，但不放弃处理器的执行时间，看看持有锁的线程是否很快就会释放锁。为了让线程等待，我们只需让线程执行一个忙循环(自旋)，这项技术就是所谓的自旋锁。
  * **锁粗化**-原则上，我们在编写代码的时候，总是推荐将同步块的作用范围限制得尽量小——只在共享数据的实际作用域中才进行同步，这样是为了使得需要同步的操作数量尽可能变小，如果存在锁竞争，那等待锁的线程也能尽快拿到锁。大部分情况下，上面的原则都是正确的，但是如果一系列的连续操作都对同一个对象反复加锁和解锁，甚至加锁操作是出现在循环体中的，那即使没有线程竞争，频繁地进行互斥同步操作也会导致不必要的性能损耗。如果虚拟机探测到有这样一串零碎的操作都对同一个对象加锁，将会把加锁同步的范围扩展（粗化）到整个操作序列的外部，这样只需要加锁一次就可以了。
  * **轻量锁**-轻量级锁是JDK 1.6之中加入的新型锁机制，它名字中的“轻量级”是相对于使用操作系统互斥量来实现的传统锁而言的，因此传统的锁机制就称为“重量级”锁。首先需要强调一点的是，轻量级锁并不是用来代替重量级锁的，它的本意是在没有多线程竞争的前提下，减少传统的重量级锁使用操作系统互斥量产生的性能消耗。
  * **锁消除**-锁消除是指虚拟机即时编译器在运行时，对一些代码上要求同步，但是被检测到不可能存在共享数据竞争的锁进行消除。锁消除的主要判定依据来源于逃逸分析的数据支持，如果判断在一段代码中，堆上的所有数据都不会逃逸出去从而被其他线程访问到，那就可以把它们当做栈上数据对待，认为它们是线程私有的，同步加锁自然就无须进行。
## 4-Java虚拟机
-  ### **4.1 简单介绍一些概念**</br>
  * JDK就是Java Development Kit.简单的说JDK是面向开发人员使用的软件开发包，它提供了Java的开发化境和运行环境
  * Java Runtime Enviroment是指Java的运行环境，是面向Java程序的使用者，而不是开发者。
  * JVM -- java virtual machineJVM就是我们常说的java虚拟机，它是整个java实现跨平台的最核心的部分，所有的java程序会首先被编译为.class的类文件，这种类文件可以在虚拟机上执行，也就是说class并不直接与机器的操作系统相对应，而是经过虚拟机间接与操作系统交互，由虚拟机将程序解释给本地系统执行
  * JDK安装之后内部包含了JRE，这个JRE是供开发使用的；其实在安装JDK的过程中外部也会有一个JRE，这个是给普通使用者使用的，可以用来运行编译后的字节码，当我们进行开发时要指定JRE的安装目录，这个时候应该选择JDK下面的JRE。另外JRE中的bin目录就是Java虚拟机，我们需要运行Java程序时需要安装Java虚拟机，就是指安装Java的运行环境JRE（包含bin目录）的过程。
  * 虚拟机就是JVM，虚拟机是一种抽象化的计算机，通过在实际的计算机上仿真模拟各种计算机功能来实现的。Java虚拟机有自己完善的硬体架构，如处理器、堆栈、寄存器等，还具有相应的指令系统。Java虚拟机屏蔽了与具体操作系统平台相关的信息，使得Java程序只需生成在Java虚拟机上运行的目标代码（字节码），就可以在多种平台上不加修改地运行。
  * Java源代码->编译器->jvm可执行的Java字节码(即虚拟指令)->jvm->jvm中解释器->机器可执行的二进制机器码->程序运行。
 -  ### **4.2 虚拟机内存划分**</br> 
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/jvmMemory2.jpg)
####  * 程序计数器(寄存器)　
  * 当前线程所执行的字节码行号指示器,字节码解释器工作依赖计数器控制完成,通过执行线程行号记录，让线程轮流切换各条线程之间计数器互不影响,线程私有，生命周期与线程相同，随JVM启动而生，JVM关闭而死,线程执行Java方法时，记录其正在执行的虚拟机字节码指令地址,线程执行Nativan方法时，计数器记录为空（Undefined）,唯一在Java虚拟机规范中没有规定任何OutOfMemoryError情况区域。
####  * 本地方法栈
  * 算法或者一个功能的实现，都被java封装到了本地方法中，实现该功能的代码可能是C也可能是C++。
####  * 虚拟机栈
  * 虚拟机栈描述的是Java方法执行的内存模型：每个方法在执行的同时都会创建一个栈帧用来存放存储局部变量表、操作数表、动态连接、方法出口等信息，每一个方法从调用直至执行完成的过程，就对应着一个栈帧在虚拟机栈中入栈到出栈的过程。
  * 如执行一个类(类中有main方法)时，执行到main方法，就会把为main方法创建一个栈帧，然后在加到虚拟机栈中，栈帧中会存放这main方法中的各种局部变量，对象引用等东西，同样在main()方法中调用另外一个方法也会创建这个方法的栈帧加到虚拟机栈中，保存方法里面的变量属性等。
####  * 堆
  * 堆对于java开发者来说就很熟悉了，所有线程共享的一块内存区域。Java虚拟机所管理的内存中最大的一块，因为该内存区域的唯一目的就是存放对象实例。几乎所有的对象实例度在这里分配内存，也就是通常我们说的new对象，该对象就会在堆中开辟一块内存来存放对象中的一些信息，比如属性呀什么的。同时堆也是垃圾收集器管理的主要区域。
####  * 方法区与运行时常量池
  * 同样也是各个线程共享的内存区域，用于存储已被虚拟机加载的类信息、常量、静态变量、和编译器编译后的代码(也就是存储字节码文件。.class)，通常和永久区(Perm)关联在一起。
####  * java程序运行时数据图
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/jvmMemory1.jpg)

 -  ### **4.3 类加载机制**</br> 
  * 一般来说当Java文件被编译为class文件后，就可以通过(java ClassName)来执行你的Java程序，JRE的类加载器从硬盘中读取class文件，载入到系统分配给JVM的内存区域–运行数据区（Runtime Data Areas). 然后执行引擎解释或者编译类文件，转化成特定CPU的机器码，CPU执行机器码，至此完成整个过程。
  * 那么编译后的类文件是如何被加载及使用的呢？
 ![](https://rainron.github.io/JAVA-LINUX-IS/img/java/class.jpg)
  * 类的一生就是从被加载到虚拟机内存开始，直到卸载出内存为止。整个生命周期中，一个类经历了加载（Loading）、验证（Verfication）、准备（Preparation）、解析（Resolution）、初始化（Initialization）、使用（Using）和卸载（Unloading）等七个阶段。其中，验证、准备、解析三个阶段称为连接（Linking）。
  * 虚拟机类加载概述
    * 虚拟机将描述类的Class文件加载到内存，并对数据进行校验，转换解析和初始化，最终形成可以直接被虚拟机使用的Java类型，Java语言支持动态加载和动态连接。
  * 加载步骤
* #### 4.3.1 加载
* 通过一个类的全限定名来获取此类的二进制字节流。
* 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构。
* 在Java堆中生成一个代表这个类的Class对象，作为方法区这些数据的访问入口。
* 加载阶段尚未完成，连接阶段可能以及开始，但这些夹在加载阶段进行的动作，仍然属于连接阶段的内容，两个阶段的开始时间仍然保持着先后顺序。

* #### 4.3.2 验证
* **文件格式验证**：验证字节流是否符合Class文件格式的规范，并且能被当前版本的虚拟机处理。这个阶段的验证是基于字节流进行的，经过了这个阶段的验证之后，字节流才会进入内存的方法区中进行存储所以后面的验证阶段都是基于方法区的存储结构进行的。
* **元数据验证**：对类的元数据信息进行语义校验，保证不存在不符合java语言规范的元数据信息。
* **字节码验证**：进行数据流和控制流分析，对类的方法体进行校验分析，保证被校验的类的方法在运行时不会做出危害虚拟机安全的行为。
* **符号引用验证**：发生在虚拟机将符号引用转化为直接引用的时候(解析阶段)，对常量池中的各种符号引用的信息进行匹配性的校验。

* #### 4.3.3 准备
* 准备阶段是正式为类变量分配并设置类变量初始值的阶段，变量所使用的内存都将在方法区中进行分配,需要说明的是：
这时候进行内存分配的仅包括类变量(被static修饰的变量),而不包括实例变量,实例变量将会在对象实例化时随着对象一起分配在Java堆中;这里所说的初始值“通常情况”是数据类型的零值，假如:
public static int value = 123;
value在准备阶段过后的初始值为0而不是123,而把value赋值的putstatic指令将在初始化阶段才会被执行。

* #### 4.3.4 解析
* 解析阶段是在虚拟机将常量池内的符号引用替换为直接引用的过程。
* **符号引用**：符号引用以一组符号来描述所引用的目标，符号可以是任何形式的字面量，只要使用时能无歧义地定位到目标即可。符号引用与虚拟机实现的内存布局无关，引用的目标并不一定已经加载到内存中。
* **直接引用**：直接引用可以是直接指向目标的指针、相对偏移量或者一个能间接定位到目标的句柄。如果有了直接引用，那引用的目标必定已经在内存中存在。

* #### 4.3.5 初始化
* 初始化阶段是执行类构造器< clinit>()方法的过程。
<*  clinit>()方法是由编译器自动收集类中的所有类变量的赋值动作和静态语句块(static{}块)中的语句合并产生的，编译器收集的顺序是由语句在源文件中出现的顺序决定的。静态语句块只能访问到定义在静态语句块之前的变量，定义在它之后的变量，在前面的静态语句块中可以赋值，但是不能访问。
* 方法与实例构造器< init>()不同，不需要显示的调用父类构造器，虚拟机会保证在子类的< clinit>()方法执行之前，父类的< clinit>()已经执行完毕。
* < clinit>()方法对于类或接口来说不是必须的，如果一个类中没有静态语句块也没有对变量的赋值操作，那么编译器可以不为这个类生成< clinit>()方法。
* 执行接口的< clinit>()不需要先执行父接口的< clinit>()方法，只有当父接口中定义的变量被使用时，父接口才会被初始化。接口的实现类在初始化时也不会执行接口的< clinit>()方法。
* 虚拟机会保证一个类的< clinit>()方法在多线程环境中被正确的加锁和同步，如果多个线程同时去初始化一个类，则只会有一个线程去执行这个类的< clinit>()方法，其他线程需要阻塞等待。
* #### 4.3.6 类加载器
  * 类加载的过程是通过类加载器来完成的。类加载器是Java语言的一个重要创新，许多有用的技术都是基于类加载器实现的，比如类层次划分、OSGi、热部署、代码加密等。
  * 从Java虚拟机的角度看，只有两种不同的类加载器，一种是启动类加载器，这个类加载是由C++实现的，是虚拟机的一部分；另一个是所有其它的类加载器，都是由Java实现的，独立在虚拟机外部，并且全部继承自java.lang.ClassLoader抽象类。
  * 类加载器的细致划分可以划分为三种：
   * **启动类加载器**：负责将存放在<JAVA_HOME>\lib目录中的，或者被-Xbootclasspath参数所指定的路径中的，并且是虚拟机识别的类库加载到虚拟机内存中。启动类加载器无法被Java程序直接引用，用户在编写自定义类加载器时，如果需要把加载请求委派给引导类加载器，那直接使用null代替即可。
   * **扩展类加载器**：这个加载器由sun.misc.Launcher$ExtClassLoader实现，负责加载<JAVA_HOME>\lib\ext目录下的，或者被java.ext.dirs系统变量所指定的路径中的所有类库，开发者可以直接使用扩展类加载器。
   * **应用程序类加载器**：这个类加载器是由sun.misc.Launcher$AppClassLoader实现的。由于这个类加载器是ClassLoader中的getSystemClassLoader方法的返回值，所以也叫系统类加载器。它负责加载用户类路径上所指定的类库，开发者可以直接使用这个类加载器，如果应用程序中没有自定义过自己的类加载器，一般情况下这个就是程序中默认的类加载器。
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/ClassLoader.jpg)
  * 这种类加载的层次关系，称为**类加载器的双亲委派模型**。双亲委派模型要求除了顶层的启动类加载器之外，其余的类加载器都应当有自己的父类加载器。不过这个父子关系不是通过继承实现的，而是使用组合关系来复用父加载器的代码。
  * 双亲委派模型的工作过程如下：如果一个类加载器收到了类加载的请求，它首先不会自己去尝试加载这个类，而是把这个请求委派给父类加载器去完成，每一个层次的类加载器都是如此，因此所有的加载请求最终都会传送到顶层的启动类加载器中，只有当父类加载器反馈自己无法完成这个加载请求（它的搜索范围内没找到这个类）时，自加载器才会尝试自己加载。
  * 这种模型的一个好处就是由于类加载器有一种层次关系，导致类也有一种层次关系，从而有了优先级。比如类java.lang.Object，它存放在rt.jar中，无论哪个类加载器要加载这个类，最终都要委派给启动类加载器去加载，因此Object类在各个类加载器环境中都是同一个类。相反，如果没有使用双亲委派模型，由各个类加载器去自行加载，如果用户自己编写了一个称为java.lang.Object的类，并放在程序的ClassPath中，那系统将会有多个不同的Object类，java类型体系中最基础的行为也就没有办法保证了。
* #### 4.3.7 垃圾回收机制
* 程序计数器、虚拟机栈、本地方法栈、堆区、方法区。其中程序计数器、虚拟机栈、本地方法栈3个区域随线程而生、随线程而灭，因此这几个区域的内存分配和回收都具备确定性，就不需要过多考虑回收的问题，因为方法结束或者线程结束时，内存自然就跟随着回收了。而Java堆区和方法区则不一样，这部分内存的分配和回收是动态的，正是垃圾收集器所需关注的部分。
* 垃圾回收机制是由垃圾收集器Garbage Collection GC来实现的，GC是后台的守护进程。它的特别之处是它是一个低优先级进程，但是可以根据内存的使用情况动态的调整他的优先级。因此，它是在内存中低到一定限度时才会自动运行，从而实现对内存的回收。
* 如何判断是否需要回收？
 * 引用计数是垃圾收集器中的早期策略。在这种方法中，堆中每个对象实例都有一个引用计数。当一个对象被创建时，就将该对象实例分配给一个变量，该变量计数设置为1。当任何其它变量被赋值为这个对象的引用时，计数加1（a = b,则b引用的对象实例的计数器+1），但当一个对象实例的某个引用超过了生命周期或者被设置为一个新值时，对象实例的引用计数器减1。任何引用计数器为0的对象实例可以被当作垃圾收集。当一个对象实例被垃圾收集时，它引用的任何对象实例的引用计数器减1。
   * 优点：引用计数收集器可以很快的执行，交织在程序运行中。对程序需要不被长时间打断的实时环境比较有利。
   * 缺点：无法检测出循环引用。如父对象有一个对子对象的引用，子对象反过来引用父对象。这样，他们的引用计数永远不可能为0。
 * 可达性分析算法是从离散数学中的图论引入的，程序把所有的引用关系看作一张图，从一个节点GC ROOT开始，寻找对应的引用节点，找到这个节点以后，继续寻找这个节点的引用节点，当所有的引用节点寻找完毕之后，剩余的节点则被认为是没有被引用到的节点，即无用的节点，无用的节点将会被判定为是可回收的对象。
   * **可以作为GC Roots的对象包括下面几种**：
    * 虚拟机栈中引用的对象（栈帧中的本地变量表）。
    * 方法区中类静态属性引用的对象。
    * 方法区中常量引用的对象。
    * 本地方法栈中JNI（Native方法）引用的对象。
 * 无论是通过引用计数算法判断对象的引用数量，还是通过可达性分析算法判断对象的引用链是否可达，判定对象是否存活都与“引用”有关。在Java语言中，将引用又分为强引用、软引用、弱引用、虚引用4种，这四种引用强度依次逐渐减弱。
   * **强引用**-在程序代码中普遍存在的，类似 Object obj = new Object() 这类引用，只要强引用还存在，垃圾收集器永远不会回收掉被引用的对象。
   * **软引用**-用来描述一些还有用但并非必须的对象。对于软引用关联着的对象，在系统将要发生内存溢出异常之前，将会把这些对象列进回收范围之中进行第二次回收。如果这次回收后还没有足够的内存，才会抛出内存溢出异常。
   * **弱引用**-也是用来描述非必需对象的，但是它的强度比软引用更弱一些，被弱引用关联的对象只能生存到下一次垃圾收集发生之前。当垃圾收集器工作时，无论当前内存是否足够，都会回收掉只被弱引用关联的对象。
   * **虚引用**-也叫幽灵引用或幻影引用（名字真会取，很魔幻的样子），是最弱的一种引用关系。一个对象是否有虚引用的存在，完全不会对其生存时间构成影响，也无法通过虚引用来取得一个对象实例。它的作用是能在这个对象被收集器回收时收到一个系统通知。

 * 即使在可达性分析算法中不可达的对象，也并非是“非死不可”，这时候它们暂时处于“缓刑”阶段，要真正宣告一个对象死亡，至少要经历两次标记过程。
   * **第一次标记**如果对象在进行可达性分析后发现没有与GC Roots相连接的引用链，那它将会被第一次标记。
   * **第二次标记**第一次标记后接着会进行一次筛选，筛选的条件是此对象是否有必要执行finalize()方法。在finalize()方法中没有重新与引用链建立关联关系的，将被进行第二次标记。
   * **第二次标记**成功的对象将真的会被回收，如果对象在finalize()方法中重新与引用链建立了关联关系，那么将会逃离本次回收，继续存活。
 * 方法区如何判断是否需要回收？
 * 方法区主要回收的内容有：废弃常量和无用的类。对于废弃常量也可通过引用的可达性来判断，但是对于无用的类则需要同时满足下面3个条件：
    * 该类所有的实例都已经被回收，也就是Java堆中不存在该类的任何实例。
    * 加载该类的ClassLoader已经被回收。
    * 该类对应的java.lang.Class对象没有在任何地方被引用，无法在任何地方通过反射访问该类的方法。
 
* 一般来说，创建一个对象，首先会在eden区域分配区域，如果内存不够，就会将年龄大的转移到Survivor区，当survivor区域存储不下，则会转移年老代的。对于一些静态变量不需要使用对象，直接调用的，则会被放入永生代。一般来说长期存活的对象最终会被存放到年老代，还有一种特殊情况也会被存放到年老代，就是创建大对象时，比如数据这种需要申请连续空间的，如果空间比较大的，则会直接进入年老代。
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/memory.jpg)
## 5-Java中的反射
 -  ### **5.1 什么是反射**</br>
 *  JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；这种动态获取信息以及动态调用对象方法的功能称为java语言的反射机制。
 * 简单来讲就是动态获取一个类的所有信息，动态创建调用类的实例。
 * Java中的反射使用的API基本集中在java.lang.reflect包里面，Class 类与 java.lang.reflect 类库一起对反射的概念进行了支持，该类库包含了 Field,Method,Constructor 类 (每个类都实现了 Member 接口)。这些类型的对象时由 JVM 在运行时创建的，用以表示未知类里对应的成员。
 * Java中获取Class类的主要三种方法
   * 通过 Object 类中的 getClass() 方法，想要用这种方法必须要明确具体的类并且创建该类的对象。
   * 所有数据类型都具备一个静态的属性.class 来获取对应的 Class 对象。
   * 通过给定类的字符串名称就可以获取该类的字节码对象，这样做扩展性更强。通过 Class.forName() 方法完成，必须要指定类的全限定名，由于前两种方法都是在知道该类的情况下获取该类的字节码对象，因此不会有异常，但是 Class.forName() 方法如果写错类的路径会报 ClassNotFoundException 的异常。
*  通过反射机制创建对象，在创建对象之前要获得对象的构造函数对象，通过构造函数对象创建对应类的实例。
*  通过反射机制获取 Class 中的相关属性及相关方法。
 ```java 
package data_structure;
public class Student {
	private int age;
	private String name;
	public String className;
	
	public Student(){
		System.out.println("Constructor");
	}
	public Student(int age, String name, String className) {
		super();
		this.age = age;
		this.name = name;
		this.className = className;
		System.out.println("Constructor use Fields");
	}
	
	public int getAge() {
		return age;
	}
	
	public void setAge(int age) {
		this.age = age;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	
	@Override
	public String toString() {
		return "Student [age=" + age + ", name=" + name + "]";
	}
	
	public void fun(){
		System.out.println("name:"+name);
	}
	public void fun(String name){
		System.out.println("name:"+name);
	}
}

package data_structure;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

public class Test {
	
@SuppressWarnings("unchecked")
public static void main(String[] args) throws Exception {

	Student s = new Student();
	Class c1 = s.getClass();
	Class c2 = Student.class;

	try {
		Class c3 = Class.forName("data_structure.Student");
		Constructor<Student> constructor1 = c3.getConstructor();//无参构造
		Constructor<Student> constructor2 = c3.getConstructor(int.class,String.class,String.class);//有参构造

		Student s1 = constructor1.newInstance();
		Student s2 = constructor2.newInstance(10,"Tom","SIX");

		System.out.println(s1.toString());
		System.out.println(s2.toString());

		Field field1 = c3.getField("className");//不能获取私有属性
		Field field2 = c3.getDeclaredField("name");//获取私有属性

		System.out.println(field1);
		System.out.println(field2);
//		Field[] f1 = c3.getFields();遍历获取公有属性 Constructor/Method一样
//		for(Field f:f1){
//			System.out.println(f);
//		}
//		Field[] f2 = c3.getDeclaredFields();遍历获取所有属性
//		for(Field f:f2){
//			System.out.println(f);
//		}

		field2.setAccessible(true);//取消访问私有属性检查
		field2.set(s1, "Jack");//为无参对象实例属性赋值
		Object o = field2.get(s1);  //通过field2对象获取属性值
		System.out.println(o);

		Method m1 = c3.getMethod("fun");//调用空参方法
		m1.invoke(s2);
		Method m2 = c3.getMethod("fun",String.class);//调用有参方法
		m2.invoke(s2, "Jay");

		System.out.println(c3.getName());//获取对象全限定名称
		System.out.println(c3.getPackage());// 获取包名
		Class[] interfaces = c3.getInterfaces();//获取该类实现的所有接口
		for(Class in:interfaces){
			System.out.println(in);
		}

	} catch (ClassNotFoundException e) {
		e.printStackTrace();
	}

}
}

run
Constructor
Constructor
Constructor use Fields
Student [age=0, name=null]
Student [age=10, name=Tom]
public java.lang.String data_structure.Student.className
private java.lang.String data_structure.Student.name
Jack
name:Tom
name:Jay
data_structure.Student
package data_structure
 ```

  
