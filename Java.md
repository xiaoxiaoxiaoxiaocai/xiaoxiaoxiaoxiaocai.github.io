### Java

#### 数据类型

基本数据类型

数值型 int short long byte float double

字符型 char

布尔型 boolean

声明float类型的数据的时候加f或者F;

引用数据类型

class

interface

数组 [ ]

```java
\t制表符：

在打印的时候，把前面字符串的长度补齐到8，或者8的整数倍。最少补1个空格，最多补8个空格：

public class Main {
    public static void main(String[] args){
        System.out.println("name"+'\t'+"age");
        System.out.println("Tom"+'\t'+"23");
    }
}
输出对齐：


name    age
Tom     23
\n换行符：


public class Main {
    public static void main(String[] args){
        System.out.println("Hello\nWorld");
    }
}
输出换行：


Hello
World
```

**一、.存储上的区别**

1.基本数据类型是存放在栈中的简单数据段。

2.引用数据类型是存放在堆内存中的对象，在栈内存中存放的是堆内存中具体内容的引用地址，通过这个地址可以快速查找到对象。

**二、比较上的区别**

1.基本数据类型的比较是值的比较

2.引用类型的比较是引用的比较

引用类型比较的是地址，即比较对象保存栈区的只想堆内存的地址是否相同。

**三、赋值上的区别**

1.基本数据类型的赋值是简单赋值，如果一个变量向另一个变量赋值基本类型的值，会在变量对象上创建一个新值，然后把这个值复制到为新变量分配的位置上。

2.引用类型的赋值是对象引用

这个变量其实复制了一个地址，两个地址指向同一个对象，改变其中任何一个变量都会互相影响。

#### Scanner

next():

- 1、一定要读取到有效字符后才可以结束输入。
- 2、对输入有效字符之前遇到的空白，next() 方法会自动将其去掉。
- 3、只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符。
- next() 不能得到带有空格的字符串。

nextLine()：

- 1、以Enter为结束符,也就是说 nextLine()方法返回的是输入回车之前的所有字符。
- 2、可以获得空白。









javabean类不写main方法（描述事物）

```java
public class phone{
//属性（成员变量：修饰符+数据类型+变量名称=初始化值；）
    
//行为 （成员方法）   
}
```

```java
public class gf{

String name;

String age;

public void sleep(){

system.out.printlen(2);

}

}
```

#### 方法重载

同类之中，无关返回值。

#### private关键字

权限修饰符，修饰成员，只能在本类中访问。

需要用public的方法俩访问。

#### this关键字

对变量具有就近原则。

可以使用this来调用成员变量。

#### StringBuilder

public StringBuilder() 创建一个空白字符串对象，不含有任何内容。

public StringBuilder(String s) 根据字符串内容，来创建可变字符串对象。

public StringBuilder append(任意类型) 添加数据，并返回对象本身。

public StringBuilder reverse()返回相反的字符串 

#### StringBuffer

使用StringBuffer 时，会对本身进行操作不后悔产生新的对象。

StringBuilder和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。

StringBuilder 相较于 StringBuffer 有速度优势。

#### 数组

##### 数组变量的声明

```java
dataType[] arrayRefVar;   // 首选的方法  

或  

dataType arrayRefVar[];  // 效果相同，但不是首选方法
```

##### 创建数组

```java
arrayRefVar = new dataType[arraySize];
```

或

```Java
dataType[] arrayRefVar = {value0, value1, ..., valuek};
```

##### 处理数组

数组的元素类型和数组的大小都是确定的，所以当处理数组元素时候，我们通常使用基本循环或者 For-Each 循环。

##### For-Each循环

用来遍历数组。

```Java
for(type element: array)
{
    System.out.println(element);
}
```

##### 数组作为函数参数

```Java
public static void printArray(int[] array) {
  for (int i = 0; i < array.length; i++) {
    System.out.print(array[i] + " ");
  }
}
```

```Java
printArray(new int[]{3, 1, 2, 6, 4, 2});
```

##### 作为返回值

```Java
public static int[] reverse(int[] list) {
  int[] result = new int[list.length];
 
  for (int i = 0, j = result.length - 1; i < list.length; i++, j--) {
    result[j] = list[i];
  }
  return result;
}
```





##### Arrays类

