# flink笔记
## 框架比较
storm +低延时
spark streaming +高吞吐 +压力下保持正确 不能低延时
flink +时间正确/语义化窗口 +操作简单/表现力好

DataSet DataStream api flatmap函数 

job manager  task magnager slot=cpus 每一段一个task

flink on yarn  session-cluster  per-job-cluster

resource manager  jobManager taskManager
rm负责分配资源
tm是一个独立的jvm，里面有多个slots slots之间内存隔离 cpu不隔离 因此设置slots=cpus 任务某一个阶段的并行度决定了可以安排多少个slots并行执行
一个slot可以保存整个job的全部分段 通过设置共享组控制是否放在一个slot里面 




