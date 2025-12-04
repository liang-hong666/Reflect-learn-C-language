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
main 和 swap 中的 a 和 b 都具有自动生存期和块作用域。它们在各自的函数被调用时创建，在函数返回时销毁。