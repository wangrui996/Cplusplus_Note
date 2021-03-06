# UDP协议  

UDP : User Datagram Protocol 用户数据报协议[RFC 768]

* 基于IP协议  
    * 复用/分用  
    * 简单的错误校验  因为不能保证链路层都有错误检验机制，路由器端也可能出错，出于一种端到端的原则，需要在传输层添加这种机制  
  
 * “Best effort“ 服务，UDP段可能发生  
    * 丢失
    * 非按序到达 
    * 因为UDP简单的错误检验，不会做错误恢复，它相当于把IP层暴露给了应用层，IP层就是一种Best effort服务因此UDP也是，因为IP层可能会发生丢失，非按序到达，所以UDP也有

* 无连接  
    * UDP发送方和接收方之间不需要握手
    * 每个UDP段的处理独立于其他段  

## UDP的优点  

* 无需建立连接(减少延迟)  
* 实现简单：无需维护连接状态  
* 头部开销少 (UDP头部 8个字节   TCP头部20个字节)  
* 没有拥塞控制：应用可更好地控制发送时间和速率   TCP有拥塞控制，会根据实际情况调整速率，不会完全按应用设定的速率来  


## 应用  

* 流媒体的应用  
    * 容忍丢失
    * 速率敏感

* DNS 
* SNMP  

## UDP上实现可靠数据传输  

* 在应用层增加可靠性机制 
* 应用特定的错误恢复机制  


## UDP报文段格式  

![image](https://user-images.githubusercontent.com/58176267/158095381-51c60936-f17a-41b6-b3de-4bdf9505c90b.png)

源端口号 目的端口号 各16字节  
length：UDP段的长度  checksum: 校验和  
应用数据


### UDP校验和 checksum  

目的： 检测UDP段在传输中是否发生错误(如位翻转)  

#### 实现  

* 发送方  
   * 将段的内容视为16-bit整数  
   * 检验和计算：计算所有整数的和，将得到的值按位求反，得到校验和    注意16bit二进制相加时，最高位的进位要加在和上 具体看后面例子  
   * 发送方将检验和放入 UDP报文段的checksum字段  
 
* 接收方  
   * 计算所收到段的校验和
   * 将其与校验和字段进行对比  
      * 不相等 ： 检测出错误
      * 相等 ： 没有检测出错误(但可能有错误)  
* 注意：接收方计算段的检验和后和段中的checksum字段的数据进行比较，相等的话，也可能出现错误，比如有两个位发生了反转  

 
##### 计算检验和例子  

下面例子中，最高位进位了1，然后1要加在后面得到最终的sum，然后对sum按位取反  



![image](https://user-images.githubusercontent.com/58176267/158096413-ab854908-ec3b-4c63-8ef2-6cf8409bdb94.png)

