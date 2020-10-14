
# 关于宏观傅里叶叠层成像中傅里叶平面对应关系的推导
**（公式使用latex敲入）**

* **成像模型如下图所示：**

![image1](https://github.com/Hao-Xu-optics/MyBlog/blob/master/images/%E6%88%90%E5%83%8F%E6%A8%A1%E5%9E%8B.png)

* **推导过程如下：**
![image2](https://github.com/Hao-Xu-optics/MyBlog/blob/master/images/%E6%8E%A8%E5%AF%BC.png)


* **推导过程的排版如下：**
``` markdown
取经过$f_1$汇聚后的光源为点光源，紧靠Lens2前表面的光场为：

$\tilde{E}(x_1,y_1) = Aexp(ikl) \cdot exp[\frac{ik}{2l}(x_1^2 + y_1^2)]$

经过Lens2的傅里叶变换之后，在Lens2后表面的光场分布为：

$\tilde{E'}(x_1,y_1) = Aexp(ikl') \cdot exp[-\frac{ik}{2l'}(x_1^2 + y_1^2)]$

再经过被测物体之后，带有被测物体的透过率信息：

$\tilde{E''}(x_1,y_1) = \tilde{t}(x_1,y_1) \cdot \tilde{E'}(x_1,y_1)$

从Object平面到Aperture平面，使用菲涅尔衍射公式：
 
$$
\begin{aligned}

\tilde{E}(x,y) 
&= \frac{exp(ikl')}{i \lambda l' }  \iint_{- \infty}^{\infty} \, \tilde{E''}(x_1,y_1) \cdot exp\{ \frac{ik}{2l'}[(x-x_1^2)+(y-y_1^2)] \}\mathrm{d}x_1\,\mathrm{d}y_1 \\ 

&= \frac{exp(ikl')}{i \lambda l' } \iint_{- \infty}^{\infty} \, \tilde{E''}(x_1,y_1) \cdot exp[ \frac{ik}{2l'}(x^2+y^2) ]\cdot exp[\frac{ik}{2l'}(x_1^2+y_1^2)] \cdot exp[-\frac{ik}{l'}(xx_1+yy_1)] \mathrm{d}x_1\,\mathrm{d}y_1 \\

&= \frac{exp(ikl')}{i \lambda l' } \cdot exp[\frac{ik}{2l'}(x^2+y^2) ] \iint_{- \infty}^{\infty} \, \tilde{E''}(x_1,y_1) \cdot exp[\frac{ik}{2l'}(x_1^2+y_1^2)] \cdot exp[-i2\pi (\frac{x}{\lambda l'} x_1 + \frac{y}{\lambda l'}y_1)] \mathrm{d}x_1\,\mathrm{d}y_1
    
\end{aligned}
$$

将$\tilde{E''}(x_1,y_1)$代入上式，并用$C$表示$\frac{exp(ikl')}{i \lambda l' }$，用$C'$表示$C\cdot A exp(-ikl')$则有

$$
\begin{aligned}

    \tilde{E}(x,y) 
    &= C \iint_{- \infty}^{\infty} \, \tilde{t}(x_1,y_1) \cdot A exp(-ikl') \cdot exp[-i2\pi (\frac{x}{\lambda l'} x_1 + \frac{y}{\lambda l'}y_1)] \mathrm{d}x_1\,\mathrm{d}y_1 \\
    &= C' \iint_{- \infty}^{\infty} \, \tilde{t}(x_1,y_1) \cdot exp[-i2\pi (\frac{x}{\lambda l'} x_1 + \frac{y}{\lambda l'}y_1)] \mathrm{d}x_1\,\mathrm{d}y_1 \\
    &= C \cdot \mathcal{F}[\tilde{t}(x_1,y_1)] |_{u=\frac{x}{\lambda}l',v=\frac{y}{\lambda}l'}
    
\end{aligned}


$$
```
