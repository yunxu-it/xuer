1. 在 `Created` 获取服务端数据
2. `@hook` 用于监听子组件生命周期时间（例如： `mounted`, `created`）
3. 组件是用来复用的。如果 `data` 是对象，那么作用域之间没有隔离，子组件的 `data` 会相互影响
4. `v-bind: => :`  `v-on: => @`
5. 事件侦听
   1. `$on(eventName, eventHandler)` 侦听一个事件
   2. `$once(eventName, eventHandler)` 一次性侦听一个事件
   3. `$off(eventName, eventHandler)` 取消侦听一个事件，
6. `v-if` 惰性的条件渲染，如果开始为假，则不会渲染，相较 `v-show` 只改动显隐，有更高的切换开销，所以需要频繁切换使用 `v-show`，较少改变使用 `v-if`

6. 生命周期

   ![Vue 实例生命周期](https://cn.vuejs.org/images/lifecycle.png){:height="50%" width="50%"}

