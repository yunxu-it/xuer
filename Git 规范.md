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

- feat：功能(feature)
- fix：修复 bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

**如果 `type` 为 `feat` 和 `fix`，则该 commit 将肯定出现在 Change log 之中**

##### (2) scope（option）

- 说明 commit 影响的范围，数据层、控制层，视图层等

##### (3) subject

- 简单描述 commit 的基本内容
  - 以动词开头，使用第一人称现在时，比如`change`，而不是`changed`或`changes`
  - 第一个字母小写
  - 结尾不加句号（`.`）

### 二、分支管理

##### 1.1 Branch

> master 和 develop，其中所有的功能发布都应发到 develop 分支，master 只能由 develop 分支提交的 commit 合并。

##### 1.2 Tag

> 每个发布版本至少对应一个 Tag
>
> 应用程序遵照`<major>.<minor>.<patch>`命名，例如 `2.3.1`；
>
> 服务器端程序以发布日期命名，如2018.02.05，如果有 bugfix，则在后面增加小写字母，如 2018.02.05，2018.02.05a，2018.02.05b

### 三、推荐工具

1. SourceTree 图形化Git管理工具，支持git flow。
2. Commitizen commit格式规范工具。

