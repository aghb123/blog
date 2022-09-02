---
title: MarkDown基础
date: 2022-09-03
---

# MarkDown基础

## 快捷键

| 快捷键             | 作用                    |
| ------------------ | ----------------------- |
| Ctrl + 1/2/3/4/5/6 | 创建1到6级标题          |
| Ctrl + Shift + K   | 创建代码块              |
| Ctrl + Shift + M   | 创建数学块              |
| Ctrl + K           | 创建链接                |
| Ctrl + Shift + I   | 添加图片                |
| Ctrl + /           | 源代码模式              |
| ctrl + shift + L   | 展开/收起侧边栏(Typora) |



## 标题

标题使用#加内容书写，注意#后面要加空格，#的数量决定标题的级别

#  标题1

## 标题2

### 标题3



## 文字

### 删除线

~~文字~~

`~~文字~~`

### 斜体

*文字*

`*文字*`

### 加粗

**文字**

`**文字**`

### 斜体+加粗

***文字***

`***文字***`

### 下划线

HTML语法(快捷键ctrl+u)

<u>文字</u>

`<u>文字</u>`

### 高亮（需勾选扩展语法，去选严格模式）

==1111==

`==1111==`

### 下标（需勾选扩展语法）

水 H~2~O

`H~2~O`

### 上标（需勾选扩展语法）

面积m^2^

`m^2^`

### 表情符号

Emoji支持表情符号，你可以用系统默认的Emoji符号（无法支持Windows用户）。也可以用图片的表情，输入：会出现智能提示

:smile:`:smile:`

:cow:`:cow:`​

:100:`:100:`

:alarm_clock:



### 表格

使用`|`来分割不同的单元格，使用`-`来分隔表头和其他行

```
name | price
--- | ---
fried chicken | 19
cola|5
```

> 为了使MarkDown更清晰，`|`和`-`两侧需要至少有一个空格（最左侧和最右侧的`|`外就不需要了）。

| name          | price |
| ------------- | ----- |
| fried chicken | 19    |
| cola          | 5     |

为了美观，可以使用空格对齐不同行的单元格，并在左右两侧都使用`|`来标记单元格边界，在表头下方的分隔线标记中加入`:`，即可标记下方单元格内容的对齐方式：

```markdown
| name       | price |
| :--------- |:---:|
| fried chicken | 19 |
| cola | 32|
单个:在左边为左对齐，在右边为右对齐；两端都有:为居中
```

| name          | price |
| :--------- | :---: |
| fried chicken |  19   |
| cola          |  32   |

### 引用

```markdown
>"后悔创业"
```

> "后悔创业"

```
>也可以在引用中
>>使用嵌套的引用
```

>也可以在引用中
>
>>使用嵌套的引用

### 列表

#### 无序列表--符号 空格

```
* 可以使用`*`作为标记
+ 也可以使用`+`
- 或者`-`
```

* 可以使用`*`作为标记
+ 也可以使用`+`

- 或者`-`

#### 有序列表--数字`.`空格

```
1. 有序列表以数字和`.`开始；
2. 数字的序列并不会影响生成的列表序列；
3. 但仍然推荐按照自然顺序（1.2.3...）编写。
```

1. 有序列表以数字和`.`开始；
3. 数字的序列并不会影响生成的列表序列；
3. 但仍然推荐按照自然顺序（1.2.3...）编写。

### 代码

#### 代码块

```markdown
```语言名称
```

```java
public static void main(String[] args){
}
```

#### 行内代码

```
也可以通过``,插入行内代码（`是`Tab`键上边、数字`1`左侧的那个按键）:
例如`Markdown`
```

`Markdown`

`java`

`C`

##### 转换规则

代码块中的文本（包括Markdown语法）都会显示为原始内容

### 分割线

可以在一行中使用三个或更多的`*`、`-`或`_`来添加分割线（``）:

```markdown
***
-----
____
```

***

----

___

### 跳转

#### 外部跳转--超链接

格式为`[link text](link)`。

```
[帮助文档](https://support.typora.io/Links/#faq)
```

[帮助文档](https://support.typora.io/Links/#faq)

#### 内部跳转--本文件内跳（Typora支持）

格式为`[link text](#要去的目的地--标题)`。

```markdown
[我想跳转](#代码)
```

[我想跳转](#代码)

#### 自动链接

使用`<>`包括的URL或邮箱地址会被自动转换为超链接：

```markdown
<https://www.baidu.com>
<123@email.com>
```

<https:www.bilibili.com>

### 图片

```markdown
![自己起的图片名字](图片地址或者图片本地存储的路径)
```

#### 网上的图片

![friedChicken](../images/MarkDown基础/timg)

#### 本地图片

```markdown
![friedChicken](MarkDown基础.assets\timg.jfif)
在同一个文件夹里（用相对路径）
或者直接拷贝
```

![变形金刚](../images/MarkDown基础/timg.jfif)

### 改变字体和颜色

`<font face="黑体">我是黑体字</font>`

<font face="黑体">我是黑体字</font>



`<font face="微软雅黑">我是微软雅黑</font>`

<font face="微软雅黑">我是微软雅黑</font>



`<font color=red>我是红色</font>`

<font color=red>我是红色</font>



`<font color=#008000>我是绿色</font>`

<font color=#008000>我是绿色</font>



`<font size=5>我是5号大小</font>`

<font size=5>我是5号大小</font>



`<font size=5>**我是加粗5号大小**</font>`

<font size=5>**我是加粗5号大小**</font>



`<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>`

<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>

<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>

