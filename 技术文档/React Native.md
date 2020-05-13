![](https://img.shields.io/badge/ReactNative-0.45+-green.svg)

#### import React来源问题

0.45正式版更新，**移除从 ‘react-native’ 中导入 React 的错误警告**，从 ‘react-native’ 中导入 react 模块早在 0.25 的版本中被比标记为过期，现在如果再继续这样导入会直接报错。

#### Android 5.0以下真机调试红屏问题

1. 手机电脑处于同一网段下（电脑使用网线，手机wifi亦可）
2. 打开开发者菜单（摇晃设备或运行`adb shell input keyevent 82`）
3. `Dev Settings` -> `Debug server host for device` -> 输入电脑IP:8081(例如：10.10.1.1:8081)

4. Reload JS

> **重点：如果上面的方法没有效果，需要检查电脑防火墙是否屏蔽了NodeJS** 

#### 运行失败

> Could not install the app on the device, read the error above for details.
> Make sure you have an Android emulator running or a device connected and have
> set up your Android development environment:
> https://facebook.github.io/react-native/docs/getting-started.html

- 检查`gradlew`权限是否可执行