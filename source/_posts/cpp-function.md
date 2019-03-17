---
title: C++部分常用函数
date: 2019-03-17 14:09:53
tags: C++
categories: C++
---
## 常用函数
### 1. strtok  
  分解字符串为一组字符串。s为要分解的字符，delim为分隔符字符（如果传入字符串，则传入的字符串中每个字符均为分割符）。首次调用时，s指向要分解的字符串，之后再次调用要把s设成NULL。  
  例如：strtok("abc,def,ghi",",")，最后可以分割成为abc def ghi.尤其在点分十进制的IP中提取应用较多。
strtok的函数原型为char *strtok(char *s, char *delim)，功能为“Parse S into tokens separated by characters in DELIM.If S is NULL, the saved pointer in SAVE_PTR is used as the next starting point. ” 翻译成汉语就是：作用于字符串s，以包含在delim中的字符为分界符，将s切分成一个个子串；如果，s为空值NULL，则函数保存的指针SAVE_PTR在下一次调用中将作为起始位置。
```
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
    char sentence[]="This is a sentence with 7 tokens";
    cout << "The string to be tokenized is:\n" << sentence << "\n\nThe tokens are:\n\n";
    char *tokenPtr=strtok(sentence," ");
    while(tokenPtr!=NULL)　{
        cout<<tokenPtr<<endl;
        tokenPtr=strtok(NULL," ");
    }
    //cout << "After strtok,sentence=" << tokenPtr<<endl;
    return 0;
}
```
函数第一次调用需设置两个参数。第一次分割的结果，返回串中第一个 ',' 之前的字符串,也就是上面的程序第一次输出abc。
第二次调用该函数strtok(NULL,","),第一个参数设置为NULL。结果返回分割依据后面的字串，即第二次输出d。
strtok是一个线程不安全的函数，因为它使用了静态分配的空间来存储被分割的字符串位置
线程安全的函数叫strtok_r,ca
运用strtok来判断ip或者mac的时候务必要先用其他的方法判断'.'或':'的个数，因为用strtok截断的话，比
### 2.strcmp
C/C++函数，比较两个字符串
设这两个字符串为str1，str2，
若str1=str2，则返回零；
若str1<str2，则返回负数；
若str1>str2，则返回正数。
matlab中函数，strcmp(s1，s2) 判断两个字符串s1和s2是否相同，相同返回true ,不同返回false  
源码：
```c
int strcmp(const char *str1,const char *str2)
{
    /*不可用while(*str1++==*str2++)来比较，当不相等时仍会执行一次++，
    return返回的比较值实际上是下一个字符。应将++放到循环体中进行。*/
    while(*str1 == *str2)
    {
                assert((str1 != NULL) && (str2 != NULL));
                 
        if(*str1 == '\0')
            return 0;
         
        str1++;
        str2++;
    }
    return *str1 - *str2;
}
```
### 3. Erase
* c.erase(k)  
从c中删除元素k，返回一个size_type值，指出删除的元素的数量
* c.erase(p)  
从c中删除迭代器p指定的元素，p必须指向c中的一个真实元素，不能等于c.end()
* c.erase(b,e)  
从c中删除迭代器对b和e所表示的范围中的元素，返回e
### 4. List
List 反向迭代器  
begin和end成员  
begin和end操作产生指向容器内第一个元素和最后一个元素的下一个位置的迭代器，如下所示。这两个迭代器通常用于标记包含容器中所有元素的迭代范围。  
c.begin() 返回一个迭代器，它指向容器c的第一个元素  
c.end() 返回一个迭代器，它指向容器c的最后一个元素的下一个位置  
c.rbegin() 返回一个逆序迭代器，它指向容器c的最后一个元素  
c.rend() 返回一个逆序迭代器，它指向容器c的第一个元素前面的位置  
上述每个操作都有两个不同的版本：一个是const成员，另一个是非const成员。这些操作返回什么类型取决于容器是否为const。如果容器不是const，则这些操作返回iterator或reverse_iterator类型。如果容器是const，则其返回类型要加上const_前缀，也就是const_iterator和const_reverse_iterator类型。  
### 5. strcpy
描述  
C 库函数 char *strcpy(char *dest, const char *src) 把 src 所指向的字符串复制到 dest。

声明  
下面是 strcpy() 函数的声明。  
`char *strcpy(char *dest, const char *src)`  
参数  
dest -- 指向用于存储复制内容的目标数组。  
src -- 要复制的字符串。  
返回值  
该函数返回一个指向最终的目标字符串 dest 的指针。  
实例  
下面的实例演示了 strcpy() 函数的用法。  
```
#include <stdio.h>
#include <string.h>

int main()
{
   char src[40];
   char dest[100];
  
   memset(dest, '\0', sizeof(dest));
   strcpy(src, "This is runoob.com");
   strcpy(dest, src);

   printf("最终的目标字符串： %s\n", dest);
   
   return(0);
}
```
### 5.转换函数
#### 5.1 Atoi
字符串转整型



