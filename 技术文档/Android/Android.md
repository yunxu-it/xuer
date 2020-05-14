### Todo

- [ ] A resource failed to call destroy

### 异常处理

- ImageView 设置 MaxHeight 无效 

```xml
// An optional argument to supply a maximum height for this view. Only valid if `setAdjustViewBounds(boolean)` has been set to true. 
// 此二者必须同时存在
android:adjustViewBounds="true"
android:maxHeight="10dp"
```

- Android Duplicate files copied in APK

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

- Glide默认图，error图使用circleCrop无效

```kotlin
// Glide提供了Transformation 可以让图片显示成各种样式，但是使用Transformation时会有个问题，比如使用CircleCrop时预览图和加载失败后显示的图并不是圆形 https://www.jianshu.com/p/c087239333e0
Glide.with(it).load(userData.avatar)
    .error(Glide.with(it).load(R.mipmap.photo).circleCrop())
    .diskCacheStrategy(DiskCacheStrategy.ALL)
    .circleCrop()
    .into(avatar)
```

- 三方库属性与项目属性冲突

  在 `Application` 节点加入 `tools:replace` 属性

  例如： `tools:replace="android:icon, android:label"` 

#### 内存泄露

- 高德地图Memory Leak

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

### 功能代码

- 获取唯一设备ID [Code](https://gist.github.com/yunxu-it/2c1d69bb238b4605fee9efaff664daff)


- 透明状态栏

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

- 默认EditText不获取 focus


```xml
//  在其父级组件添加以下代码
android:focusable="true"
android:focusableInTouchMode="true"
```

- RecyclerView瀑布流


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

- 全面屏适配

```xml
<meta-data android:name="android.max_aspect"
    android:value="ratio_float"/>
// value 最好在2.1以上，官方推荐
```

#### 视图类优化

[那些 Android 程序员必会的视图优化策略](https://mp.weixin.qq.com/s/ep-Assy2j_EOUW8uWUQfSQ)

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

#### Note

##### CPU架构

|  日期   |         |    2010+    | 2011+ | 2012+ |           |        | 2014+  |
| :---: | :-----: | :---------: | :---: | :---: | :-------: | :----: | :----: |
| CPU架构 |  ARMv5  |    ARMv7    |  x86  | MIPS  |   ARMv8   | MIPS64 | x86_64 |
| 对应ABI | armeabi | armeabi-v7a |  x86  | mips  | arm64-v8a | mips64 | x86_64 |

- 使用android-21平台版本编译的.so文件运行在android-15的设备上

  使用NDK时，你可能会倾向于使用最新的编译平台，但事实上这是错误的，因为NDK平台不是后向兼容的，而是前向兼容的。推荐使用app的minSdkVersion对应的编译平台。
  

##### Activity

###### 生命周期

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

### 命令技巧

- 查看apk签名类型

```shell
// apksigner命令来源于 androidSdk/build-tools/*.*.* 文件夹
apksigner verify -v xxx.apk

Verifies
Verified using v1 scheme (JAR signing): true
Verified using v2 scheme (APK Signature Scheme v2): false
Verified using v3 scheme (APK Signature Scheme v3): false
```