java.util.Arrays 类能方便地操作数组，它提供的所有方法都是静态的。

public static void sort(Object[] a)

 对指定对象数组根据其元素的自然顺序进行升序排列。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。

public static int binarySearch(Object[] a, Object key)

用二分查找算法在给定数组中搜索给定值的对象(Byte,Int,double等)。数组在调用前必须排序好的。如果查找值包含在数组中，则返回搜索键的索引；否则返回 (-(*插入点*) - 1)。 



#### ArrayList



ArrayList 类位于 java.util 包中，使用前需要引入它，语法格式如下：



```Java
import java.util.ArrayList; // 引入 ArrayList 类

ArrayList<E> objectName =new ArrayList<>();　 // 初始化
```

添加元素

ArrayList 类提供了很多有用的方法，添加元素到 ArrayList 可以使用 add() 方法:

实例

**

```Java
import** java.util.ArrayList;

**public** **class** RunoobTest {
  **public** **static** **void** main(String[] args) {
    ArrayList<String> sites = **new** ArrayList<String>();
    sites.add("Google");
    sites.add("Runoob");
    sites.add("Taobao");
    sites.add("Weibo");
    System.out.println(sites);
  }
}
```

以上实例，执行输出结果为：

```
[Google, Runoob, Taobao, Weibo]
```



##### 访问元素

使用get方法

```Java
 System.out.println(sites.get(1)); 
```



##### 修改元素

```Java
        sites.set(2, "Wiki"); // 第一个参数为索引位置，第二个为要修改的值

```

##### 删除元素

```Java
  sites.remove(3); // 删除第四个元素

```

##### 计算大小

计算ArrayList的元素数量使用size（）方法

```Java
  System.out.println(sites.size());
```

##### 迭代数组列表

```Java
for(int i = 0; i < sites.size(); i++) {
      System.out.println(sites.get(i));
    }
```

n

##### 其他引用类型

此外，BigInteger、BigDecimal 用于高精度的运算，BigInteger 支持任意精度的整数，也是引用类型，但它们没有相对应的基本类型。

```Java
ArrayList<Integer> li=new ArrayList<>();     // 存放整数元素
ArrayList<Character> li=new ArrayList<>();   // 存放字符元素
```



##### ArrayList排序

Collections 类也是一个非常有用的类，位于 java.util 包中，提供的 sort() 方法可以对字符或数字列表进行排序。

```Java
import java.util.ArrayList;
import java.util.Collections;  // 引入 Collections 类

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Taobao");
        sites.add("Wiki");
        sites.add("Runoob");
        sites.add("Weibo");
        sites.add("Google");
        Collections.sort(sites);  // 字母排序
        for (String i : sites) {
            System.out.println(i);
        }
    }
}
```









#### 正则表达式

java.util.regex 包主要包括以下三个类：

- Pattern 类：

  pattern 对象是一个正则表达式的编译表示。Pattern 类没有公共构造方法。要创建一个 Pattern 对象，你必须首先调用其公共静态编译方法，它返回一个 Pattern 对象。该方法接受一个正则表达式作为它的第一个参数。

- Matcher 类：

  Matcher 对象是对输入字符串进行解释和匹配操作的引擎。与Pattern 类一样，Matcher 也没有公共构造方法。你需要调用 Pattern 对象的 matcher 方法来获得一个 Matcher 对象。

