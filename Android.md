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







