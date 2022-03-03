# QListWidget控件  

## 1.List Weight  

### 添加一行内容 可设置对齐方式  

```cpp
//QListWidget对象 每一行都是一个QListWidgetItem
QListWidgetItem * item = new QListWidgetItem("举头望明月");
ui->listWidget->addItem(item);

//设置水平居中
item->setTextAlignment(Qt::AlignHCenter);
```  
![image](https://user-images.githubusercontent.com/58176267/156514195-2b87dc01-67a6-4823-b11e-c1af54a1a236.png)


### 一次性加入多行  

```cpp
//一次性加多行 QStringList  (List<string> List容器放的是string)
// QStringList----QList<string>
QStringList list;
list << "举头望明月" << "低头思故乡";
ui->listWidget->addItems(list);
```
