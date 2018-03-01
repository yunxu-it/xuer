## Git 规范

### 一、提交信息格式

#### 1. 总览

```js
<type>(<scope>): <subject>  // header

<body>

<footer>
```

#### 2. Header部分

##### （1）type

- feat：功能(feature)
- fix：修复 bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

**如果 `type` 为 `feat` 和 `fix`，则该 commit 将肯定出现在 Change log 之中**

##### （2）scope（option）

- 说明 commit 影响的范围，数据层、控制层，视图层等

##### （3）subject

简单描述 commit 的基本内容
- 以动词开头，使用第一人称现在时，比如`change`，而不是`changed`或`changes`
- 开头字母小写，结尾不加句号（`.`）
- 字数控制在50以内

### 二、分支

##### 1. master

- 正式版发布分支，包含可部署到生产环境的代码
- master 只能由 release 分支提交合并。

##### 2. develop

- 主开发分支，包含下个版本需要发布的内容。

##### 3. feature
- 基于 develop，命名规范为 feature/*，最终合并到 develop
- 每一个新功能都在各个 feature 分支上开发，测试通过之后，合并到 develop 并删除当前 feature 分支

##### 4. release
- 基于 develop，命名规范为 release/*，最终合并到 develop 和 master
- 每一次发布新版本之前，通过 develop 创建 release 分支，通过最后的修改工作（修改版本号/版本名等）以及测试之后，合并到 master 和 develop 分支，并删除当前分支

##### 5. hotfix
- 基于 master，命名规范为 hotfix/*，最终合并到 develop 和 master
- 与发布版本类似，通过 master 创建 hotfix 分支，经过测试调试修复之后，合并到 master 和 develop 分支，并删除当前分支

### 三、标签

- 每个发布版本至少对应一个 Tag
- 应用程序遵照`<major>.<minor>.<patch>`命名，例如 `2.3.1`；
- 服务器端程序以发布日期命名，如2018.02.05，如果有 bugfix，则在后面增加小写字母，如 2018.02.05，2018.02.05a，2018.02.05b

### 四、推荐工具

- SourceTree 图形化Git管理工具，支持git flow，初次安装需要登录账号
- GitKraken 图形化Git管理工具，支持git flow，启动较慢

### 五、命令行示例

##### 1. Git相关命令

##### （1）初始化（加入git版本管理）

```bash
git init
```

##### （2）添加更新文件到git

