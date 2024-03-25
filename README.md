# dbtrain

此仓库为2023年之前清华大学《数据库专题训练》课程的实验文档，2024年起将使用 [huadb](https://github.com/thu-db/huadb-doc) 作为课程实验。

## 准备工作

该实验代码由 git 管理，构建需要 cmake, make, flex, bison 等依赖，你可以通过系统包管理器进行安装。

以 Ubuntu 为例，使用 apt 安装依赖：

```bash
apt install git ca-certificates make cmake g++ flex bison libreadline-dev python3
```

编译及测试方法：

```bash
bash prepare.sh
```

详细环境配置与测试流程见[文档](https://thu-db.github.io/dbtrain-tutorial/test.html)
