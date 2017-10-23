## Java代码性能优化总结

> 代码优化的目标:
>
> 1. 减小代码的体积
> 2. 提高代码的运行效率

1. 尽量指定类，方法的`final`的修饰符
2. 尽量重用对象
3. 尽可能使用局部变量
4. 及时关闭流
5. 尽量减少对变量的重复计算,例如：

```java
for (int i = 0; i < list.size(); i++)

{...}
```

应该替换为

```
for (int i = 0, int length = list.size(); i < length; i++)

{...}
```

6. 尽量使用懒加载策略，在需要的时候再创建，例如

```java
String str = "aaa";
if ( i == 1){
  list.add(str);
}
//建议替换为
if ( i == 1){
  String str = "aaa";
  list.add(str);
}
```

7. 慎用异常

   异常对性能不利。抛出异常首先要创建一个新的对象，Throwable接口的构造函数调用名为fillInStackTrace()的本地同步方法，fillInStackTrace()方法检查堆栈，收集调用跟踪信息。只要有异常被抛出，Java虚拟机就必须调整调用堆栈，因为在处理过程中创建了一个新的对象。异常只能用于错误处理，不应该用来控制程序流程。

8. 不要在循环中使用try…catch…，应该把其放在最外层

   除非不得已。

9. 如果能估计到待添加的内容长度，为底层以数组方式实现的集合、工具类指定初始长度

   比如ArrayList、LinkedLlist、StringBuilder、StringBuffer、HashMap、HashSet等等，

10. 当复制大量数据时，使用System.arraycopy()命令

11. 乘法和除法使用移位操作

    ```java
    for (val = 0; val < 100000; val += 5){
      a = val * 8;
      b = val / 2;
    }

    //可以用如下

    for (val = 0; val < 100000; val += 5){
      a = val << 3;
      b = val >> 1;
    }
    //移位操作虽然快，但是可能会使代码不太好理解，因此最好加上相应的注释。
    ```

12. 循环内不要不断创建对象引用

    ```java
    for ( i = 0; i < 10;i++){
      Object o = new Object();
    }

    // 可以使用如下

    Object o = null;
    for ( i = 0; i < 10;i++){
      o = new Object();
    }
    ```

13. 基于效率和类型检查的考虑，应该尽可能使用`数组`，无法确定数组大小时才使用ArrayList

14. 尽量使用HashMap、ArrayList、StringBuilder，除非线程安全需要，否则不推荐使用Hashtable、Vector、StringBuffer，后三者由于使用同步机制而导致了性能开销

15. 不要将数组声明为public static final

    因为这毫无意义，这样只是定义了引用为static final，数组的内容还是可以随意改变的，将数组声明为public更是一个安全漏洞，这意味着这个数组可以被外部类所改变

16. 尽量在合适的场合使用单例

    使用单例可以减轻加载的负担、缩短加载的时间、提高加载的效率，但并不是所有地方都适用于单例，简单来说，单例主要适用于以下三个方面：

    （1）控制资源的使用，通过线程同步来控制资源的并发访问

    （2）控制实例的产生，以达到节约资源的目的

    （3）控制数据的共享，在不建立直接关联的条件下，让多个不相关的进程或线程之间实现通信

17. 尽量避免随意使用静态变量

18. 及时清除不再需要的会话(**有问题**)

    为了清除不再活动的会话，许多应用服务器都有默认的会话超时时间，一般为30分钟。当应用服务器需要保存更多的会话时，如果内存不足，那么操作系统会把部分数据转移到磁盘，应用服务器也可能根据MRU（最近最频繁使用）算法把部分不活跃的会话转储到磁盘，甚至可能抛出内存不足的异常。如果会话要被转储到磁盘，那么必须要先被序列化，在大规模集群中，对对象进行序列化的代价是很昂贵的。因此，当会话不再需要时，应当及时调用HttpSession的invalidate()方法清除会话。