- PatternSyntaxException：

  PatternSyntaxException 是一个非强制异常类，它表示一个正则表达式模式中的语法错误。

  Java正则表达式（Regular Expression，也称作Regex）是一种用来描述、匹配和替换文本的模式。Java内置的正则表达式工具类是java.util.regex。

  在Java中，通过使用正则表达式可以做以下操作：

  - 检索：查找字符串中满足指定正则表达式模式的子字符串；
  - 匹配：判断字符串与正则表达式是否完全匹配；
  - 替换：使用正则表达式替换匹配的字符串；
  - 验证：检查指定的字符串是否符合特定的正则表达式。

  以下是一些Java中正则表达式的基本语法：

  - 元字符：使用特殊字符来描述模式，比如.（匹配任意字符）或*（零个或多个前面的字符）；
  - 字符类：表示一组可选字符，使用[]括起来，比如[abc]（匹配a、b或c中的任意一个字符），[0-9]（匹配任意一个数字）；
  - 量词：用来指定模式出现的次数，通常作用于前面的字符或元字符，比如*（匹配零个或多个前面的字符），+（匹配一个或多个前面的字符），?（匹配零个或一个前面的字符），{n}（匹配恰好n次前面的字符），{n,}（匹配n次或更多前面的字符），{n,m}（匹配n到m次前面的字符）。

  以下是一个简单的Java正则表达式示例：

  ```java
  import java.util.regex.Matcher;
  import java.util.regex.Pattern;
  
  public class RegexTest {
      public static void main(String[] args) {
          String pattern = "abc+";
          String input = "abcccabc";
          Pattern p = Pattern.compile(pattern);
          Matcher m = p.matcher(input);
          while (m.find()) {
              System.out.println("Found: " + m.group());
          }
      }
  }
  ```

  

  该示例中，我们使用正则表达式模式"abc+“来匹配输入字符串"abcccabc"中的子字符串。该模式匹配以a开头，后面紧跟多个b，最后以c结尾的字符串。程序中先使用Pattern.compile方法来创建模式的实例，然后使用Matcher类来实现匹配和替换。执行该程序后，将输出匹配到的子字符串"abccc"和"abc”。

#### 继承

Java类支持单继承，不支持多继承。

Java类支持多层继承，

#### super

调用父类成员变量。

#### 方法重写

声明相同

@Override    // 注解，检查方法重写声明是否相同。

父类之中的private方法无法重写。

子类的访问权限不能比父类低，才能进行方法重写。

#### package

包 package 包名；

#### 接口

类实现接口

public class Dog implements 接口名

public class Interface 接口名 {}

成员变量：

只能是常量

默认修饰符 public static final构造方法：

9.v 接口没有构造方法，对行为进行抽象的，如果没有父类，看默认继承Object类。

成员方法：

默认修饰符：public abstract

#### 集合框架

高性能。（动态数组，链表，树，哈希表）也必须高效。

允许不同的集合，以相似的方式工作。

对一个集合的扩展和适应必须简单。

集合框架围绕**nkedList**, **HashSet**, 和 **TreeSet** 等,除此之外你也可以通过这些接口实现自己的集合。

