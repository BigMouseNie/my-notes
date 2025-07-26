# commit

## ✅ 推荐格式

标准格式如下：

```bash
<type>: <简洁的修改说明>
```

> 可选增加 body：

```tex
<type>(<scope>): <short summary>

<details>

<footer>

// 示例
feat(network): 添加异步连接池支持

实现了基于 epoll 的异步连接池，支持连接复用与最大连接限制
同时修复了连接泄漏的 bug

BREAKING CHANGE: 修改了原有 connect() 接口参数
Closes #123
```

| 部分        | 内容说明                                                     |
| ----------- | ------------------------------------------------------------ |
| **type**    | 变更类型（见下方）                                           |
| **scope**   | 可选：模块、目录、功能范围                                   |
| **summary** | 50 字以内简要说明改动内容（首字母小写、无句号）              |
| **details** | 可选：更详细的描述，说明背景、实现思路、动机等               |
| **footer**  | 可选：breaking change(破坏性变更,标记这次提交引入了不兼容的更改)、issue(Close、Fixes、Related to) 关联等元信息 |
|             |                                                              |

🔖 其他关键词还包括：

| 关键词            | 作用                   |
| ----------------- | ---------------------- |
| `Closes #123`     | 自动关闭对应 issue     |
| `Fixes #123`      | 同上                   |
| `Related to #123` | 表示相关但不关闭 issue |



------

## 🔖 常见的类型（type）说明

| 类型       | 用途描述                                           |
| ---------- | -------------------------------------------------- |
| `feat`     | 新功能，比如增加一个远程锁机功能                   |
| `fix`      | 修复 bug，比如修复鼠标事件坐标错误                 |
| `refactor` | 重构代码，没有新增功能或修复，比如优化文件传输逻辑 |
| `docs`     | 修改文档，比如 README 或注释改进                   |
| `style`    | 修改格式/空格/缩进等，不影响逻辑                   |
| `test`     | 添加或修改测试代码                                 |
| `chore`    | 构建流程、脚本、依赖项等非业务代码改动             |



------

## 🧱 示例

```
feat: 添加远程锁机和解锁功能

fix: 修复远程文件下载时路径错误的问题

refactor: 重构图像传输协议结构体以支持压缩字段

docs: 更新 README 中的安装说明部分

style: 格式化 client 文件中的缩进和空行

chore: 添加 .gitignore 文件
```

------

## 🧠 命名建议

- 使用**祈使句**（相当于命令式），比如“添加”而不是“已添加”
- 保持简洁，主语省略，比如“添加 XX 功能”，而不是“我添加了 XX 功能”
- 如果是多语言项目，commit 推荐统一使用英文（你也可以选择中文，但需统一）

------

## ✍️ 推荐写法总结（模板）

```bash
<type>(模块): <简短说明>

<可选 - 详细内容>
```

示例：

```bash
feat(file): add remote file delete support

fix(monitor): fix mouse click position offset on high DPI

docs(readme): add feature list and build steps
```

------

## 🚀 配合工具（可选）

你还可以借助一些工具让提交更规范：

- [Commitizen](https://github.com/commitizen/cz-cli)：交互式提交规范工具
- [Husky + lint-staged](https://github.com/typicode/husky)：强制检查 commit 格式





# rebase

## ✏️ 进入 rebase 编辑界面（修改行为）

进入后你会看到这样的内容：

```text
pick 123abcd commit A
pick 456defg commit B
pick 789ghij commit C
```

你可以将 `pick` 替换为：

| 命令     | 作用说明                          |
| -------- | --------------------------------- |
| `pick`   | 保留原样                          |
| `reword` | 修改 commit 信息                  |
| `edit`   | 修改该提交的内容（代码）          |
| `squash` | 把当前 commit 合并到上一个        |
| `drop`   | 删除该 commit                     |
| `fixup`  | 类似 squash，但不保留 commit 信息 |



------

## 🧱 修改 commit 信息（`reword`）

```txt
reword 123abcd commit A
pick   456defg commit B
```

保存退出后 Git 会让你修改那条 commit message。

------

## 🧰 修改 commit 内容（`edit`）

```text
edit 123abcd commit A
```

然后 Git 会停下来，你可以：

```bash
# 修改文件或内容
vim myfile.cpp

# 添加修改
git add myfile.cpp

# 重新提交
git commit --amend

# 继续 rebase
git rebase --continue
```

------

## 🔄 合并多个 commit（`squash`）

```txt
pick 123abcd Initial version
squash 456defg Fix typo
squash 789ghij Add more tests
```

Git 会提示你编辑合并后的 commit message。

------

## ❌ 删除 commit（`drop`）

```txt
drop 456defg commit you don't want
```