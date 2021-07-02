## Kotlin

#### **with** 对一个对象调用多个方法

```kotlin
class Turtle {
    fun penDown()
    fun penUp()
    fun turn(degrees: Double)
    fun forward(pixels: Double)
}

val myTurtle = Turtle()
with(myTurtle) { // 画一个 100 像素的正方形
    penDown()
    for (i in 1..4) {
        forward(100.0)
        turn(90.0)
    }
    penUp()
}
```

#### **apply** 配置对象属性

```kotlin
val myRectangle = Rectangle().apply {
    length = 4
    breadth = 5
    color = 0xFAFAFA
}
```

#### let 

```kotlin
object.let{
   it.todo()//在函数体内使用it替代object对象去访问其公有的属性和方法
   ...
}

//另一种用途 判断object为null的操作
object?.let{//表示object不为null的条件下，才会去执行let函数体
   it.todo()
}
```

