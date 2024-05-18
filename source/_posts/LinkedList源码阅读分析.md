---

layout: LinkedList源码阅读分析

title: LinkedList源码阅读分析

tags: Web

categories: Web

top: 29

path: /article/1784846430

abbrlink: 1784846430



date: 2024-02-25 21:00:00


---

# LinkedList源码阅读分析



<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202402252130297.png" alt="image-20211013144335715" style="zoom:150%;" />

**LinkedList** 是一个继承于**AbstractSequentialList**的双向链表。它也可以被当作堆栈、队列或双端队列进行操作。
**LinkedList** 实现 **List** 接口，能对它进行队列操作。
**LinkedList** 实现 **Deque** 接口，即能将LinkedList当作双端队列使用。
**LinkedList** 实现了**Cloneable**接口，即覆盖了函数clone()，能克隆。
**LinkedList** 实现**java.io.Serializable**接口，这意味着LinkedList支持序列化，能通过序列化去传输。
**LinkedList** 是**非同步**的

## 1.2 LinkedList源码

```java
 复制代码 隐藏代码public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
{
    // 元素个数
    transient int size = 0;

    /**
     * Pointer to first node.
     * Invariant: (first == null && last == null) ||
     *            (first.prev == null && first.item != null)
     */
    // 链表首节点
    transient Node<E> first;

    /**
     * Pointer to last node.
     * Invariant: (first == null && last == null) ||
     *            (last.next == null && last.item != null)
     */
    // 链表尾节点
    transient Node<E> last;

    .
```

### 1.2.1 主要构造方法

#### (1). LinkedList()

```java
 复制代码 隐藏代码public LinkedList() {
}
```

LinkedList 的无参构造就是构造一个空的list集合

#### (2). LinkedList(Collection<? extends E> c)

```java
 复制代码 隐藏代码public LinkedList(Collection<? extends E> c) {
    this();
    addAll(c);
}
```

构造一个包含指定集合的元素的列表，按照它们由集合的迭代器返回的顺序。

### 1.2.2 主要内部类

典型的双链表结构。

```java
 复制代码 隐藏代码private static class Node<E> {
    // item表示当前存储元素
    E item;
    // next表示当前节点的后置节点
    Node<E> next;
    // prev表示当前节点的前置节点
    Node<E> prev;

    Node(Node<E> prev, E element, Node<E> next) {
        this.item = element;
        this.next = next;
        this.prev = prev;
    }
}
```

LinkedList 是通过双向链表实现的，而双向链表就是通过Node类来实现的，Node类中通过item变量存储当前元素，通过next变量指向当前节点的下一个节点，通过prev变量指向当前节点的上一个节点。

### 1.2.3 LinkedList增加节点

#### (1). add(E e)

```java
 复制代码 隐藏代码public boolean add(E e) {
    //在末尾添加一个元素
    linkLast(e);
    return true;
}

void linkLast(E e) {
    // 获取链表的最后一个节点
    final Node<E> l = last;
    // 创建一个新节点
    final Node<E> newNode = new Node<>(l, e, null);
     // 使新的一个节点为最后一个节点
    last = newNode;
     // 如果最后一个节点为null，则表示链表为空，则将newNode赋值给first节点
    if (l == null)
        first = newNode;
    // 否则尾节点的last指向 newNode
    else
        l.next = newNode;
    // 元素的个数加1
    size++;
    // 结构修改的次数自增+1
    modCount++;
}
```

- 第一步，获取链表的最后一个节点
- 第二步，创建一个新节点
- 第三步，使新的一个节点为最后一个节点
- 第四步，如果最后一个节点为null，则表示链表为空，则将newNode赋值给first节点；否则尾节点的last指向 newNode

#### (2). add(int index, E element)

在指定位置插入元素

