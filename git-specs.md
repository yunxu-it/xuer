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

- 尽量使用英语，如果英语描述不准确，可使用中文


- 以动词开头，使用第一人称现在时，比如`change`，而不是`changed`或`changes`
- 开头字母小写，结尾不加句号（`.`）
- 字数控制在50以内

#### 3. Body部分

- 与 subject 部分相似，对本次提交进行详细的描述

#### 4. Footer部分
- **关闭Issue** 如果当前 commit 针对某个 issue，可以在 Footer 关闭此 issue
- **不兼容变动** 如果当前代码与上一版本不兼容，则 Footer 以 `BREAKING CHANGE` 开头，后面是对变动的描述、变动的理由以及迁移方法

#### 5. Revert(特殊)

- 如果当前 commit 用于撤销之前的 commit，则必须以 `revert:` 开头，后面跟着被撤销 commit 的 Header
- Body 部分写成 `This reverts commit <hash> ` ，`hash` 为被撤销 commit 的 SHA 标识符

```bash
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```



### 二、分支

#### 1. master

- 正式版发布分支，包含可部署到生产环境的代码
- master 只能由 release 分支提交合并

#### 2. develop

- 主开发分支，包含下个版本需要发布的内容

#### 3. feature
- 基于 develop，命名规范为 `feature/*`，最终合并到 develop
- 每一个新功能都在各个 feature 分支上开发，测试通过之后，合并到 develop 并删除当前 feature 分支

#### 4. release
- 基于 develop，命名规范为 `release/*`，最终合并到 develop 和 master
- 每一次发布新版本之前，通过 develop 创建 release 分支，通过最后的修改工作（修改版本号/版本名等）以及测试之后，合并到 master 和 develop 分支，并删除当前分支

**git flow 会根据分支名自动生成tag，故分支名以versionCode命名**

#### 5. hotfix
- 基于 master，命名规范为 `hotfix/*`，最终合并到 develop 和 master
- 与发布版本类似，通过 master 创建 hotfix 分支，经过测试调试修复之后，合并到 master 和 develop 分支，并删除当前分支

**git flow 会根据分支名自动生成tag，故分支名以versionCode命名**

### 三、标签

- 每个发布版本至少对应一个 Tag
- 应用程序遵照`<major>.<minor>.<patch>`命名，例如 `2.3.1`
- 服务器端程序以发布日期命名，如`2018.02.05`，如果有 bugfix，则在后面增加小写字母，如 `2018.02.05a`，`2018.02.05b`

### 四、推荐工具

- `SourceTree` 图形化Git管理工具，支持git flow，初次安装需要登录账号
- `GitKraken` 图形化Git管理工具，支持git flow，启动较慢

### 五、示例

#### 1.  commit 格式示例
```javascript
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
----------------------------------------------------------------------------
fix($compile): couple of unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
Breaks foo.bar api, foo.baz should be used instead
----------------------------------------------------------------------------
feat(directive): ng:disabled, ng:checked, ng:multiple, ng:readonly, ng:selected

New directives for proper binding these attributes in older browsers (IE).
Added coresponding description, live examples and e2e tests.

Closes #351
```
#### 2. 常用Git相关命令示例

##### （1）初始化（加入git版本管理）

```bash
git init # 初次加入git版本管理
git clone remote-url # 从远程仓库clone新代码库
```

##### （2）添加更新文件到git

```bash
git add filename.txt
git add . # 添加当前目录下的所有文件
```

##### （3）提交更新

```bash
git commit -m "feat: 增加了某功能"
# 进入vi编辑器，详细填写单行或多行 commit 信息（vim编辑器操作与一般编辑器不同，使用前需学习基本操作）
git commit -v 
```

#####（4）推送到远程仓库

```bash
git push origin master
# origin 远程仓库名
# master 远程仓库分支
```

#####（5）远程仓库管理

```bash
git remote -v # 查看当前远程仓库详情
git remote add origin "git@github.com:example/example.git" # 添加新的远程仓库
```

#####（6）分支管理

```bash
# 查看分支
git branch

# 创建 feature/f01 分支，并切换到 feature/f01 分支
git checkout -b feature/f01 
# 相当于以下两条命名
git branch feature/f01
git checkout feature/f01 

# 合并分支的新内容到当前分支，假设当前处于master分支
git merge feature/f01

# 删除分支
git branch -d feature/f01
```

#####（7）其他命令

```bash
# 查看提交记录
git log 
git log --pretty=oneline

# 当前状态
git status

# 撤销当前修改
git checkout -- filename.txt
```

#### 3. Git flow相关命令示例

#####（1）初始化

```bash
git flow init
# 以 git flow 格式初始化，选择默认即可
# 如已存在开发分支，则需先以 git flow 命名方式重命名
```

#####（2）开启新功能
```bash
git flow feature start feature-name
git flow feature finish feature-name
# finish 之前先 commit 当前修改
```

#####（3）发布版本
```bash
git flow release start 1.0.0
git flow release finish 1.0.0
```

#####（4）热修复
```bash
git flow hotfix start 1.0.1
git flow hotfix finish 1.0.1
```
