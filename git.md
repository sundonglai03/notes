# Git 常用命令笔记

Git 是一个分布式版本控制系统，用来记录代码修改历史、协同开发和回退版本。

## 0. 最常用命令速查

```bash
git status              # 查看当前仓库状态：哪些文件被修改、未提交等
git add .               # 把当前目录所有改动放进暂存区
git commit -m "提交说明" # 提交暂存区内容，生成一个提交记录
git push origin <分支名> # 把本地提交推到远程仓库对应分支
git pull origin <分支名> # 拉取远程分支最新代码并合并
git checkout -b <分支名> # 创建并切换到新分支
git switch <分支名>     # 直接切换分支（更简洁）
git branch              # 查看当前有哪些分支
git log --oneline       # 查看简洁版提交历史
git stash               # 临时保存当前修改，方便切分支或恢复状态
git reset --hard HEAD~1 # 回退到前一个提交，丢弃当前提交
```

如果你只是想快速使用，先记住这几条最常用命令即可。

---

## 1. 基础配置

```bash
git --version

git config --global user.name "你的名字"
git config --global user.email "你@example.com"

git config --global --list
```

说明：
- `user.name`：提交者名称
- `user.email`：提交者邮箱
- `--global`：全局配置，适用于当前用户

---

## 2. 仓库初始化与克隆

### 初始化仓库

```bash
git init
```

在当前目录创建一个新的 Git 仓库。

### 手动新建一个 Git 仓库并上传到 GitHub

```bash
mkdir my-project
cd my-project

git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/你的用户名/你的仓库.git
git push -u origin main
```

说明：
- `git init`：把当前目录变成 Git 仓库
- `git add .`：把所有文件加入暂存区
- `git commit -m "first commit"`：第一次提交
- `git branch -M main`：把默认分支改名为 `main`
- `git remote add origin ...`：绑定远程仓库
- `git push -u origin main`：第一次推送并设置跟踪关系

### 克隆仓库

```bash
git clone <仓库地址>
git clone https://github.com/user/repo.git
```

### 复制指定分支

```bash
git clone -b <分支名> --single-branch <仓库地址>
```

---

## 3. 查看状态与日志

### 记住 GitHub 登录信息（避免重复输入密码）

如果你用的是 HTTPS 推送到 GitHub，想让 Git 记住用户名和密码/Token，可以这样配置：

#### macOS 上用系统钥匙串

```bash
git config --global credential.helper osxkeychain
```

然后第一次执行：

```bash
git push
```

输入：
- Username: 你的 GitHub 用户名
- Password: 你的 Personal Access Token（PAT）

之后 Git 就会记住，后续 push 不再反复要求输入。

#### 取消已保存的凭证

```bash
git credential-manager erase
```

或者直接清理系统钥匙串中的 Git 凭证。

#### 查看当前远程地址

```bash
git remote -v
```

#### 如果已经推送过一次但还要输入密码

先确认是不是 HTTPS 地址：

```bash
git remote -v
```

如果是类似：

```bash
https://github.com/用户名/仓库.git
```

就可以用上面的 `osxkeychain` 方式保存。

如果还不行，可以重新设置远程地址并重新授权：

```bash
git remote set-url origin https://github.com/用户名/仓库.git
git config --global credential.helper osxkeychain
```

然后再执行一次：

```bash
git push
```

---

### 查看当前状态

```bash
git status
```

### 查看修改内容

```bash
git diff
git diff --staged
```

### 查看提交历史

```bash
git log
git log --oneline
git log --graph --decorate --oneline --all
```

### 查看最近一次提交

```bash
git show
```

### 查看分支信息

```bash
git branch
git branch -a
```

---

## 4. 添加、提交与暂存

### 查看未跟踪文件

```bash
git status
```

### 添加到暂存区

```bash
git add <文件名>
git add .
```

### 提交

```bash
git commit -m "提交说明"
```

### 提交并跳过暂存区

```bash
git commit -am "提交说明"
```

> 只适用于已跟踪文件，不包括新文件。

### 修改最近一次提交

```bash
git commit --amend -m "修正后的提交说明"
```

---

## 5. 分支管理

### 创建分支

```bash
git branch <分支名>
```

### 切换分支

```bash
git checkout <分支名>
```

新版本也可写成：

