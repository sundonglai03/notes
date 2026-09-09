# uv 常用命令笔记

```bash
uv init                    # 初始化项目
uv venv                    # 创建虚拟环境
source .venv/bin/activate # 激活环境
uv add <包名>              # 添加依赖
uv sync                    # 同步项目依赖
uv lock                    # 锁定依赖版本
uv run python app.py       # 运行项目脚本
uv run pytest              # 运行测试
uv pip install -r requirements.txt  # 从 requirements 安装
uv pip freeze              # 查看依赖列表
uv python install 3.12    # 安装指定 Python 版本
```

```bash
# 常用补充
uv remove <包名>           # 删除依赖
uv pip list                # 查看已安装包
uv pip install <包名>      # 安装单个包
uv pip uninstall <包名>    # 卸载包
rm -rf .venv               # 删除虚拟环境
uv venv                    # 重新创建环境
```

```bash
# 安装 uv
curl -LsSf https://astral.sh/uv/install.sh | sh  # 安装 uv
uv --version                                      # 查看版本
```

```bash
# 直接用，不手动激活
uv run python app.py  # 直接运行程序
uv run pytest         # 直接运行测试
```

```bash
# 一个项目的最短流程
uv init
uv venv
source .venv/bin/activate
uv add requests
uv sync
uv run python app.py
```