## Android 异常整理

#### android.content.res.Resources$NotFoundException: String resource ID #0x1

原因：一般发生在参数 int resId错误，你把String赋值给int的resId，所以编译器找不到正确的resource于是报错。

最简单的例子，检查一下你的Toast.makeText()啊textView.setText啊之类的函数，这种函数通常有几个重载，如：

textView.setText(CharSequence text);

textView.setText(int resId);

如果不小心将一个int值传给了它，那它不会显示该int值，而是跑到工程下去找一个对应的resource的id,当然是找不到的，于是就报错啦。

解决办法：

如果要显示该int值，就要将int转化成String或者CharSequence，百度上很多办法。

个人比较喜欢这么干：在该int值后面+""，强制转为String。简单易用。╮(╯_╰)╭

#### java.util.ConcurrentModificationException

> 引起原因：对Vector、ArrayList在迭代的时候如果同时对其进行修改就会抛出java.util.ConcurrentModificationException异常

解决方法：使用迭代器进行操作,就不会再出现异常了

```java
public class Test {
    public static void main(String[] args)  {
        ArrayList<Integer> list = new ArrayList<Integer>();
        list.add(2);
        Iterator<Integer> iterator = list.iterator();
        while(iterator.hasNext()){
            Integer integer = iterator.next();
            if(integer==2)
                iterator.remove();   //注意这个地方
        }
    }
}
```



