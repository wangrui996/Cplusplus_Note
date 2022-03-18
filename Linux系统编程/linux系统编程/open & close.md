# open & close 函数 

使用linux程序员手册 即man手册查看函数介绍  


## open  

man 2 open 查看  

open函数 ：打开或创建一个文件/设备  

linux提供的函数原型有两种  

```c
int open(const char *pathname, int flags);
int open(const char *pathname, int flags, mode_t mode);
```


### 第一个函数原型  

```c
int open(const char *pathname, int flags);
```

### 参数  

* pathname ： 要打开的文件路径  
* flags参数 ：查看手册发现有以下三种参数  O_RDONLY, O_WRONLY, or O_RDWR

* **返回值： file descriptor  文件描述符  实际上是一个整数** or -1 (错误就返回-1并设置。。。。)

```shell
RETURN VALUE
       open(), openat(), and creat() return the new file descriptor, or -1  if
       an error occurred (in which case, errno is set appropriately).

```

### 第二个函数原型  

```c
int open(const char *pathname, int flags, mode_t mode);
```

* mode_t mode ： mode_t是一个8进制整形 如 0 664  会给文件加权限  文件在创建的时候可能需要

* 创建文件时。指定文件访问权限  

### flag参数  

完整的flag参数在手册中也给出了，包括  
* O_APPEND 追加  
* O_CREAT 创建
* O_EXCL 是否存在  
* O_TRUNC 截断  
* O_NONBLOCK 非阻塞  

### open函数 demo  






