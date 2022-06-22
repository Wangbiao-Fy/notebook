# [Centos7解压Zip文件](https://www.cnblogs.com/ourlang/p/12230972.html)

## 安装支持ZIP的工具

```python
yum install -y unzip zip
```

### 1、把文件解压到当前目录下

```python
unzip test.zip
```

### 2、如果要把文件解压到指定的目录下，需要用到-d参数。

```bash
unzip -d /temp test.zip
```

### 3、解压的时候，有时候不想覆盖已经存在的文件，那么可以加上-n参数

```python
unzip -n test.zip
unzip -n -d /temp test.zip
```

### 4、只看一下zip压缩包中包含哪些文件，不进行解压缩

```python
unzip -l test.zip
```

### 5、查看显示的文件列表还包含压缩比率

```python
unzip -v test.zip
```

### 6、检查zip文件是否损坏

```python
unzip -t test.zip
```

### 7、将压缩文件test.zip在指定目录tmp下解压缩，如果已有相同的文件存在，要求unzip命令覆盖原先的文件

```bash
unzip -o test.zip -d /tmp/
```