# 终端命令

- 查看apk详细信息

  ```bash
  aapt dump badging *.apk
  
  需要先配置`build-tools`目录环境变量，如`ANDROID_HOME/build-tools/29.0.3`
  ```

- 使用管理员权限提交命令

```java
Runtime.getRuntime().exec("su -c \"command\"")
// 如果无效，使用双层""
Runtime.getRuntime().exec("su -c \"\"command\"\"")                        
```



- Android签名流程
  
  1. V1 签名
  
  ```bash
  // jarsigner 在java sdk中
  jarsigner -verbose 
  -keystore xxx.jks 
  -signedjar xxx.apk（签名后的apk名字） 
  xxx.apk（需要签名的apk） 
  xxx（keystore别名)
  ```
	2. zip对齐
	
  zip对齐，因为APK包的本质是一个zip压缩文档，经过边界对齐方式优化能使包内未压缩的数据有序的排列，从而减少应用程序运行时的内存消耗 ，通过空间换时间的方式提高执行效率
  
  ```bash
  需要先配置`build-tools`目录环境变量，如`ANDROID_HOME/build-tools/29.0.3`
  
  zipalign -v -p 4 input.apk output.apk
  
  zipalign命令选项：
  -f : 输出文件覆盖源文件
  -v : 详细的输出log
  -p : outfile.zip should use the same page alignment for all shared object files within infile.zip
  -c : 检查当前APK是否已经执行过Align优化。
  另外上面的数字4是代表按照4字节（32位）边界对齐。
  ```
  3. apksigner
  
  `v2签名方式 ` 是在Android7.0后才推出的，所以只有**版本>25**的SDK\build-tools\中才能找到apksigner.jar
  
  ```bash
  java -jar apksigner.jar sign  --ks key.jks  --ks-key-alias releasekey  --ks-pass pass:pp123456  --key-pass pass:pp123456  --out output.apk  input.apk
  
  java -jar apksigner.jar sign           	//执行签名操作
  --ks 你的jks路径                        //jks签名证书路径
  --ks-key-alias 你的alias           			//生成jks时指定的alias
  --ks-pass pass:你的密码          				 //KeyStore密码
  --key-pass pass:你的密码   							 //签署者的密码，即生成jks时指定alias对应的密码
  --out output.apk                        //输出路径
  input.apk                               //被签名的apk
  ```
  4. 查看apk签名类型
  
  ```bash
  `apksigner` 命令来源于 `androidSdk/build-tools/*.*.*` 文件夹
  
  apksigner verify -v xxx.apk
  
  Verifies
  Verified using v1 scheme (JAR signing): true
  Verified using v2 scheme (APK Signature Scheme v2): false
  Verified using v3 scheme (APK Signature Scheme v3): false
	```
  
- 使用 `gradle` 查看 Android依赖树

  ```bash
   ./gradlew :app:dependencies 

   # 根据条件查看
   ./gradlew :app:dependencies --configuration implementation
  ```

