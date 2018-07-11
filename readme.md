hello world!

#### 日记 20180711

#### 20180711 

1. 火焰图及生成 

https://github.com/brendangregg/FlameGraph
https://github.com/nswbmw/node-in-debugging/blob/master/1.1%20perf%20%2B%20FlameGraph.md

2. 压缩算法lz4 arm

3. 使用time命令统计命令行执行时间
http://www.runoob.com/linux/linux-comm-time.html

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
