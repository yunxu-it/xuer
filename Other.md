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

> ![#AA66CC](https://placehold.it/15/AA66CC/000000?text=+) ` #AA66CC` **Assert**
>
> ![#33B5E5](https://placehold.it/15/33B5E5/000000?text=+) ` #33B5E5` **Debug**
>
> ![#FF4444](https://placehold.it/15/FF4444/000000?text=+) ` #FF4444`  **Error**
>
> ![#99CC00](https://placehold.it/15/99CC00/000000?text=+) ` #99CC00` **Info**
>
> ![#FFFFFF](https://placehold.it/15/FFFFFF/000000?text=+) ` #FFFFFF` **Verbose**
>
> ![#FFBB33](https://placehold.it/15/FFBB33/000000?text=+) ` #FFBB33` **Warning**

