### 单元测试

##### 需要测试

1. 所有的Model、Presenter/ViewModel、Api、Utils等类的public方法
2. Data类除了getter、setter、toString、hashCode等一般自动生成的方法之外的逻辑部分
3. 自定义View的功能：比如set data以后，text有没有显示出来等等，简单的交互，比如click事件，负责的交互一般不测，比如touch、滑动事件等等。
4. Activity的主要功能：比如view是不是存在、显示数据、错误信息、简单的点击事件等。比较复杂的用户交互比如onTouch，以及view的样式、位置等等可以不测。因为不好测。

##### 需要注意

- 尽量写出易于测试的代码

> static method、直接new object、singleton、Global state等等这些都是一些不利于测试的代码方式，应该尽量避免，用依赖注入来代替这些方式。

