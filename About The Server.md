# 作为一个萌新在设置服务器时遇到的问题
参考网址:[成像工程实验室关于服务器配置的教程](https://github.com/Imaging-Engineering-Lab-ZJU/ServerInfos/blob/master/Environments.md)

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
