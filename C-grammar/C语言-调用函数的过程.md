## 如何调用函数
### 函数的组成
```C
int calculate(int x, int y, int z)
```
1.$int$:返回值类型。
还有其他类型：$void(无返回值),short,char$等等。  

⚠️**main函数中接受返回值的数据类型也要与此相同**   

2.$calculate$：函数名。  
3.$( ):函数体$。**每个参数都必须单独声明其数据类型**

### ⚠️调用
**1.** 可以先声明，再写$main$ 函数，再定义函数。  
**2.** 直接先定义函数，再在 $main$ 函数中调用。
**C语言中，调用之前前面一定要有声明**

### 例1：计算表达式的值
```C
#include<stdio.h>
int calculate(int x, int y, int z) 
{
    int result;
    result = (x + y) * z;
    return result; 
}

int main()
{
    int a, b, c; 
    int s;
    scanf("%d %d %d", &a, &b, &c);
    s = calculate(a, b, c); 
    printf("%d\n",s);
    return 0;
}
```

#### 定义函数
```C
int calculate(int x, int y, int z);
```
#### 调用过程
###### 第一步
```C
scanf("%d %d %d", &a, &b, &c);
```
$scanf$让用户输入$a,b,c$，编译器接收确定实参。
###### 第二步
```C
s = calculate(a, b, c);
```
调用开始，参数传递，将$a,b,c$的值复制给 $calculate$函数定义中的形参$x, y, z$。
###### 第三步
```C
int result;
result = (x + y) * z;
return result;
```
定义函数开始执行，计算结果储存到变量$result$中，作为返回值。
###### 第四步
```C
s = calculate(a, b, c); 
printf("%d\n",s);
```
回到$main$函数，定义函数$calculate$的返回值赋值给变量$s$
由$main$函数调用$printf$函数打印输出变量$s$的值

#### 有些分析
###### 如果只这样写会怎样
```C
calculate(a, b, c);
```
定义函数$calculate$虽然被执行了，但返回值没有被存储，也不会输出。  

### 例二：调用函数过程中参数的变化
```C
#include<stdio.h>
int max(int a,int b)
{
    int ret;
    if( a>b )
    {
        ret = a;
    }
    else
    {
        ret = b;
    }
    return ret;
}
int main()
{
    int a,b,c;
    a = 5;
    b = 6;
    c = max(10,12);
    c = max(a,b);
    c = max(c,23);
    printf("%d\n",max(a,b));
    return 0;
}
```
#### 调用过程
###### 第一步
```C
c = max(10,12);
```
将实参$10$和$12$赋值给形参$a$，$b$，将$max$函数的返回值$ret$赋值给变量$c$
###### 第二步
```C
c = max(a,b);
```
将$main$函数实参$a$和$b$赋值($a = 5$)($b = 6$)给形参$a$，$b$，将$max$函数的返回值$ret$赋值给变量$c$  
编译完后，此时$c = 6$
###### 第三步
```C
c = max(c,23);
```
将实参$c$和$23$赋值给形参$a$，$b$，将返回值$ret$赋值给变量$c$ 
编译完后，此时$c = 23$
###### 第四步
```C
 printf("%d\n",max(a,b));
 ```
 $printf$打印的值为编译$max(a,b)$后的返回值  
 输出：$6$
 #### 有些分析
 **1.** 我们可以看到变量$c$ 的值随着程序的执行不断变换。
 **2.** 函数的返回值，既可以赋值给变量，也可以再传递给其他函数，还可以被丢弃。

 #### ⚠️单一出口原则
 一个函数最好只有一个返回值，有多个返回值（即有多个出口），以后修改的时候不方便。






