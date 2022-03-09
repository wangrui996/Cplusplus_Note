# CPU管理总结  


## 实现在屏幕上交替打印字母A和B

1.用户代码  
![image](https://user-images.githubusercontent.com/58176267/157414749-293d8cb3-3e6b-4655-a49b-7393633c9de0.png)  

![image](https://user-images.githubusercontent.com/58176267/157414630-131b52a2-f49c-4736-86b8-4cbc9b9ce1b9.png)  

用户代码的汇编代码如上，将中断调用号__NR_fork赋值给eax 并调用系统中断int 0x80  中断处理中创建子进程，然后会将子进程TSS中的eax置为0，接下来将物理寄存器eax赋值给res，如果子进程创建成功，并且父进程系统调用中经过阻塞后切换到了子进程(eax = TSS->eax)，此时物理寄存器eax为0，如果没有切换到子进程，是父进程系统调用结束后返回(前面讲过，切换到子进程，子进程一开始也是执行int 0x80后面的代码因为我们
