# -java_relevant
### 部分基于thinkinJava
### 目录结构
- [0. 面向对象概述](#0-面向对象概述)
- [1.Static Final 关键字](#1-Static_Final关键字)
- [2.Java常用数组](#2-Java常用数组)
- 3.
- 4.
- 5.
- 6.
- 7.
#### 0-面向对象概述
#####    一切都是对象</br>
  * 在java中一切都被视为对象，因此可采用单一固定的语法。尽管一切都看成对象，但操纵的标识符实际上是对象的一个"引用"。可以将此情形想象为"遥控器"(引用)与"电视机"(对象)，只要握住这个遥控器，就能保持与电视机连接.当想减少音量，实际操控的是"遥控器"(引用)，在由遥控器来控制"电视机"(对象)如果你想在房间里面到处走走，同时可以控制"电视机"，那么只需要携带"遥控器"(引用)，而不是电视机(对象)此外，即使没有电视机，遥控器也可以独立存在，也就是说，你拥有一个引用，并不一定需要有一个对象与它关联。像这样创建一个引用:String s;但这里创建非只是引用，并不是对象。如果这是向s发送一个消息，就会返回一个运行时的 错误。因为这会s实际并没有与任何事物关联。

- **0.1 封装**</br>
  * 封装是保证软件部件具有优良的模块性的基础，封装的目标就是要实现软件部件的“高内聚、低 耦合”，防止程序相互依赖性而带来的变动影响。在面向对象的编程语言中，对象是封装的最基本单 位，面向对象的封装比传统语言的封装更为清晰、更为有力。面向对象的封装就是把描述一个对象的属性和行为的代码封装在一个“模块”中，也就是一个类中，属性用变量定义，行为用方法进行定义，方法可以直接访问同一个对象中的属性。把握一个原则：把对同一事物进行操作的方法和相关的方法放在同一个类中，把方法和它操作的数据放在同一个类中。 
- **0.2 继承**</br>
  * 在创建一个类之后，即使另一个新类与其具有相似的功能(但还是有一些不同的地方)，你还是等创建一个新类。如果能以现有的类为基础，复制它，然后通过添加和修改这个 副本 来创建新类就要好多了。通过继承就可以达到这种效果，不过也有例外，当源类(被称为基类，超类或父类)发生变动时，"被修改的副本"(被称为导出类，继承类或子类)也会变动。继承是子类自动共享父类数据和方法的机制，这是类之间的一种关系，提高了软件的可 重用性和可扩展性。 

- **0.3 多态**</br>
  * 多态是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时 并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量 发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才 确定具体的类，这样，不用修改源程序代码，就可以让引用变量绑定到各种不同的类实现上，从 而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具 体代码，让程序可以选择多个运行状态，这就是多态性。

#### 1-Static_Final关键字

- **1.1 Static**</br>
通过static关键字可以满足下面两个方面的需要:
  * ·只想为某特定域分配单一的存储空间，而不去考虑要创建多少对象，甚至根本不需要创建任何的对象
  * ·希望某个方法不与这个类型的任何对象相关联
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

- **1.2 Final**</br>
一般来说final关键字主要以下三个方面:
  * 声明数据为常量，可以是编译时常量，也可以是在运行时被初始化后不能被改变的常量。
  * 声明方法不能被子类覆盖。
  * 声明类不允许被继承。

#### 2-Java常用数组
- **2.1 集合框架关联图**</br>
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/Collections.jpg)
* 常用集合
![](https://rainron.github.io/JAVA-LINUX-IS/img/java/Iterable.jpg)
 * Collection是最基本的集合接口，声明了适用于JAVA集合（只包括Set和List）的通用方法。 Set 和List 都继承了Conllection,Map。

- **2.2 List列表**</br>
 * List的特征是其元素以线性方式存储，列表中可以存放重复对象。
 * List接口主要实现类包括ArrayList()-LinkedList()
 * 次序是List最重要的特点：它保证维护元素特定的顺序。List为Collection添加了许多方法，使得能够向List中间插入与移除元素(这只推 荐LinkedList使用。)一个List可以生成ListIterator,使用它可以从两个方向遍历List,也可以从List中间插入和移除元素。 
 * ArrayList：由数组实现的List。允许对元素进行快速随机访问，但是向List中间插入与移除元素的速度很慢。ListIterator只应该用来由后向前遍历 ArrayList,而不是用来插入和移除元素。因为那比LinkedList开销要大很多。 
 * LinkedList ：对顺序访问进行了优化，向List中间插入与删除的开销并不大。随机访问则相对较慢。(使用ArrayList代替。)还具有下列方法：addFirst(),addLast(), getFirst(), getLast(), removeFirst() 和 removeLast(), 这些方法 (没有在任何接口或基类中定义过)使得LinkedList可以当作堆栈、队列和双向队列使用。
 * 源码实现及对比
 ```java
 ArrayList
 插入
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
Arrays.copyOf(elementData, newCapacity);这行代码非常关键，他是影响ArrayList插入性能的主要因素，当数组下表超过数组长度时会调用这个方法，调用Arrays.copyOf的方法时会重新copy构建一个新的数组,会消耗大量的资源，导致性能变的很差。
指定插入
public void add(int index, E element) {
        rangeCheckForAdd(index);
  
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index);
        elementData[index] = element;
        size++;
}
大量copy导致大量的数组移动，导致性能底下。remove方法与add方法实现类似。
随机访问和遍历
public E get(int index) {
        rangeCheck(index);
        return elementData(index);
}
直接指向数组下标位置的元素返回。

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
普通的add会调用linkLast,linkdLast方法内部会新建一个Node对象，将要存储的值放入node中，同时把当前的node绑定到集合最末端，算法时间复杂度为O(n)，数量增大n倍所需要的时间增加n倍。
指定插入
public void add(int index, E element) {
        checkPositionIndex(index);
  
        if (index == size)
            linkLast(element);
        else
            linkBefore(element, node(index));
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
当需要插入的位置为集合大小时，可以直接插入集合尾部，否则，则需要找到指定位置的下标然后修改他们next、prev的指向，这里会有一个遍历，JDK对其做了优化，不同位置从两端遍历，这样让遍历的查找时间降到最低。
remove方法与add方法实现类似。
 ```

- **2.3 Set集合**</br>
 * Set是最简单的一种集合。集合中的对象不按特定的方式排序，并且没有重复对象。 Set接口主要实现了两个实现类。
 * HashSet类按照哈希算法来存取集合中的对象，存取速度比较快，基于hashMap,底层使用HashMap保存所有元素。
 * TreeSet类实现了SortedSet接口，能够对集合中的对象进行排序。 
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

map的put方法：
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
               boolean evict) {
    Node<K,V>[] tab; Node<K,V> p; int n, i;

    //确认初始化
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length;

    //如果桶为空，直接插入新元素，也就是entry
    if ((p = tab[i = (n - 1) & hash]) == null)
        tab[i] = newNode(hash, key, value, null);
    else {
        Node<K,V> e; K k;
        //如果冲突，分为三种情况
        //key相等时让旧entry等于新entry即可
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))
            e = p;
        //红黑树情况
        else if (p instanceof TreeNode)
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        else {
            //如果key不相等，则连成链表
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

hashset不允许重复的元素加入，但允许元素连成链表，因为只要key的equals方法判断为true时它们是相等的，此时会发生value的替换，因为所有entry的value一样，所以和没有插入时一样的。

TreeSet
与HashSet是基于HashMap实现一样，TreeSet同样是基于TreeMap实现的。
TreeMap是一个有序的二叉树，那么同理TreeSet同样也是一个有序的，它的作用是提供有序的Set集合。
通过源码知道TreeSet基础AbstractSet，实现NavigableSet、Cloneable、Serializable接口
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable
{
    /**
     * The backing map.
     */
    private transient NavigableMap<E,Object> m;

    // Dummy value to associate with an Object in the backing Map
    private static final Object PRESENT = new Object();

    /**
     * Constructs a set backed by the specified navigable map.
     */
    TreeSet(NavigableMap<E,Object> m) {
        this.m = m;
    }

    /**
     * Constructs a new, empty tree set, sorted according to the
     * natural ordering of its elements.  All elements inserted into
     * the set must implement the {@link Comparable} interface.
     * Furthermore, all such elements must be <i>mutually
     * comparable</i>: {@code e1.compareTo(e2)} must not throw a
     * {@code ClassCastException} for any elements {@code e1} and
     * {@code e2} in the set.  If the user attempts to add an element
     * to the set that violates this constraint (for example, the user
     * attempts to add a string element to a set whose elements are
     * integers), the {@code add} call will throw a
     * {@code ClassCastException}.
     */
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
- **2.4 Map映射**</br>


