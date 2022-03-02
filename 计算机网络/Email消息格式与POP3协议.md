# Email消息格式与POP3协议  


## SMTP协议  

### 文本消息格式标准  RFC822  

* 头部行(header)  
    * To
    * From
    * Subject
与SMTP命令不同  

* 消息体(body)    
    * 消息本身  
    * 只能是ASCII码  

### MIME：多媒体邮件扩展  RFC2045,2056  

* 通过在邮件头部增加额外的行以声明MIME的内容类型  

![image](https://user-images.githubusercontent.com/58176267/156285864-59c5ce1c-9929-4cee-83fa-b588ff806a85.png)
