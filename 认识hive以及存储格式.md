## 认识hive以及存储格式

**hive是一个大数据仓库**
**hive是一个基于hadoop的数据仓库**
**hive是一个基于hadoop的数据仓库，可以通过类sql语句来对数据进行读、写、管理（管理元数据）**

### hive的特点
Built on top of Apache Hadoop™, Hive provides the following features:

1、Tools to enable easy access to data via SQL, thus enabling data warehousing tasks such as extract/transform/load (ETL), reporting, and data analysis.
2、A mechanism to impose structure on a variety of data formats
3、Access to files stored either directly in Apache HDFS™ or in other data storage systems such as Apache HBase™ 

4、Query execution via Apache Tez™, Apache Spark™, or MapReduce
5、Procedural language with HPL-SQL
6、Sub-second query retrieval via Hive LLAP, Apache YARN and Apache Slider.

==========================================================================================
### hive的架构
用户连接客户端：cli、jdbc/odbc、web gui
第三方服务：thrift server
metastore：存储hive的元数据（库、表、字段、数据类型、分区、分桶、创建时间、创建人）

解释器：将hql语句抽象成表达式树
编译器：对hql语句进行语法、词法、语言的编译（需要关联元数据进行查找），编译完成后会生成一个有向无环的执行计划。
优化器：将执行计划进行优化，减少一些不必要的列、使用分区等。
执行器：将优化好的执行计划提交给hadoop的mapredcue框架去执行。

==========================================================================================

### 创建数据库
```sql
create database if not exists sharewinfo;
```

### 使用数据库
```sql
use sharewinfo;
```

```sql
create table if not exists sharewinfo.t_1(uid int,uname string,uage int);
```

**创建库的本质：在hive的数据仓库目录（/user/hive/warehouse/）下创建一个子目录（库名.db）**

### 创建表

```sql

create table if not exists sharewinfo.t_1(
uid int,
uname string,
uage int
)
row format delimited
fields terminated by 'u\0001'
lines terminated by '\n'
;
```

### 加载数据

```sql
load data local inpath '/root/user.csv' into table t_1;
```

**创建表的本质：**
**在hive的数据仓库下的数据库目录下创建一个表目录**

```sql
create table if not exists t_1(
uid int,
uname string,
uage int
)
row format delimited
fields terminated by ','
;
```

===========================================================================================================

### hive中表的类型
​	1.内部表：表目录会创建在hdfs的/user/hive/warehouse下的相应的数据库目录下
​	2.外部表：外部表会根据创建表时location关键字指定的路径创建表目录（如果没有指定location，则表目录的创建位置与内部表相同）

**内部表的创建和外部表的创建，主要就差两个关键字：EXTERNAL LOCATION**

**内部表：CREATE TABLE IF NOT EXISTS T_INNER(ID INT);**
**外部表：CREATE EXTERNAL TABLE IF NOT EXISTS T_OUTER(ID INT) LOCATION '/AAA/BBB/XXX';**

### hive中建表语句所做的两件事
​	1.创建hdfs上相应的表目录
​	2.在元数据库中创建表相应的描述数据（元数据）

### 删除表
​	1.drop时，元数据会被清除。
​	2.drop时，如果是内部表，则表目录会被删除；但是外部表的表目录不会被删除

### 外部表的使用场景
**使用后数据不删除则使用外部表**

**所以，整个数据仓库的最底层的表（与仓库外的数据对接的表，ODS层）应该使用外部表**

### 建表语法

```sql
CREATE [EXTERNAL] TABLE [IF NOT EXISTS] table_name 
   [(col_name data_type [COMMENT col_comment], ...)] 
   [COMMENT table_comment] 
   [PARTITIONED BY (col_name data_type [COMMENT col_comment], ...)] 
   [CLUSTERED BY (col_name, col_name, ...) 
   [SORTED BY (col_name [ASC|DESC], ...)] INTO num_buckets BUCKETS] 
   [ROW FORMAT row_format] 
   [STORED AS file_format] 
   [LOCATION hdfs_path]
```

====================================================================================================================

### 存储格式

