### 使用git在vscode中将代码文档等推送至远程github仓库
* 问题背景：以及拥有一个github仓库，并且以及下载安装初始化git等步骤，并且按照以下步骤配置好git，
```
git init //初始化仓库
git add .(文件name)                  //添加文件到本地暂存
git commit -m “first commit”        //添加文件描述信息
git remote add origin    远程仓库地址 //链接远程仓库
git push -u origin master          //把本地仓库的文件推送到远程仓master                                      分支
```
当想要推送至仓库时，发现存在报错.如下图所示
![](images/2023-03-29-11-05-07.png)

根据信息提示我们可以知道大概的原因是：这是因为在本地新建库后，与远程仓库的内容不一致导致的（远程仓库有一些内容本地没有）。因为我使用的远程仓库是早就存在的，里面存在一些文档，而工作目录中没有这些文件

* 解决方法
思路：将远程仓库的文件先拉到工作目录中，再将工作目录中的文件推送至远程仓库。
``` git pull origin master --allow-unrelated-histories ```

总结：正确的步骤为
git init //初始化仓库
git add .(文件name) //添加文件到本地仓库
git commit -m “first commit” //添加文件描述信息
git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支
git pull origin master --allow-unrelated-histories// 把本地仓库的变化连接到远程仓库主分支
git push -u origin master //把本地仓库的文件推送到远程仓库
