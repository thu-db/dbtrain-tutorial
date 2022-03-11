# 测试说明

## 环境配置

本实验依赖 cmake, make, g++ 构建工具，解析器编译需要 flex 和 bison 工具，需先在本地环境安装这些依赖。

由于实验框架底层文件操作调用了 Unix 相关接口，故不支持 Windows 环境，Windows 用户建议使用 WSL，也可以使用 Virtualbox 或 VMWare 开一个 Ubuntu 虚拟机，然后参考下面的 Ubuntu 环境配置。

### Ubuntu 环境配置

建议使用 Ubuntu 20.04 及更高版本，使用 apt 安装依赖：

```bash
sudo apt install cmake make flex bison g++
```

### macOS 环境配置

使用 homebrew 安装依赖：

```bash
brew install cmake flex bison
```

### 测试是否配置好了环境

```bash
g++ -v
flex --version
bison --version
```

## 运行实验框架

配好环境后，按照以下步骤进行操作：

### 拉取实验仓库并重命名

使用 git clone 和 mv 命令（将 xxxxxxxxxx 替换为你的学号）：

```bash
git clone git@git.tsinghua.edu.cn:dbtrain/2022/dbtrain-lab-xxxxxxxxx.git
mv dbtrain-lab-xxxxxxxxx dbtrain-lab
```

仓库重命名操作是必须的，否则测试脚本无法正常工作。

### 拉取测试仓库

在**同一文件夹**下，使用 git clone 命令拉取测试仓库。

测试仓库应与实验仓库在同一父文件夹下，目录结构应为：

```
<diretory>
├── dbtrain-lab
│   ├── src
│   ├── CMakeLists.txt
│   ├── .gitlab-ci.yml
│   ├── ...
├── dbtrain-lab-test
│   ├── lab1
│   ├── check.py
│   ├── ...
└── ...
```

### 编译实验框架

进入`dbtrain-lab`目录，运行如下命令进行编译：

```bash
cd dbtrain-lab
mkdir build && cd build
cmake ..
make -j4
```

由于实验框架中部分函数需要同学们自己实现，所以编译过程中出现`no return statement in function returning non-void`的 warning 是正常的。

如果环境配置没有问题，应成功编译出可执行程序`main`：

```
...
[ 94%] Linking CXX static library ../lib/libthdb.a
[ 94%] Built target thdb
Scanning dependencies of target main
[ 97%] Building CXX object src/CMakeFiles/main.dir/cli.cpp.o
[100%] Linking CXX executable ../bin/main
[100%] Built target main
```

运行 `./bin/main` 即可进入数据库交互界面：

```
$ ./bin/main
dbtrain> show databases;
+----------+
| Database |
+----------+

dbtrain> create database test;
+---------+
| SUCCESS |
+---------+

dbtrain> show databases;
+----------+
| Database |
+----------+
| test     |
+----------+
(1 rows)

dbtrain> 
```

通过 ctrl+c 或 ctrl+d 即可退出数据库交互界面
