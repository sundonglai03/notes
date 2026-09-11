# Git 常用命令

## 高频速查

```bash
git status                         # 查看当前分支和修改
git add <文件>                     # 暂存指定文件
git add .                          # 暂存全部修改
git diff                          # 查看未暂存差异
git diff --staged                  # 查看已暂存差异
git commit -m "说明"              # 提交
git pull --rebase                 # 拉取并整理本地提交
git push                          # 推送当前分支
```

## 分支和远程

```bash
git branch                        # 查看本地分支
git branch -a                     # 查看所有分支
git switch <分支>                 # 切换分支
git switch -c feature/demo        # 创建并切换新分支
git branch -M main                # 重命名当前分支
git push -u origin <分支>         # 首次推送并建立跟踪
git remote -v                     # 查看远程地址
git fetch --all --prune           # 更新远程分支
git pull origin main              # 拉取指定分支
```

## 暂存、撤销与历史

```bash
git stash                         # 暂存未提交修改
git stash pop                     # 恢复最近一次暂存
git restore --staged <文件>       # 取消暂存
git restore <文件>                # 丢弃指定文件修改（谨慎）
git revert <提交号>               # 安全撤销历史提交
git log --oneline --graph --all   # 查看提交图
git show <提交号>                 # 查看某次提交
```

`git reset --hard` 会直接丢弃未提交修改，执行前确认没有需要保留的内容。

## 代理配置

```bash
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
git config --global --unset http.proxy       # 取消 HTTP 代理
git config --global --unset https.proxy      # 取消 HTTPS 代理
git config --show-origin --get-regexp 'proxy' # 查看代理配置
```

SSH 地址代理配置（`~/.ssh/config`）：

```sshconfig
Host github.com
    ProxyCommand nc -X 5 -x 127.0.0.1:7890 %h %p
```

## 新项目首次推送

```bash
git init
git branch -M main
git add .
git commit -m "initial commit"
git remote add origin <仓库地址>
git push -u origin main
```
