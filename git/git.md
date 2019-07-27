# Git原理

> 关于版本控制

	版本控制是一种记录一个或者若干个文件内容变化，以便将来查询特定

	版本修订情况的系统，主要有三种：本地版本控制系统，集中式版本控

	制系统（SVN），分布式版本控制系统（Git）

> Git的优势

	速度快，设计简单，允许上千个并行分支，分布式（不怕断网等情况）

## Git入门使用

> 新建项目和科隆已有项目（如图）
 
	1 登录你的github账号，点击绿色按钮
![](https://i.imgur.com/I5cXrmn.png)
	2 填写相关信息
![](https://i.imgur.com/1LDPcD4.png)
	3 继续点击绿色按钮，使用SSH
![](https://i.imgur.com/Y2i0r5K.png)
	4 复制其地址
![](https://i.imgur.com/Ue4Z4Kn.png)
	5 打开终端，输入git clone git@github.com:x1059455449/blogtest.git

	此时可能会报错，原因是没有设置公钥
![](https://i.imgur.com/Jv4gwjD.png)
	6 创建公钥私钥对，输入ssh-keygen -t rsa -b 4096 -C "GITHUB邮箱" 
![](https://i.imgur.com/bRT0eY2.png)
	7 后面的提示，直接全部按ENTER
![](https://i.imgur.com/fMADJhM.png)
	8 输入cat ~/.ssh/id_rsa.pub,拷贝公钥内容
![](https://i.imgur.com/EEe1ILP.png)
![](https://i.imgur.com/HmkzlxH.png)
![](https://i.imgur.com/0A4SSPi.png)
![](https://i.imgur.com/UztQOtT.png)
![](https://i.imgur.com/496qMRb.png)
	9 现在进行克隆，输入git clone git@github.com:x1059455449/blogtest.git

	10 接下来依次输入下图所示指令
![](https://i.imgur.com/ej1e9ze.png)
	11 最后在GITHUB的设置里面把GITHUB主页选择为master branch
![](https://i.imgur.com/6qYmCap.png)
### Github 的使用

	1 同GIT前六步基本类似

	2 添加文件，输入vim index.html,随意输入一些内容，保存退出
	
	3 输入git add .

		git commit -am "add"

		git push origin master

![](https://i.imgur.com/P7oAl4b.png)
	
	4 舒心网页之后就会发现有新的文件和缩写的内容
![](https://i.imgur.com/hWYt7yi.png)
![](https://i.imgur.com/Ly9w42f.png)

#### Git基本命令

> 几个重要概念

	已提交：该文件已经被安全地保存在本地数据库中了
	
	已修改：修改了某个文件，但还没有提交保存

	已暂存：把已修改的文件放在下次提交时要保存的清单中

![](https://i.imgur.com/QW0ktXZ.png)

> 起步 初次使用时需要设置姓名和邮箱

	git config --global user.name "nide xingming "

	git config --global user.email xxxxxx@163.com

> Clone项目 用于把一个GitHub的项目clone(下载)到本地变为本地仓库

	git clone SSH的拷贝地址
	
	cd 所放文件夹

> 添加文件并提交

	1 创建文件 touch a.md	
	
	2 在文件里写入若干字符串 echo "5201314" > a.md
	
	  git status

	3 把当前目录下的新增和修改的文件添加到暂存区

	  git add . (表示把当前文件夹下的新增和删除都放在这个区)

	4 把暂存区的更新提交到本地库

	  git commit -am "add file" (-a直接提交新增修改，m做点备注，一般用来做什么就写什么)

	  git status

	5 把当前本地库里的改动推送到远程库（origin）的master分支

	  git push origin master	

![](https://i.imgur.com/3TVC5Fu.png)
![](https://i.imgur.com/Bb23aEF.png)

> 修改删除文件

	1 把远程仓库的变动更新合并到本地仓库 git pull
	
	2 修改文件

	  vim a.md

	  git add .(这里需要注意，这里提交消息包含大量的字符串，提交参数不用加m，此时会进入vim界面，按下i进入编辑模式，进行编辑，编辑完成后按下ESC进入命令状态，输入：wq保存退出vim)

	3 git commit -a

	  git push origin master

	  rm -rf a.md 

	  git add .

	  git commit -am "删除a.md"

	如果之前已经执行过git push origin master，后面可以直接简化成git push 

	4 使用前必须先git pull保持远程仓库的更新,更新代码

	5 若远程仓库放生改变，必须先git pull保持远程仓库的更新,更新代码，不然会报错（本地仓库同理）
**注意：不管远程仓库还是本地仓库做了什么改动，都必须先git pull更新代码，然后再git add .  git commit -am "删除a.md"**

> 效果图如下

![](https://i.imgur.com/C6HhKSN.png)
![](https://i.imgur.com/opkQ3p3.png)
![](https://i.imgur.com/LzTZE8V.png)
![](https://i.imgur.com/QwkWmwB.png)
![](https://i.imgur.com/kMEEav5.png)
![](https://i.imgur.com/EeLt5z4.png)

> git clone url和git pull的区别

参考博客[https://blog.csdn.net/zhou_xiaomiao/article/details/53185712](https://blog.csdn.net/zhou_xiaomiao/article/details/53185712)
[https://blog.csdn.net/riddle1981/article/details/74938111](https://blog.csdn.net/riddle1981/article/details/74938111)

> 本地仓库和远程仓库的区别

	1.本地与远程的差集 :（显示远程有而本地没有的commit信息）

	git log local_branch..origin/remote_branch

	2.统计文件的改动

	git diff --stat local_branch origin/remote_branch

> origin 表示

参考博客和知乎
[https://www.zhihu.com/question/27712995](https://www.zhihu.com/question/27712995)

[https://blog.csdn.net/abo8888882006/article/details/12375091](https://blog.csdn.net/abo8888882006/article/details/12375091)

##### Git高级指令

> 本地创建一个的git项目推送至远程空仓库

**指令图**
![](https://i.imgur.com/GKukHKY.png)
![](https://i.imgur.com/bMC2oYH.png)
![](https://i.imgur.com/N5L80Yq.png)
![](https://i.imgur.com/9EBlogP.png)
![](https://i.imgur.com/9Kd9V13.png)


> 分支操作

git branch -a查看本地分支
git checkout master 切换回主干
git merge dev 把分支的东西合并到主干上

![](https://i.imgur.com/RTjO4Fs.png)
![](https://i.imgur.com/A7thYbj.png)

> 冲突

![](https://i.imgur.com/k6yy43r.png)

##### Git常见问题及解答（来源饥人谷）

[https://xiedaimala.com/tasks/7d659df8-ce04-4002-865c-6f07f7f4bc07/text_tutorials/8b4fad30-40de-4dc6-bffe-2f2c80cb4de5](https://xiedaimala.com/tasks/7d659df8-ce04-4002-865c-6f07f7f4bc07/text_tutorials/8b4fad30-40de-4dc6-bffe-2f2c80cb4de5)