```bash
git switch <分支名>
```

### 创建并切换分支

```bash
git checkout -b <分支名>
# 或
git switch -c <分支名>
```

### 删除分支

```bash
git branch -d <分支名>
```

强制删除未合并分支：

```bash
git branch -D <分支名>
```

### 合并分支

```bash
git checkout main
git merge <分支名>
```

### 取消合并

```bash
git merge --abort
```

---

## 6. 暂存与恢复

### 暂存当前修改

```bash
git stash
git stash save "临时保存说明"
```

### 查看暂存列表

```bash
git stash list
```

### 恢复暂存内容

```bash
git stash apply stash@{0}
# 或直接弹出
git stash pop
```

### 删除暂存记录

```bash
git stash drop stash@{0}
git stash clear
```

---

## 7. 撤销与回退

### 撤销工作区修改

```bash
git checkout -- <文件名>
# 或
git restore <文件名>
```

### 撤销暂存区内容

```bash
git reset HEAD <文件名>
# 或
git restore --staged <文件名>
```

### 回退到某个提交

```bash
git reset --hard <提交号>
```

### 软回退

```bash
git reset --soft <提交号>
```

### 保留修改但回退提交

```bash
git reset --mixed <提交号>
```

### 反向提交（推荐用于公共分支）

```bash
git revert <提交号>
```

---

## 8. 远程仓库管理

### 查看远程仓库

```bash
git remote -v
```

### 添加远程仓库

```bash
git remote add origin <仓库地址>
```

### 修改远程仓库地址

```bash
git remote set-url origin <新地址>
```

### 删除远程仓库

```bash
git remote remove origin
```

### 拉取远程更新

```bash
git fetch origin
git pull origin <分支名>
```

### 推送代码

```bash
git push origin <分支名>
```

### 首次推送并设置跟踪分支

```bash
git push -u origin <分支名>
```

---

## 9. 标签管理

### 创建标签

```bash
git tag <标签名>
```

### 创建带注释的标签

```bash
git tag -a v1.0 -m "版本1.0"
```

### 查看标签

```bash
git tag
```

### 推送标签到远程

```bash
git push origin <标签名>
```

### 推送所有标签

```bash
git push origin --tags
```

---

## 10. 文件忽略

### 创建 .gitignore

```bash
# .gitignore
node_modules/
.env
*.log
```

### 查看忽略规则是否生效

```bash
git check-ignore -v <文件名>
```

### 取消跟踪某个文件但保留本地文件

```bash
git rm --cached <文件名>
```

---

## 11. 代码比较

### 比较工作区和暂存区

```bash
git diff
```

### 比较暂存区和最近提交

```bash
git diff --cached
```

### 比较两个提交之间差异

```bash
git diff <提交1> <提交2>
```

### 查看某个文件的历史

```bash
git log -- <文件名>
```

---

## 12. 常见实际场景

### 1）从远程拉取最新代码

```bash
git pull origin main
```

### 2）新功能开发

```bash
git checkout -b feature/login
git add .
git commit -m "add login feature"
git push -u origin feature/login
```

### 3）切回主分支并合并开发分支

```bash
git checkout main
git merge feature/login
```

### 4）发现错误想回退

```bash
git reset --hard HEAD~1
```

### 5）想保留修改但不想提交

```bash
git stash
```

### 6）提交信息写错了

```bash
git commit --amend -m "修正后的说明"
```

---

## 13. Git 常用快捷记忆

- `git status`：查看状态
- `git add .`：加入暂存区
- `git commit -m "..."`：提交代码
- `git log --oneline`：查看提交记录
- `git branch`：查看分支
- `git checkout/switch`：切分支
- `git merge`：合并分支
- `git pull`：拉取远程更新
- `git push`：推送代码
- `git stash`：临时保存修改
- `git reset --hard`：强制回退
- `git revert`：安全回退

---

## 14. 进阶建议

- 提交前先 `git status`，确认修改内容
- 提交信息尽量简短且清晰
- 多人协作时先 `git pull` 再开发
- 不要在主分支上直接提交，优先使用分支
- 重要回退操作优先用 `git revert`，避免丢失历史

---

## 15. 一份最简工作流

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin <仓库地址>
git push -u origin main
```

这是一套最常见的 Git 使用流程，适合新手快速上手。
