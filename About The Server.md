# 作为一个萌新在设置服务器时遇到的问题
参考网址:[成像工程实验室关于服务器配置的教程](https://github.com/Imaging-Engineering-Lab-ZJU/ServerInfos/blob/master/Environments.md)

**手动目录**

1.2020.10.06（安装Anaconda）

2.VScode添加Remote SSH

3.2021.03.25（安装Pytorch）

4.2021.06.03 安装tensorflow

5.2021.08.16 VScode Remote SSH连不上服务器，报错："command '_workbench.downloadResource' failed"

6.2021.11.03 如何快速迁移一个服务器上安装好的环境到另外一台服务器（利用.yaml文件）

## 缘由
关于服务器的配置问题，实验室的师兄师姐都写了很详细的教程，按照教程来做肯定没有问题，这里只是记录一下我个人配置的过程，仅适用于本实验室

## 2020.10.06
由于账号师兄已经帮忙创建好了，所以这里直接在mobaxterm上面直接登录就行，下面是登录成功的界面：
![Image](https://github.com/Hao-Xu-optics/Test-Project1/blob/master/images/%E7%99%BB%E9%99%86%E6%88%90%E5%8A%9F.png)

随后输入（结合自己的实际情况）
```
xuhao@ubun:~$ cp /home/ubuntu/.bashrc /hdd4T_1/xuhao/
xuhao@ubun:~$ source .bashrc
xuhao@ubun:~$ nvcc -V
```
会显示服务器的信息

然后安装anaconda3，输入指令如下（依然还是结合自己实际情况，主要是用户名）：
```
xuhao@ubun:~$ cp /home/ubuntu/Downloads/Anaconda3-5.3.1-Linux-x86_64.sh /hdd4T_1/xuhao
xuhao@ubun:~$ bash Anaconda3-5.3.1-Linux-x86_64.sh
```
自动安装期间需要按很多次回车键，大致看看没问题就按照默认，直接回车安装就行，安装anaconda3成功之后还会推荐安装vscode，安装成功的界面如下面所示：
![image2](https://github.com/Hao-Xu-optics/Test-Project1/blob/master/images/anaconda3%E5%AE%89%E8%A3%85%E6%88%90%E5%8A%9F.png)

我选择了yes安装vscode（安装过程也是自动的）

随后就是在.bashrc里面添加刚刚安装anaconda3的路径，涉及到一些vim的输入，可参考[菜鸟教程](https://www.runoob.com/linux/linux-vim.html)
>个人认为当前最应该知道的几个指令就是
>>输入"i"进入输入模式；

>>"Del"与"Enter"操作与正常一样不变；

>>按"Esc"结束输入；

>>结束输入之后，输入指令":wq"退出

输入"vim .bashrc"进入操作，并输入"i"进入输入模式，如下图所示：
![image3](https://github.com/Hao-Xu-optics/Test-Project1/blob/master/images/%E6%BB%91%E5%88%B0%E6%9C%80%E5%90%8E%E6%A0%B9%E6%8D%AE%E8%87%AA%E5%B7%B1%E7%9A%84%E5%AE%9E%E9%99%85%E6%83%85%E5%86%B5%E8%BE%93%E5%85%A5.png)

看起来有点吓人，但是暂时别管，直接滑到最后，然后输入
```
export PATH=/hdd4T_1/xuhao/anaconda3/bin:$PATH
```
然后"Esc"退出输入模式，":wq"退出
输入"source .bashrc"保存
自此添加完毕，输入以下指令测试一下是否添加成功：
```
which python
conda list
```
我自己的添加成功的截图是这样的：
![image4](https://github.com/Hao-Xu-optics/Test-Project1/blob/master/images/%E8%AE%BE%E7%BD%AE%E6%88%90%E5%8A%9F.png)

**至此10.06的分享到此结束**

**后面可能会继续更新遇到的问题**

## 2020.10.07 
**今天的主要内容是有关vscode配置Remote SSH的内容，相关教程网上也比较多**
还是先po出来部分参考网址：1.[VSCode:Remote-SSH配置实录](https://blog.csdn.net/sixdaycoder/article/details/89947893)（虽然评论褒贬不一，个人认为可以参考）

首先要做的就是下载vscode[[Download]](https://code.visualstudio.com/)，随后安装vscode，相应的教程也比较多，可以参考[vscode安装教程](https://zhuanlan.zhihu.com/p/106357123)，在汉化，安装好对应的包之后，在**扩展**中搜索Remote -SSH，并安装好，如下图
![image5](https://github.com/Hao-Xu-optics/Test-Project1/blob/master/images/%E6%90%9C%E7%B4%A2.png)

随后在**扩展**上面的**远程资源管理器**处添加自己的账户和IP地址，添加格式为：
```
username@ip  #eg:mike@11.11.11.111
```
![image6](https://github.com/Hao-Xu-optics/Test-Project1/blob/master/images/%E6%B7%BB%E5%8A%A0%E8%B4%A6%E6%88%B7.png)
![image7](https://github.com/Hao-Xu-optics/Test-Project1/blob/master/images/%E8%BE%93%E5%85%A5%E7%94%A8%E6%88%B7%E5%90%8D%E5%92%8Chost.png)

输入了账户之后应该会弹出来一个选项选择保存config文件的位置，选择第一个即可，随后让选择platform的时候咱们实验室要选择**Linux**，别选**Windows**，登录过程中可能会让输入几次密码，登陆成功之后，再把自己的文件调出来（网上教程有讲），看到的文件跟自己在mobaxterm上面看到的是一样的，只不过这里vscode可能用起来方便一点，而且vscode里面可以很方便地编辑，运行文件

**下面说一些部分库的安装**
```
#更新pip install（非必要，出错的之后让更新再更新也行）
pip install --upgrade pip
#安装Python OpenCV
pip install opencv-python
#安装Keras
pip install keras  #理论上这样应该是没问题的，但是一般还是选择镜像源安装
#镜像源安装Keras示例
pip install keras -i https://pypi.tuna.tsinghua.edu.cn/simple  #采用清华镜像源，如果对版本有要求可以为
pip install keras==2.2.1 -i https://pypi.tuna.tsinghua.edu.cn/simple  #这里就对版本要求为2.2.1，如果想要别的镜像源可以为
pip install keras -i http://pypi.mirrors.ustc.edu.cn/simple/  #采用中科大镜像源，常用镜像源
>	http://pypi.douban.com/simple/ 豆瓣 
	http://mirrors.aliyun.com/pypi/simple/ 阿里 
	http://pypi.hustunique.com/simple/ 华中理工大学 
	http://pypi.sdutlinux.org/simple/ 山东理工大学 
	http://pypi.mirrors.ustc.edu.cn/simple/ 中国科学技术大学
```

类似的，很多库也都可以使用这些镜像源进行安装，安装过程中出现的任何问题及时百度就行，大部分情况都会有解决方案的。虽然有的解决方案也不一定适用于自己，就挺糟心的，但是心态别崩就行_[:(]__

**至此10.07的分享到此结束，祝晚安**

## 2021.03.25（没错，时隔半年我又回来了，梅开三度再开始学深度学习）
**今天的主要内容是在服务器上安装pytorch（这里的版本是1.5.1）**

首先列出来参考的几个链接：

1.[看起来最简单明了](https://blog.csdn.net/qq_39214686/article/details/109009406)

2.[主要是关于镜像](https://blog.csdn.net/lelelek/article/details/114290971)

3.2021.11.03镜像碰到的问题[解决方案](https://zhuanlan.zhihu.com/p/260034241)

**第零步————首先当然是创建环境啦！**
创建环境的教程网上也有很多，这里给出参考：

```
conda create -n pytorch python=3.X #pytorch指的是自己pytorch环境的名字，随意好了！py版本根据实际情况定
source activate pytorch #激活环境
```

![image8](https://github.com/Hao-Xu-optics/MyBlog/blob/master/images/2021.03.25/0.png)


（这里还是有个小插曲的，时隔半年再用服务器，不知道为啥conda居然啥也干不了，干啥都出错，一怒之下把Anaconda全部删了，然后再按照前文的记录重新装了一遍（XXX！，装的时候还是心态不要崩）


**第一步————上pytorch官网找conda指令**
[Pytorch官网](https://pytorch.org/get-started/locally/)

![image9](https://github.com/Hao-Xu-optics/MyBlog/blob/master/images/2021.03.25/1.png)

进了官网之后，可以根据你电脑的系统、语言、CUDA版本选择相应的安装指令，对我们实验室来说，CUDA版本稍微有点旧，PyTorch一般也不会装比较新的，倾向于装以前的稳定版本，所以这里不能直接找到想要安装的指令，但是好在上面有一句话：“install previous versions of PyTorch”，那么直接进这个之前版本，在里面选择想要的就好

![image10](https://github.com/Hao-Xu-optics/MyBlog/blob/master/images/2021.03.25/2.png)

![image11](https://github.com/Hao-Xu-optics/MyBlog/blob/master/images/2021.03.25/3.png)

这里给出我今天安装的版本指令：
```
conda install pytorch==1.5.1 torchvision==0.6.1 cudatoolkit=9.2 -c pytorch #如果想要使用镜像源的话，最后的-c pytorch要删掉，具体参考上面的参考链接2
```

**第二步————在服务器上面无脑安装**

看着进度条慢慢滑就好了，不知道为啥今天格外的顺利！

不过也还有一点小插曲，可能是网络的原因，pytorch这些比较大的文件没有下载下来，所以又重新配置了镜像源（具体参考之前提到的参考链接2），不过！一定要看清楚那个镜像源的细节，比如说用第一个好像里面就没有pytorch，就是网址的最后几个名词注意一下

顺利装好！然后测试！

**测试的时候，记得进到Python再import torch**

安装成功：

![image12](https://github.com/Hao-Xu-optics/MyBlog/blob/master/images/2021.03.25/4.png)

（别跟我一样蠢，要不然当然是导入不进来的）

## 2021.06.03 安装tensorflow1.10.0

首先当然还是要创建一个环境：
```Linux
conda create -n tf110 python=3.6
```

随后进入环境并安装tensorflow的指定版本：
```Linux
source activate tf110
conda install tensorflow-gpu==1.10.0
```

sad，用不了，卸载重装
```LInux
pip uninstall tensorflow
```

double sad 还是用不了，再重新卸载，然后这回不用conda装了。这回用pip装：
```Linux
pip install tensorflow-gpu==1.10.0
# 测试是否装成功
import tensorflow as tf
print(tf.__version__)
```

好耶！装成功了！


## 关于VScode Remote -SSH连不上服务器的问题

放完假回来之后，连接的时候一直出现下面这个问题

```
"command '_workbench.downloadResource' failed"
```

网上找了好多办法都不太行（其实主要是新的tar文件下载地址不对），后来看到了这个博客

https://developer.huawei.com/consumer/cn/forum/topic/0201623711683330148?fid=26

很快奥，问题一下子得到了解决，2021.08.16记录

这里可能还有一个更简单的方法，在服务器里面直接把.vscode server文件删掉，然后在Vscode里面重新连接，这样就会自动帮你下载相应的，已经更新过的配置文件，就不用自己下载，解压这些了

## 关于环境迁移的问题

之前237服务器上资源比较紧张，所以拜托管理员在239服务器上又新建了一个账号，但是之前安装过好多包，怎么一次性全部给迁移过来呢？

这边参考了网上的几个博客，操作还算简单：

https://blog.csdn.net/ft_sunshine/article/details/92215164
https://zhuanlan.zhihu.com/p/87344422

1. 首先进入原来环境
```
可以先查看当前有哪些环境:
conda env list

conda activate pytorch170
```
2. 随后导出已有环境
```
conda env export > pytorch170.yaml
```
3. 在当前路径找到生成的pytorch170.yaml文件，拷贝到另一台服务器上
4. 直接进行一个安装（按照我的经验是不需要创建环境的，会自动帮你创建一个一样的环境）
```
conda env create -f pytorch170.yaml
```

有一点需要注意的是，新服务器上的CUDA版本最高只到10.2，所以pytorch应该是需要自己重新装的，这里的安装方法前面也介绍过，不过可能先配置好镜像源会快一点（今天直接用官网的指令安装的时候pytorch一直下载不下来）

但是用了镜像之后，本来是计划安装torch 1.10的，镜像源给自动安装的版本是1.4.0，目前正在解决，看看是卸载重新装看是怎么样


## 2021.11.10 10.12.13.239 安装Pytorch 1.7.0 环境命名为pytorch17
之前也安装成功过，但是好像方法不能复现了？这里重新记录下
```
pip install torch==1.7.0 torchvision==0.8.0 -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install torchaudio==0.7.0  -i https://pypi.tuna.tsinghua.edu.cn/simple
torch.cuda.is_available() #验证是否安装成功
```