```java
 复制代码 隐藏代码public void add(int index, E element) {
    // 检查索引index的位置
    checkPositionIndex(index);
        // 如果index是在队列尾节点之后的一个位置
    // 把新节点直接添加到尾节点之后
    // 否则调用linkBefore()方法在中间添加节点
    if (index == size)
        linkLast(element);
    else
        linkBefore(element, node(index));
}

private void checkPositionIndex(int index) {
    if (!isPositionIndex(index))
        throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
}

private boolean isPositionIndex(int index) {
    return index >= 0 && index <= size;
}

void linkLast(E e) {
    // 获取链表的最后一个节点
    final Node<E> l = last;
    // 创建一个新节点
    final Node<E> newNode = new Node<>(l, e, null);
     // 使新的一个节点为最后一个节点
    last = newNode;
     // 如果最后一个节点为null，则表示链表为空，则将newNode赋值给first节点
    if (l == null)
        first = newNode;
    // 否则尾节点的last指向 newNode
    else
        l.next = newNode;
    // 元素的个数加1
    size++;
    // 结构修改的次数自增+1
    modCount++;
}

void linkBefore(E e, Node<E> succ) {
    // assert succ != null;
    // succ是待添加节点的后继节点
    // 找到待添加节点的前置节点
    final Node<E> pred = succ.prev;
    // 在其前置节点和后继节点之间创建一个新节点
    final Node<E> newNode = new Node<>(pred, e, succ);
    // 构建双向链表，succ的前驱节点为新的节点
    succ.prev = newNode;
    // 如果前置驱节点为null，则把newNode赋值给first
    if (pred == null)
        first = newNode;
    else
        // 构建双向列表
        pred.next = newNode;
    // 元素的个数加1
    size++;
    // 结构修改的次数自增+1
    modCount++;
}

// 寻找index位置的节点
Node<E> node(int index) {
    // 因为是双链表
    // 所以根据index是在前半段还是后半段决定从前遍历还是从后遍历
    // 这样index在后半段的时候可以少遍历一半的元素
    if (index < (size >> 1)) {
        // 如果是在前半段
        // 就从前遍历
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        // 如果是在后半段
        // 就从后遍历
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}
```

#### (3). addAll(Collection<? extends E> c)

```java
 复制代码 隐藏代码public boolean addAll(Collection<? extends E> c) {
    // 在链表末尾添加一个集合
    return addAll(size, c);
}
```

#### (4).addAll(int index, Collection<? extends E> c)

在指定位置添加一个集合

```java
 复制代码 隐藏代码public boolean addAll(int index, Collection<? extends E> c) {
    //检查索引是否越界
    checkPositionIndex(index);
        // 将集合转换成一个数组
    Object[] a = c.toArray();
    int numNew = a.length;
    // 如果集合为空，添加失败，返回false
    if (numNew == 0)
        return false;
   // 声明Node<E>类型变量pred（元素直接前驱）, succ（元素直接后继）
    Node<E> pred, succ;
    // 如果给定下标等于链表原有元素个数
    if (index == size) {
        succ = null; // 设置给定尾集合元素直接后继为null
        pred = last; // 设置给定集合头元素直接前驱为last(原链表尾元素)
    } else {
        succ = node(index); // 给定集合尾元素直接后继为node(index)
        pred = succ.prev;   // 给定集合头元素直接前驱为succ.prev（确定上一个链表元素pred）
    }
        // 遍历集合元素，依次添加进链表
    for (Object o : a) {
        @SuppressWarnings("unchecked") E e = (E) o;
        // 添加尾元素
        Node<E> newNode = new Node<>(pred, e, null);
        // 如果是头元素,创建第一个元素
        if (pred == null)
            first = newNode;
        else
                   // 不为空则插入下一个元素
            pred.next = newNode;
        //为下一次循环做准备，设置元素直接前驱为newNode
        pred = newNode;
    }
        ////如果元素直接后继为null，说明这是尾元素 
    if (succ == null) {
        last = pred; //因上个循环最后将pred = newNode;        所以将最后一个元素赋值为尾元素
    } else {

        //赋值后置节点
        pred.next = succ;
        //赋值前置节点
        succ.prev = pred;
    }
        // 修改链表元素个数
    size += numNew;
    // 结构性改变次数自增
    modCount++;
    return true;
}
```

