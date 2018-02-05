### Git 规范

### 一、提交信息格式

##### 1.1 总览

```js
<type>(<scope>): <subject>  // header

<body>

<footer>
```

##### 1.2 Header部分

###### （1）type

- feature：功能
- bug：修复 bug
- refactor：重构，不新增功能
- style：格式（不影响代码运行的变动）
- test：增加测试代码

### 二、分支管理

##### 1.1 Branch

> master 和 develop，其中所有的功能发布都应发到 develop 分支，master 只能由 develop 分支提交的 commit 合并。

##### 1.2 Tag

> 每个发布版本至少对应一个 Tag
>
> 应用程序遵照<major>.<minor>.<patch>命名，例如2.3.1；
>
> 服务器端程序以发布日期命名，如2018.02.05，如果有 bugfix，则在后面增加小写字母，如 2018.02.05，2018.02.05a，2018.02.05b