## 1.git的使用

先解释一些概念，git分四层管理代码。

> 1. 你目录中的文件是第一层
> 2. 缓存区，每次add之后，当前目录中要追踪的文件会作为一个版本会存放在缓存区。注意不是所有的文件。一般一个文件生成之后，会标记为“未追踪”，但是否对其做版本管理还是要选择的。例如一些编译文件就没有必要追踪。对需要做版本管理的问件，用add添加，不需要的用clean删除。
> 3. 本地仓库，每次commit之后，缓存区最新的版本就会存放在本地仓库。这里要提及一个HEAD的概念。HEAD是当前的版本指向，每次更新或者回退都会修改HEAD的指向，但对仓库中每一个版本并不会删除。所以即使回退到过去还是有机会回到现在的版本的。
> 4. 远程仓库，每次push之后，会将本地仓库中HEAD所指向的版本存放到远程仓库

附上一些常用的命名方便查看

![](/home/woaixsy/happy/Operatelog/Git一些命令.png)

![](/home/woaixsy/happy/Operatelog/Git本地常见使用命令.png)

![](/home/woaixsy/happy/Operatelog/Git远程常见使用命令.png)

![](/home/woaixsy/happy/Operatelog/Git形象描述图.png)



## 2. git与github的链接

首先我们认为你已经有一个github的账户。

然后我们要建立SSH链接。这是一种通讯的加密协议。我先在我的笔记本上计算一对公钥和私钥，将公钥存储在github中，这样本地就可以通过SSH与github展开加密通讯。详细的内容可以参考[SSH原理与运用（一）：远程登录](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)。

建立方法，输入命令

```shell
ssh-keygen -t rsa -C "your_email@youremail.com" //双引号里面是你的常用邮箱
```

输入之后要输入口令，可以不用输入直接按“enter”一路确认就可以了。然后在账户的根目录（/或者/home/你的账户名，具体取决于你执行上述命令时所采用的账户）查找隐藏目录.ssh/id_rsa.pub文件，将当中内容添加到github中。

这样你就可以通过SSH链接到github中了。但是github作为一个远程仓库，你可以链接这个仓库，并保持同步。但是你不能把本地仓库直接上传到github中去。所以你应该先在github中建立一个对应的仓库，然后再在本地建立一个仓库，将两者进行链接，再去写入文件执行版本管理。所用到的命令有

```shell
git remote add origin git@github.com:<用户名>/<仓库名>.git
git pull origin master //因为github建立仓库时会有readme.md文件，先要拷贝一份
git push -u origin master //将本地仓库链接到master分支上，你当然可以链接到其他分支
git push//上传你的本地仓库
```

还有一种方法不用分两地建库再去链接。你可以只在github上建库，然后clone到本地目录中。

```shell
git clone git@github.com:<用户名>/<仓库名>.git
```

至于团队合作中的分支管理，由于现在还用不到，等以后有机会试用在去学习吧。