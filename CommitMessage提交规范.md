https://www.cnblogs.com/wuhairui/p/13679944.html

最近在实习，写了一个小需求。本地调试没问题后，提交代码，发现一直有两个错误：

```powershell
subject may not be empty [subject-empty]
type may not be empty [type-empty]
```

Mentor 指出，是我提交时的 Commit Message 不规范造成的。

后来自己学习了一下 Commit Message 规范，记录成此笔记，若有不妥之处，欢迎批评指出～

## Commit Message 组成

按照业界流行的 [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) 的相关规定，一个 Commit Message 的格式如下：

```powershell
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

整体的格式：

- 包含三个部分：Header、Body、Footer
- 其中，Header 是必需的，而 Body 和 Footer 可选
- 每个部分之间有一个**空行**
- 每行内容长度不能超过 100 个字符

## 每部分规范说明

### Header（必写）

```powershell
<type>(<scope>): <subject>
```

> 注意：冒号`:`和`<subject>`之间有一个**空格**。

（1）type

必填项，表示本次改动的提交类型，包括的类型有：

- `build`：影响内部依赖和构建的修改，例如 glup，webpack，rollup 的配置等。
- `chore`：其他不修改`src`或`test`文件的更改。
- `ci`：更改`CI`的配置文件。
- `docs`：文档更新。
- `feat`：添加新功能。
- `fix`：修复代码库的 Bug。
- `perf`：提升性能的更改。
- `refactor`：代码重构，没有设计修改 Bug 和新加功能。
- `revert`：回滚到某个 commit 的提交。
- `style`：格式修改，不涉及程序逻辑。
- `test`：涉及测试用例的修改。

（2）scope

非必填，用于描述改动的影响范围，格式为`项目名/模块名`，标识此次提交主要涉及到代码中哪个模块。

（3）subject

必填项，此次提交的**描述内容**，语语句尽量简短。

- 以动词原型开头，比如`change`，而不是`changes`
- 第一个字母小写
- 结尾不加句号`.`

### Body（可选）

Body 部分是针对本次 commit 的**详细描述**，内容较长时，要进行合理的换行，要表达清楚变动的动机以及与之前行为的对比。好的提交信息要回答下面的内容：

- 为什么要提交这次修改？
- 怎么解决的问题？
- 可能影响哪些内容？

如果在 Body 上需要附上相关链接，则`ref: url`。

### Footer（可选）

Footer 部分只用于两种情况：

- BREAKING CHANGE（不兼容变动）
- 关闭 Issue

## 一些 Commit 举例

都省略了 Body 和 Footer。

```powershell
chore: run tests on travis ci
fix(server): send cors headers
feat(web): add comment section
```

## 使用 commitlint 进行规范检查

commitlint 可以检查 Commit Message 是否符合 [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) 的格式。

详情配置见 [commitlint](https://github.com/conventional-changelog/commitlint)。

## 代码格式化规范

1.ECMAScript中的语句以分号结尾。省略分号意味着由解析器确定语句在哪里结尾。

2.标识符使用  小驼峰写法

3.大驼峰写法  常用于类名，命名空间等

4.在项目中目录文件夹的名字为小驼峰  ,组件的名称需要使用大驼峰