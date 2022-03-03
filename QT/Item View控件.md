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

# QTreeWidget  树控件  
下面代码中，设置水平头使用了**匿名对象**的概念  

```cpp
    //树控件 treeWidget
    //设置水平头
    ui->treeWidget->setHeaderLabels(QStringList() << "英雄" << "英雄介绍"); //匿名对象

    //树控件的每一行都叫QTreeWidgetItem
    QTreeWidgetItem * liItem = new QTreeWidgetItem(QStringList() << "力量");
    QTreeWidgetItem * minItem = new QTreeWidgetItem(QStringList() << "敏捷");
    QTreeWidgetItem * zhiItem = new QTreeWidgetItem(QStringList() << "智力");
    //加载顶层的节点(根节点)
    ui->treeWidget->addTopLevelItem(liItem);
    ui->treeWidget->addTopLevelItem(minItem);
    ui->treeWidget->addTopLevelItem(zhiItem);

    //追加子节点 也是 QTreeWidgetItem
    QStringList hero1;
    hero1 << "www" << "1111111111";
    QTreeWidgetItem * l1 = new QTreeWidgetItem(hero1);
    //追加子节点
    liItem->addChild(l1);
    //其他同理
```
