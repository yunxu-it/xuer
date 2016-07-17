#### Android常用
* [常用混淆](./Android-proguard-rules.md)


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



