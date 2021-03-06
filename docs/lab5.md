# LAB 5 并发控制

## 实验概述

本次实验主要关注于数据库系统的并发控制，重点关注于基于MVCC技术的多线程事务处理。通过实现MVCC机制实现多线程情况下的并发事务处理，让同学们对于数据库系统中并发控制机制有进一步的理解。

## 实验任务

本次实验主要有3个任务：
1. 设置和获取记录隐藏列，添加对应的接口。
2. 修改PageHandle，实现多线程情境下的记录页面控制。
3. 修改Table接口，实现适应MVCC场景的增删改查。

实验开始前，请按照文档中[更新说明](https://thu-db.github.io/dbtrain-tutorial/intro.html#%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)中的步骤合并新增代码。

本次实现需要使用事务编号作为版本号，因此需要开启日志记录功能来保证系统重启时可以正确恢复事务编号。合并代码后重新编译默认将开启事务记录功能，请同学们一定不要手动关闭，否则会出现无法通过Lab 5测试的问题。

## 相关模块

1. tx/lock_manager: 锁管理服务，可以定义并操作共享锁。可以用于保护数据页面的读写并发。
2. tx/signal_manager: 信号管理服务，可以定义信号并等待信号。可以利用信号机制控制不同线程之间的执行顺序。

## 基础功能实现顺序

1. record/record_factory: 添加操作隐藏列的接口。
2. table/page_handle.cpp: 实现多线程场景下的记录页面的插入、删除和查找。
3. table/table.cpp: 修改多线程场景下的表的插入、删除和更新。

## 测试说明

本次实验主要考察并发过程中事务之间的隔离性问题，通过多版本并发控制实现快照隔离，测试中增加了 declare, enddecl, signal, wait, run 等指令。

declare 和 enddecl 用于声明一个事务块，定义一个事务所包含的 SQL 语句，但并不执行这些 SQL。

run 用于并发执行事务，如 run t1, t2, t3 表示并发执行 t1, t2, t3 三个事务。

wait 和 signal 用于控制事务之间的并发，wait t1_2 表示等待信号 t1_2，其他事务可以通过 signal t1_2 发出信号 t1_2，从而使等待信号 t1_2 的事务继续进行。

## 可选高级功能

不要求将高级功能集成到主分支中，建议单开分支完成实验。但是建议同学们设计验证自己实验结果的测例并给出测试的可视化结果展示。

1. MVCC 的垃圾回收(1分)。由于 MVCC 机制中删除操作并没有真正删除对应的记录，仅仅标记了相应记录对应的版本号，使系统存在一些不需要的垃圾数据。设计算法回收垃圾数据所占用的空间，说明算法设计的要点，如垃圾回收的时机，垃圾数据的判定方法等，并需设计测例证明垃圾回收前后存储空间的变化情况。

2. 写写冲突的处理(2分)。当前测例仅包含读写冲突，在 MVCC 并发控制机制下不会发生阻塞，设计算法正确处理并发条件下的写写冲突问题，需详细给出写写冲突的处理方法，并设计测例证明算法正确性。

高级功能满分3分。

## 报告说明

一门好的课程实验，都是需要多年学生的吐槽和反馈、多届助教和老师一起提升的。本次实验报告除了基本要求外，也欢迎写出对这门课的一些想法、评价和建议，如课程安排、授课方式、实验难度和工作量等，课程进行过程中有哪些好和不好的地方，未来这门课程也会根据大家的建议不断更新和改良。

## 截止时间

2022年5月22日（第十三周周日）晚23:59分。

{% include "/footer.md" %}
