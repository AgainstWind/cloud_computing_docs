hello world!

#### 日记 20180711

#### 20180711 

1. 火焰图及生成 

https://github.com/brendangregg/FlameGraph
https://github.com/nswbmw/node-in-debugging/blob/master/1.1%20perf%20%2B%20FlameGraph.md

2. 压缩算法lz4 arm

3. 使用time命令统计命令行执行时间

http://www.runoob.com/linux/linux-comm-time.html
http://man.linuxde.net/time

4. Shell 输入/输出重定向

http://www.runoob.com/linux/linux-shell-io-redirections.html

5. linux process&thread

https://unix.stackexchange.com/questions/31595/are-linux-kernel-threads-really-kernel-processes
The documentation can be pretty confusing, so here is the "real" Linux model:
inside the Linux kernel, something that can be run (& scheduled) is called a "process",
each process has a system-unique Process ID (PID), and a Thread Group ID (TGID),
a "normal" process has PID=TGID and no other process shares this TGID value,
a "threaded" process is a process which TGID value is shared by other processes,
several processes sharing the same TGID also share, at least, the same memory space and signal handlers (sometimes more),
if a "threaded" process has PID=TGID, it can be called "the main thread",
calling getpid() from any process will return its TGID (= "main thread" PID),
calling gettid() from any process will return its PID (!),
any kind of process can be created with the clone(2) system call,
folders' numeric names you can list with ls /proc as /proc/NUMBER are TGIDs,
folders' numeric names in /proc/TGID/task as /proc/TGID/task/NUMBER are PIDs,
even though you don't see every existing PIDs with ls /proc, you can still do cd /proc/any_PID.
Conclusion: from the kernel point of view, only processes exist, each having their own unique PID, and a so-called thread is just a different kind of process.

6. linux内核设计与实现阅读--进程管理

进程间通信http://www.cs.rochester.edu/courses/256/fall2014/slides/04-IPC.pdf
http://www.cs.rochester.edu/courses/256/fall2014/
http://windegger.org/docs/c-programming-in-linux.pdf
http://users.cs.cf.ac.uk/Dave.Marshall/C/
进程间通信：共享内存、消息传递
线程

7. postgres技术会议资料

http://www.pgcon.org/2018/


##### 20180712

1.一些电子书 
https://legacy.gitbook.com/@wizardforcel
https://wizardforcel.gitbooks.io/the-art-of-programming-by-july/content/06.07.html

2. linux shell特殊符号
http://wangqiaowqo.iteye.com/blog/983757
case语句：
```shell
name=`basename $0 .sh`
case $1 in
 s|start)
        echo "start..."
        ;;
 stop)
        echo "stop ..."
        ;;
 reload)
        echo "reload..."
        ;;
 *)
        echo "Usage: $name [start|stop|reload]"
        exit 1
        ;;
esac
exit 0
```

3. centos with desktop on vagrant

http://www.interdb.jp/blog/tips/vagrant_gnome/


4. cap 12年

http://www.infoq.com/cn/articles/cap-twelve-years-later-how-the-rules-have-changed/

https://blog.csdn.net/dellme99/article/details/15340955


5. postgres


http://www.interdb.jp
http://momjian.us/main/presentations/
http://momjian.us/main/writings/pgsql/internalpics.pdf
https://wiki.postgresql.org/images/8/81/FSM_and_Visibility_Map.pdf
http://momjian.us/main/writings/pgsql/
http://rachbelaid.com/introduction-to-postgres-physical-storage/
https://doxygen.postgresql.org
PostgreSQL源码分析之shared buffer的分配与替换http://blog.chinaunix.net/uid-24774106-id-3761272.html
PostgreSQL源码分析之shared buffer状态信息及性能测量http://blog.chinaunix.net/uid-24774106-id-3761861.html
https://madusudanan.com/blog/understanding-postgres-caching-in-depth/
http://www.craigkerstiens.com/2013/01/10/more-on-postgres-performance/


* 使用pg_buffercache观察postgres shared buffer使用情况
postgres=# create extension pg_buffercache;
ERROR:  could not open extension control file "/usr/share/pgsql/extension/pg_buffercache.control": No such file or directory
[root@localhost bin]# yum install postgresql92-contrib
postgres=# create extension pg_buffercache;
CREATE EXTENSION
postgres=# select * from pg_buffercache;
 bufferid | relfilenode | reltablespace | reldatabase | relforknumber | relblocknumber | isdirty | usagecount
----------+-------------+---------------+-------------+---------------+----------------+---------+------------
        1 |       12920 |          1664 |           0 |             0 |              0 | f       |          5
        2 |       12671 |          1664 |           0 |             0 |              0 | f       |          5
        3 |       12690 |          1663 |       12924 |             0 |              0 | t       |          5
        4 |       12690 |          1663 |       12924 |             0 |              1 | f       |          5





