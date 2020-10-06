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