#### (5). addFirst(E e)

从队列首添加元素

```java
 复制代码 隐藏代码public void addFirst(E e) {
    // 从队列首添加元素 
    linkFirst(e);
}

private void linkFirst(E e) {
    // 首节点
    final Node<E> f = first;
    // 创建新节点，新节点的next是首节点
    final Node<E> newNode = new Node<>(null, e, f);
    // 让新节点作为新的首节点
    first = newNode;
    // 判断是不是第一个添加的元素
    // 如果是就把last也置为新节点
    // 否则把原首节点的prev指针置为新节点
    if (f == null)
        last = newNode;
    else
        f.prev = newNode;
    // 元素个数加1
    size++;
    // 结构性改变次数自增
    modCount++;
}
```

#### (6). addLast(E e)

从队尾添加元素

```java
 复制代码 隐藏代码public void addLast(E e) {
    linkLast(e);
}

void linkLast(E e) {
    // 获取链表的最后一个节点
    final Node<E> l = last;
    // 创建一个新节点
    final Node<E> newNode = new Node<>(l, e, null);
     // 使新的一个节点为最后一个节点
    last = newNode;
     // 如果最后一个节点为null，则表示链表为空，则将newNode赋值给first节点
    if (l == null)
        first = newNode;
    // 否则尾节点的last指向 newNode
    else
        l.next = newNode;
    // 元素的个数加1
    size++;
    // 结构修改的次数自增+1
    modCount++;
}
```

### 1.2.3 LinkedList删除节点

#### (1). remove()

从队首删除元素

```java
 复制代码 隐藏代码public E remove() {
    return removeFirst();
}

public E removeFirst() {
    final Node<E> f = first;
    // 首节点为null抛出异常
    if (f == null)
        throw new NoSuchElementException();
    //从队首删除节点
    return unlinkFirst(f);
}

// 删除首节点
private E unlinkFirst(Node<E> f) {
    // assert f == first && f != null;
    // 首节点的元素值
    final E element = f.item;
    // 首节点的next指针
    final Node<E> next = f.next;
    // 设置首节点,首节点的next指针为null，协助GC
    f.item = null;
    f.next = null; // help GC
    // 把首节点的next作为新的首节点
    first = next;
    // 如果只有一个元素，删除了，把last也置为空
    // 否则把next的前置指针置为空
    if (next == null)
        last = null;
    else
        next.prev = null;
    // 链表元素个数自减-1
    size--;
    //结构性修改次数自增+1
    modCount++;
    // 返回删除的元素
    return element;
}
```

#### (2). remove(int index)

删除指定索引位置元素

```java
 复制代码 隐藏代码public E remove(int index) {
    //检查索引是否越界
    checkElementIndex(index);
    //删除节点
    return unlink(node(index));
}
// 检查索引越界
private void checkElementIndex(int index) {
    if (!isElementIndex(index))
        throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
}

private boolean isElementIndex(int index) {
    return index >= 0 && index < size;
}

 // 寻找index位置的节点
Node<E> node(int index) {
    // assert isElementIndex(index);
        // 所以根据index是在前半段还是后半段决定从前遍历还是从后遍历
    // 这样index在后半段的时候可以少遍历一半的元素
    if (index < (size >> 1)) {
        // 如果是在前半段
        // 就从前遍历
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        // 如果是在后半段
        // 就从后遍历
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}

E unlink(Node<E> x) {
    // assert x != null;
    // x的元素值
    final E element = x.item;
    // x的前置节点
    final Node<E> next = x.next;
    // x的后置节点
    final Node<E> prev = x.prev;
        // 如果前置节点为空
    // 说明是首节点，让first指向x的后置节点
    // 否则修改前置节点的next为x的后置节点
    if (prev == null) {
        first = next;
    } else {
        prev.next = next;
        x.prev = null;
    }

    // 如果后置节点为空
    // 说明是尾节点，让last指向x的前置节点
    // 否则修改后置节点的prev为x的前置节点
    if (next == null) {
        last = prev;
    } else {
        next.prev = prev;
        x.next = null;
    }
         // 清空x的元素值，协助GC
    x.item = null;
    // 元素个数减1
    size--;
    // 结构修改次数加1
    modCount++;
    // 返回删除的元素
    return element;
}
```

