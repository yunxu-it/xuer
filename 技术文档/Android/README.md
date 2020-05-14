> 关于Android的相关记录

### 文件引导

- [特殊功能的代码块](./特殊功能.md)
- [编码或者运行安装时遇到的异常问题解决方式](./异常处理.md)
- [性能优化](./性能优化.md)
- [设计模式](./设计模式.md)

### 特殊代码

- 查看apk详细信息

  ```bash
  aapt dump badging *.apk
  
  // 需要先配置`build-tools`目录环境变量，如`ANDROID_HOME/build-tools/29.0.3`
  ```


- 查看apk签名类型

  ```bash
  // `apksigner` 命令来源于 `androidSdk/build-tools/*.*.*` 文件夹
  apksigner verify -v xxx.apk
  
  Verifies
  Verified using v1 scheme (JAR signing): true
  Verified using v2 scheme (APK Signature Scheme v2): false
  Verified using v3 scheme (APK Signature Scheme v3): false
  ```

### 未分类笔记

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

