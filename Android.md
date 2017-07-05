### Android

#### 涉及progress的，可以在子线程刷新UI (关键词: 线程/Thread)

* [非UI线程可以去刷新UI吗（timertask调用progressbar的setProgress的特例)](http://blog.csdn.net/androidzhaoxiaogang/article/details/8136222)

#### 在使用Fragment保存参数的时候，可能是因为需要保存的参数比较大或者比较多，引起异常(关键词: fragment)

- 开始

  ```java
  Bundle b = new Bundle();
  b.putParcelable("bitmap", bitmap2);
  imageRecognitionFragment.setArguments(b);
  ```

- 设置好参数，并且添加hide(),add()方法之后，需要commit()，来实现两个Fragment跳转的时候，这种情形下参数需要进行系统保存，但是这个时候你已经实现了跳转，系统参数却没有保存。
  则会引起异常

  ```java
  java.lang.IllegalStateException: Can not perform this action after onSaveInstanceState
  ```

- 你并不需要系统保存的参数，只要你自己设置的参数能够传递过去，在另外一个Fragment里能够顺利接受就行了，现在android里提供了另外一种形式的提交方式commitAllowingStateLoss()，从名字上就能看出，这种提交是允许状态值丢失的。
### Android Studio
#### Android Duplicate files copied in APK
原因是依赖库文件重合了

打开项目下面的 build.gradle 文件，在 android 代码块中添加下面代码

```java
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
### Realm

#### Relam自动更新导致fori数据出错

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

当Rxjava1和Rxjava2同时出现就可能出现这个情况，但是如果只保留了一个版本，编译之后还出现这种情况，就要看看是否遗漏了`adapter-rxjava`与`adapter-rxjava2`的版本切换







