# C / C++ 编译常用命令（CentOS / RHEL）

## 高频速查

```bash
sudo dnf install -y gcc gcc-c++ make cmake gdb   # 安装工具链
cmake -S . -B build                              # 配置 CMake
cmake --build build -j$(nproc)                   # 并行编译
make -j$(nproc)                                  # Makefile 编译
make clean                                       # 清理
./build/<程序名>                                 # 运行
```

## 单文件编译

```bash
gcc hello.c -o hello                             # C
g++ hello.cpp -o hello                           # C++
gcc -Wall -Wextra -O2 hello.c -o hello           # 警告和优化
g++ -Wall -Wextra -g hello.cpp -o hello         # 调试信息
gcc hello.c -lm -o hello                         # 链接数学库
```

## 常见项目类型

```bash
# CMake
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build -j$(nproc)
ctest --test-dir build --output-on-failure

# configure / autotools
./configure
make -j$(nproc)
sudo make install
```

## 编译代理配置

```bash
# dnf 临时使用代理
sudo dnf --setopt=proxy=http://127.0.0.1:7890 install -y cmake

# CMake FetchContent / 外部下载
export HTTP_PROXY=http://127.0.0.1:7890
export HTTPS_PROXY=http://127.0.0.1:7890

# git 子模块代理见 git.md
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

## 调试与排错

```bash
gdb ./build/<程序名>                             # 启动调试
gdb --args ./build/<程序名> <参数>               # 带参数调试
ldd ./build/<程序名>                             # 动态库依赖
file ./build/<程序名>                            # 架构和文件类型
which gcc g++ cmake                             # 工具路径
gcc --version && g++ --version && cmake --version
```

## 最短流程

```bash
cd project
ls
cmake -S . -B build
cmake --build build -j$(nproc)
./build/<程序名>
```