#### (3). remove(Object o)

根据元素删除

```java
 复制代码 隐藏代码public boolean remove(Object o) {
    //如果元素为null,查找链表中元素值为null第一次出现的位置将其删除
    if (o == null) {
        for (Node<E> x = first; x != null; x = x.next) {
            if (x.item == null) {
                unlink(x);
                return true;
            }
        }
    } else {
         //如果元素不为null,查找链表中元素值第一次出现的位置将其删除
        for (Node<E> x = first; x != null; x = x.next) {
            if (o.equals(x.item)) {
                unlink(x);
                return true;
            }
        }
    }
    return false;
}
```

#### (4). removeFirst()

删除首节点

```java
 复制代码 隐藏代码public E removeFirst() {
    // 判断首节点是否为空，为空则抛出异常
    final Node<E> f = first;
    if (f == null)
        throw new NoSuchElementException();
    return unlinkFirst(f);
}
// 删除首节点
private E unlinkFirst(Node<E> f) {
    // assert f == first && f != null;
    // 首节点的元素值
    final E element = f.item;
    // 首节点的next指针
    final Node<E> next = f.next;
    // 清空首节点的内容，协助GC
    f.item = null;
    f.next = null; // help GC
    // 把首节点的next作为新的首节点
    first = next;
    // 如果只有一个元素，删除了，把last也置为空
    // 否则把next的前置指针置为空
    if (next == null)
        last = null;
    else
        next.prev = null;
    // 元素个数减1
    size--;
    // 结构修改次数加1
    modCount++;
    // 返回删除的元素
    return element;
}
```

#### (5). removeLast()

删除尾结点

```java
 复制代码 隐藏代码public E removeLast() {
    // 判断尾节点是否为空，为空则抛出异常
    final Node<E> l = last;
    if (l == null)
        throw new NoSuchElementException();
    // 删除尾结点
    return unlinkLast(l);
}

private E unlinkLast(Node<E> l) {
    // assert l == last && l != null;
    // 尾节点的元素值
    final E element = l.item;
    // 尾节点的上一指针
    final Node<E> prev = l.prev;
    //清空尾节点的内容，协助GC
    l.item = null;
    l.prev = null; // help GC
    // 让前置节点成为新的尾节点
    last = prev;
    // 如果只有一个元素，删除了把first置为空
    // 否则把前置节点的next置为空
    if (prev == null)
        first = null;
    else
        prev.next = null;
    // 元素个数减1
    size--;
    // 结构修改次数加1
    modCount++;
    // 返回删除的元素
    return element;
}
```

#### (6). removeFirstOccurrence(Object o)

删除指定元素第一次出现在该列表中(遍历从头部到尾部列表时)。如果列表中不包含该元素，它是不变的。

```java
 复制代码 隐藏代码public boolean removeFirstOccurrence(Object o) {
    return remove(o);
}
```

#### (7).removeLastOccurrence(Object o)

删除此列表中最后一次出现的指定元素(从头到尾遍历列表时)。如果列表不包含该元素，则它保持不变。

```java
 复制代码 隐藏代码public boolean removeLastOccurrence(Object o) {
    if (o == null) {
        for (Node<E> x = last; x != null; x = x.prev) {
            if (x.item == null) {
                unlink(x);
                return true;
            }
        }
    } else {
        for (Node<E> x = last; x != null; x = x.prev) {
            if (o.equals(x.item)) {
                unlink(x);
                return true;
            }
        }
    }
    return false;
}
```

### 1.2.4 LinkedList修改节点

