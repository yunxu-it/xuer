# 1、概述

Android系统中，涉及到多进程间的通信底层都是依赖于Binder IPC机制。

整个Android系统架构中，大量采用了Binder机制作为IPC（进程间通信，Interprocess Communication）方案。

例如当进程A中的Activity要向进程B中的Service通信，这便需要依赖于Binder IPC。

### 目的

- 性能

  在移动设备上，广泛使用跨进程通信对通信机制的性能有严格的要求。对比传统的 Socket 方式，Binder 更加高效。

  **Binder数据拷贝只需要一次，而管道、消息队列、Socket都需要2次，共享内存方式一次内存拷贝都不需要，但实现方式又比较复杂。**

- 安全

  传统的进程通信方式对于通信双方的身份并没有做出严格的验证，比如Socket通信的IP地址是客户端手动填入，很容易进行伪造。

  Binder机制从协议本身就支持对通信双方做身份校检，从而大大提升了安全性。

