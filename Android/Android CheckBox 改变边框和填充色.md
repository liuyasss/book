## Android CheckBox 改变边框和填充色

>  参考来自http://blog.csdn.net/vaneasley/article/details/64127792

如果我们想要改变边框和填充色，同时也保存material design动画效果，应该怎么做呢。 

需要新建一个`style`：

```xml
<style name="My_CheckBox" parent="@android:style/Widget.Material.CompoundButton.CheckBox">
        <item name="android:colorControlActivated">@color/colorAccent</item>
        <item name="android:colorControlNormal">@color/colorPrimary</item>
</style>
```

设置checkbox 时如下

```xml
<CheckBox
    android:id="@+id/save_pass"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:theme="@style/My_CheckBox"/>	<!--需要注意的是 用theme 而不是 style -->
```

ps：如果`style` 不起作用

修改为如下

```xml
<item name="android:colorControlNormal" tools:targetApi="lollipop">@color/colorPrimaryDark</item>
```



> 测试的平台：AS 3.0 ，Android 5.1

