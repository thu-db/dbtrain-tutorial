# LAB 3 执行器实验文档

## 实验概述

本次实验主要关注于 SQL 执行流程，重点为 join 算子的实现。

## 实验任务

1. 完成 AndConditionNode 和 OrConditionNode 的构建过程。
2. 实现 JoinNode 的构建和执行过程。

实验开始前，请按照文档[更新说明](https://thu-db.github.io/dbtrain-tutorial/intro.html#%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)中的步骤合并新增代码。

## 相关模块

1. optim 模块：负责新建执行算子节点。
2. join_node 模块：定义了 join 算子的执行过程。

## 基础功能实现顺序

1. optim/optim.cpp: 实现 AndConditionNode 和 OrConditionNode 的 visit 函数。
2. optim/optim.cpp: 实现 JoinConditionNode 的 visit 函数。
3. optim/optim.cpp: 在 Select 的 visit 函数中添加连接算子的部分。
4. oper/join_node.cpp: 实现 Next 函数，进行连接运算。

## 可选高级功能

1. 实现多种 join 算法(1分)：至少实现三种不同的连接算法，如 Nested Loop Join, Sort Merge Join, Hash Join，设计测例比较不同算法的效率。
2. 基于外存的 join 算子(2分)：至少实现一种外存算法，如外存 Hash、外存 Sort Merge 等。
3. 实现聚合算子(2分)：实现 SUM, AVG, MIN, MAX, COUNT 算子，设计测例验证正确性。

高级功能满分 3 分。

## 实现要点

1. 对于多个 AND 或 OR 连接的条件，解析器会将条件解析为左深树，即所有 AND 结点的右孩子均为比较条件或连接条件，不会是其他 AND OR 条件。

2. 所有 visit 函数必须具有返回值，即必须以 return 语句结尾。如不需要返回值可返回 nullptr，没有返回值可能出现 Segmentation fault。

3. 实现 visit 函数时可参考 optim 中其他节点 visit 函数的代码。

4. 使用并查集维护表的连接信息，并查集实现代码位于 utils/uf_set.h 文件。

## 报告说明

一门好的课程实验，都是需要多年学生的吐槽和反馈、多届助教和老师一起提升的。本次实验报告除了基本要求外，也欢迎写出对这门课的一些想法、评价和建议，如课程安排、授课方式、实验难度和工作量等，课程进行过程中有哪些好和不好的地方，未来这门课程也会根据大家的建议不断更新和改良。

## 截止时间

2023 年 5 月 7 日（第十一周周日）晚 23:59 分。
