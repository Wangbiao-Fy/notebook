

## VM docker 安装 nginx



### 1.安装docker 

```
yum -y install docker
```

### 2.查看docker信息

```
docker info
```

**注意：重新启动的虚机可能docker不好使，可以使用*systemctl restart docker*这个命令重新启动doocker**

```python
systemctl restart docker # 重启docker
systemctl start docker # 启动docker
systemctl enable docker # 开机自动启动docker
```



### 3.取最新版的 Nginx 镜像

这里我们拉取官方的最新版本的镜像： 

```
docker pull nginx:latest
```

### 4.查看本地镜像
使用以下命令来查看是否已安装了 nginx：

```
docker images
```


安装完成后，我们可以使用以下命令来运行 nginx 容器：

```
docker run --name nginx-test -p 8080:80 -d nginx
```

参数说明：

- name nginx-test：容器名称。
- p 8080:80： 端口进行映射，将本地 8080 端口映射到容器内部的 80 端口。
- d nginx： 设置容器在在后台一直运行。

### 5.安装成功
最后我们可以通过浏览器可以直接访问 8080 端口的 nginx 服务：

![](D:\wb980\BigData\docu\VM docker 安装 nginx.assets\image-20220527174323510.png)

### 6.替换默认nginx显示web页面

进入容器

```
docker exec -it mynginx /bin/bash
```


更新容器内部的安装源

备注：可以理解为：进入到一个初始化的环境，没有 apt-get，也没有 vi，需要重新安装。

```
apt-get update
```


安装 vi 文本编辑器

```
apt-get install vim
```


编辑 nginx 配置文件，查看红框中的路径

将第一个红圈中的路径改为你要访问的 html 所在路径，建议将 html 取名为 index.html ，因为 nginx 默认访问的是 index.html 文件。

备注：

进入文件后，按 i 进入编辑模式
按 esc 退出编辑模式（也称命令行模式）
在命令行模式下，按冒号进入底行模式；
在底行模式下
输入 wq：保存并退出
q!：不保存并强制退出

```
vim etc/nginx/conf.d/default.conf
```

![image-20220530131911898](D:\wb980\BigData\docu\VM docker 安装 nginx.assets\image-20220530131911898.png)

将宿州机中的文件传输到docker容器中

```
docker cp 你的文件路径 容器长ID:docker容器路径
```

在宿主机上执行命令例如：

```
docker cp /var/backup/nginx.zip 68b99:/usr/share/nginx/html
```

安装zip解压包

```
apt-get install unzip zip
```

退出容器

输入 exit 并回车，或直接按 ctrl+d 即可退出容器

重启容器

```
docker restart mynginx
```

**docker其他操作**

查看创建的docker容器

```
 docker ps -a
```

查看运行的docker容器

```
docker ps
```

启动指定的docker容器 （后面的是id）

```
docker start f905e1150ca3 （或者是容器名称）
```



