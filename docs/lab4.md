# LAB 4 优化器

## 实验概述

## 实验任务

## 相关模块

## 基础功能实现顺序

## 可选高级功能

## 测试说明

本次实验主要考察多表连接顺序的选择，测试中主要使用了 analyze 和 explain 指令。

测试数据库中共有 4 张表：

```
t1(id int, score float): 共 10 行
t2(id int, score float): 共 50 行
t3(id int, score float, temp float): 共 100 行
t4(id int, score float): 共 100 行
```

id 列为单调递增序列。

score 列为均匀随机值，范围 [0, 100]。

temp 列为均匀随机值，范围 [35, 38]。

score 列和 temp 列分布独立。

analyze 指令用于生成直方图，计算当前数据库所有表的数值型列的统计信息，保存至 StatsManager 的 stats\_map\_ 中。**统计信息只要求保存至内存，无需持久化到磁盘。**

explain 指令用于打印查询计划树节点，本次实验主要涉及投影节点（Project Node）、连接节点（Join Node）、选择节点（Filter Node）、扫描节点（Table Scan Node）。

根据节点高度不同，打印节点前会先打印一定数量的'\t'，高度相同的节点打印的'\t'数量相同。

例如，对于以下 SQL 语句：

```sql
explain select t2.id from t1, t2, t3 where t3.id = t1.id and t3.id = t2.id and t3.score < 30.0 and t3.temp < 36.0;
```

一种可能的查询计划树如下：

![plan_tree](./pics/plan_tree.svg)

该计划树打印后如下所示：

```
Select:
	Project Node:
		Join Node:JOIN
			Join Node:JOIN
				Filter Node:
					Table Scan Node(t3):
				Table Scan Node(t1):
			Table Scan Node(t2):
```

本次实验主要关注连接顺序的选择，对测试数据的每条 SQL 语句，需确保优化器选择了正确的连接顺序。对于以上示例，需确保表 t3 和 t1 先连接，其次再和表 t2 连接。

对于同一树高的左右节点顺序没有要求，因此以下几个查询计划树都可以通过测试：

```
Select:
	Project Node:
		Join Node:JOIN
			Table Scan Node(t2):
			Join Node:JOIN
				Filter Node:
					Table Scan Node(t3):
				Table Scan Node(t1):
```

```
Select:
	Project Node:
		Join Node:JOIN
			Table Scan Node(t2):
			Join Node:JOIN
				Table Scan Node(t1):
				Filter Node:
					Table Scan Node(t3):
```

## 截止时间

2022年5月8日（第十一周周日）晚23:59分。

{% include "/footer.md" %}
