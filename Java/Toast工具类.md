## Toast工具类

####  ToastUtils

```java
public class ToastUtils {

    private static Toast toast;

    /**
     * 短时间显示 Toast,位置居下
     *
     * @param msg 显示字符串
     */
    public static void showShortToast(String msg) {
        if (getAppContext() != null) {
            if (toast == null) {
                toast = Toast.makeText(getAppContext(), msg, Toast.LENGTH_SHORT);
            } else {
                toast.setText(msg);
            }
        }
        toast.show();
    }

    /**
     * 短时间显示 Toast,位置居中
     *
     * @param msg 显示字符串
     */
    public static void showShortToastCenter(String msg) {
        if (getAppContext() != null) {
            if (toast == null) {
                toast = Toast.makeText(getAppContext(), msg, Toast.LENGTH_SHORT);
                toast.setGravity(Gravity.CENTER, 0, 0);
            } else {
                toast.setText(msg);
            }
        }
        toast.show();
    }

    /**
     * 短时间显示Toast【居上】
     *
     * @param msg 显示的内容-字符串
     */
    public static void showShortToastTop(String msg) {
        if (MyAPP.getAppContext() != null) {
            if (toast == null) {
                toast = Toast.makeText(MyAPP.getAppContext(), msg, Toast.LENGTH_SHORT);
                toast.setGravity(Gravity.TOP, 0, 0);
            } else {
                toast.setText(msg);
            }
            toast.show();
        }
    }

    /**
     * 长时间显示Toast【居下】
     *
     * @param msg 显示的内容-字符串
     */
    public static void showLongToast(String msg) {
        if (MyAPP.getAppContext() != null) {
            if (toast == null) {
                toast = Toast.makeText(MyAPP.getAppContext(), msg, Toast.LENGTH_LONG);
            } else {
                toast.setText(msg);
            }
            toast.show();
        }
    }

    /**
     * 长时间显示Toast【居中】
     *
     * @param msg 显示的内容-字符串
     */
    public static void showLongToastCenter(String msg) {
        if (MyAPP.getAppContext() != null) {
            if (toast == null) {
                toast = Toast.makeText(MyAPP.getAppContext(), msg, Toast.LENGTH_LONG);
                toast.setGravity(Gravity.CENTER, 0, 0);
            } else {
                toast.setText(msg);
            }
            toast.show();
        }

```

#### MyAPP

```java
public class MyAPP extends Application {

    private static Context AppContext;

    @Override
    public void onCreate() {
        super.onCreate();
        AppContext = getApplicationContext();
    }

    public static  Context getAppContext(){
        return AppContext;
    }
}
```



