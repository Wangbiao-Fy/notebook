# SSDT和Power BI 内部集成git并推送到GitLab

默认前提下需要安装git，git 工具下载链接为 : https://git-scm.com/download/win。

## SSDT内部集成git并推送到GitLab

### 1、配置全局

鼠标右击桌面空白，使用git bash输入下面两行指令，名称和邮箱自定义。

```shell
git config --global user.name "wangbiao"
git config --global user.email "sdfdsffffff@163.com"
```

### 2、创建项目

创建项目需要勾选新建GIT存储库

![image-20200721133214775](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200721133214775.png)

### 3、添加远程

点击团队资源管理器，点击设置。

![image-20200721133609437](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200721133609437.png)

选择存储库设置，勾选覆盖全局用户名和电子邮件设置。

![image-20200721133709451](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200721133709451.png)

这里可以自定义推送的用户名和邮箱。

我这边由于添加过一个远程，所以会有显示，默认是没有的。我们点击添加。

![image-20200721134204106](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200721134204106.png)

弹出一个窗口，填写名称时注意需要写入origin，提取和推送是gitlab服务器项目的http地址。需要进入gitlab服务器点击，点击蓝色的chone。


![image-20200717102619563](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200717102619563-1595828452258.png)

![image-20200721134441614](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20200721134441614.png)
### 4、添加更改

当我们修改项目并想将项目推送的话，我们需要先在本地git库中存储，然后推送到服务器上。

我们点击团队资源管理器，点击更改

![image-20200722095656825](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722095656825.png)

进入了更改页面，在更改数选项下会出现我们添加更改的次数。

在这里我添加了，一个SQL任务，相对于一次修改，所以显示的是更改数（1）。

然后我们必选填入提交信息，因为这个是必填项，填完以后提交按钮解锁。然后我们点击全部提交。

![image-20200722100541102](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722100541102.png)

**全部提交并推送**

我们可以在更改设置页面下，直接将更改的文件推送到gitlab服务器。

点击全部提交右边的下三角，选择全部提交并推送。

### 5、同步推送

我们全部提交后，已经在本地git存储库中存储，但是我们需要同步到gitlab服务器中，所以我们要回到主页或者在我们提交成功后点击同步也可以，点击同步，进入同步设置页，点击推送即可。

![image-20200722101142455](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722101142455.png)

**从本地提取git服务器最新版本**

我们添加远程后，点击同步中的提取，即可从服务器中拿到最新的数据。

![image-20200722145118944](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722145118944.png)

### 6、添加标签并推送

为了更好的实现版本控制，我们可以为每一次的推送添加一个标签。

添加标签有两种方式，第一种是我们提交完成后有添加标签的选项，第二种是在主页设置标签。下面为大家，演示第二种。

点击标记，点击新建标记，输入标记名称和标记信息。

![image-20200722102708899](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722102708899.png)

第一种与第二种的区别是省略了在主页点击标记的步骤。

然后我们将添加的标记推送到服务器上。

点击想推送的标记，右击选择推送。

![image-20200722103013046](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722103013046.png)

**可以为历史提交文件创建标签**

我们可以为历史提交文件，创建标签。我们打开历史记录，选择我们想要添加标记的记录双击，在右侧点击添加标签即可。

![image-20200722140845157](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722140845157.png)



**切换SSDT项目版本**

我们可以在本地切换各个标签所对于的文件，只需要鼠标双击标签名称，即可进行切换。

**推送全部标签**

我们修改多个版本的项目文件，可以一次性的全部推送，点击全部推送即可。

![image-20200722141040081](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722141040081.png)

### 7、查看历史记录和使用命令行

我们可以在更改、分支、同步这些选项下，点击操作可以参看历史记录和命令行。

![image-20200722103344616](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722103344616.png)

点击操作，选择历史记录。

![image-20200722103425708](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722103425708.png)

点击操作，选择命令行。

![image-20200722103457071](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722103457071.png)

### 8、创建分支

上述的操作都是在主分支上操作的，一般是创建分支进行操作，然后把创建的分支合并到主分支中。

