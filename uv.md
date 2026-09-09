# uv 常用命令笔记

uv 是一个极快的 Python 包管理和虚拟环境工具，常用于：
- 创建隔离环境
- 安装依赖
- 管理 Python 版本
- 运行项目脚本

## 0. 最常用命令速查（适合隔离环境 + 可移植性）

```bash
uv init                    # 初始化项目，生成 pyproject.toml
uv venv                    # 创建虚拟环境（默认 .venv）
source .venv/bin/activate  # 激活环境（macOS/Linux）
uv add <包名>              # 把依赖写进项目配置，适合正式项目
dep ./                    # 这个示例不用，忽略
uv sync                    # 根据 pyproject.toml 和 lock 文件同步依赖
uv run python app.py       # 直接运行程序，不用手动激活环境
uv run pytest              # 直接在项目环境中运行测试
uv pip install -r requirements.txt  # 从 requirements 安装依赖
uv pip freeze              # 查看当前环境依赖列表
uv lock                    # 生成锁文件，保证可复现
uv python install 3.12    # 安装指定 Python 版本
```

如果你的重点是“隔离环境 + 可移植”，最重要的就是：
- `uv venv`
- `uv add`
- `uv sync`
- `uv lock`
- `uv run`

---

## 1. 适合你的核心工作流

### 新项目初始化

```bash
uv init
uv venv
source .venv/bin/activate
```

### 安装依赖并记录到项目中

```bash
uv add requests
uv add pandas
```

### 生成锁文件，保证环境可复现

```bash
uv lock
```

### 其他人或另一台电脑同步环境

```bash
uv sync
```

### 直接运行程序

```bash
uv run python app.py
```

### 测试

```bash
uv run pytest
```

---

## 2. 为什么这个方案最适合你

你的目标是：
- 隔离环境
- 可移植
- 项目依赖可复现

所以更推荐使用这种方式：

```bash
uv init
uv venv
uv add <依赖>
uv lock
uv sync
```

这套流程会让项目依赖在 `pyproject.toml` 和 `uv.lock` 中被稳定记录，别人拿到项目后，可以直接：

```bash
uv sync
```

而不必手动一个一个 pip 安装。

---

## 3. 额外常用命令

### 从 requirements.txt 安装

```bash
uv pip install -r requirements.txt
```

### 查看当前环境中装了什么

```bash
uv pip list
uv pip freeze
```

### 删除依赖

```bash
uv remove requests
```

### 重新创建环境

```bash
rm -rf .venv
uv venv
uv sync
```

---

## 4. 最简日常用法

```bash
uv init
uv venv
source .venv/bin/activate
uv add requests
uv lock
uv run python app.py
```

这就是最适合“隔离环境 + 可移植性”的 uv 日常开发流程。

---

## 1. 安装 uv

### macOS / Linux

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Windows PowerShell

```bash
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### 重新加载环境变量

```bash
source $HOME/.cargo/env
```

### 查看是否安装成功

```bash
uv --version
```

---

## 2. 创建虚拟环境

### 在当前目录创建虚拟环境

```bash
uv venv
```

默认会创建 `.venv`。

### 指定虚拟环境目录

```bash
uv venv .venv
```

### 指定 Python 版本创建虚拟环境

```bash
uv venv --python 3.12
```

### 查看当前虚拟环境目录

```bash
ls -a
```

---

## 3. 激活虚拟环境

### macOS / Linux

```bash
source .venv/bin/activate
```

### Windows PowerShell

```bash
.venv\Scripts\Activate.ps1
```

### Windows cmd

```bash
.venv\Scripts\activate.bat
```

### 退出环境

```bash
deactivate
```

---

## 4. 安装依赖

### 安装单个包

```bash
uv pip install requests
```

### 安装多个包

```bash
uv pip install requests pandas numpy
```

### 从 requirements.txt 安装

```bash
uv pip install -r requirements.txt
```

### 安装开发依赖

```bash
uv pip install pytest
```

### 升级包

```bash
uv pip install --upgrade requests
```

### 卸载包

```bash
uv pip uninstall requests
```

---

## 5. 查看已安装依赖

```bash
uv pip list
```

### 查看冻结依赖列表

```bash
uv pip freeze
```

### 生成 requirements.txt

```bash
uv pip freeze > requirements.txt
```

---

## 6. 运行 Python 程序

### 直接使用当前环境中的 Python

```bash
uv run python app.py
```

### 运行脚本

```bash
uv run script.py
```

### 执行一个命令（临时环境）

```bash
uv run --python 3.12 python --version
```

### 运行测试

```bash
uv run pytest
```

### 运行模块

```bash
uv run python -m http.server
```

---

## 7. 管理 Python 版本

### 安装某个版本的 Python

```bash
uv python install 3.12
```

### 查看已安装 Python

```bash
uv python list
```

### 选择某个 Python 版本

```bash
uv python find 3.12
```

### 使用指定 Python 版本创建环境

```bash
uv venv --python 3.12
```

---

## 8. 项目依赖管理（推荐方式）

### 初始化项目依赖文件

```bash
uv init
```

这会生成常见项目结构，比如：
- `pyproject.toml`
- `.python-version`
- `README.md`

### 安装项目依赖

```bash
uv sync
```

### 新增依赖

```bash
uv add requests
```

### 删除依赖

```bash
uv remove requests
```

### 锁定依赖版本

```bash
uv lock
```

---

## 9. 常用工作流

### 新建项目并隔离环境

```bash
uv init
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

### 直接运行，不手动激活

```bash
uv run python app.py
```

### 在项目中安装依赖

```bash
uv add flask
uv sync
```

### 只想临时跑个脚本

```bash
uv run python -c "print('hello')"
```

---

## 10. uv 与 pip 的比较

### pip

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### uv

```bash
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

uv 更快，适合 Python 项目和依赖管理。

---

## 11. 常见问题

### 1）`uv: command not found`

重新加载 shell 配置：

```bash
source $HOME/.cargo/env
```

或者重新打开终端。

### 2）找不到 Python 版本

```bash
uv python install 3.12
```

### 3）想重新创建环境

```bash
rm -rf .venv
uv venv
```

### 4）依赖装不上

```bash
uv pip install --upgrade pip
uv pip install -r requirements.txt
```

---

## 12. 最简的日常命令清单

```bash
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
uv run python app.py
```

这是一套最常见、最简洁的 uv 使用方式，适合快速上手。
