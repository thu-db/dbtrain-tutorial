# LAB 3 执行器实验文档

## 实验概述

本次实验主要关注于 SQL 执行流程，重点为 join 算子的实现，理解数据库执行引擎的工作原理。

## 实验任务

1. 完成 AndConditionNode 和 OrConditionNode 的构建过程。
2. 实现 JoinNode 的构建和执行过程。

实验开始前，请按照文档[更新说明](https://thu-db.github.io/dbtrain-tutorial/intro.html#%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)中的步骤合并新增代码。

## 基础功能实现顺序

1. optim/optim.cpp: 实现 AndConditionNode 和 OrConditionNode 的 visitor 函数。
2. optim/optim.cpp:
3. optim/optim.cpp:
4. oper/join_node.cpp:
