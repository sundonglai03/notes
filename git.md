# Git 常用命令笔记

```bash
git init                    # 初始化项目
git branch -M main          # 把默认分支改为 main
git add .                   # 添加所有改动到暂存区
git commit -m "提交说明"     # 提交到本地仓库
git remote add origin <地址> # 绑定远程仓库
git push -u origin main     # 第一次推送并跟踪主分支
git pull origin main        # 拉取远程更新
git switch <分支名>         # 切换分支
git switch -c <分支名>      # 创建并切换分支
git branch                  # 查看分支
git log --oneline           # 查看提交记录
git stash                  # 暂存当前修改
git reset --hard HEAD~1    # 回退到上一条提交
```

```bash
# 常用补充
git status                         # 查看当前状态
git diff                          # 查看工作区差异
git diff --staged                 # 查看暂存区差异
git add <文件名>                  # 添加单个文件
git commit --amend -m "修正说明"  # 修改最近一次提交说明
git remote -v                     # 查看远程仓库地址
git fetch origin                  # 拉取远程分支信息
git merge <分支名>                # 合并分支
git revert <提交号>              # 反向回退某次提交
git restore --staged <文件>       # 取消暂存
git restore <文件>                # 恢复文件到最近提交
```

```bash
# 一个项目的最短流程
git init
git branch -M main
git add .
git commit -m "first commit"
git remote add origin <仓库地址>
git push -u origin main
```

```bash
# 普通工作流
git pull origin main
git switch -c feature/demo
git add .
git commit -m "新增功能"
git push -u origin feature/demo
```

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