在主页点击分支，然后点击新建分支，默认是勾选**签出分支**，创建后会从主分支转到创建的新分支。不勾选的话不会转到新分支。

![image-20200722104838928](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722104838928.png)

![image-20200722104935790](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722104935790.png)

我们在dev分支上进行更改，然后将更改后的项目合并到主分支，然后在推送。

在合并之前，我们先转到主分支，鼠标双击主分支即可，然后点击合并。

![image-20200722105145261](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722105145261.png)

如何判断是否转到主分支，可以看上图。

![image-20200722105250624](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722105250624.png)

默认是勾选合并后提交更改，不需要我们在更改设置，直接推送即可。

## Power BI Desktop 内部扩展git并推送到GitLab

默认前提需要将Power BI Desktop 更新为最新版本和下载git

### 添加git为外部工具

我们需要创建一个json文件，官方给的实例代码如下

```json
{
    "name": "<tool name>",
    "description": "<tool description>",
    "path": "<tool executable path>",
    "arguments": "<optional command line arguments>",
    "iconData": "image/png;base64,<encoded png icon data>"
}
```

**name**-工具的名称

**description**-工具说明，这个选项是可选的，这个说明会在外部工具上提示。

**path**-工具可执行文件路径

**argument**-命令行参数字符串，可选功能

**iconData**-图像数据，使用的base64编码。

json文件名称格式为**<tool name>.pbitool.json**，64位的存放路径是 **Program Files (x86)\Common Files\Microsoft Shared\Power BI Desktop\External Tools**，**如果没有这个路径的话，需要自己创建。**

iconData是power  bi desktop 外部工具的图像，所以需要一张图片，然后设置图片的base64编码。图片的base64编码，可以使用谷歌浏览器。步骤是将图片拖入谷歌浏览器，打开开发者选项

![image-20200722112930539](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722112930539.png)

复制代码即可。

下面提供我的json文件，供大家参考。
```json
{
	"name": "Git",
	"path": "D:\\Git\\git-bash.exe",
	"iconData": "image/png;base64,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"
}
```

在Power BI Desktop中。

![image-20200722113307737](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200722113307737.png)

**注意：打开后，是power bi /bin 文件路径，需要我们CD到要推送的项目路径下。**

### 常用的git命令

**配置全局的name和email**
```shell
git config --global user.name"your_name"
git config --global user.email "your_email"
```
![image-20200717100902659](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200717100902659.png)

这样提交记录才会在gitlab上显示带有你名字的记录。

如果想使用ssh方式，需要配置ssh密钥。

```shell
git remote add origin ssh/http
```

![image-20200717102619563](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200717102619563.png)

**注意：将所有的修改添加 也可以添加单个文件**

```shell
git add . 
git commit -m "说明信息"
git push -u origin master # 提交
```

**注意：如果提交后报错，使用下面命令**

```shell
git pull --rebase origin master 

git push -u origin master
```

当我们想要将更新的文件加入到项目中，建议不要在master进行操作，这样多人使用master分支，在提交是会报错。所以我们需要创建新的分支。如何创建新的分支呢。请看下面命令

**创建分支**

```shell
git branch 分支名(例如dev)
```

**切换分支**

```shell
git checkout 分支名
```

我们将功能更新后，我们需要将更新的功能合并到master分支，这时需要使用**合并分支**

```shell
git merge 分支名
```

我们可以**看一下是否把更新的功能加入到项目中**，可以使用以下的命令

```shell
git status
```

![image-20200717104728169](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200717104728169.png)

对项目添加完新的功能后，我们可以使用标签进行版本的标记，以便以后对项目的维护

如何创建一个新的标签跟新的项目进行绑定了，我们可以使用以下命令

首先我们要创建一个标签

```shell
git tag -a 标签名 -m “描述信息”
```

我们可以通过命令查看标签的信息

```shell
git show v1.0 
```

最后我们将建好的标签提交到项目中

```shell
git push origin 标签名
```

![image-20200717104944322](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200717104944322.png)

![image-20200717104958152](SSDT和Power BI 内部集成git并推送到GitLab.assets/image-20200717104958152.png)