Java 集合框架主要包括两种类型的容器，一种是集合（Collection），存储一个元素集合，另一种是图（Map），存储键/值对映射。Collection 接口又有 3 种子类型，List、Set 和 Queue，再下面是一些抽象类，最后是具体实现类，常用的有 [ArrayList](https://www.runoob.com/java/java-arraylist.html)、[LinkedList](https://www.runoob.com/java/java-linkedlist.html)、[HashSet](https://www.runoob.com/java/java-hashset.html)、LinkedHashSet、[HashMap](https://www.runoob.com/java/java-hashmap.html)、LinkedHashMap 等等。

集合框架是一个用来代表和操纵集合的统一架构。所有的集合框架都包含如下内容：

- 

  **接口：**是代表集合的抽象数据类型。例如 Collection、List、Set、Map 等。之所以定义多个接口，是为了以不同的方式操作集合对象

- **实现（类）：**是集合接口的具体实现。从本质上讲，它们是可重复使用的数据结构，例如：ArrayList、LinkedList、HashSet、HashMap。

- **算法：**是实现集合接口的对象里的方法执行的一些有用的计算，例如：搜索和排序，这些算法实现了多态，那是因为相同的方法可以在相似的接口上有着不同的实现。

除了集合，该框架也定义了几个 Map 接口和类。Map 里存储的是键/值对。尽管 Map 不是集合，但是它们完全整合在集合中。

#### 集合接口

##### collection

Collection 是最基本的集合接口，一个 Collection 代表一组 Object，即 Collection 的元素, Java不提供直接继承自Collection的类，只提供继承于的子接口(如List和set)

单列集合的接口。

定义的是共性的方法，不能通过索引来删除。

```java 
Collection <String> c=new ArrayList<>();
```

```
boolean add(E e)//在List中添加永远返回True             在Set中添加，如果已经存在返 false
void clear（）//清空
boolean remove（）//删除的元素不存在，删除失败。
boolean contains（）//依赖equals方法判断，如果是自定义对象，没有重写equals方法按object方法（依赖地址）
```

##### list

List接口是一个有序的 Collection，使用此接口能够精确的控制每个元素插入的位置，能够通过索引(元素在List中位置，类似于数组的下标)来访问List中的元素，第一个元素的索引为 0，而且允许有相同的元素。

List 接口存储一组不唯一，有序（插入顺序）的对象。

有序：存取顺序

可重复



##### set

Set 具有与 Collection 完全一样的接口，只是行为上不同，Set 不保存重复的元素。

Set 接口存储一组唯一，无序的对象。

无序，不重复，无。索引

#####  Map

Map 接口存储一组键值对象，提供key（键）到value（值）的映射。

##### set和list的区别

-  Set 接口实例存储的是无序的，不重复的数据。List 接口实例存储的是有序的，可以重复的元素。
-  Set 检索效率低下，删除和插入效率高，插入和删除不会引起元素位置改变 **<实现类有HashSet,TreeSet>**。
-  List 和数组类似，可以动态增长，根据实际存储的数据的长度自动增长 List 的长度。查找元素效率高，插入删除效率低，因为会引起其他元素位置改变 **<实现类有ArrayList,LinkedList,Vector>** 。

#### 集合类（集合实现类）

##### [ LinkedList]

双链表

前地址+值+后地址

该类实现了List接口，允许有null（空）元素。主要用于创建链表数据结构，该类没有同步方法，如果多个线程同时访问一个List，则必须自己实现访问同步，解决方法就是在创建List时候构造一个同步的List。例如：

```
List list=Collections.synchronizedList(newLinkedList(...));
```

LinkedList 查找效率低。

链表（Linked list）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的地址。

链表可分为单向链表和双向链表。

**以下情况使用 ArrayList :**

- 频繁访问列表中的某一个元素。
- 只需要在列表末尾进行添加和删除元素操作。

**以下情况使用 LinkedList :**

- 你需要通过循环迭代来访问列表中的某些元素。
- 需要频繁的在列表开头、中间、末尾等位置进行添加和删除元素操作。

```java 
// 引入 LinkedList 类
import java.util.LinkedList; 

LinkedList<E> list = new LinkedList<E>();   // 普通创建方法
或者
LinkedList<E> list = new LinkedList(Collection<? extends E> c); // 使用集合创建链表
```

```java 
// 引入 LinkedList 类
import java.util.LinkedList;

public class RunoobTest {
    public static void main(String[] args) {
        LinkedList<String> sites = new LinkedList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        // 使用 addFirst() 在头部添加元素
        sites.addFirst("Wiki");
        sites.addLast("123");//在结尾添加元素
        System.out.println(sites);
    }
```





##### ArrayList

该类实现了List接口，允许有null（空）元素。主要用于创建链表数据结构，该类没有同步方法，如果多个线程同时访问一个List，则必须自己实现访问同步，解决方法就是在创建List时候构造一个同步的List。例如：

```
List list=Collections.synchronizedList(newLinkedList(...));
```

LinkedList 查找效率低。

ArrayList 类位于 java.util 包中，使用前需要引入它

```java 
ArrayList<E> objectName =new ArrayList<>();　 // 初始化
```

```java 
ArrayList<String> sites = new ArrayList<String>();
```

添加元素到 ArrayList 可以使用 add() 方法

```java 
 ArrayList<String> sites = new ArrayList<String>();
    sites.add("Google");
```



空参创造集合，默认创建0长度的数组。

添加第一个元素时，长度为10

存满是扩容1.5倍

之后以实际为准。

##### HashSet

该类实现了Set接口，不允许出现重复元素，不保证集合中元素的顺序，允许包含值为null的元素，但最多只能一个。

HashSet 基于 HashMap 来实现的，是一个不允许有重复元素的集合。

HashSet 允许有 null 值。

HashSet 是无序的，即不会记录插入的顺序。

HashSet 不是线程安全的， 如果多个线程尝试同时修改 HashSet，则最终结果是不确定的。 您必须在多线程访问时显式同步对 HashSet 的并发访问。

HashSet 实现了 Set 接口。



```Java 
// 引入 HashSet 类      
import java.util.HashSet;

public class RunoobTest {
    public static void main(String[] args) {
    HashSet<String> sites = new HashSet<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        sites.add("Runoob");  // 重复的元素不会被添加
        System.out.println(sites);
        System.out.println(sites.contains("Taobao"));//contains()可以用来判断元素是否存在集合之中
         sites.clear(); //删除集合所有元素
    }
}//[Google, Runoob, Zhihu, Taobao]为输出结果。
```



#### HashMap

HashMap 是一个散列表，它存储的内容是键值对(key-value)映射。

HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，最多允许一条记录的键为 null，不支持线程同步。

HashMap 是无序的，即不会记录插入的顺序。

HashMap 继承于AbstractMap，实现了 Map、Cloneable、java.io.Serializable 接口。

HashMap 的 key 与 value 类型可以相同也可以不同，可以是字符串（String）类型的 key 和 value，也可以是整型（Integer）的 key 和字符串（String）类型的 value。

HashMap 中的元素实际上是对象，一些常见的基本类型可以使用它的包装类。

| 基本类型 | 引用类型  |
| :------- | :-------- |
| boolean  | Boolean   |
| byte     | Byte      |
| short    | Short     |
| int      | Integer   |
| long     | Long      |
| float    | Float     |
| double   | Double    |
| char     | Character |

```Java
以下实例我们创建一个 HashMap 对象 Sites， 整型（Integer）的 key 和字符串（String）类型的 value：

HashMap<Integer, String> Sites = new HashMap<Integer, String>();
```

```Java
HashMap 类提供了很多有用的方法，添加键值对(key-value)可以使用 put() 方法:

实例
// 引入 HashMap 类      
import java.util.HashMap;

public class RunoobTest {
    public static void main(String[] args) {
        // 创建 HashMap 对象 Sites
        HashMap<Integer, String> Sites = new HashMap<Integer, String>();
        // 添加键值对
        Sites.put(1, "Google");
        Sites.put(2, "Runoob");
        Sites.put(3, "Taobao");
        Sites.put(4, "Zhihu");
        System.out.println(Sites);
    }
}//{1=Google, 2=Runoob, 3=Taobao, 4=Zhihu}
```

访问元素可以通过访问key来获取value

```Java
get(key)获取value

// 引入 HashMap 类      
import java.util.HashMap;

public class RunoobTest {
    public static void main(String[] args) {
        // 创建 HashMap 对象 Sites
        HashMap<Integer, String> Sites = new HashMap<Integer, String>();
        // 添加键值对
        Sites.put(1, "Google");
        Sites.put(2, "Runoob");
        Sites.put(3, "Taobao");
        Sites.put(4, "Zhihu");
        System.out.println(Sites.get(3));
        Sites.remove(3);//通过删除键值，来删除对应的value
        Sites.clear();//清空集合
    }
}
```

迭代HashMap

```java
实例
// 引入 HashMap 类      
import java.util.HashMap;

public class RunoobTest {
    public static void main(String[] args) {
        // 创建 HashMap 对象 Sites
        HashMap<Integer, String> Sites = new HashMap<Integer, String>();
        // 添加键值对
        Sites.put(1, "Google");
        Sites.put(2, "Runoob");
        Sites.put(3, "Taobao");
        Sites.put(4, "Zhihu");
        // 输出 key 和 value
        for (Integer i : Sites.keySet()) {
            System.out.println("key: " + i + " value: " + Sites.get(i));
        }
        // 返回所有 value 值
        for(String value: Sites.values()) {
          // 输出每一个value
          System.out.print(value + ", ");
        }
    }
}
```

#### Iterator

迭代器

Iterator<E> iterator() 返回迭代器对象，默认指向0索引。

依靠指针。

报错NoSuchElemertExeception

遍历结束，指针不会复位

循环中只能用一次next方法

遍历时不用集合的方法增加或删除。

```java 
boolean hasNexr()     
Iterator<String> it=list.iterator();    
while(it.hasNext()){
    String str =it.next();
    sout;
}   
    
    
```



#### 增强for

for中的变量为第三方变量，不会改变集合之中的数据。

```java
for (String s : list){

s="q";

}//【list中的数据】
```

#### Lambda

```java
(parameters) -> expression
或
(parameters) ->{ statements; }
```



```java
coll.forEach(String s)->{sout;};



coll.forEach(s-> sout;);
```

#### 列表迭代器

ListIterator<String> it=list.listiterator()

可以添加元素

#### 泛型

如果没有泛型，就存储任意数据。
