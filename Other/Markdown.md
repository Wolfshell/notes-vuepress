# Markdown


[[toc]]




## flag

> 该文件用来测试和展示书写README的各种markdown语法。
>
> GitHub的markdown语法在标准的markdown语法基础上做了扩充，称之为`GitHub Flavored Markdown`。简称`GFM`，GFM在GitHub上有广泛应用，
> 除了README文件外，issues和wiki均支持markdown语法。


* [https://github.com/commonmark](https://github.com/commonmark)

* [GitHub Flavored Markdown基本撰写和格式语法](https://help.github.com/cn/github/writing-on-github/basic-writing-and-formatting-syntax)

* [https://segmentfault.com/markdown](https://segmentfault.com/markdown)


## 横线

```vim
***
```

```vim
---
```

```vim
___
```



## 标题

`#` 一级标题  
`##` 二级标题  
`###` 三级标题  
`####` 四级标题  
`#####` 五级标题  
`######` 六级标题  


## 文本

### 普通文本

这是一段普通的文本

### 单行文本

> 在一行开头加入1个Tab或者4个空格。

    Hello,大家好，我是果冻虾仁。


### 文本块

**语法1**

> 在连续几行的文本开头加入1个Tab或者4个空格。

    欢迎到访
    很高兴见到您
    祝您，早上好，中午好，下午好，晚安

**语法2**

> 使用一对各三个的反引号

> 该语法也可以实现代码高亮，见[代码高亮](#代码高亮)

```
欢迎到访
我是C++码农
你可以在知乎、CSDN、简书搜索【果冻虾仁】找到我
```

### 文字高亮

> 文字高亮功能能使行内部分文字高亮，使用一对反引号。

> 也适合做一篇文章的tag

```
`linux` `网络编程` `socket` `epoll` 
```

> 效果：`linux` `网络编程` `socket` `epoll`


**换行**

> 直接回车不能换行，可以在上一行文本后面补两个空格，这样下一行的文本就换行了。
>
> 或者就是在两行文本直接加一个空行。也能实现换行效果，不过这个行间距有点大。

## 字体

- 斜体、粗体、删除线

|语法|效果|
|----|-----|
|`*斜体1*`|*斜体1*|
|`_斜体2_`| _斜体2_|
|`**粗体1**`|**粗体1**|
|`__粗体2__`|__粗体2__|
|`这是一个 ~~删除线~~`|这是一个 ~~删除线~~|
|`***斜粗体1***`|***斜粗体1***|
|`___斜粗体2___`|___斜粗体2___|
|`***~~斜粗体删除线1~~***`|***~~斜粗体删除线1~~***|
|`~~***斜粗体删除线2***~~`|~~***斜粗体删除线2***~~|

> 斜体、粗体、删除线可混合使用

## 图片

- 基本格式：`![alt](URL title)`

- alt和title即对应HTML中的alt和title属性（都可省略）
    - alt表示图片显示失败时的替换文本
    - title表示鼠标悬停在图片时的显示文本（注意这里要加引号）

> URL即图片的url地址，如果引用本仓库中的图片，直接使用**相对路径**就可了，

> 如果引用其他github仓库中的图片要注意格式，即：`仓库地址/raw/分支名/图片路径`，如

```
https://github.com/guodongxiaren/ImageCache/raw/master/Logo/foryou.gif
```

|语法|效果|
|---|----|
|`![baidu](http://www.baidu.com/img/bdlogo.gif "百度logo")`|![baidu](http://www.baidu.com/img/bdlogo.gif "百度logo")|
|`![][foryou]`|![][foryou]|

> 注意例2的写法使用了**URL标识符**的形式，在[链接](#链接)一节有介绍。

- 在文末有foryou的定义

```
[foryou]:https://github.com/guodongxiaren/ImageCache/raw/master/Logo/foryou.gif
```

## 链接

### 链接外部URL

|#|语法|效果|
|---|----|-----|
|1|`[我的博客](https://www.bajins.com "悬停显示")`|[我的博客](https://www.bajins.com "悬停显示")|
|2|`[我的知乎][zhihu] `|[我的知乎][zhihu] |

**语法2由两部分组成**
- 第一部分使用两个中括号，[ ]里的标识符（本例中zhihu），可以是数字，字母等的组合，标识符上下对应就行了（**姑且称之为URL标识符**）
- 第二部分标记实际URL。

>使用URL标识符能达到复用的目的，一般把全文所有的URL标识符统一放在文章末尾，这样看起来比较干净。
>>URL标识符是我起的名字，不知道是否准确。囧。。

### 链接本仓库里的URL

|语法|效果|
|----|-----|
|`[我的简介](/example/profile.md)`|[我的简介](/example/profile.md)|
|`[Book](./Book)`|[Book](/Book)|

### 图片链接

> 给图片加链接的本质是混合图片显示语法和普通的链接语法。普通的链接中[ ]内部是链接要显示的文本，而图片链接[ ]里面则是要显示的图片。  
> 直接混合两种语法当然可以，但是十分啰嗦，为此我们可以使用URL标识符的形式。

|#|语法|效果|
|---|----|:---:|
|1|`[![weibo-logo]](http://weibo.com/linpiaochen)`|[![weibo-logo]](http://weibo.com/linpiaochen)|
|2|`[![](/img/zhihu.png "我的知乎，欢迎关注")][zhihu]`|[![](/img/zhihu.png "我的知乎，欢迎关注")][zhihu]|
|3|`[![csdn-logo]][csdn]`|[![csdn-logo]][csdn]|

> 因为图片本身和链接本身都支持URL标识符的形式，所以图片链接也可以很简洁（见例3）。  

> 注意，此时鼠标悬停时显示的文字是图片的title，而非链接本身的title了。

> 本文URL标识符都放置于文末

### 锚点

> 其实呢，每一个标题都是一个锚点，和HTML的锚点（`#`）类似，比如我们 

|语法|效果|
|---|---|
|`[回到顶部](#readme)`|[回到顶部](#readme)|

> 不过要注意，标题中的英文字母都被转化为**小写字母**了。

> 以前GitHub对中文支持的不好，所以中文标题不能正确识别为锚点，但是现在已经没问题啦！

- 注意

> 标题中不能带有空格

> 标题中有除字体或字母数字以外的符号时应该在锚点中直接去除后方可跳转

```diff
* [获得当前日期+时间`date+time`函数](#获得当前日期时间datetime函数)

## 获得当前日期+时间`date+time`函数
```
```diff
* [获得当前日期+时间（date+time）函数](#获得当前日期时间datetime函数)

## 获得当前日期+时间（date+time）函数
```


## 列表

### 无序列表

* 昵称：果冻虾仁
- 别名：隔壁老王
+ 英文名：Jelly

### 多级无序列表

* 编程语言
    * 脚本语言
        * Python

### 有序列表

**一般效果**

> 就是在数字后面加一个点，再加一个空格。不过看起来起来可能不够明显。    

- 面向对象的三个基本特征：

1. 封装
2. 继承
3. 多态


**多级有序列表**

> 和无序列表一样，有序列表也有多级结构 

1. 这是一级的有序列表，数字1还是1
   1. 这是二级的有序列表，阿拉伯数字在显示的时候变成了罗马数字
      1. 这是三级的有序列表，数字在显示的时候变成了英文字母
	 

### 复选框列表

- [x] 需求分析
- [x] 系统设计
- [x] 详细设计
- [ ] 编码
- [ ] 测试
- [ ] 交付

> 您可以使用这个功能来标注某个项目各项任务的完成情况。

> Tip:
>> 在GitHub的**issue**中使用该语法是可以实时点击复选框来勾选或解除勾选的，而无需修改issue原文。

## 块引用

### 常用于引用文本

- 文本摘自《深入理解计算机系统》P27

　令人吃惊的是，在哪种字节顺序是合适的这个问题上，人们表现得非常情绪化。
实际上术语“little endian”（小端）和“big endian”（大端）出自Jonathan Swift的《格利佛游记》一书，
其中交战的两个派别无法就应该从哪一端打开一个半熟的鸡蛋达成一致。因此，争论沦为关于社会政治的争论。
只要选择了一种规则并且始终如一的坚持，其实对于哪种字节排序的选择都是任意的。

> **“端”（endian）的起源**  
以下是Jonathan Swift在1726年关于大小端之争历史的描述：  
“……下面我要告诉你的是，Lilliput和Blefuscu这两大强国在过去36个月里一直在苦战。
战争开始是由于以下的原因：我们大家都认为，吃鸡蛋前，原始的方法是打破鸡蛋较大的一端，
可是当今的皇帝的祖父小时候吃鸡蛋，一次按古法打鸡蛋时碰巧将一个手指弄破了，因此他的父亲，
当时的皇帝，就下了一道敕令，命令全体臣民吃鸡蛋时打破较小的一端，违令者重罚。”

### 块引用有多级结构

> 数据结构
>> 树
>>> 二叉树
>>>> 平衡二叉树
>>>>> 满二叉树

## 代码高亮

> 在三个反引号后面加上编程语言的名字，另起一行开始写代码，最后一行再加上三个反引号。

```Java
public static void main(String[]args){} //Java
```

```c
int main(int argc, char *argv[]) //C
```

```Bash
echo "hello GitHub" #Bash
```

```javascript
document.getElementById("myH1").innerHTML="Welcome to my Homepage"; //javascipt
```

```cpp
string &operator+(const string& A,const string& B) //cpp
```

## 表格

| 表头1  | 表头2|
| ---------- | -----------|
| 表格单元   | 表格单元   |
| 表格单元   | 表格单元   |

### 对齐

> 表格可以指定对齐方式

| 左对齐 | 居中  | 右对齐 |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |

### 混合其他语法

> 表格单元中的内容可以和其他大多数GFM语法配合使用

- 使用普通文本的删除线，斜体等效果

| 名字 | 描述 |
| ------------- | ----------- |
| Help      | ~~Display the~~ help window.|
| Close     | _Closes_ a window     |

- 表格中嵌入图片（链接）

> 其实前面介绍图片显示、图片链接的时候为了清晰就是放在在表格中显示的。

| 图片 | 描述 |
| ---- | ---- |
|![baidu][baidu-logo] | 百度|


## 表情

> Github的Markdown语法支持添加emoji表情，输入不同的符号码（两个冒号包围的字符）可以显示出不同的表情。

> 比如`:blush:`，可以显示:blush:。

> 具体每一个表情的符号码，可以查询GitHub的官方网页[http://www.emoji-cheat-sheet.com](http://www.emoji-cheat-sheet.com)。


## diff语法

> 版本控制的系统中都少不了`diff`的功能，即展示一个文件内容的增加与删除。

> GFM中可以显示的展示diff效果。使用绿色表示新增，红色表示删除。

> 其语法与代码高亮类似，只是在三个反引号后面写`diff`，并且其内容中，以 `+ `开头表示新增，`- `开头表示删除。

- 效果如下：

```diff
+ 鸟宿池边树，僧敲月下门
- 鸟宿池边树，僧推月下门
```


## 行内HTML元素

> 目前只支持部分段内HTML元素效果，包括 `<kdb></kdb>`、`<b></b>`、`<i></i>`、`<em></em>`、`<sup></sup>`、`<sub></sub>`、
> `<br/>`、`<details><summary></summary></details>`



## 工具

### 微信公众号排版

* [md.aclickall.com](https://md.aclickall.com)

* [https://github.com/doocs/md](https://github.com/doocs/md)

* [https://github.com/mdnice/markdown-nice](https://github.com/mdnice/markdown-nice)

* [https://github.com/lyricat/wechat-format](https://github.com/lyricat/wechat-format)

* [https://github.com/zkqiang/wechat-mdeditor](https://github.com/zkqiang/wechat-mdeditor)

* [https://github.com/dyc87112/online-markdown](https://github.com/dyc87112/online-markdown)

* [https://github.com/didadi599/wechat-markdown-editor](https://github.com/didadi599/wechat-markdown-editor)

* [wechat-editor](https://so-easy.cc/wechat-editor)

* [https://knb.im/mp](https://knb.im/mp)

* [https://github.com/ufologist/wechat-mp-article](https://github.com/ufologist/wechat-mp-article)

---

* [mp-transform-public](https://github.com/ZhuPeng/mp-transform-public)



### 表格生成

> `HTML`表格转`Excel`可以直接在`office Excel`中点击 `数据` -> `自网站` -> `URL` 然后进行操作

* [tableconvert](https://tableconvert.com)

* [https://github.com/stevecat/table-magic](https://github.com/stevecat/table-magic)

* [markdown_tables](http://www.tablesgenerator.com/markdown_tables)

* [https://github.com/domchristie/turndown](https://github.com/domchristie/turndown)



### 生成文件结构树

* [mddir](https://github.com/JohnByrneRepo/mddir)

* [treer](https://github.com/derycktse/treer)


### 生成标题目录树

> `TOC` [https://en.wikipedia.org/wiki/Table_of_contents](https://en.wikipedia.org/wiki/Table_of_contents)


* [tocdown](https://dohliam.github.io/tocdown) [https://github.com/dohliam/tocdown](https://github.com/dohliam/tocdown)

* [markdown-toc-generate](https://magnetikonline.github.io/markdown-toc-generate)
[源码](https://github.com/magnetikonline/markdown-toc-generate)

* [tocenize](https://github.com/nochso/tocenize)

* [doctoc](https://github.com/thlorenz/doctoc)

* [MDToc](https://github.com/dkyaorui/MDToc)

* [markdown-it-toc-and-anchor](https://github.com/medfreeman/markdown-it-toc-and-anchor)

* [gulp-format-md](https://github.com/jonschlinkert/gulp-format-md)


### 转换器

* [https://github.com/domchristie/turndown](https://github.com/domchristie/turndown)

* [https://github.com/markdown-it/markdown-it](https://github.com/markdown-it/markdown-it)


### 在线版客户端

* [https://github.com/mdnice/markdown-resume](https://github.com/mdnice/markdown-resume)

* [xkeditor](https://github.com/syfxlin/xkeditor)

> XK-Editor | 一个支持富文本和Markdown的编辑器

* [editor.md](https://github.com/pandao/editor.md)

> Editor.md 是一款开源的、可嵌入的 Markdown 在线编辑器（组件），基于 CodeMirror、jQuery 和 Marked 构建。

* [remarkable](https://github.com/jonschlinkert/remarkable)

* [markdown](https://tool.lu/markdown)

* [dillinger](http://dillinger.io)

> 漂亮强大，支持md, html, pdf 文件导出。支持dropbox, onedrive，google drive, github. 来自国外，可能不够稳定。

* [StackEdit](https://stackedit.io)

* [MaHua](http://mahua.jser.me)

* [马克飞象](https://maxiang.io)

* [Markdown Plus](http://mdp.tylingsoft.com)

* [小书匠](http://markdown.xiaoshujiang.com)

* [Cmd Markdown](https://www.zybuluo.com/mdeditor)


### 本地版客户端

* [typora](https://www.typora.io)

* [MarkPad](https://github.com/Code52/DownmarkerWPF)

> MarkPad 是款开源的 Markdown 编辑器，与 Window 8 风格和谐友好的界面，可以直接在你的博客或者 GitHub 中打开、保存文档，
> 直接将图片粘贴到 Markdown 文档中。

* [Haroopad](http://pad.haroopress.com/user.html)

* [https://github.com/MacDownApp/macdown](https://github.com/MacDownApp/macdown)


### 其他

* [github-corners](https://github.com/tholman/github-corners)

> GitHub图标



