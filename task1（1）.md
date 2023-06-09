﻿# task1
运用C语言，使用Euler法、梯形法、改进Euler法、Taylor级数法、Runge-Kutta法、线性多步法等任意一种方法，实现对下述简单微分方程的各个瞬时值与最终定态（收敛值）求解：

        [![1](https://camo.githubusercontent.com/fd0fcbf5e69e324502d1c7fe05e3f5f6fdf427359b204656410fd7d49bd07ccd/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535436c656674253543253742253543626567696e2537426d617472697825374479272b793d302673706163653b253543253543792830293d61253543656e642537426d617472697825374425354372696768742e)](https://camo.githubusercontent.com/fd0fcbf5e69e324502d1c7fe05e3f5f6fdf427359b204656410fd7d49bd07ccd/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535436c656674253543253742253543626567696e2537426d617472697825374479272b793d302673706163653b253543253543792830293d61253543656e642537426d617472697825374425354372696768742e)

注：a为常数，可由用户输入确定该值。你可以使用scanf()函数来获取输入的a值。瞬时值求解时步长为0.001，当迭代计算时前后两个值的差小于0.001倍的步长时，该值就认为是定态值。

----------

### 运行结果截图

 - 当a=1时
![1](https://raw.githubusercontent.com/chfissogoodman/task/master/a=1%20jpg.png)
 - 当a=e时
![e](https://raw.githubusercontent.com/chfissogoodman/task/master/a=e%20jpg.png)
 - 当a=π时
![pi](https://raw.githubusercontent.com/chfissogoodman/task/master/a=pi.png)

----------

### 思考题（请给出思考结论）：

1.  当a为1，给出x在区间[0，25]之间方程的各个瞬时值，该方程的最终定态（收敛值）是多少？
**答：0.000999**
2.  当a为e，给出x在区间[0，25*e]之间方程的各个瞬时值，最终定态（收敛值）是多少？（e为指数）
**答：0.000999**
3.  当a为π，给出x在区间[0，25*π]之间方程的各个瞬时值，最终定态（收敛值）是多少？
**答：0.000999**
4.  上面三小问中不同初值的方程最终都能取到各自的最终定态（收敛值），为什么？
**答：因为步长在足够小的情况下，加上函数为递减的，在规定好定义域后，最后可以取得收敛值。**

附加题：

使用C语言对上述前三问的数值求解过程用Excel画图显示，即将每一个x对应的y值在坐标系上画出来，并将绘出的图片附在下面。

 1. a=1
![1](https://raw.githubusercontent.com/chfissogoodman/task/master/aa=1.png)
 2. a=e
![e](https://raw.githubusercontent.com/chfissogoodman/task/master/aa=e.png)
 3. a=π
![pi](https://raw.githubusercontent.com/chfissogoodman/task/master/aa=pi.png)

### 代码
这里我用的是改进的Euler法
```
#include <stdio.h>  
  
#define ABS(x) (x > 0) ? x : -x  
  
double f(double x, double y)  
{  
return -y ;//这里写想要求解的函数  
}  
int main() {  
int m;  
int i;  
double a, b, y0;  
double xn, yn, xnl, ynl, ynlb;  
double h, tmp;  
printf("please write down Xmin and Xmax:\n");//确定想要查找的范围  
scanf("%lf%lf", &a, &b);  
printf("please write down y0:\n");//写出常数a  
scanf("%lf", &y0);  
printf("Enter m to divide the interval into m equal parts:\n");  
scanf("%d", &m);  
if (m <= 0) {  
printf("Please enter a number greater than 1\n");  
return 1;  
}  
h = (b - a) / m;//这里是不设0.001了方便观察，如果按照题目所说讲步长h设为0.001的话数据输出将会达到几万行  
//h=0.001;  
xn = a;  
yn = y0;  
for (i = 1;/* i <= m*/1; i++)//以下为改进欧拉法公式  
{  
xnl = xn + h;  
ynlb = yn + h * f(xn, yn);  
ynl = yn + h / 2 * (f(xn, yn) + f(xnl, ynlb));  
if (ABS((ynl - yn)) < h/1000) {  
printf("y%d=%lf， y%d=%lf",i, ynl,i,yn);  
break;  
}  
if(i <= m) {  
printf("x%d=%lf,y%d=%.10lf\n", i, xnl, i, ynl);  
}  
xn = xnl;  
yn = ynl;  
  
}  
return 0;  
  
}
```
