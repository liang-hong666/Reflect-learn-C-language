### C语言调用函数的一些杂事
###### 例一：不同函数中相同的参数名
```C
#include<stdio.h>
int swap(int a,int b)
{
    printf("1:%d %d\n",a,b);
    printf("2:%d\n",a+b);
    a = 2;
    b = 4;
    printf("3:%d %d\n",a,b);
    return 0;
}
int main()
{
    int a = 1;
    int b = 2;
    swap(a,b);
    printf("4:%d %d\n",a,b);
    return 0;
}
```
最终的输出：
1:1 2 <br>
2:3   <br>
3:2 4 <br>
4:1 2 <br>
**生存期和作用域** <br>
😄局部变量和全局变量：本例就是一个很好的例子，C语言传值只能传给函数,每个函数都有自己的变量空间，参数独立在这个空间中。如main函数中的a，b传给swap函数，尽管main和swap函数中的变量名相同，但他们之间毫无关系。<br>
main 和 swap 中的 a 和 b 都具有自动生存期和块作用域。它们在各自的函数被调用时创建，在函数返回时销毁。<br>
### 例二：参数类型不匹配的结果
###### 🧐初始化的一些事情
局部变量：定义在函数内部，必须手动初始化，否则就是输出就是一个垃圾值<br>
全局变量：定义在函数外部，会自动初始化，默认初始化为0<br>
静态变量（statlic）：会自动初始化为0<br>
```C
#include<stdio.h>
void swap();
int main()
{
    int a = 4;
    int b = 5;
    swap(a,b);
    printf("a=%f b=%f\n",a,b);
    printf("a=%d b=%d\n",a,b);
    return 0;
}
void swap(double a,double b)
{
    printf("a=%f b=%f\n",a,b);
}
```
只有这个输出是正确的
```C
printf("a=%d b=%d\n",a,b);
```
⚠️函数原型的作用<br>
既检查函数的调用（函数是否存在）是否正确，还会检查对函数的定义是否正确。因此刚开始我的声明，并未告诉编译器是什么类型，而我传给swap函数的时候是两个整型变量，但整型传到double那里就发生错误了，并且我没有声明double a，double b，故最终出现错误。<br>
✌️改正<br>  
以后声明函数的时候，写清楚参数类型