#### 注意事项

##### org.simpleframework.xml.core.PersistenceException: Constructor not matched for class

Java默认有一个无参构造函数，但是一旦创建了一个有参构造函数，无参构造函数就需要自己重新定义。

而当前问题的原因就是无参构造函数找不到。