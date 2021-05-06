# flink笔记
## 框架比较
storm +低延时
spark streaming +高吞吐 +压力下保持正确 不能低延时
flink +时间正确/语义化窗口 +操作简单/表现力好

## flink架构
DataSet DataStream api flatmap函数 

job manager  task magnager slot=cpus 每一段一个task

flink on yarn  session-cluster  per-job-cluster

resource manager  jobManager taskManager
rm负责分配资源
tm是一个独立的jvm，里面有多个slots slots之间内存隔离 cpu不隔离 因此设置slots=cpus 任务某一个阶段的并行度决定了可以安排多少个slots并行执行
一个slot可以保存整个job的全部分段 通过设置共享组控制是否放在一个slot里面

数据传输：one to one，redistributing： keyby hash， broadcast，rebalance
需要时one to one并且并行度相同才可以进行前后任务的共享slot合并
disableChain startNewChain来开启 关闭 链式合并
reduce操作
keyby后 datastream 转化成 keyedStream 
split流与 select
connect和comap 连接多条流
tuple2 tuple3
union流合并多条类型一致的流


shuffle global keyby rebalance rescale

### sink
kafka
redis
jdbc
es
窗口api
keyed window  windowAll
滑动窗口 滚动窗口 session window  global window
watermark lateness sideOutStream三种纠错机制
窗口分配器
窗口起始点和偏移量的计算
时间语义
事件时间 处理时间 到达时间
watermark的生成规则 传递规则
watermark的设定原则

状态管理
context中保存的跨任务的状态
算子状态
keyed state






