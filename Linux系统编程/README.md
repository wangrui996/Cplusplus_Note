# Linux系统编程  

## Linux终端基本shell命令  

**终端**：一系列输入输出设备的集合  

### 终端常用命令  

pwd：查看当前路径  
cat：读一个文件的内容

### 常用快捷键  

Crtl+a :移动到输入命令最前端  
Crtl+e :移动到输入命令末端  
Crtl+u :直接删除整行命令  

## 类Unix系统目录  

/bin：系统自带的可执行文件，里面有个date，可以用/date执行， 在命令行输入date也可以执行但这是通过shell命令解释器帮忙执行的  
/boot：开机的启动例程　　
/dev: linux系统中有一句话叫**所见皆文件**  
/etc:当前系统用户的配置信息  如passwd存放着用户信息（用户id等）  
/home: 用户主目录  
/lib:库文件  
/media:挂载磁盘相关  
/opt:
/proc:linux系统编程进程相关？  
/root:
/usr: unix software resource  用户安装的软件、第三方库  

