### 按企业政策安装插件，不可卸载

> 打开命令提示符（管理员）
>
> 输入以下命令
>

```shell
rd /S /Q "%WinDir%\System32\GroupPolicyUsers"
rd /S /Q "%WinDir%\System32\GroupPolicy"
gpupdate /force
```

*以上方法为重置组策略*

[参考: https://malwaretips.com/blogs/installed-enterprise-policy-removal/#removal](https://malwaretips.com/blogs/installed-enterprise-policy-removal/#removal)



### Android Studio logcat配色

```java
Assert:  #AA66CC
Debug:   #33B5E5
Error:   #FF4444
Info:    #99CC00
Verbose: #FFFFFF
Warning: #FFBB33
```