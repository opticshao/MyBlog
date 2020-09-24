# Test-Project1
测试第一个工程，此工程是按照CSDN教程新建 [链接地址](https://blog.csdn.net/tichimi3375/article/details/79844514?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param)

## 关于写这篇README的缘由
2020年09月24日，在实验室开完组会之后，看到大佬们的操作猛到不行，于是我意识到是时候好好管理我的GitHub账户了，不能当一个只down别人代码的白嫖怪了。因此我来GitHub**更新了头像**并创建了属于我的第一个工程**Test-Project1**，对于GitHub的使用还不是很明白，所以只有边学边看

**这里的README.md只是为了熟悉Markdown常用语法**<br>
Markdown常用语法是参考链接[GitHub上README.md教程](https://blog.csdn.net/a15920804969/article/details/80460537)

## 第一章 分享一个Python代码
```Python
import cv2

capture = cv2.VideoCapture(0)

while(True):
    ret, frame = capture.read()
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    #打印出获取图像的信息
    width, height = capture.get(3), capture.get(4)
    #print(width, height)
    frame_rate = capture.get(5)
    #print(frame_rate)
    text = 'Frame rate = '+str(frame_rate)+' '+'Image size = '+str(width)+'*'+str(height)
    cv2.putText(frame,text, (20,20), cv2.FONT_HERSHEY_SIMPLEX, 0.7,(0,0,255), 1, cv2.LINE_AA)
    
    cv2.imshow('frame',frame)
    
    if cv2.waitKey(1) == ord('q'):
        break

capture.release()
cv2.destroyAllWindows()
