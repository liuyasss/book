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

