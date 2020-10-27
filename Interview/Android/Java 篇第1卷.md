- String a = new String("abc") 与 String a = "abc" 的区别

> 创建对象个数不同
>
> `String str="abc"` 只在字符串常量池里创建一个对象。（如果字符串常量池里有"abc"，则一个都不创建直接返回地址值给str）
> `String str = new String("abc")` 在堆内存和字符串常量池各创建一个对象。（如果字符串常量池里有"abc"，则只在堆内存创建对象并返回地址值给str）

```java
拓展面试题： String s = new String(“xyz”); 产生几个对象？
答：一个或两个。
    如果常量池中没有，就创建一个“xyz”，再创建一个堆中的拷贝对象。
    如果有，就直接创建一个堆中拷贝对象。
```

- ArrayList 与 LinkedList 的区别，查找的时间复杂度是多少？
  - ArrayList 是实现了基于动态数组的数据结构，LinkedList 基于链表的数据结构
  - 对于随机访问 get 和 set，ArrayList 优于 LinkedList，因为 LinkedList 要移动指针
  - 对于新增和删除操作 add 和 remove，LinedList 比较占优势，因为 ArrayList 要移动数据。 

```java
ArrayList 是线性表（数组）
	get() 直接读取第几个下标，复杂度 O(1)
	add(E) 添加元素，直接在后面添加，复杂度O(1)
	add(index, E) 添加元素，在第几个元素后面插入，后面的元素需要向后移动，复杂度O(n)
	remove() 删除元素，后面的元素需要逐个移动，复杂度O(n)

LinkedList 是链表的操作
	get() 获取第几个元素，依次遍历，复杂度O(n)
	add(E) 添加到末尾，复杂度O(1)
	add(index, E) 添加第几个元素后，需要先查找到第几个元素，直接指针指向操作，复杂度O(n)
	remove（）删除元素，直接指针指向操作，复杂度O(1)
```

