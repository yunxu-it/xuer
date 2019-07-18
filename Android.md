## Todo 

- [ ] A resource failed to call destroy

## Solution

#### 获取唯一设备ID

```java
// 好处：

// 1.不需要特定权限.
// 2.在99.5% Android装置（包括root过的）上，即API => 9，保证唯一性.
// 3.重装app之后仍能取得相同唯一值.
     
public static String getUniquePsuedoID() {
    // If all else fails, if the user does have lower than API 9 (lower
    // than Gingerbread), has reset their device or 'Secure.ANDROID_ID'
    // returns 'null', then simply the ID returned will be solely based
    // off their Android device information. This is where the collisions
    // can happen.
    // Thanks http://www.pocketmagic.net/?p=1662!
    // Try not to use DISPLAY, HOST or ID - these items could change.
    // If there are collisions, there will be overlapping data
    String m_szDevIDShort = "35"
        + (Build.BOARD.length() % 10)
        + (Build.BRAND.length() % 10)
        + (Build.DEVICE.length() % 10)
        + (Build.MANUFACTURER.length() % 10)
        + (Build.MODEL.length() % 10)
        + (Build.PRODUCT.length() % 10);

    // Thanks to @Roman SL!
    // http://stackoverflow.com/a/4789483/950427
    // Only devices with API >= 9 have android.os.Build.SERIAL
    // http://developer.android.com/reference/android/os/Build.html#SERIAL
    // If a user upgrades software or roots their device, there will be a duplicate entry
    String serial = null;
    try {
      serial = android.os.Build.class.getField("SERIAL").get(null).toString();

      // Go ahead and return the serial for api => 9
      return new UUID(m_szDevIDShort.hashCode(), serial.hashCode()).toString();
    } catch (Exception exception) {
      // String needs to be initialized
      serial = "serial"; // some value
    }

    // Thanks @Joe!
    // http://stackoverflow.com/a/2853253/950427
    // Finally, combine the values we have found by using the UUID class to create a unique identifier
    return new UUID(m_szDevIDShort.hashCode(), serial.hashCode()).toString();
  }
```



#### ImageView 设置 MaxHeight 无效 

> An optional argument to supply a maximum height for this view. Only valid if `setAdjustViewBounds(boolean)` has been set to true. 

```xml
// 此二者必须同时存在
android:adjustViewBounds="true"
android:maxHeight="10dp"
```

#### 单例模式

```java
// 基础懒汉式，线程不安全
public class Singleton {
    private static Singleton instance;
    private Singleton (){}
    public static Singleton getInstance() {
     if (instance == null) {
         instance = new Singleton();
     }
     return instance;
    }
}

// 静态内部类
public class Singleton {
    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }
    private Singleton (){}
    public static final Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}

// 枚举
public enum Singleton{
    INSTANCE;
}
```

#### Android Duplicate files copied in APK

```groovy
android {
	packagingOptions {
        exclude 'META-INF/DEPENDENCIES'
        exclude 'META-INF/NOTICE'
        exclude 'META-INF/LICENSE'
        exclude 'META-INF/LICENSE.txt'
        exclude 'META-INF/NOTICE.txt'
    }
}
```

#### 透明状态栏

```Java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
      // 透明状态栏，导航栏
      View decorView = getWindow().getDecorView();
      int option = View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
          | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN
          | View.SYSTEM_UI_FLAG_LAYOUT_STABLE;
      decorView.setSystemUiVisibility(option);
      getWindow().setNavigationBarColor(Color.TRANSPARENT);
      getWindow().setStatusBarColor(Color.TRANSPARENT);
}

if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M && useStatusBarColor) {
      // Android6.0以后可以对状态栏文字颜色和图标进行修改
      getWindow().getDecorView() .setSystemUiVisibility(View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN | View.SYSTEM_UI_FLAG_LIGHT_STATUS_BAR);
}
```

#### 默认EditText不获取 focus


```xml
//  在其父级组件添加以下代码
android:focusable="true"
android:focusableInTouchMode="true"
```

#### RecyclerView瀑布流


```java
// 瀑布流位置变化
layoutManager.setGapStrategy(StaggeredGridLayoutManager.GAP_HANDLING_NONE);

// 瀑布流顶部留白
mRecyclerView.addOnScrollListener(new RecyclerView.OnScrollListener() {
  @Override
  public void onScrollStateChanged(RecyclerView recyclerView, int newState) {
    super.onScrollStateChanged(recyclerView, newState);
    //防止第一行到顶部有空白区域
    layoutManager.invalidateSpanAssignments();
  }
});
```

#### Vivo安装apk异常


1. 多数手机安装apk调试异常，都与instant run冲突有关

2. 解析包错误异常

   ```groovy
   # 在gradle.properties里面添加
   android.injected.testOnly=false
   ```