19. 实现RandomAccess接口的集合比如ArrayList，应当使用最普通的for循环而不是foreach循环来遍历

    这是JDK推荐给用户的。JDK API对于RandomAccess接口的解释是：实现RandomAccess接口用来表明其支持快速随机访问，此接口的主要目的是允许一般的算法更改其行为，从而将其应用到随机或连续访问列表时能提供良好的性能。实际经验表明，实现RandomAccess接口的类实例，假如是随机访问的，使用普通for循环效率将高于使用foreach循环；反过来，如果是顺序访问的，则使用Iterator会效率更高。可以使用类似如下的代码作判断：

    ```java
    if (list instanceof RandomAccess){ 
      
      	for (int i = 0; i < list.size(); i++){
        
      	}
      
    }else{

    	Iterator<?> iterator = list.iterable(); 
      	while (iterator.hasNext()){
          iterator.next()
        }

    }
    ```

    foreach循环的底层实现原理就是迭代器Iterator，参见Java语法糖1：可变长度参数以及foreach循环原理。所以后半句”反过来，如果是顺序访问的，则使用Iterator会效率更高”的意思就是顺序访问的那些类实例，使用foreach循环去遍历。

20. 使用同步代码块替代同步方法

    这点在多线程模块中的synchronized锁方法块一文中已经讲得很清楚了，除非能确定一整个方法都是需要进行同步的，否则尽量使用同步代码块，避免对那些不需要进行同步的代码也进行了同步，影响了代码执行效率。

21. 将常量声明为static final，并以大写命名

    这样在编译期间就可以把这些内容放入常量池中，避免运行期间计算生成常量的值。另外，将常量的名字以大写命名也可以方便区分出常量与变量

22. 不要创建一些不使用的对象，不要导入一些不使用的类

    这毫无意义，如果代码中出现”The value of the local variable i is not used”、”The import java.util is never used”，那么请删除这些无用的内容

23. 程序运行过程中避免使用反射

    关于，请参见反射。反射是Java提供给用户一个很强大的功能，功能强大往往意味着效率不高。不建议在程序运行过程中使用尤其是频繁使用反射机制，特别是Method的invoke方法，如果确实有必要，一种建议性的做法是将那些需要通过反射加载的类在项目启动的时候通过反射实例化出一个对象并放入内存—-用户只关心和对端交互的时候获取最快的响应速度，并不关心对端的项目启动花多久时间。

24. 使用数据库连接池和线程池

    这两个池都是用于重用对象的，前者可以避免频繁地打开和关闭连接，后者可以避免频繁地创建和销毁线程

25. 使用带缓冲的输入输出流进行IO操作

    带缓冲的输入输出流，即BufferedReader、BufferedWriter、BufferedInputStream、BufferedOutputStream，这可以极大地提升IO效率

26. 顺序插入和随机访问比较多的场景使用ArrayList，元素删除和中间插入比较多的场景使用LinkedList

27. 不要让public方法中有太多的形参

    public方法即对外提供的方法，如果给这些方法太多形参的话主要有两点坏处：

    1、违反了面向对象的编程思想，Java讲求一切都是对象，太多的形参，和面向对象的编程思想并不契合

    2、参数太多势必导致方法调用的出错概率增加

    至于这个”太多”指的是多少个，3、4个吧。比如我们用JDBC写一个insertStudentInfo方法，有10个学生信息字段要插如Student表中，可以把这10个参数封装在一个实体类中，作为insert方法的形参

28. 字符串变量和字符串常量equals的时候将字符串常量写在前面

    ```java
    String str = "123";
    if (str.equals("123")) {

    ...

    }

    //修改为

    String str = "123";
    if ("123".equals(str))

    {

    ...

    }// 主要作用是避免空指针
    ```

29. 请知道，在java中if (i == 1)和if (1 == i)是没有区别的，但从阅读习惯上讲，建议使用前者

    平时有人问，”if (i == 1)”和”if (1== i)”有没有区别，这就要从C/C++讲起。

30. 不要对数组使用toString()方法

    看一下对数组使用toString()打印出来的是什么：

    ```java
    public static void main(String[] args)

    { int[] is = new int[]{1, 2, 3};

    System.out.println(is.toString());

    }
    //结果是

    [I@18a992f
    ```

    本意是想打印出数组内容，却有可能因为数组引用is为空而导致空指针异常。不过虽然对数组toString()没有意义，但是对集合toString()是可以打印出集合里面的内容的，因为集合的父类AbstractCollections重写了Object的toString()方法。