**（1） Textfile**
文本格式，Hive的默认格式，数据不压缩，磁盘开销大、数据解析开销大。可结合Gzip、Bzip2使用，但使用Gzip这种方式，hive不会对数据进行切分，从而无法对数据进行并行操作。行式存储
 对应的hive API为：org.apache.hadoop.mapred.TextInputFormat和org.apache.hive.ql.io.HiveIgnoreKeyTextOutputFormat
**（2）SequenceFile**
Hadoop提供的一种二进制文件格式是Hadoop支持的标准文件格式（其他生态系统并不适用），可以直接将对序列化到文件中,所以sequencefile文件不能直接查看，可以通过Hadoop fs -text查看。具有使用方便，可分割，可压缩，可进行切片。压缩支持NONE, RECORD, BLOCK(优先)等格式，可进行切片。行式存储
 对应hive API为：org.apache.hadoop.mapred.SequenceFileInputFormat和org.apache.hadoop.hive.ql.io.HiveSequenceFileOutputFormat
**（3）RCFile**
是一种行列存储相结合的存储方式，先将数据按行进行分块再按列式存储，保证同一条记录在一个块上，避免读取多个块，有利于数据压缩和快速进行列存储。列式存储
 对应的hive API为：org.apache.hadoop.hive.ql.io.RCFileInputFormat和org.apache.hadoop.hive.ql.io.RCFileOutputFormat
**（4）ORCFile**
orcfile是对rcfile的优化，可以提高hive的读写、数据处理性能，提供更高的压缩效率（目前主流选择之一）。列式存储
org.apache.hadoop.hive.ql.io.orc.OrcSerde,org.apache.hadoop.hive.ql.io.orc.OrcInputFormat,org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat
**（5）Parquet**
一种列格式, 可提供对其他 hadoop 工具的可移植性, 包括Hive, Drill, Impala, Crunch, and Pig
 对应的hive API为：org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat和org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat
**（6）Avro**
Avro是一个数据序列化系统，设计用于支持大批量数据交换的应用。它的主要特点有：支持二进制序列化方式，可以便捷，快速地处理大量数据；动态语言友好，Avro提供的机制使动态语言可以方便地处理Avro数据。
 对应的hive API为：org.apache.hadoop.hive.ql.io.avro.AvroContainerInputFormat和org.apache.hadoop.hive.ql.io.avro.AvroContainerOutputFormat

### example

```sql
CREATE EXTERNAL TABLE `weibull`(
CODE string, 
SOURCE string, 
REL_USER_APPL_DESC string, 
REL_CMP_ENGINE_NAME string, 
REL_ENGINE_NAME_DESC string, 
REL_BUILD_YEAR string, 
REL_BUILD_QUARTER string, 
REL_OEM_NORMALIZED_GROUP string, 
WARRANTY_TYPE string, 
SIGNAL_CALC_DATE string, 
WARRANTY_PERIOD string, 
BUILD_VOLUME string, 
CALIM_COUNT string, 
MEDIAN_TIMELAG string, 
PREDICTED_RPH_LOWER_BOUND_HDI string, 
PREDICTED_RPH_PERCENTILE_50_HDI string, 
PREDICTED_RPH_UPPER_BOUND_HDI string, 
PREDICTED_CPE_LOWER_BOUND_HDI string, 
PREDICTED_CPE_PERCENTILE_50_HDI string, 
PREDICTED_CPE_UPPER_BOUND_HDI string, 
X_FLAG string, 
CUTOFF_DATE string, 
MESSAGE string,
__index_level_0__ double
)
ROW FORMAT SERDE
 'org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe'
STORED AS INPUTFORMAT
 'org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat'
OUTPUTFORMAT
 'org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat'
LOCATION
'hdfs://master:9000/hive/weibull'

CREATE EXTERNAL table `users`(
   `name` string,
   `age` int
)
ROW FORMAT SERDE
 'org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe'
STORED AS INPUTFORMAT
 'org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat'
OUTPUTFORMAT
 'org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat'
LOCATION
'hdfs://hadoop01:9000/data/user/user_info'
```

