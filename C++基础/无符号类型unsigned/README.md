
## 无符号类型unsigned  




### 注意事项

#### 1.不能在表达式中混用有符号数和无符号数  

    例如，string类型的s，s.size()返回的是一个无符号数，如果n<0,比较s.size()<n,结果为true  
因为负值n会被转换成一个比较大的无符号数
因此，如果一个表达式中有了size()函数，尽量不要再用int了






