# 常见问题

**Q: 测试脚本运行 insert 正常，但在交互式命令行中复制 insert 语句运行时会卡出。**

A: 部分 insert 语句较长，在交互式命令行无法工作，可以采用输入重定向方式运行，如：

```bash
./bin/main < /path/to/00_setup.sql
```

**Q: 测试脚本运行异常且没有输出，交互式命令行中复制 SQL 运行正常。**

A: 同上，尝试采用输入重定向方式运行 SQL。

**Q: parser 解析器无法正常工作，如输入正确的 SQL 语句却显示 Syntax Error，删除 build 文件夹重新编译依然无效。**

A: 可能是由于 flex 和 bison 生成的 cpp 文件出现异常，如被编辑器格式化等。可删除 parser 文件夹下的 lex.yy.cpp, sql.tab.cpp 和 sql.tab.h 文件，然后重新编译。
