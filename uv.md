# uv / Python 常用命令

## 高频速查

```bash
uv sync                         # 同步 pyproject.toml / uv.lock
uv run python app.py            # 在项目环境运行脚本
uv run pytest                   # 运行测试
uv add <包名>                   # 添加依赖
uv add --dev pytest ruff        # 添加开发依赖
uv remove <包名>                # 删除依赖
uv pip list                    # 查看已安装包
uv --version                   # 查看版本
```

优先使用 `uv run`，不必手动激活虚拟环境。

## 创建项目和环境

```bash
uv init                         # 初始化项目
uv venv                         # 创建 .venv
source .venv/bin/activate       # macOS / Linux
.venv\\Scripts\\activate        # Windows PowerShell
uv python install 3.12          # 安装 Python
uv python pin 3.12              # 固定项目 Python 版本
```

## 依赖管理

```bash
uv lock                         # 生成或更新锁文件
uv lock --upgrade               # 升级依赖版本
uv export --format requirements-txt > requirements.txt
uv pip install -r requirements.txt
uv pip install <包名>           # 只装入当前环境
uv pip uninstall <包名>
uv pip freeze
```

## 代理配置

```bash
export HTTP_PROXY=http://127.0.0.1:7890
export HTTPS_PROXY=http://127.0.0.1:7890
export ALL_PROXY=socks5://127.0.0.1:7891

# 只让一条命令走代理
HTTPS_PROXY=http://127.0.0.1:7890 uv sync

# 取消当前终端代理
unset HTTP_PROXY HTTPS_PROXY ALL_PROXY
unset http_proxy https_proxy all_proxy
```

使用私有镜像：

```bash
uv pip install -i https://pypi.example.com/simple <包名>
uv sync --default-index https://pypi.example.com/simple
```

## 清理与排错

```bash
rm -rf .venv                   # 确认后删除环境
uv venv                        # 重建环境
uv cache dir                   # 查看缓存目录
uv cache clean                 # 清理缓存
```

## 安装 uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```
