# git小记

---

## 命令

### 常用

- `git config --system alias.{short name} {origin name}`: 配置命令别名
- `git config --get-regexp alias`: 列出所有别名配置
- `git diff --check`: 查看是否有冲突或者空行的修改

### 打标签

- 轻量级标签 `git tag {tagname}`
- 含附注标签 `git tag -a {tagname} -m {annotation}`
- 推送分支 `git push origin {tagname}`
- 推送所有分支 `git push origin --tags`

### 分支

- 重命名任何一个分支: `git branch -m {oldname} {newname}`
- 重命名当前分支: `git branch -m {newname}`
- 列出已经合并的分支: `git branch --merged`

### 删除文件

- 从仓库中以及从文件系统中删除文件: `git rm {file name}`
- 仅从仓库中删除文件: `git rm --cached {file name}`

### git log

- 删除已合并的分支: `git branch --merged | egrep -v "(^\*|master|dev)" | xargs git branch -d`
- 搜索日志: `git log --grep=<pattern>`，相关: `git log --all-match`, `git log --grep-reflog=<pattern>`

### git rebase

### git clean

## 配置相关

- 列出所有别名: `git config --get-regexp alias`
- 列出配置目录: `git config --list --show-origin`

## 第三方

1. [命令行diff工具 diff-so-fancy](https://github.com/so-fancy/diff-so-fancy)

## 问题

1. `git status` 乱码 `git config --global core.quotepath false`
