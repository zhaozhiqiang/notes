# Vim operation manual

### 批量插入注释符#

- <C-v> 进入块编辑模式

- 选中需要插入的行

- 按I(大写i)

- 输入#，然后按ESC

### 批量删除注释符#

- <C-v> 进入块编辑模式

- 向下或向上移动光标

- 选中注释部分

- 然后按d

- 就会删除注释符号#

### 使用命令批量添加//

<table>
    <tr><td>在所有行首添加//</td><td>:%s/^/\/\//</td></tr>
    
    <tr><td>在3-7行行首添加//</td><td>:3,7s/^/\/\//g</td></tr>
    
    <tr><td>在3-7行首删除//</td><td>:3,7s/^/\//\///g</td></tr>    
    
    <tr><td>当前光标位置后连续插入10个字符#</td><td>10i#<esc></td></tr> 
    
    <tr><td>当前行末尾位置连续插入10个字符#</td><td>10A#<esc></td></tr> 
    
    <tr><td>当前光标位置往上连续插入10行一个字符#</td><td>10O#<esc></td></tr> 
    
    <tr><td>在10-20行添加//注释</td><td>:10,20s#^#//#g</td></tr> 
    
    <tr><td>在10-20行删除//注释</td><td>:10,20s#^//##g</td></tr> 
    
    <tr><td>在行首插入行号</td><td>:g/^/exec "s/^/".strpart(line(".")." ", 0, 4)</td></tr> 
</table>

### 跳转
- <C-o> 跳转到Cursor的上一个位置

- <C-i> 跳转到Cursor的下一个位置

- g; 跳转到上次修改的位置

- g, 跳转到下一次修改的位置(如果有)

- w(e) 移动光标到下一个单词

- b 移动光标到上一个单词

- 0 移动光标到本行最开头

- ^ 移动光标到本行最开头的字符处，或者数字0

- $ 移动光标到本行结尾处

- H 移动光标到屏幕的首行

- M 移动光标到屏幕的中间一行

- L 移动光标到屏幕的尾行

- gg 移动光标到文档首，或者:1

- nG 直接跳到第n行

- G 跳转到文档尾行

- <C-f> 下一屏，即 Page Down

- <C-b> 上一屏，即 Page Up

### 粘贴

- 进入paste模式            :set paste

- 粘贴内容

- 退出paste模式            :set nopaste 

- 快捷键进入/退出paste模式:
     -键盘映射：
         -:map <F10> :set paste<CR> 键启动paste模式
         -:map <F11> :set nopaste<CR> 取消paste模式
     -粘贴前按F10，粘贴后按F11

### 缩进
- :set noai nosi
- <C-t> insert模式下，当前行增加缩进
- <C-d> insert模式下，当前行减少缩进
- >> normal/visual模式下，当前行增加缩进
- << normal/visual模式下，当前行减少缩进

### 粘贴
- :"+p 粘贴剪切板内容(粘贴代码时推荐使用)
- :"*p 粘贴缓冲区中内容
- :reg 显示所有寄存器内容
- :$ xclip -out -sel clipboard 查看剪切板的内容