31. 不要对超出范围的基本数据类型做向下强制转型

    这绝不会得到想要的结果：

    ```java
    public static void main(String[] args)
    { 

    long l = 12345678901234L;

    int i = (int)l;

    System.out.println(i);

    }
    //结果
    //我们可能期望得到其中的某几位，但是结果却是：

    1942892530
    ```

    解释一下。Java中long是8个字节64位的，所以12345678901234在计算机中的表示应该是：

    0000 0000 0000 0000 0000 1011 0011 1010 0111 0011 1100 1110 0010 1111 1111 0010

    一个int型数据是4个字节32位的，从低位取出上面这串二进制数据的前32位是：

    0111 0011 1100 1110 0010 1111 1111 0010

    这串二进制表示为十进制1942892530，所以就是我们上面的控制台上输出的内容。从这个例子上还能顺便得到两个结论：

    1、整型默认的数据类型是int，long l = 12345678901234L，这个数字已经超出了int的范围了，所以最后有一个L，表示这是一个long型数。顺便，浮点型的默认类型是double，所以定义float的时候要写成””float f = 3.5f”

    2、接下来再写一句”int ii = l + i;”会报错，因为long + int是一个long，不能赋值给int

32. 公用的集合类中不使用的数据一定要及时remove掉

    如果一个集合类是公用的（也就是说不是方法里面的属性），那么这个集合里面的元素是不会自动释放的，因为始终有引用指向它们。所以，如果公用集合里面的某些数据不使用而不去remove掉它们，那么将会造成这个公用集合不断增大，使得系统有内存泄露的隐患。

33. 把一个基本数据类型转为字符串，基本数据类型.toString()是最快的方式、String.valueOf(数据)次之、数据+””最慢

    把一个基本数据类型转为一般有三种方式，我有一个Integer型数据i，可以使用i.toString()、String.valueOf(i)、i+””三种方式，三种方式的效率如何，看一个测试：

    ```java
    public static void main(String[] args)

    { 

    int loopTime = 50000;

    Integer i = 0; long startTime = System.currentTimeMillis(); for (int j = 0; j < loopTime; j++)

    {

    String str = String.valueOf(i);

    }

    System.out.println("String.valueOf()：" + (System.currentTimeMillis() - startTime) + "ms");

    startTime = System.currentTimeMillis(); for (int j = 0; j < loopTime; j++)

    {

    String str = i.toString();

    }

    System.out.println("Integer.toString()：" + (System.currentTimeMillis() - startTime) + "ms");

    startTime = System.currentTimeMillis(); for (int j = 0; j < loopTime; j++)

    {

    String str = i + "";

    }

    System.out.println("i + \"\"：" + (System.currentTimeMillis() - startTime) + "ms");

    }

    //运行结果为：
    String.valueOf()：11ms 
    Integer.toString()：5ms 
    i + ""：25ms
    ```

    所以以后遇到把一个基本数据类型转为String的时候，优先考虑使用toString()方法。至于为什么，很简单：

    1、String.valueOf()方法底层调用了Integer.toString()方法，但是会在调用前做空判断

    2、Integer.toString()方法就不说了，直接调用了

    3、i + “”底层使用了StringBuilder实现，先用append方法拼接，再用toString()方法获取字符串

    三者对比下来，明显是2最快、1次之、3最慢

34. 使用最有效率的方式去遍历Map

    遍历Map的方式有很多，通常场景下我们需要的是遍历Map中的Key和Value，那么推荐使用的、效率最高的方式是：

    ```java
    public static void main(String[] args)

    {
            HashMap<String, String> hm = new HashMap<String, String>();
            hm.put("111", "222");

            Set<Map.Entry<String, String>> entrySet = hm.entrySet();

            Iterator<Map.Entry<String, String>> iter = entrySet.iterator();
            while (iter.hasNext())
            {
                Map.Entry<String, String> entry = iter.next();

                System.out.println(entry.getKey() + "\t" + entry.getValue());

            }

    }
    ```

    如果只是想遍历一下这个Map的key值，那用”Set keySet = hm.keySet();”会比较合适一些

35. 对资源的close()建议分开操作

    ```java
    try{

    XXX.close();

    YYY.close();

    }catch (Exception e)

    {

    ...

    }
    //可以修改为
    try{
      XXX.close(); 
    }catch (Exception e)
    {
      ... }

    try{
      YYY.close(); 
    }catch (Exception e) 
    { ... }
    ```

    虽然有些麻烦，却能避免资源泄露。我们想，如果没有修改过的代码，万一XXX.close()抛异常了，那么就进入了cath块中了，YYY.close()不会执行，YYY这块资源就不会回收了，一直占用着，这样的代码一多，是可能引起资源句柄泄露的。而改为下面的写法之后，就保证了无论如何XXX和YYY都会被close掉。

    ​

