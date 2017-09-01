## Android 常用代码

#### ToolBar 菜单能够显示图标

重写onMenuOpened();方法，其他不需要改动

原理：通过java反射

```java
@Override
public boolean onMenuOpened(int featureId, Menu menu) {
    if (menu != null) {
        if (menu.getClass().getSimpleName().equalsIgnoreCase("MenuBuilder")) {
            try {
                Method method = menu.getClass().getDeclaredMethod("setOptionalIconsVisible", Boolean.TYPE);
                method.setAccessible(true);
                method.invoke(menu, true);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
    return super.onMenuOpened(featureId, menu);
}
```

#### getColor()方法

> 已被弃用，代替方法如下

```java
	//旧方法
	getResources().getColor(@ColorRes int id)；
	//新方法
	ContextCompat.getColor(Context context, @ColorRes int id);

	// 内部实现如下
    public static final int getColor(Context context, @ColorRes int id) {
        final int version = Build.VERSION.SDK_INT;
        if (version >= 23) {
            return ContextCompatApi23.getColor(context, id);
        } else {
            return context.getResources().getColor(id);
        }
    }
	//会对版本进行判断，进行优化
```

