## Origin

### Base

#### 自定义字体

```java
// 得到TextView控件对象
TextView textView = (TextView) findViewById(R.id.custom);
// 将字体文件保存在assets/fonts/目录下，www.linuxidc.com创建Typeface对象
Typeface typeFace = Typeface.createFromAsset(getAssets(),"fonts/DroidSansThai.ttf");
// 应用字体
textView.setTypeface(typeFace);
```
#### CPU架构

|  日期   |         |    2010+    | 2011+ | 2012+ |           |        | 2014+  |
| :---: | :-----: | :---------: | :---: | :---: | :-------: | :----: | :----: |
| CPU架构 |  ARMv5  |    ARMv7    |  x86  | MIPS  |   ARMv8   | MIPS64 | x86_64 |
| 对应ABI | armeabi | armeabi-v7a |  x86  | mips  | arm64-v8a | mips64 | x86_64 |

#### 使用android-21平台版本编译的.so文件运行在android-15的设备上

使用NDK时，你可能会倾向于使用最新的编译平台，但事实上这是错误的，因为NDK平台不是后向兼容的，而是前向兼容的。推荐使用app的minSdkVersion对应的编译平台。

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



### UI

#### RecyclerView

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

## IDE

### gradle

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

## Third-Party

### Realm

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

### Rxjava

#### duplicate files copied in apk meta-inf/rxjava.properties

> 当Rxjava1和Rxjava2同时出现就可能出现这个情况，但是如果只保留了一个版本，编译之后还出现这种情况，就要看看是否遗漏了`adapter-rxjava`与`adapter-rxjava2`的版本切换







