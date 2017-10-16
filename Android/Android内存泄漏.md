## Android内存泄漏

> 内容转载出自[francistao](https://github.com/francistao/LearningNotes/blob/master/Part1/Android/Android%E5%86%85%E5%AD%98%E6%B3%84%E6%BC%8F%E6%80%BB%E7%BB%93.md)



#### 集合类泄漏

集合类如果仅仅有添加元素的方法，没有相应的删除机制，导致内存被占用。如果这个类又是全局性变量(比如类中的静态属性，全局性的map等即有静态引用或者final一直指向它)那么没有相应的删除机制，很有可能导致集合所占用的内存只增不减

#### 单例造成的内存泄漏

由于单例的特性，使得单例的声明周期和应用的声明周期一样长，如果使用不恰当，很容易造成内存泄漏。

最明显的就是，一个静态类中传入了Activity的content，但是在Activity被结束之后，该静态类仍然存活，此时在静态类中含有该Activity的引用，得不到释放，造成内存泄漏。

#### 匿名内部类 && 非静态内部类 && 异步线程

- 非静态内部类创建静态实例,如下，TestResource为非静态内部类，但是在MainActivity中创建了静态实例，该静态实例的成名周期和整个应用的生命周期一样，这就导致该静态实例一直持有着MainActivity的一个引用，即使在MainActivity被摧毁的时候该引用仍然得不到清理，造成内存泄露。

```java
        public class MainActivity extends AppCompatActivity {
        private static TestResource mResource = null;
        @Override
        protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        if(mResource == null){
        mResource = new TestResource();
        }
        //...
        }
        class TestResource {
        //...
        }
        }
```

- 匿名内部类，当我们在Activity/Fragment中使用了匿名内部类，并被异步线程持有了，就需要注意了，例如，r1是实现接口，但是r2是匿名内部类的形式创建线程，此时如果MainActivity结束，但是r2又没有结束，就会导致r2持有MainActivity的引用没办法得到释放，导致内存泄漏。

```java
   public class MainActivity extends Activity {
    ...   
	Runnable r1 = new MyRunable();
    Runnable r2 = new Runnable() {
        @Override
        public void run() {

        }
    };
            ...
    }
```

#### Handler 造成的内存泄漏

Handler 的使用造成的内存泄漏问题应该说是最为常见了，很多时候我们为了避免 ANR 而不在主线程进行耗时操作，在处理网络任务或者封装一些请求回调等api都借助Handler来处理，但 Handler 不是万能的，对于 Handler 的使用代码编写一不规范即有可能造成内存泄漏。另外，我们知道 Handler、Message 和 MessageQueue 都是相互关联在一起的，万一 Handler 发送的 Message 尚未被处理，则该 Message 及发送它的 Handler 对象将被线程 MessageQueue 一直持有。

由于 Handler 属于 TLS(Thread Local Storage) 变量, 生命周期和 Activity 是不一致的。因此这种实现方式一般很难保证跟 View 或者 Activity 的生命周期保持一致，故很容易导致无法正确释放。

因此在使用Handler的时候，推荐使用静态内部类 + WeakReference 这种方式。每次使用前注意判空。

#### 尽量避免使用 static 成员变量

如果成员变量被声明为 static，那我们都知道其生命周期将与整个app进程生命周期一样。

注意：不要在类初始时初始化静态成员。可以考虑lazy初始化。 架构设计上要思考是否真的有必要这样做，尽量避免。如果架构需要这么设计，那么此对象的生命周期你有责任管理起来。

####　避免 重写finalize()

1、finalize 方法被执行的时间不确定，不能依赖与它来释放紧缺的资源。时间不确定的原因是： 虚拟机调用GC的时间不确定 ，Finalize daemon线程被调度到的时间不确定，JVM还没有快到耗尽内存的地步，它是不会浪费时间进行垃圾回收的。

2、finalize 方法只会被执行一次，即使对象被复活，如果已经执行过了 finalize 方法，再次被 GC 时也不会再执行了，原因是：

含有 finalize 方法的 object 是在 new 的时候由虚拟机生成了一个 finalize reference 在来引用到该Object的，而在 finalize 方法执行的时候，该 object 所对应的 finalize Reference 会被释放掉，即使在这个时候把该 object 复活(即用强引用引用住该 object )，再第二次被 GC 的时候由于没有了 finalize reference 与之对应，所以 finalize 方法不会再执行。

3、含有Finalize方法的object需要至少经过两轮GC才有可能被释放。

#### 资源未关闭造成的内存泄漏

对于使用了BraodcastReceiver，ContentObserver，File，游标 Cursor，Stream，Bitmap等资源的使用，应该在Activity销毁时及时关闭或者注销，否则这些资源将不会被回收，造成内存泄漏。

####　一些不良代码造成的内存压力

有些代码并不造成内存泄露，但是它们，或是对没使用的内存没进行有效及时的释放，或是没有有效的利用已有的对象而是频繁的申请新内存。

比如： Bitmap 没调用 recycle()方法，对于 Bitmap 对象在不使用时,我们应该先调用 recycle() 释放内存，然后才它设置为 null. 因为加载 Bitmap 对象的内存空间，一部分是 java 的，一部分 C 的（因为 Bitmap 分配的底层是通过 JNI 调用的 )。 而这个 recyle() 就是针对 C 部分的内存释放。 构造 Adapter 时，没有使用缓存的 convertView ,每次都在创建新的 converView。这里推荐使用 ViewHolder。