# Spark-APP-Solutions 
-----------
### [Spark问题分析](https://github.com/alixGuo/Spark-App-Solutions/blob/master/Spark%E4%B8%9A%E5%8A%A1%E9%97%AE%E9%A2%98%E5%88%86%E6%9E%90.md)
记录实际中遇到的应用问题

### [应用代码参数设置不生效问题分析](https://github.com/alixGuo/Spark-App-Solutions/blob/master/%E5%BA%94%E7%94%A8%E4%BB%A3%E7%A0%81%E5%8F%82%E6%95%B0%E8%AE%BE%E7%BD%AE%E4%B8%8D%E7%94%9F%E6%95%88%E9%97%AE%E9%A2%98%E5%88%86%E6%9E%90.md)  
用户反馈在应用代码中设置`spark.yarn.maxAppAttempts=1`不生效，跟代码分析了一下。

### [Spark任务日志过大导致磁盘溢出问题解决方案](https://github.com/alixGuo/Spark-App-Solutions/blob/master/Spark%E4%BB%BB%E5%8A%A1%E6%97%A5%E5%BF%97%E8%BF%87%E5%A4%A7%E5%AF%BC%E8%87%B4%E7%A3%81%E7%9B%98%E6%BA%A2%E5%87%BA%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88.md)  

### [Spark-Sql查询数据不存在hive分区表报错“Input path does not exist”问题]()  
[问题提出Jira](https://issues.apache.org/jira/browse/SPARK-15044)  
[解决方案]：从Spark-2.1.0版本开始，设置spark.sql.hive.verifyPartitionPath=true。如果是Spark-1.5.2以上存在问题的版本，可以在源码org/apache/spark/rdd/HadoopRDD.scala的getPartitions函数中捕获getSplits抛出的异常。  
