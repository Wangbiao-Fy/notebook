# [操作系统怎么把文件放到docker容器里](http://www.bdsoba.com/)

完美拷贝本地文件到[docker](http://www.awaedu.com/)容器:

（1）查找容器

```
docker ps -a
```

![img](https://img-blog.csdnimg.cn/img_convert/72f4704dcd038b247155c78a9005f7ec.png)

（2）确定我们的容器名，并获取容器长ID

```
docker inspect -f '{{.ID}}' store-dev
```

![img](https://img-blog.csdnimg.cn/img_convert/f23784b980ae5b449d0c9ef5302e76c9.png)

（3） 拷贝本地文件到容器

```
docker cp 你的文件路径 容器长ID:docker容器路径
```

示例：

假设容器名为68b99,现在要将宿主机/var/backup/[nginx](https://so.csdn.net/so/search?q=nginx&spm=1001.2101.3001.7020).zip文件拷贝到容器里面的/cert路径下面

在宿主机上执行命令：

```
docker cp /var/backup/nginx.zip 68b99:/cert
```

更多相关教程，请关注PHP中文网[docker教程](https://www.php.cn/docker/)栏目。

以上就是怎么把文件放到[docker](https://so.csdn.net/so/search?q=docker&spm=1001.2101.3001.7020)容器里的详细内容，更多请关注php中文网其它相关文章