#### （1） set(int index, E element)

根据索引修改节点

```java
 复制代码 隐藏代码public E set(int index, E element) {
    //检查索引是否越界
    checkElementIndex(index);
    // 根据索引查找要修改的元素
    Node<E> x = node(index);
    // 去除被修改的元素
    E oldVal = x.item;
    // 将新元素赋值
    x.item = element;
    // 返回修改之前的元素
    return oldVal;
}
```

### 1.2.5 LinkedList查找节点

#### (1). get(int index)

根据索引查找节点

```java
 复制代码 隐藏代码public E get(int index) {
    // 检查索引是否越界
    checkElementIndex(index);
    // 根据索引查找
    return node(index).item;
}

// 寻找index位置的节点
Node<E> node(int index) {
    // assert isElementIndex(index);
    // 所以根据index是在前半段还是后半段决定从前遍历还是从后遍历
    // 这样index在后半段的时候可以少遍历一半的元素
    if (index < (size >> 1)) {
        // 如果是在前半段
        // 就从前遍历
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        // 如果是在后半段
        // 就从后遍历
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}
```

#### (2). getFirst()

获取首节点

```java
 复制代码 隐藏代码public E getFirst() {
    final Node<E> f = first;
    if (f == null)
        throw new NoSuchElementException();
    return f.item;
}
```

#### (3). getLast()

获取尾结点

```java
 复制代码 隐藏代码 public E getLast() {
        final Node<E> l = last;
        if (l == null)
            throw new NoSuchElementException();
        return l.item;
    }
```

## 1.3 LinkedList作为栈使用

```java
 复制代码 隐藏代码public void push(E e) {
    addFirst(e);
}

public E pop() {
    return removeFirst();
}
```

栈的特性是LIFO(Last In First Out)，所以作为栈使用也很简单，添加删除元素都只操作队列首节点即可。

## 1.4 LinkedList总结

（1）**LinkedList**是一个以**双链表**实现的List；

（2）**LinkedList**还是一个双端队列，具有**队列、双端队列、栈**的特性；

（3）**LinkedList**在队列**首尾添加、删除元素**非常高效，时间复杂度为O(1)；

（4）**LinkedList**在**中间添加、删除元素**比较低效，时间复杂度为O(n)；

（5）**LinkedList**不支持随机访问，所以访问非队列首尾的元素比较低效；

（6）**LinkedList**在功能上等于ArrayList + ArrayDeque；

- 备忘：

  - **数组**： 是一种**线性**数据结构，使用一组**连续**的内存空间存储一组具有**相同类型**的数据。

  **线性**，表示没有分叉，任意元素的前后元素最多只有一个，同样是线性结构的还有链表、队列等。

  **连续**，它在内存空间中的存储是连续的，不间断的，前后两个元素紧挨着，不存在间隙。

  **相同类型**，数组中存储的元素的类型一定是相同的，当然，在Java中，你可以使用Object代表所有类型，本质上，它们依然是相同类型。

  正是有了上面三个特性，才使得数组具有了**随机访问**的特性

  - **链表**：它也是一种**线程数据结构**，与数组不同的是，它在内存空间中**不一定是顺序存储**的，为了**保证链表中元素的连续性**，一般使用一个**指针**来找到下一个元素

  链表**不具有随机访问**的特性，在链表中根据索引来查找元素只能**从头开始（单链表**）【双链表可从首尾查找元素】，它的时间复杂度是O(n)。

  如果在单链表的基础上再增加一个前驱指针（指向前一个元素的指针），就变成了双向链表

  *LinkedList就是典型的双向链表结构，双向链表既可以当作队列使用，又可以当作栈来使用，非常方便*。

  - **队列**：所谓队列，其实跟现实中的排队是一样的，其中的元素从一端进入，从另一端出去，英文叫做：First In，First Out，简写FIFO。**【先进先出】**
  - **栈**：栈，它是与队列表现完全相反的数据结构，它的元素是先进的后出来。**【先进后出】**