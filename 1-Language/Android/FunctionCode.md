# 功能代码

## 基础功能

1. 获取唯一设备ID [Code](https://gist.github.com/yunxu-it/2c1d69bb238b4605fee9efaff664daff)


2. 透明状态栏

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

3. 默认EditText不获取 focus


```xml
//  在其父级组件添加以下代码
android:focusable="true"
android:focusableInTouchMode="true"
```

4. RecyclerView瀑布流


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

5. 全面屏适配

```xml
<meta-data android:name="android.max_aspect"
    android:value="ratio_float"/>
// value 最好在2.1以上，官方推荐
```
6. 去除 SearchView 下划线

```xml
app:queryBackground="@color/transparent"
```

## 项目配置

1. 多渠道打包

```groovy
// 渠道维度，用于区分版本、网络、api等类型
flavorDimensions "build"

productFlavors {
  stable {
    manifestPlaceholders = [app_name: "@string/app_name"]
  }
  extranet {
    // 包名后缀
    applicationIdSuffix ".extranet"
    // 版本名后缀
    versionNameSuffix "-extranet"
    // 属性替换
    manifestPlaceholders = [app_name: "App外网测试版"]
  }
  intranet {
    applicationIdSuffix ".intranet"
    versionNameSuffix "-intranet"
    manifestPlaceholders = [app_name: "App内网测试版"]
  } 
}

// 属性配置
<application
        android:name=".MainApplication"
        android:label="${app_name}"
        ...>
```

2. 自动修改apk名称

```groovy
// before gradle 3.1
applicationVariants.all { variant ->
  variant.outputs.each { output ->
    output.outputFileName = "app_v${defaultConfig.versionName}_${variant.buildType.name}_${variant.flavorName}.apk"
  }
}

// after gradle 3.1
android.applicationVariants.all { variant ->
    variant.outputs.all { output -> outputFileName = "app_v${defaultConfig.versionName}_${variant.buildType.name}_${variant.flavorName}.apk"
   }
}
```

   