#### Android常用
* [常用混淆](./Android-proguard-rules.md)

#### SwipeRefreshLayout自动刷新（转自<http://www.jianshu.com/p/fb0d5f9adf82>）

初次进入页面自动刷新直接使用
```
	swipeRefreshLayout.setRefreshing(true)
```
是无效的

可以使用以下方法
```
	swipeRefreshLayout.post(new Runnable() {
	    @Override    
	   public void run() {
	       swipeRefreshLayout.setRefreshing(true);
	    }
	});
```

#### Fragment 嵌套 Fragment 白屏问题

本来里面的fragment用的还是getFragmentManager,Fragment嵌套Fragment时，里面要用getChildFragmentManager。(转至<http://www.cnblogs.com/rewufu/p/4499949.html>)

```java
FragmentManager childFragmentManager = getChildFragmentManager();
ViewPager_Adapter viewPager_adapter = new ViewPager_Adapter(childFragmentManager, fragments);　　　　//FragmentPagerAdapter
```

#### No layout manager attached; skipping layout错误

原因是没有设置LayoutManager
```java
mRecyclerView.setLayoutManager(new LinearLayoutManager(this));//这里用线性显示 类似于listview
//        mRecyclerView.setLayoutManager(new GridLayoutManager(this, 2));//这里用线性宫格显示 类似于grid view
//        mRecyclerView.setLayoutManager(new StaggeredGridLayoutManager(2, OrientationHelper.VERTICAL));//这里用线性宫格显示 类似于瀑布流
```

#### 在Xml文件中使用tools命名空间

- 为了看到预览效果，我们常常会在xml文件中添加测试数据，但是写完之后，常常忘记删除，这样会显示无用数据
- 我们可以通过tools命名空间解决

```
xmlns:tools="http://schemas.android.com/tools"
```
- tools可以告诉Android Studio，哪些属性在运行的时候是被忽略的，只在设计布局的时候有效。
- 比如我们要让android:text属性只在布局预览中有效可以这样

```
<TextView
		 android:id="@+id/TextView"
		 android:layout_width="wrap_content"
		 android:layout_height="wrap_content"
		 tools:text="show for preview" />
```

#### 从Eclipse迁移到Android Studio出现错误（找不到.9文件）(关键词: android studio)

- 需要重新制作.9文件
- AS中可以对.9文件直接修改,亦可以使用sdk中的draw9patch.bat来制作

*在Android studio 里面要求 .9图片必须要 左侧和上侧都要画线，如果只有一侧画线会导致运行不起来。切记 ！！！*

#### What's the difference between `commit()` and `apply()` in Shared Preference? (关键词: sharedpreference)

- `apply()` was added in 2.3, it commits without returning a boolean indicating success or failure.
- `commit()` returns true if the save works, false otherwise.
- `apply()` was added as the Android dev team noticed that almost no one took notice of the return value, so apply is faster as it is asynchronous.

#### 涉及progress的，可以在子线程刷新UI (关键词: 线程/Thread)

* [非UI线程可以去刷新UI吗（timertask调用progressbar的setProgress的特例)](http://blog.csdn.net/androidzhaoxiaogang/article/details/8136222)

#### 设置横屏不重新执行onCreate方法 (关键词: activity)

- 设置android:configChanges属性

	```java
	android:configChanges="orientation" //此设置为改变方向是不重新onCreate
	```
- 设置

	```java
	android:screenOrientation="landscape" //固定竖屏
	```

#### [关于Fragment(XXFragment) not attached to Activity 异常](http://www.eoeandroid.com/blog-469851-3594.html) (关键词: fragment)

- 出现该异常，是因为Fragment的还没有Attach到Activity时，调用了如getResource()等，需要上下文Context的函数。解决方法，就是等将调用的代码写在OnStart()中。

- **[stackoverflow回答](http://stackoverflow.com/questions/10919240/fragment-myfragment-not-attached-to-activity)**

#### 给ListView的item设定高度无效 (关键词: listview)

- 给item设置minHeight
- 给item中的控件设置高度，撑大item

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

#### 使用getBackground().setAlpha，导致其他布局背景透明度都改变的问题 (关键词: 透明度)

- 在布局中多个控件同时使用一个资源的时候，这些控件会共用一个状态，例如ColorState，如果你改变了一个控件的状态，其他的控件都会接收到相同的通知。这时我们可以使用mutate()方法使该控件状态不定，这样不定状态的控件就不会共享自己的状态了。

	```java
	titleLayout.getBackground().mutate().setAlpha(255);
	```

#### android.content.res.Resources$NotFoundException: String resource ID (关键词: NotFoundException)

- 在setText()中使用了int的参数，被误以为Resources的ID，更改为String类型就行

#### 以下情况，系统可能会弹出ANR对话框 (关键词: ANR)

-  在Activity中，Main线程消息队列中的消息在5秒内没有得到响应
-  在Service中，onStartCommand()方法执行超过5秒
-  在BroadcastReceiver中，onReceive()方法执行时间超过10秒

`UI线程阻塞时间超过20s会ANR，广播阻塞时间超过10s会ANR`


#### 关于广播 (关键词: BroadcastReceiver)

- 注册广播方法一

	```java
	IntentFilter intentFilter = new IntentFilter("android.provider.Telephony.SMS_RECEIVED " );
	registerReceiver( mBatteryInfoReceiver , intentFilter);

	//第一个参数是我们要处理广播的BroadcastReceiver（广播接收者，可以是系统的，也可以是自定义的）;
	//第二个参数是意图过滤器。
	```


- 注册广播方法二
	```java
	registerReceiver(receiver, filter, broadcastPermission, scheduler)
	//第一个参数是 BroadcastReceiver (广播接收者，可以是系统的，也可以是自定义的)；
	//第二个参数是意图过滤器；
	//第三个参数是广播权限；
	//第四个参数是   Hander
	```

- 代码中注销广播
	```java
	unregisterReceiver(mBatteryInfoReceiver);
	```
