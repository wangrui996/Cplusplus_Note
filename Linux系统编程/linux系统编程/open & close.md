# open & close 函数 

使用linux程序员手册 即man手册查看函数介绍  


# open  

man 2 open 查看  

open函数 ：打开或创建一个文件/设备  

linux提供的函数原型有两种  

```c
int open(const char *pathname, int flags);
int open(const char *pathname, int flags, mode_t mode);
```


## 第一个函数原型  

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

## 第二个函数原型  

```c
int open(const char *pathname, int flags, mode_t mode);
```

* mode_t mode ： mode_t是一个8进制整形（以0开头） 如 0664  会给文件加权限  文件在创建的时候可能需要

* 创建文件时。指定文件访问权限  

### flag参数  

完整的flag参数在手册中也给出了，包括  
* O_APPEND 追加  
* O_CREAT 创建
* O_EXCL 是否存在  
* O_TRUNC 截断  
* O_NONBLOCK 非阻塞  



# close  

关闭一个文件描述符  

函数原型  

```c 
int close(int fd);
```
参数  
* fd：文件描述符

返回值  

* 0 成功
* -1 失败  


### open函数 demo  

#### 1.打开一个已有文件

```c
#include <unistd.h>  //包含了open的两个函数原型  
#include <fcntl.h>   //file control  O_RDONLY等定义  
#include <stdio.h>


int main(int argc, char** argv) 
{
	int fd;
	fd = open("./txt/text.txt", O_RDONLY);
	printf("fd = %d\n", fd);
	
	close(fd);
	
	return 0;
}
```
输出
```shell
wr@wr:~/linux系统编程/open$ gcc open.c -o open
wr@wr:~/linux系统编程/open$ ls
open  open.c  txt
wr@wr:~/linux系统编程/open$ ./open 
fd = 3
```

#### 2.创建一个文件   需指定权限  

```c
#include <unistd.h>  //包含了open的两个函数原型  
#include <fcntl.h>   //file control  O_RDONLY等定义  
#include <stdio.h>


int main(int argc, char** argv) 
{
	int fd;
	//创建一个文件并以只读方式打开
	//权限是 rw-r--r-- 用户，同组用户和其他组权限分别为 可读写-只读-只读  
	fd = open("./txt/text2.txt", O_RDONLY | O_CREAT, 0664); 
	printf("fd = %d\n", fd);
	
	close(fd);
	
	return 0;
}
```
执行  
```shell
wr@wr:~/linux系统编程/open$ gcc open.c -o open
wr@wr:~/linux系统编程/open$ ./open 
fd = 3
```  

查看文件  
```shell
wr@wr:~/linux系统编程/open/txt$ ls -l
总用量 4
-rw-r--r-- 1 wr wr  0 3月  18 15:04 text2.txt
-rw-r--r-- 1 wr wr 36 3月  18 14:50 text.txt
```

#### 3.以追加方式打开文件  

该方式打开一个已有内容的文件后，再向里写不会清空原有内容  


#### 4.O_TRUNC 截断文件  把文件长度截断为0，相当于清零  

```c
#include <unistd.h>  //包含了open的两个函数原型  
#include <fcntl.h>   //file control  O_RDONLY等定义  
#include <stdio.h>

int main(int argc, char** argv) 
{
	int fd;
	//如果./txt/text.txt存在，以只读方式打开并将其清空    如果不存在，创建，并且权限为644
	fd = open("./txt/text.txt", O_RDONLY | O_CREAT | O_TRUNC, 0644); 
	printf("fd = %d\n", fd);
	
	close(fd);
	
	return 0;
}
```

执行
```shell
wr@wr:~/linux系统编程/open$ gcc open.c -o open
wr@wr:~/linux系统编程/open$ ./open 
fd = 3
```

查看文件属性及内容  

```shell
wr@wr:~/linux系统编程/open/txt$ ll
总用量 8
drwxr-xr-x 2 wr wr 4096 3月  18 15:04 ./
drwxr-xr-x 3 wr wr 4096 3月  18 15:13 ../
-rw-r--r-- 1 wr wr    0 3月  18 15:04 text2.txt
-rw-r--r-- 1 wr wr    0 3月  18 15:13 text.txt
wr@wr:~/linux系统编程/open/txt$ cat text.txt
wr@wr:~/linux系统编程/open/txt$ 
```  














