# Markdown 语法

## 标题 Header

Input:

```
# H1
## H2
### H3
#### H4
##### H5
###### H6

Alt-H1
====== // H1

Alt-H2
------ // H2
```

Output:

# H1
## H2
### H3
#### H4
##### H5
###### H6

H1 下划线写法
=

H2 下划线写法
-

## 文字

Input:

```
**加粗**
__加粗__
*斜体*
_斜体_
**_斜体+加粗_**
~~删除线~~
```

Output:
**加粗**
__加粗__
*斜体*
_斜体_
**_斜体+加粗_**
~~删除线~~

## 列表

有序列表：数字加点
无序列表：*, +, -加空格
嵌套：上下级加3个空格

Input:

```
1. 有序列表项1
2. 有序列表项2
··* 无序列表项*
··- 无序列表项-
··+ 无序列表项+
··* 上级1
·····* 下级1.1
```

(··表示2个空格，表示换行)

Output:

1. 有序列表项1
2. 有序列表项2
  * 无序列表项*
  - 无序列表项-
  + 无序列表项+
  * 上级1
     * 下级1.1

## 链接

Input:
```
[超链接名](超链接地址)
[超链接名](超链接地址 "超链接title")
[引用链接1](引用1)
[引用相对链接](../frontend-tool-relearn-notes/easy_ladder.md)
[引用数字对应链接][1]
直接添加链接地址[引用2]
直接将url加在<http://www.baidu.com>中

[引用1]: https://www.mozilla.org
[1]: http://slashdot.org
[引用2]: http://www.reddit.com
```

Output:
[超链接名](http://www.baidu.com)
[超链接名](http://www.baidu.com "title")
[引用链接1][引用1]
[引用相对链接](../frontend-tool-relearn-notes/easy_ladder.md)
[引用数字对应链接][1]
直接添加链接地址[引用2]
直接将url加在<http://www.baidu.com>中

[引用1]: https://www.mozilla.org
[1]: http://slashdot.org
[引用2]: http://www.reddit.com

## 图片

```
内联模式:
![图片描述文字](https://github.com/cqy0000/frontend-tool-relearn-notes/blob/master/images/v2ray.png "Logo Title Text 1")

引用模式:
![图片描述文字][logo]

[logo]: https://github.com/cqy0000/frontend-tool-relearn-notes/blob/master/images/v2ray.png
```

内联模式:
![图片描述文字](https://github.com/cqy0000/frontend-tool-relearn-notes/blob/master/images/v2ray.png "Logo Title Text 1")

引用模式:
![图片描述文字][logo]

[logo]: https://github.com/cqy0000/frontend-tool-relearn-notes/blob/master/images/v2ray.png

## 代码和语法高亮

```
内联代码:
`code`

多行代码:
·```JavaScript
let a = 10;
·```
```

（此处多一个·，防止转义）

内联代码:
`code`

多行代码:

```JavaScript
let a = 10;
```

## 表格

```
表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容
```

表头|表头|表头
---|:--:|---:
靠左边|居中居中居中|靠右边
靠左|居中居中居中|靠右

## 引用

```
> 引用文字
> 引用文字
>> 嵌套引用
```
> 引用文字

> 引用文字
>> 嵌套引用

## 嵌入HTML代码

```
<h1>标题1<h1>
<div>div<span>span</span></div>
```

<h5>标题1</h5>
<div>div <span>span</span></div>

## 分割线

3个及以上的*, -, _

```
***
---
___
```

***
---
___

## 定义list

```
term
: definition
```

term
: definition

## 任务list

```
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media
```

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media