# Email应用  

## Email应用的构成组件  

* 邮件客户端  
    * 读写Email消息 
    * 与服务器交互，收，发Email消息  
    * 典型的邮件客户端Outlook，Foxmail
    * Web客户端(使用Web Email时)   

* 邮件服务器/Mail Server  
    * 邮箱：存储发给该用户的Email  
    * 消息队列：存储等待发送的Email  
    
* **SMTP协议(Simple Mail Transfer Protocol)  简单邮件传输协议**  
    * 邮件服务器之间传递消息所使用的的协议  
    * 客户端：发送消息的服务器  
    * 服务器：接收消息的服务器  

## 存在邮件服务器的好处  

* 如果没有邮件服务器，我们的PC机或其它网络设备无法保证24小时接入网络，对方也是，因此无法保证对方发送的时候我们刚好可以接收，反过来也是  


## SMTP协议  

* 使用TCP进行Email消息的可靠传输
* 端口 25
* 传输的三个阶段  
    * 握手
    * 消息的传输  
    * 关闭
* 命令/响应的交互模式  (HTTP是请求响应模式)  
    * 命令(command) :ASCII文本  
    * 响应(response)：状态代码和语句  
   
* Email消息只能包含7位ASCII码
