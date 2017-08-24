## Tnink in Java 读书笔记

### 第七章 复用类

- 当创建一个子类的对象的时候，该对象包含一个父类的子对象

举例:

```java
public class A {
    public A() {
        System.out.println("A");
    }
}

public class B extends A{
    public B() {
        System.out.println("B");
    }
}

public class C extends B {
    public C() {
        System.out.println("C");
    }
}

public class Main {

    public static void main(String[] args) {
        C c = new C();
    }

}

// 运行输出结果是
A
B
C
Process finished with exit code 0
```

- 如果子类继承的父类只有`含参`构造器，在子类的构造其中必须调用父类的含参构造器，采用`super`关键字，否则报错

> 因为如果是一无参的构造器，编译器可以轻松调用，不需要考虑传递什么样的参数，如果是含参，则必须传递参数

#### 继承

> - 为新的类提供方法
> - 新类是现有类的一种类型

> 向上转型:从一个较专用的类型向较通用的类型转换

#### 抽象类

- 重构工具---->通过将公共方法沿着继承层的方式向上移动

#### 接口

- 只提供形式，未提供任何具体实现
- 表示“所有实现了该特定接口的类看起来都像这样”
- 被用来建立类与类之间的协议
- 允许有成员变量，默认都有`static` 和`final`关键字修饰