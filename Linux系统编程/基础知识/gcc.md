# gcc  



## gcc编译程序四步骤  

预处理————>编译—————>汇编————>链接   

### 预处理  

指令： gcc -E

hello.c————>hello.i

* 展开宏  头文件  
* 替换条件编译  
* 删除注释  空行  空白   

###  编译  

指令： gcc -S

hello.i————>hello.s  

* 检查语法规范  
    * 是否有拼写错误
    * 是否少了匹配括号  

* 消耗时间、系统资源最多  因此想提高编译效率主要从这一步骤入手   


### 汇编  

指令： gcc -c

hello.s————>hello.o  

将汇编指令(hello.s) **翻译**成机器指令 (hello.o)  

### 链接  

指令： gcc  (无参数，注意 -o是指定生成文件的名字)

hello.o————>a.out  

* 数据段合并
* 地址回填  

### 指令生成文件名字  

-o 文件名  


## 常用指令  

### -I 指定头文件  

当头文件与源码不在同一目录下时，源文件包含自定义的头文件会找不到，编译时可以指定  

gcc -I 头文件目录位置 hello.c -o hello  
-I参数放在最后也可以且大写I与后面目录直接可以不加空格(但一般会加)    

###  -c  只做 预处理、编译、汇编  

同理，
gcc hello.c -E hello.i  只做预处理  
gcc hello.c -S hello.s  只做预处理、编译两个步骤  
前两个很少用

gcc hello.c -c  hello.o **做了预处理、编译、汇编   得到的.o文件是一个二进制文件**  

### -g 编译时添加调试文件/语句  

加上该参数，编译的程序可以调试
gcc hello.c -o hello1
gcc hello.c -o hello2 -g  

ls -l （ll）查看，两个文件大小不一样  hello2要大  

#### gdb调试  

**hello2才可使用gdb进行调试，否则无法使用gdb进行调试**    


### -On  n=0~3  编译优化  n越大优化得越多  

默认选择的优化级是2级 -O2    

如程序段如下,while循环体不可能被执行，因此不需要里面内容进行预处理，编译等操作  
```cpp
while(0) {
   xxxxxx
   xxx
   x
   xx
}
```
* -O0和某些嵌入式编程有关，如代码段,可能表示某引脚高低电平循环，灯亮灭交替，如果使用默认的-O2就会优化成只留最后的a = 1  此时可以指定-O0
```c
int a = 0;
a = 1;
a = 0;
a = 1;
a = 0;
a = 1;
a = 0;
a = 1;
```


### -Wall  显示所有警告信息  

加了以后，不管什么级别的警告都会显示  如定义了一个变量但未使用  

### -D 向程序动态注册一个宏  

**一般作为开关使用**，例如在程序中定义打印一些调试信息等，我们如果没有某个宏就不输出，有才输出  因此一般调试信息只在程序开发时使用，后面就需要删除或者注释掉，但是如果调试信息多了的话，删除或注释起来就很费劲； **可以在写调试信息时就加上“开关”，将来需要调试信息就打开，不需要时就关闭**  

例子,表示，如果定义了宏 XXX,则执行宏定义PI   但是这里XXX没有宏定义，因此后面如果使用PI会报错  如果使用，可以在#ifdef XXX前添加 #define XXX xxx  

也可以在编译时，向hello.c注册一个宏
gcc hello.c -D XXX

```c
#include "hello.h"  
#ifdef XXX  
#define PI 3.14  
#endif
```