### 删除
- dd 删除一行
- dw 删除一个单词
- D 删除从当前光标到光标到行尾的内容
- cc 删除一行并且插入新文本
- d /text 删除当前光标到第一个匹配之间的内容
- 1,$d 删除整个文档
- :%s/^\\(.*\\)\\n\\1/\\1$/ 删除重复行 非贪婪匹配
- :g/^\\s*$/d 删除所有空行
- :g/text/d 删除包含text的行
- :g/^text/d 删除text开头的行
- :g!/^text/d 删除不是text开头的行
- :%norm jdd 隔行删除
- di[ 删除一对 [] 中的所有字符
- di( 删除一对 () 中的所有字符
- di< 删除一对 <> 中的所有字符
- di{ 删除一对 {} 中的所有字符
- dit 删除一对 HTML/XML 的标签内部的所有字符
- di"  di'  di` 删除一对引号字符 (" 或 ' 或 `) 中所有字符

### 列编辑
- <c-v> Ctrl-v 进入VISUAL BLOCK模式，即列编辑
- <c-v> 1h3j 选中两列三行
- <c-v> d 删除选中的列
- <c-v> c <esc> 编辑选中的列，按ESC后生效
- <c-v> A; <esc> 在选中的列后插入;，按ESC后生效
- <c-v> I// <esc> 在选中的列行首插入//，按ESC后生效

### 折叠文本
- zf 创建折叠，默认没动作需要输入后续目标指令
- zf3j 从当前行往下折叠3行
- zf3k 从当前行往上折叠3行
- zfG 从当前行往下折叠到文件末尾
- zfgg 从当前行折叠至行首
- zf10G 从当前行折叠至第10行
- zo 打开折叠
- zc 再次折叠
- v zf 折叠V模式下选中的文本，大写V为行操作
- zf`a 折叠当前光标处到标记a处的文本 (ma就表示在当前光标出做a标记)
- zf% 光标移至'{'时，vim会去匹配'}'，这样'{}'之间的内容就可以折叠起来
- zO 打开所有当前光标下的折叠
- zC 关闭所有当前光标下的折叠
- zM 关闭所有折叠
- zR 打开所有折叠

### 标记
- mx 将当前位置标记为x(x为26个大小写字母中的任一个)
- 'x (单引号)只移到标记所在行的行首
- `x (反引号)跳转到标记所在行列位置
- `` (双反引号)来回切换
- '' (双单引号)来回切换
- :marks 取得所有的标记的列表，vim自身的记录也会包含在内
- :delmarks x 删除指定标记
- :delmarks! 删除所有标记
- visualmark.vim 该插件可实现标记功能，且标记可见

### 文本转换
- Vu 当前行转换为小写
- VU 当前行转换为大写
- g~~ 当前行大小写转换
- vEU 选择性转换为大小，E指从光标处到下一个空白字符处，可连续按
- vE~ 选择性大小写转换，E指从光标处到下一个空白字符处，可连续按
- ggguG 全文小写
- ggVGg? 将全文转换为rot13码(简单加密)，重复执行此命令回复原样
- <C-a> 递增当前光标出的数字
- <C-x> 递减当前光标处的数字
- xp 左右交换光标处两字符的位置
- ddp 上下交换光标处两行的位置

### 复制文件
- :w new_file 另存为一个新文件
- :20,$w new_file 将文件从20行处到结尾另存到一个新文件中
- :.,20w new_file 将光标所在行到第20行另存到一个新文件中
- :20,30w >> new_file 追加当前从20到30行得内容到new_file文件中
- :r other_file 把其它文件的内容插入到光标所在行的下一行
- :100r other_file 把其它文件的内容插入到100行的后面
- :$r other_file 把其它文件的内容插入行尾
- :0r other_file 把其它文件的内容插入行首
- :/parttern/r other_file 把其它文件的内容插入到首个匹配pattern的行
- vim -o file1 file2 打开的两个文件上下窗口分布
- vim -O file1 file2 打开的两个文件左右窗口分布
- :sp new_file 横向分割出一个窗口, 并在该窗口中打开新文件
- :vsp new_file 纵向分割出一个窗口, 并在该窗口中打开新文件
- <C-w> w 在打开的多个窗口中切换
- <C-w> q 关闭多个窗口中当前的窗口
- :bufdo /searchstr/ 在所有打开的(缓冲区)文件中搜索searchstr
-     1.:bufdo %s/pattern/replace/ge
-     2.:update 所有缓冲区文件中替换并生效

### 打开文件
- vim +n file 打开文件，并将光标定位到n行
- vim + file 打开文件，并将光标定位到最后一行
- vim +/pattern file 打开文件，并将光标定位到pattern匹配处
- vim -R file 以只读的方式打开文件
- vim -r 显示已保存的缓冲区的文件
- vim -r file 从已保存的缓冲区恢复文件

### diff
- 可以通过如下两种方式diff：
-     vim -d file1 file2
-     :vert diffsplit file2
- 操作：
- ]c 下一个不同
- [c 上一个不同
- <c-w> w 多个窗口间切换
- <c-w> h 当前窗口移到左边
- <c-w> l 当前窗口移到右边
- <c-w> k 当前窗口移到上边
- <c-w> j 当前窗口移到下边
- dp Diff Put.将当前差异点合并过去到另一个文件
- do Diff Get.将当前差异点从另一个文件合并过来
- :diffupdate 如果没有实时刷新结果
- <esc> u 取消修改结果
- :qa 同时关闭所有比较文件
- :qa! 同时强制关闭所有比较文件
- :wa 同时保存所有比较文件
- :wqa 同时保存并关闭所有比较文件

### 文本串替换
- :s/str1/str2/ 替换当前行中首次出现的str1
- :s/str1/str2/g 替换行当前中所有的str1
- :.,$ s/str1/str2/g 替换当前行到末尾所有的str1
- :%s/str1/str2/g 替换所有的str1



# Vim操作

## 命令格式

vim的命令采用下面的格式。

```
[OPERATOR][NUMBER][MOTION]
```

Operator是动词。

- d – Delete (等同于cut命令)
- c – Change
- y – Yank
- p – Insert last deleted text after cursor (put command)
- r – Replace
- v - 可视化选择

Motion表示操作的上下文。

- w – 直到下一个单词的起始位置前面。
- s - sentence
- p - paragraph
- t - tag
- b - block
- e – 直到当前单词的最后一个位置。
- $ – 直到当前行的最后一个位置。
- ) – 下一个句子的开始。
- ( – 当前句子的开始。
- } – 下一段的开始。
- { – 当前段的开始。
- ] – 下一段部分(section)的开始
- [ – 当前部分(section)的开始
- H – 当前屏幕的第一行
- M – 当前屏幕的中间行
- L – 当前屏幕的最后一行

Count是可选的，表示command和motion的重复次数。

- i - inside
- a - around
- NUM: number (e.g.: 1, 2, 10)

实例

- dw 删除当前光标到单词末尾
- daw 删除当前光标所在单词
- d4w 删除四个词
- dd 删除当前行
- 2dd 删除两行
- cis - Change inside sentence，删除当前句子，并进入insert模式
- yip - yank inside paragrah 复制当前段落

## 撤销命令

- u 撤销上个命令

## 移动光标

- h – Left
- k – Up
- l – Right
- j – Down
- G 移动到文件最后一行
- :123 跳到123行
- gg 移动到文件第一行
- <C-g> 显示当前文件名
- 1<C-g> 显示当前文件完整路径
- % 跳转到当前代码区块的开始/结尾(匹配`()`，`[]`，`{}`)

## 插入文字

- i 当前光标
- s 删除当前光标文字并进入插入模式
- a 光标后面
- A 当前行末尾
- ^i 当前行第一个非空字符
- 0i 当前行首
- o 当前行下方新增一行
- O 当前行上方新增一行

## 删除

- x 删除当前字符，不进入插入模式

## 搜索，替换

- :/cat 搜索光标位置后面
- :?dogs 搜索光标位置前面
- n 移动到下一个匹配
- N 移动到上一个匹配
- :s/cat/dog 只替换下一个
- :s/cat/dog/g 替换所有
- # 向上搜索当前光标所在单词
- * 向下搜索当前光标所在单词

## 执行shell命令

- :!ls -al

## 复制，粘贴，剪切

### 选择文本

- v+光标移动 (按字符选择)高亮选中所要的文本，然后进行各种操作(比如，d表示删除)。
- V (按行选择)
- v+选中的内容+c 更改选中的文字
- <C-v>进入块选择模式

### 复制：y(ank)

- y 用v命令选中文本后，用y进行复制
- yy 复制当前行，然后用p进行复制
- 5yy 复制从当前行开始的5行
- y_ 等同于yy
- Y 等同于yy
- yw 复制当前光标所在位置至单词末尾
- yaw 复制当前光标所在单词
- y$ 从当前位置复制到行尾
- y0 从当前位置复制到行首
- y^ 从当前位置复制到第一个非空白字符
- yG 从当前行复制到文件结束
- y20G 从当前行复制到第20行
- y?bar 复制至上一个出现bar的位置

### 粘贴

- p 在光标位置之后粘贴
- P 在光标位置之前粘贴

### 剪切

- v + 选中的内容 + d 剪切

### 剪贴板

(1) 简单复制和粘贴

vim提供12个剪贴板，它们的名字分别为vim有11个粘贴板，分别是`0`、`1`、`2`、`...`、`9`、`a`、`“`。如果开启了系统剪贴板，则会另外多出两个：`+`和`*`。使用`:reg`命令，可以查看各个粘贴板里的内容。

```bash
:reg
```

在vim中简单用y只是复制到`“`(双引号)粘贴板里，同样用p粘贴的也是这个粘贴板里的内容。

(2)复制和粘贴到指定剪贴板

要将vim的内容复制到某个粘贴板，需要退出编辑模式，进入正常模式后，选择要复制的内容，然后按"Ny完成复制，其中N为粘贴板号(注意是按一下双引号然后按粘贴板号最后按y)，例如要把内容复制到粘贴板a，选中内容后按"ay就可以了。

要将vim某个粘贴板里的内容粘贴进来，需要退出编辑模式，在正常模式按"Np，其中N为粘贴板号。比如，可以按"5p将5号粘贴板里的内容粘贴进来，也可以按"+p将系统全局粘贴板里的内容粘贴进来。

(3)系统剪贴板

Vim支持系统剪贴板，需要打开clipboard功能。使用下面的命令，检查当前版本的Vim，是否支持clipboard。

```bash
$ vim --version
```

如果不支持的话，需要安装图形化界面的vim(即gvim)，或者重新编译vim。

```bash
$ sudo apt-get install gvim
正在读取软件包列表... 完成
正在分析软件包的依赖关系树
正在读取状态信息... 完成
Package gvim is a virtual package provided by:
  vim-gtk 2:7.4.488-7
  vim-gnome 2:7.4.488-7
  vim-athena 2:7.4.488-7
You should explicitly select one to install.

E: Package 'gvim' has no installation candidate

$ sudo apt-get install vim-gnome
```

另一种方法，是安装vim-gui-common。

```bash
$ sudo apt-get install vim-gui-common
```

安装以后，可以用命令行界面，启动gvim，这时可用系统剪贴板。

```bash
$ gvim -v
```

星号(`*`)和加号(`+`)粘贴板是系统粘贴板。在windows系统下， * 和 + 剪贴板是相同的。对于 X11 系统， * 剪贴板存放选中或者高亮的内容， + 剪贴板存放复制或剪贴的内容。打开clipboard选项，可以访问 + 剪贴板；打开xterm_clipboard，可以访问 * 剪贴板。 * 剪贴板的一个作用是，在vim的一个窗口选中的内容，可以在vim的另一个窗口取出。

复制到系统剪贴板
- `"*y`
- `"+y`
- `"+2yy` – 复制两行
- `{Visual}"+y` - copy the selected text into the system clipboard
- `"+y{motion}` - copy the text specified by {motion} into the system clipboard
- `:[range]yank +` - copy the text specified by `[range]` into the system clipboard

剪切到系统剪贴板
- `"+dd` – 剪切一行

从系统剪贴板粘贴到vim
- `"*p`
- `"+p`
- `Shift+Insert`
- `:put +` - Ex command puts contents of system clipboard on a new line
- `<C-r>`+ - From insert mode (or commandline mode)

`"+p`比 Ctrl-v 命令更好，它可以更快更可靠地处理大块文本的粘贴，也能够避免粘贴大量文本时，发生每行行首的自动缩进累积，因为`Ctrl-v`是通过系统缓存的stream处理，一行一行地处理粘贴的文本。

## 多窗口

垂直切分窗口，Ctrl-w + s 或者使用下面的命令。

```bash
:split <文件名>
```

水平切分窗口，Ctrl-w + v 或者使用下面的命令。

```bash
:vsplit <文件名>
```

如果省略文件名，则打开的是当前文件。

切换窗口的命令。

- Ctrl-w +  Ctrl-w
- Ctrl-w + direction key

## vimrc文件配置

打开语法高亮

```bash
:syntax on
```

禁止使用箭头键。

```bash
nnoremap <Left> :echoe "Use h"<CR>
nnoremap <Right> :echoe "Use l"<CR>
nnoremap <Up> :echoe "Use k"<CR>
nnoremap <Down> :echoe "Use j"<CR>
```

在窗口间移动。

```bash
nnoremap <c-j> <c-w>j
nnoremap <c-k> <c-w>k
nnoremap <c-h> <c-w>h
nnoremap <c-l> <c-w>l
```

## 命令行模式

```bash
# 列出所有buffer
:ls

# 列出所有buffer(包括不可见buffer)
:ls!

# 在当前窗口打开一个新的文件，
# 新建一个buffer，原有文件成为不可见buffer
:e file1

# 新建一个未命名的buffer，然后将其存为 /tmp/foo
:enew
:w /tmp/foo
```

## 插件

- [Markdown语法高亮](https://github.com/plasticboy/vim-markdown)

### dmw多窗口管理

网址：http://www.vim.org/scripts/script.php?script_id=4186

窗口按下面方式组织。

```
================= 
|      |     S1 | 
|      |==========
|  M   |     S2 | 
|      |========== 
|      |     S3 | 
================= 
```

操作
- CTRL-N 在[M]区域创建一个新窗口，将以前的窗口都堆在[S]区域
- CTRL-C 关闭当前窗口
- CTRL-J 跳到下一个窗口(顺时针方向)
- CTRL-K 跳到前一个窗口(逆时针方向)
- CTRL-F 将当前窗口放入[M]区域，并将其他窗口放在[S]区域

## 提示行操作

- :w: write your changes to the file
- :q!: get out of vim (quit), but without saving your changes (!)
- :wq: write your changes and exit vim
- :saveas ~/some/path/: save your file to that locationvim
- ZZ: a faster way to do :wq



