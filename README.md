# study\_nginx
nginx源码学习笔记

## 利用 gdb 调试 Nginx 源码

gdb 调试 Nginx，需要生编译生成 Nginx 二进制程序时，把 -g 编译选项打开。我们需要修改 auto/cc/conf 文件，把 `ngx_compile_opt="-c"` 加上 `-g` 选项，变为`ngx_compile_opt="-c -g"`。下一步执行 ``./configure --prefix=`pwd`/target`` 生成 Makefile 文件，然后使用 vim objs/Makefile 确认一下 -g 参数是否加上了。

确认 -g 参数已经打开，然后执行 make 命令编译 Nginx。

编译完成之后，执行 make install 命令将 Nginx 程序文件安装到 target 目录下。

设置 Nginx 为单进程前台工作模式，将下列指令添加到 target/conf/nginx.conf 的全局区域。

```
worker_processes  1;
daemon off;
master_process off;
```

执行 gdb target/sbin/nginx 进入调试模式。

> gdb -tui target/sbin/nginx 使用带源码窗口的模式

* l 查看代码
* b 打断点
* n 调到下一步
* c 跳到下一个断点

run 开始调试

