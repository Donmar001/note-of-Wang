##  <center>GIT</center>

Git是目前世界上最先进的**分布式版本控制系统**

> 分布式控制系统
>
> 集中式控制系统

先说集中式版本控制系统，版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。

集中式版本控制系统最大的毛病就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个10M的文件就需要5分钟，这还不得把人给憋死啊。

![central-repo](https://www.liaoxuefeng.com/files/attachments/918921540355872/l)



分布式版本控制将完整版本库放在每台电脑中，没有绝对的中央服务器，需要协作时只需要将

修改的部分推送给对方。与集中式版本控制相比分布式的安全性大大增加。但在实际使用时，会有一台充当中央服务器的电脑，方便用来交换修改

![distributed-repo](https://www.liaoxuefeng.com/files/attachments/918921562236160/l)



### <center>安装GIT</center>

##### 在Linux之ubuntu下安装

先输入```$ git```查看系统是否已经安装git

若没有安装则会显示如下提示

```
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```

接着使用命令 ```sudo apt install git```就可以直接完成git的安装



##### 在windows下安装git

在官网下载[git](https://git-scm.com/downloads),但往往会下载失败，此时可以将下载地址复制到其他下载工具中下载，如迅雷

具体步骤：

带开git官网，按f12显示网页前端代码，再按住鼠标的图标，指向点击下载的地方，随即右边就会出现详细的下载地址，将地址复制，即可在迅雷下载git。

安装完成后还需要最后一步设置自己的用户名和邮箱

```
$ git config --global user.name "Your name"
$ git config --global user.email "email@example.com"
```



#### 　　创建版本库

版本库又名仓库，英文为repository，也可以理解为一个目录，目录中的文件都可以被git管理

创建一个版本库

创建一个空目录

```
$ mkdir learngit              //创建一个名为learngit的仓库，
cd learngit
$ pwd                         //显示地址命令
/c/user/用户名                  //默认创建在该位置
```

使用```git init```该目录变成git可以管理的仓库

```
$ git init 
Initialized empty Git repository in 
/Users/用户名/learngit/.git/
```

当前目录中会出现.git文件用于管理版本库，不要随意修改

首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。V

不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件

使用Windows的童鞋要特别注意：

千万不要使用Windows自带的**记事本**编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。建议你下载[Notepad++](http://notepad-plus-plus.org/)代替记事本，不但功能强大，而且免费！记得把Notepad++的默认编码设置为UTF-8 without BOM即可：

```
$ git add 文件名
```

执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。

```
$ git commit -m "提交的说明"
```

`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录

`git commit`命令执行成功后会告诉你，`1 file changed`：1个文件被改动（我们新添加的readme.txt文件）；`2 insertions`：插入了两行内容（提交的文件有两行内容）



可以add多个文件，而只需commit一次



```
$ git status         //命令可以让我们时刻掌握仓库当前的状态
$ git diff 文件名     //上一次被修改的内容
$ git log             //显示历史记录
$ git log --pretty=oneline     //单行显示版本号
```



```
$ gir reset --hard HEAD^       //返回上一版本
```

Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。



```
$ git reset --hard 版本号   //返回该版本号对应的版本
```

 ```
$ git reflog        //显示历史命令
 ```

```
$ git chekout -- readme.txt            //丢弃工作区的修改
```

![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。



当修改的文件被添加到暂存区时用命令`git reset HEAD `可以把暂存区的修改撤销（untage），重新放回<font color = red >工作区</font>

```
$ git reset HEAD readme.txt          //将暂存区的修改回退至工作区
Unstaged changes after reset:
M	readme.txt
```



#### 将本地的git仓库同步至远程的github仓库

本地仓库与github传输时是使用<font color = "red">***ssh***</font>加密的,所以需要先在本地创建SSH KEY。先在用户的主目录下看是否有.SSH文件，若无则执行下列步骤

```
$ ssh-keygen -t rsa -C "你的email地址"
```

接着全部回车，按默认即可

![image-20200229144233777](../typora-user-images/image-20200229144233777.png)



接着就可以在用户主目录中找到，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

![image-20200229145011650](../typora-user-images/image-20200229145011650.png)



接着登陆github，点击右上角点击头像框->再进入settings->SSH and GPG keys ->点击添加后，将id_rsa.pub复制到key的文本框，title可以随便填



![image-20200229145608936](../typora-user-images/image-20200229145608936.png)

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。



想要在github上建立一个同步仓库即可，将本地的git仓库远程同步了

首先在github上新建一个仓库

![image-20200229151803458](../typora-user-images/image-20200229151803458.png)

在仓库名中填入本地需要同步仓库的名字，其他保持默认设置

再按照github中的提示在git bash中输入

```
$ git remote add origin https://github.com/github账户名/本地仓库名.git
```

添加后origin就是远程库的名字，可以将其改为其他名字

下一步就可以将本地的仓库推送到远程库中

```
$ git push -u origin master
```

![image-20200229152809823](../typora-user-images/image-20200229152809823.png)

接着在github的仓库中就可以看到本地仓库中的内容了

![image-20200229153018779](../typora-user-images/image-20200229153018779.png)

![image-20200229152957285](../typora-user-images/image-20200229152957285.png)



上面讲了如何现有本地库再推送至远程库中，下面可将远程库中的仓库克隆至本地

首先建立一个实验的仓库名为testlib

![image-20200301102114852](../typora-user-images/image-20200301102114852.png)

勾选自动建立readme的选项

首次使用clone时会出现警告

![image-20200301103903312](../typora-user-images/image-20200301103903312.png)

只需yes即可，这个警告只会出现一次，后面的操作就不会有任何警告了。

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入`yes`回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：



克隆好后打开改文件夹就可以看到readme文件

![image-20200301104045133](../typora-user-images/image-20200301104045133.png)

你也许还注意到，GitHub给出的地址不止一个，还可以用`https://github.com/michaelliao/gitskills.git`这样的地址。实际上，Git支持多种协议，默认的`git://`使用ssh，但也可以使用`https`等其他协议。

使用`https`除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`。

Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快。



#### 创建与合并分支

创建一个分支dev,并切换到dev

```
$ git checkout -b dev(分支名)
```

相当于以下两条命令

```
$ git branch dev         //创建 
$ git checkout dev       //切换到分支dev
```

查看分支

```
$ git branch 
```

列出所有分支，并在当前分支前标*

![image-20200301113131869](../typora-user-images/image-20200301113131869.png)



在提交到dev分支中

![image-20200301113220699](../typora-user-images/image-20200301113220699.png)



合并分支

```
$ git merge dev
```

`git merge`命令用于合并指定分支到当前分支。合并后，再查看`readme.txt`的内容，就可以看到，和`dev`分支的最新提交是完全一样的。

注意到上面的`Fast-forward`信息，Git告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。

当然，也不是每次合并都能`Fast-forward`.合并完成后，就可以放心地删除`dev`分支了：

```
$ git branch -d dev
```

删除后，查看`branch`，就只剩下`master`分支了：

因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在`master`分支上工作效果是一样的，但过程更安全。

![image-20200301113427892](../typora-user-images/image-20200301113427892.png)



##### 新switch命令

我们注意到切换分支使用`git checkout `，而前面讲过的撤销修改则是`git checkout -- `，同一个命令，有两种作用，确实有点令人迷惑。

实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的`git switch`命令来切换分支：

创建并切换到新的`dev`分支，可以使用：

```
$ git switch -c dev
```

直接切换到已有的`master`分支，可以使用：

```
$ git switch master
```



查看分支：`git branch`

创建分支：`git branch `

切换分支：`git checkout `或者`git switch `

创建+切换分支：`git checkout -b `或者`git switch -c `

合并某分支到当前分支：`git merge `

删除分支：`git branch -d `



当两个防止存在不同的修改时，不能快速合并，这是需要修改冲突再合并

用带参数的`git log`也可以看到分支的合并情况：

```
$ git log --graph --pretty=oneline --abbrev-commit
*   cf810e4 (HEAD -> master) conflict fixed
|\  
| * 14096d0 (feature1) AND simple
* | 5dc6824 & simple
|/  
* b17d20e branch test
* d46f35e (origin/master) remove test.txt
* b84166e add test.txt
* 519219b git tracks changes
* e43a48b understand how stage works
* 1094adb append GPL
* e475afc add distributed
* eaadf4e wrote a readme file
```

当分支合并时，默认会使用fast forward模式，但在这种合并时，删除分支后会丢掉分支信息

如果禁用FAST forward模式，就会再merge分支时生成一个新的commit，就可以从分支历史看到分支后信息

使用```--no--ff```的方式的```git merge```禁用fast forward



#### 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)



修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick `命令，把bug提交的修改“复制”到当前分支，避免重复劳动。