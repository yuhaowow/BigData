
## map-red编程框架
### 数据类型
Text String类型
各种原生类型的Writable实现 为了更高效率的序列化
### mapper类
接受<K, V>读取文件 处理每一行 输出<K, V>
### reduce类
接受<K, V>读取文件 对每一个K获取 V list 输出<K, V>
### driver类
设置job对象
设置jar存储路径
关联mapper和reducer类 setMapperClass setReducerClass
设置mapper输出的key和value类型
设置输入输出路径 通常是hdfs文件系统路径
提交job
## 序列化
实现writable接口write readFields方法  序列化字段先进先出
实现comparable接口 shuffle过程key需要排序
## InputFormat
### job提交流程
提交
连接集群
设置上传路径stagingDir
分配jobId
分片并序列化job.split 写job.xml
上传切片文件 配置文件*.xml 和jar包
### 文件切片 
切片大小决定MapTask数量 影响并发度

#### 默认切片 FileInputFormat
默认为blockSize 按照文件和切片大小切片 file1 128m file2 65m 切片大小64 则切片 64 64 65三个 文件剩余大小需要大于切片大小*1.1比例才切片
#### 合并文件切片 CombineTextInputFormat
将小文件合并到 split_size再切片

### 文件输入
#### TextInputFormat
---
默认输入器 K = 文件内偏移量 value=line_text 按行读取文本文件 
#### KeyValueTextInputFormat
每一行用 \t 分割成 key value的格式 也可以设置分隔符
#### NLineInputformat
map不再按照块切分 而是按照行数来划分 map进程
#### 自定义InputFormat
重写 isSplitable
重写 createRecordReader
改写RecordReader 

