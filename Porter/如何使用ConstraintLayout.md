[原文地址](https://android.jlelse.eu/how-to-use-constraintlayout-736a78e2971c)

如果你很熟悉RelativeLayout，那么ConstraintLayout对你来说必定得心应手。ConstraintLayout相比RelativeLayout来说，具有更高的灵活性。一般情况下，你应该优先使用ConstraintLayout。

添加ConstraintLayout到项目中，需要添加以下代码到`build.gradle`文件中

```groovy
// Add the Google maven repository
repositories {
    maven {
        url 'https://maven.google.com'
    }
}

// Add to your app's dependencies
dependencies {
  compile 'com.android.support.constraint:constraint-layout:1.0.2'
}
```

我们先看一下RelativeLayout的示例。

我想得到以下的界面：

![img](https://cdn-images-1.medium.com/max/800/0*eMXq1Qtcg5AwuTpl.png)

为了达到这样的效果，如果使用RelativeLayout，需要如下代码：

```xml
<RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <TextView
            android:id="@+id/textView1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentLeft="true"
            android:background="@android:color/holo_blue_bright"
            android:text="1"
            android:textSize="44sp"/>

        <TextView
            android:id="@+id/textView2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_toRightOf="@+id/textView1"
            android:background="@android:color/holo_blue_dark"
            android:text="2"
            android:textSize="44sp"/>

        <TextView
            android:id="@+id/textView3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentRight="true"
            android:layout_toRightOf="@+id/textView2"
            android:background="@android:color/holo_green_dark"
            android:text="3"
            android:textSize="44sp"/>

        <TextView
            android:id="@+id/textView4"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@+id/textView1"
            android:layout_toRightOf="@+id/textView1"
            android:background="@android:color/holo_orange_dark"
            android:text="4"
            android:textSize="44sp"/>
</RelativeLayout>
```