#### fori循环更新出错

```java
 RealmResults<Data> dataList = realm.where(Data.class)
                        .equalTo("example", true)
                        .findAll();
 //size = 2
 for (int i = 0; i < dataList.size(); i++) {
     dataList.get(i).setExample(false);
 }
//当经过一次循环，i为1时，dataList的size变成了1,结果是只有一半的数据操作成功
//所以最好使用如下方法
 for (Data data : dataList) {
     data.setExample(false);
 }
```

#### 高德地图Memory Leak

如果开启了`amap.setMyLocationEnabled(true)`

记得在你 `onDestroy`内设置`amap.setMyLocationEnabled(false)`

```Java
@Override
public void onDestroy() {
	super.onDestroy();
    mMapView.onDestroy();
    if (mMap != null) {
        mMap.setMyLocationEnabled(false);
        mMap.clear();
    }
}
```

#### Glide默认图，error图使用circleCrop无效

```kotlin
// Glide提供了Transformation 可以让图片显示成各种样式，但是使用Transformation时会有个问题，比如使用CircleCrop时预览图和加载失败后显示的图并不是圆形 https://www.jianshu.com/p/c087239333e0
Glide.with(it).load(userData.avatar)
    .error(Glide.with(it).load(R.mipmap.photo).circleCrop())
    .diskCacheStrategy(DiskCacheStrategy.ALL)
    .circleCrop()
    .into(avatar)
```

#### org.simpleframework.xml.core.PersistenceException: Constructor not matched for class

Java默认有一个无参构造函数，但是一旦创建了一个有参构造函数，无参构造函数就需要自己重新定义,而当前问题的原因就是无参构造函数找不到。

#### 全面屏适配

- 官方推荐

```xml
<meta-data android:name="android.max_aspect"
    android:value="ratio_float"/>
// value 最好在2.1以上
```



## Note

#### CPU架构

|  日期   |         |    2010+    | 2011+ | 2012+ |           |        | 2014+  |
| :---: | :-----: | :---------: | :---: | :---: | :-------: | :----: | :----: |
| CPU架构 |  ARMv5  |    ARMv7    |  x86  | MIPS  |   ARMv8   | MIPS64 | x86_64 |
| 对应ABI | armeabi | armeabi-v7a |  x86  | mips  | arm64-v8a | mips64 | x86_64 |

- 使用android-21平台版本编译的.so文件运行在android-15的设备上

  使用NDK时，你可能会倾向于使用最新的编译平台，但事实上这是错误的，因为NDK平台不是后向兼容的，而是前向兼容的。推荐使用app的minSdkVersion对应的编译平台。
  
  

#### 视图类优化

- 移除布局中不需要的背景（`theme`自带背景）

  ```xml
  // 方法一
  <style name="AppTheme" parent="parent">
      <item name="android:windowBackground">@null</item>
  </style>
  
  // 方法二，在onCreate()中使用
  getWindow().setBackgroundDrawable(null);
  ```

- 移除控件不需要的背景

- 扁平化layout

  - `LinearLayout`使用`layout_weight`时，子View需要测量两次，特别是List时，重复测量多次
  - 减少布局的嵌套，使用merge标签合并相同布局嵌套，使用include复用布局
  - 使用lint来优化布局的层次结构，相关优化意见在`Android>Lint>Performance`

- 多张重叠图层使用，使用clipRect()减少自定义View的过度绘制

- 使用更优布局

  - 在无嵌套布局的情况下，`FrameLayout`和`LinearLayout`的性能比`RelativeLayout`更好。因为`RelativeLayout`会测量每个子节点两次
  - `ConstraintLayout`的性能比`RelativeLayout`更好，推荐使用`ConstraintLayout`。后面会介绍`ConstraintLayout`的使用

- 使用ViewStub延迟加载

- onDraw()中不要创建新的局部变量，不做耗时操作

##### 来源

- [那些 Android 程序员必会的视图优化策略](https://mp.weixin.qq.com/s/ep-Assy2j_EOUW8uWUQfSQ)

#### Activity

##### 生命周期

- onUserInteraction

> activity在分发各种事件的时候会调用该方法（只要与用户在进行交互）
>
> 注意：启动另一个activity，Activity#onUserInteraction()会被调用两次，一次是activity捕获到事件，另一次是调用Activity#onUserLeaveHint()之前会调用Activity#onUserInteraction()。
>
> 使用场景：监听用户是否长时间未交互(屏保)

- onUserLeaveHint

> 用户手动离开当前activity，会调用该方法，比如用户主动切换任务，短按home进入桌面等。
>
> 系统自动切换activity不会调用此方法，如来电，灭屏等。
>
> 使用场景：监听用户主动离开页面(home，back，menu 键)