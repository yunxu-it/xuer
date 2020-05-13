### App 安装运行异常原因记录

> 多数情况与`instant run`有关，优先检查

#### 解析包错误异常

- Vivo 手机
  ```gradle
  # 在gradle.properties里面添加
  android.injected.testOnly=false
  ```

- 小米平板

  ```bash
  在 Android4.4.4 异常，高版本正常
  
  Installation did not succeed.
  The application could not be installed.
Installation failed due to: 'UNKNOWN'
  
  解决方法：安装包名称含有`中文或者中文冒号`
  ```
  
  