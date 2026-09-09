# C / C++ 编译笔记（CentOS / RHEL，dnf 版）

```bash
sudo dnf update -y             # 更新系统包
sudo dnf install -y gcc gcc-c++ make cmake gdb   # 安装编译工具
```

```bash
cd project                    # 进入项目目录
ls                            # 看目录里有没有 Makefile / CMakeLists.txt / configure
```

```bash
# Makefile 项目
make                          # 按 Makefile 编译
./app                        # 运行程序

# CMake 项目
cmake -S . -B build          # 生成构建目录
cmake --build build          # 编译项目
./build/app                  # 运行程序

# configure 项目
./configure                  # 检查环境并生成配置
make                         # 编译
./app                        # 运行程序
```

```bash
# 单文件编译
gcc hello.c -o hello        # 编译 C 文件
./hello                      # 运行 C 程序

g++ hello.cpp -o hello      # 编译 C++ 文件
./hello                      # 运行 C++ 程序
```

```bash
# 常用补充
gcc -Wall hello.c -o hello       # 打开警告
gcc -g hello.c -o hello          # 生成调试信息
gcc hello.c -lm -o hello         # 链接数学库
make clean                        # 清理编译产物
```

```bash
# 一个项目的最短流程
cd project
ls
make
# 或
cmake -S . -B build
cmake --build build
# 或
./configure
make
```
