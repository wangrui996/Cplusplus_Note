# grep命令  

根据文件内容检索  

1. grep -r "内容" 路径   
-r 递归搜索

![image](https://user-images.githubusercontent.com/58176267/157048874-45e40acf-5d25-4100-ae6a-7672108e32a0.png)

2. grep -r "内容" 路径 -n  
 
-n 显示行号  

![image](https://user-images.githubusercontent.com/58176267/157049248-556b2218-d44d-4c13-bd17-313fdb3e255d.png)


2.ps命令  

监控后台进程的工作情况  

如果只输入ps，默认只显示可以和当前用户交互的进程  

3.ps aux  

显示所有运行的进程  

4.ps aux | grep xxx  
检索进程内容包含xxx的进程  

下图显示和内核相关的进程
![image](https://user-images.githubusercontent.com/58176267/157050847-8eb20dd7-bca1-4e64-9410-556e545c3908.png)

**注意** 如果使用ps配合grep命令搜索结果只有一条，说明没有搜索到包含xxx内容的进程；因为搜索结果中有一条是搜索命令本身，所以如果有其他进程包含内容xxx，则搜索结果最少有两条  


**这里ps aux的结果是个结果集，可以交给管道|再操作，但是find命令结果也是个结果集，可以配合 | 使用吗？ 需要配合xargs使用** 

5.find … | xargs ls -l 对 find搜索的结果集进行操作  

等价于find … -exec ls -l {} \;   

两者差别：
xargs要借助管道 | 执行  
在于当结果集很大的时候，exec会将所有结果都直接执行    xargs 会对结果集进行分片映射再执行，效率高一点  
但 xargs 也有缺陷，xargs 默认用空格来分割结果集，当文件名有空格的时候，会因为文件名被切割
失效



6. touch abc xyz  

直接执行上面的命令会创建两个文件  但如果想创建一个abc空格xyz的文件呢？  

* 通过转义字符解决    
![image](https://user-images.githubusercontent.com/58176267/157053384-17e71c05-0127-460d-83fb-022e55b27da8.png)


问题
