---
title: 使用Python操作Excel文件
date: 2021-05-15 01:06:26
tags: Python
categories: Learn
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/20211114221504.png
---

一直看到有用python进行自动化办公的视频，但没有去学习过，正好yby找我帮忙处理一个excel文件，借此机会简单学习一下，简单了解之后发现不是很难，都有现成的库来支持。
<!-- more -->

### 用到的库

``` python
import xlrd # 读取excel库：xlrd
import xlwt # 读取excel库：xlwt
```
### 基本操作

#### 打开文件

```python
book = xlrd.open_workbook('input.xls')
# 使用xlrd中的open_workbook方法打开input.xls
sheet1 = book.sheet_by_index(0)
# workbook对象的sheet_by_index方法打开第一个工作表，注意这里的索引值是从0开始的
```
#### 读取文件

在xlrd中读取excel表格中的指定行列有三种方法：

+ row方法

```python
row_1 = sheet1.row(1).value # 读取第二行
pos_1_0  =sheet1.row(1)[0].value # 读取第二行的第一个单元格
```

+ col方法

```python
col_1 = sheet1.col(1).value # 读取第二列
pos_0_1  =sheet1.col(1)[0].value # 读取第二列的第一个单元格
```

+ cell方法

```python
pos_1_0 = sheet1.cell(1, 0).value # 读取第二行的第一个单元格
```

### 简单示例

#### 代码示例

```python
import xlrd
# 打开excel文件
sheet1 = xlrd.open_workbook('123.xls').sheet_by_index(0)
# 打开txt文件
output = open('output.txt', 'w', encoding='utf-8')

for i in range(1, sheet1.nrows):
    if sheet1.row(i)[0].value in [1, 2]:
        output.write(f'{sheet1.row(i)[1].value}:{sheet1.row(i)[2].value}\n')
        output.write(f'答案：{str(sheet1.row(i)[3].value)}\n')
        output.write(f'A: {sheet1.row(i)[4].value}\n')
        output.write(f'B: {sheet1.row(i)[5].value}\n')
        output.write(f'C: {sheet1.row(i)[6].value}\n')
        output.write(f'D: {sheet1.row(i)[7].value}\n')
        output.write(f'E: {sheet1.row(i)[8].value}\n')
    if sheet1.row(i)[0].value == 3:
        output.write(f'{sheet1.row(i)[1].value}:{sheet1.row(i)[2].value}\n')
        output.write(f'答案：{str(sheet1.row(i)[3].value)}\n')
output.close()
```

#### 运行结果

+ 原excel文件

![image-20211112111350937](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211112111350937.png)

+ 输出文件

![image-20211112110443570](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211112110443570.png)