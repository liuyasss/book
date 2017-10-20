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

https://juejin.im/entry/58ef265061ff4b0058db6b8b 第七条