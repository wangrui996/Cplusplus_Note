# CPU管理总结  


## 实现在屏幕上交替打印字母A和B

1.用户代码  
![image](https://user-images.githubusercontent.com/58176267/157414749-293d8cb3-3e6b-4655-a49b-7393633c9de0.png)  

![image](https://user-images.githubusercontent.com/58176267/157414630-131b52a2-f49c-4736-86b8-4cbc9b9ce1b9.png)  

用户代码的汇编代码如上，将中断调用号__NR_fork赋值给eax 并调用系统中断int 0x80  中断处理中创建子进程，然后会将子进程TSS中的eax置为0，接下来将物理寄存器eax赋值给res，如果子进程创建成功，并且父进程系统调用中经过阻塞后切换到了子进程(eax = TSS->eax)，此时物理寄存器eax为0，如果没有切换到子进程，是父进程系统调用结束后返回，此时res(eax)不为0，接下来因为函数体中是printf("A"),所以通过判断res是否为0，如果不为0，执行208也就是父进程，等于0的话，子进程执行printf  

* 前面讲过，切换到子进程，子进程一开始也是执行int 0x80后面的代码,在内核级代码实现的例子中，fork创建子进程，返回来以后，判断如果是子进程，那么会调用一个系统调用exec去执行cmd，exec中会修改子进程的eip为cmd的入口，exec调用结束后子进程会执行cmd   


2. int 0x80就要进入内核，中断处理函数 调用system_call  而system_call调用sys_call_table就会知道是调用sys_fork

![image](https://user-images.githubusercontent.com/58176267/157417445-6c53fe86-fb20-4c29-81e5-9d5feb51cb06.png)

![image](https://user-images.githubusercontent.com/58176267/157417982-4740a42e-6b68-419e-b961-55fd047af127.png)

3.sys_fork调用copy_process 做出一套新的PCB，栈，其中申请PCB内存后一部分做了内核栈，然后将PCB中tss的eip、esp、eax等赋好值(PCB中除了tss，还有该进程的状态等)  
