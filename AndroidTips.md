#### Intent传递数据时，不能被传递的数据类型是**Thread**
* Serializable
* File
* Parcelable
* charssequence
* Bundle

#### 以下情况，系统可能会弹出ANR对话框

3.  在Activity中，Main线程消息队列中的消息在5秒内没有得到响应
4.  在Service中，onStartCommand()方法执行超过5秒
5.  在BroadcastReceiver中，onReceive()方法执行时间超过10秒

`UI线程阻塞时间超过20s会ANR，广播阻塞时间超过10s会ANR`

<!--more-->

#### Android系统对下列对象提供了资源池

4. Message
5. AsyncTask

`
Message提供了消息池，有静态方法Obtain从消息池中取对象；
Thread默认不提供资源池，除非使用线程池ThreadPool管理；
AsynTask是线程池改造的，默认提供最多5个线程进行并发操作；
Looper，每个Looper创建时创建一个消息队列和线程对象，也不是资源池；
`

#### IntentService 与 Service的关系是

5. IntentService 是 Service的子类
6. IntentService在运行时会启动新的线程来执行任务
7. 两者启动方式相同

#### 构造正确的对话框

* AlertDialog的构造方法被声明为protected，所以不能直接使用new关键字来创建AlertDialog类的对象实例。要想创建AlertDialog对话框，需要使用Builder类，该类是AlertDialog类中定义的一个内嵌类。因此必须创建AlertDialog.Builder类的对象实例，然后再调用show()来显示对话框。

```java
AlertDialog.Builder db= new Builder(this);
db..create().show();
```
* ProgressDialog的构造方法为public

```java
ProgressDialog pDialog;//进度条对话框对象
pDialog = new ProgressDialog(Context); //构造进度条对话框
```
* AlertDialog.Builder的create() 和show()方法都返回AlertDialog对象

#### 调用bindService()启动服务：会调用如下生命周期方法：     

```java
onCreate()---->onBind---->onDestory()---->onUnBind()
```
#### 关于广播

##### 注册广播方法一

```java
IntentFilter intentFilter = new IntentFilter("android.provider.Telephony.SMS_RECEIVED " );
registerReceiver( mBatteryInfoReceiver , intentFilter);

//第一个参数是我们要处理广播的BroadcastReceiver（广播接收者，可以是系统的，也可以是自定义的）;
//第二个参数是意图过滤器。
```


##### 注册广播方法二
```java
registerReceiver(receiver, filter, broadcastPermission, scheduler)
//第一个参数是 BroadcastReceiver (广播接收者，可以是系统的，也可以是自定义的)；
//第二个参数是意图过滤器；
//第三个参数是广播权限；
//第四个参数是   Hander
```

##### 代码中注销广播
```java
unregisterReceiver(mBatteryInfoReceiver);
```

#### 使用SimpleAdapter作为ListView的适配器，行布局中支持下列哪些组件？

* 使用SimpleAdapter作为适配器时，支持三种类型的 View，而且是按照如下顺序进行匹配：

	1. 继承Checkable接口
	2. TextView
	3. ImageView
