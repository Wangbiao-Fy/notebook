## HDFS,YARN测试过程和结果

### 1.上传文件

#### 1.HDFS根目录下创建wbinput目录

```
hadoop fs -mkdir /wbinput
```

#### 2.将 README.txt上传到/wbinput目录中

```
hadoop fs -put /opt/hadoop-2.7.2/README.txt /wbinput
```

![image-20220606170141229](D:\BigData\docu\HDFS,YARN测试过程和结果.assets\image-20220606170141229.png)

### 2.MapReduce测试程序测试YARN

执行命令

```
hadoop jar /opt/hadoop-2.7.2/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar pi 100 100
```

![image-20220606170355970](D:\BigData\docu\HDFS,YARN测试过程和结果.assets\image-20220606170355970.png)

![image-20220606170443993](D:\BigData\docu\HDFS,YARN测试过程和结果.assets\image-20220606170443993.png)

![image-20220606174753206](D:\BigData\docu\HDFS,YARN测试过程和结果.assets\image-20220606174753206.png)



![image-20220607103309001](D:\BigData\docu\HDFS,YARN测试过程和结果.assets\image-20220607103309001.png)

