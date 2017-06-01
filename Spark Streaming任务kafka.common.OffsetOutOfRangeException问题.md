## Spark Streaming任务kafka.common.OffsetOutOfRangeException问题  

** 问题背景**  
用户反馈在SSMP平台准实时计算SparkStreaming任务出现“kafka.common.OffsetOutOfRangeException”，任务失败退出。  
batch大小10秒，executor 6个，任务执行时间26小时，AM重试一次，第二次失败退出。

** 问题分析**  
问题定位到某任务提交四次均失败，导致app退出。找到了该任务执行日志，其对应的kafka partition号为11，见下面错误截图：  
`图片待传`
通过其Streaming页面batch信息，初步结论为：  
batch间隔（10秒）太短，但是实际ProcessTime大部分在10S以上，并且在业务高峰耗时还可能在分钟级，总延时时间逐渐积累，导致任务delay严重  
，同时线上kafka 日志保存时间log.retention.hours参数设置的时间是12小时，任务失败的时刻kafka端的offset实际已经是71581500左右，但任务  
消费的offset 还停留在【69536335 -> 69536355】，请求的offset已不在kafka保存的offset范围内（请求的offset已被清除），从而引发【kafka  
.common.OffsetOutOfRangeException】异常。失败时刻Kafka 11号partition offset曲线图如下：  
`图片待传`  

