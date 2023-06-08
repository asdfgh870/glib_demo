**双冒号**

```makefile
$(OBJS):%.o:%.c
	$(CC) -c $(CPPFLAGS) $(CFLAGS) -o $@ $<
```

对于 $(OBJS):%.o:%.c，其中 $(OBJS) 是目标文件列表，%.o 是目标文件的模式规则，%.c 是源文件的模式规则。

在这种规则中，通过模式匹配，Makefile可以根据源文件的模式规则（%.c）找到对应的目标文件的模式规则（%.o）。

在执行这个规则时，Makefile会尝试为每个目标文件（$(OBJS) 中的每个目标）找到对应的源文件。例如，如果目标文件为 foo.o，那么对应的源文件为 foo.c。通过这种匹配关系，Makefile可以根据模式规则自动构建依赖关系。

在命令行行动部分，$@ 代表当前目标文件，$< 代表当前依赖文件（第一个依赖文件，即源文件）。因此，$(CC) -c $(CPPFLAGS) $(CFLAGS) -o $@ $< 表示使用指定的编译器和编译选项，将当前源文件编译为当前目标文件。

**扩展通配符wildcard**

在Makefile规则中，通配符会被自动展开。但在变量的定义和函数引用时，通配符将失效。这种情况下如果需要通配符有效，就需要使用函数wildcard

eg：

```makefile
SRCS += $(wildcard *.c)
OBJS += $(patsubst %.c, %.o, $(SRCS))
```

一般我们可以使用“$(wildcard *.c)”来获取工作目录下的所有的.c文件列表。复杂一些用法；可以使用“$(patsubst %.c,%.o,$(wildcard *.c))”，首先使用“wildcard”函数获取工作目录下的.c文件列表；之后将列表中所有文件名的后缀.c替换为.o。这样我们就可以得到在当前目录可生成的.o文件列表。因此在一个目录下可以使用上述例子内容的Makefile来将工作目录下的所有的.c文件进行编译并最后连接成为一个可执行文件。

**patsubst ：替换通配符**

在$(patsubst %.c,%.o,$(dir) )中，patsubst把$(dir)中的变量符合后缀是.c的全部替换成.o

**notdir  去除路径**

```第一行输出：
src=$(wildcard *.c ./sub/*.c)
dir=$(notdir $(src))
```

第一行输出：
a.c b.c ./sub/sa.c ./sub/sb.c

wildcard把 指定目录 ./ 和 ./sub/ 下的所有后缀是c的文件全部展开。

第二行输出：
a.c b.c sa.c sb.c
notdir把展开的文件去除掉路径信息





# makefile手册

https://www.gnu.org/software/make/manual/html_node/Wildcard-Function.html
