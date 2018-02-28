

# 四大组件

## Activity

### 生命周期

#### onUserInteraction

> activity在分发各种事件的时候会调用该方法（只要与用户在进行交互）
>
> 注意：启动另一个activity，Activity#onUserInteraction()会被调用两次，一次是activity捕获到事件，另一次是调用Activity#onUserLeaveHint()之前会调用Activity#onUserInteraction()。

使用场景：监听用户是否长时间未交互(屏保)

##### onUserLeaveHint

> 用户手动离开当前activity，会调用该方法，比如用户主动切换任务，短按home进入桌面等。
>
> 系统自动切换activity不会调用此方法，如来电，灭屏等。

使用场景：监听用户主动离开页面(home，back，menu 键)