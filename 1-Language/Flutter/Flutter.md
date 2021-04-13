# Flutter笔记

## Solution

#### bottom overflowed by * PIXELS

使用 `SingleChildScrollView` 包裹即可



## Note

####  性能优化

1. 优先使用` StatelessWidget`，含有大量子 Widget（如根布局、次根布局）慎用 `StatefulWidget`，尽量在叶子节点使用 `StatefulWidget`

2. 将会调用到setState((){}) 的代码尽可能的和要更新的视图封装在一个尽可能小的模块里。如果一个Widget需要reBuild，那么它的子节点、兄弟节点、兄弟节点的子节点应该尽可能少

#### 避坑

1. 打印错误信息，不要使用`print('exception='+e)`

```dart
// 因为当e为null，print 语句会报错，+ 号连接的左右不能是 null，所以不会正常打印
//替换写法一
print('exception=');
print(e);
//替换写法二
print('exception='+(e ?? ''));
//替换写法三
var printContent = e ?? '';
print('exception='+printContent);
```



