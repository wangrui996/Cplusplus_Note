# open & close 函数 

使用linux程序员手册 即man手册查看函数介绍  


## open  

man 2 open 查看  

open函数 ：打开或创建一个文件/设备  

linux提供的函数原型有两种  

```c
int open(const char *pathname, int flags);
int open(const char *pathname, int flags, mode_t mode);


### 参数  

* pathname ： 要打开的文件路径  
* flags参数 ：查看手册发现有以下三种参数  O_RDONLY, O_WRONLY, or O_RDWR

* **返回值： file descriptor  文件描述符  实际上是一个整数**


