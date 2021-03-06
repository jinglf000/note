## MAC 

[TOC]

### 1、Mac commend 命令行

https://www.cnblogs.com/hopelee/p/7049551.html

使用：

```
man command line // 使用man + 命令，输出命令使用指南，可以使用上下箭头移动，输入/和关键字来搜索 按Q退出使用指南。如果你连命令名称都不知道怎么办呢？输入man -k和关键字来对整个使用指南数据库进行搜索。
```

#### 路径：

绝对路径：形如，开头为反斜杠 `/User/xxx`

相对路径：形如`../ ../`

鄂化符`~`（tilde）在command line 中可以代表当前用户的 home folder,不代表根目录

`/bin/` 通常为命令执行目录

####  文件操作和查看

如果你想将当前 command line 会话切换到其他目录，需要用到三个命令：`pwd`，`ls`和`cd`。

1. `pwd`的含义是“print working directory”，会显示当前目录的绝对路径。
2. `ls`的含义是“list directory contents”，它会列出当前目录的内容。这个命令还有其他参数可选。`ls -l`列出所有文件，包含相信信息；
3. `cd`的含义是“change directory”，它会改变当前目录到你指定的目录。如果你不指定，则会返回你的 home folder。
4. cat 查看文件
5. less 使用和 man的方式查看文件，which 查看命令所在的位置
6. find 查找文件

#### 文件操作
`mkdir cp mv rm rmdir`
- 1 mkdir
“make directory”的缩写，用来创建文件夹，语法为mkdir后接新文件夹的目录。可以用-p选项，来一起创建路径中不存在的文件夹（这样你就不用挨层创建了）。

-  cp
  “copy”的缩写，用来把文件从一处复制到另一处。语法为cp后接原始路径，后接目标路径。如果你想复制整个文件夹和所有内容，需要添加-R选项。如果指定的目标路径不含文件名，则 cp 命令会按原名复制。如果指定的目标路径包括文件名，则会复制为你指定的文件名。如果仅指定新文件名，则会在原处以新名称创建文件副本。注意，系统会自动替换同名文件而不出现提示。

- mv
  “move”的缩写，用来移动文件。语法为mv后接原路径，后接新路径。mv 的指定路径规则和 cp 是一样的（没错，如果仅指定新文件名，它就成了重命名命令）。

- rm
  “remove”的缩写，会永久删除文件。注意，command-line中没有废纸篓。语法为rm后接文件路径。然而，使用 rm 命令删除的文件有可能可以通过数据恢复工具恢复。如果希望安全删除文件，可以使用srm命令。

- rmdir和rm -R
  rmdir是“remove directory”的缩写，这个命令会永久删除文件夹。再强调一遍，CLI 中木有废纸篓。语法为rmdir后接希望删除目录的路径。然而，rmdir 命令无法删除含有任何其他文件的文件夹，所以大多数情形下rmdir命令是不适用的。不过，你可以利用rm添加-R选项来删除文件夹及包含的所有文件。

- vi
  代表“visual”（视觉的），然而这个名称相当具有讽刺意味：vi可能是可视化效果最差的文本编辑器了。然而，vi 是 command line 中最常见的文本编辑器。用vi打开文本文件，只需要输入vi后接文件路径即可。Mac OS X 还提供了nano，一个更加现代的文本编辑器。它也更加方便，例如在底部包含了一个作弊小条（=_=），上面有常用的快捷键列表（你就不用背下来它们了）。然而，vi却有时是默认的文本编辑器，所以掌握vi是很有用的。

和less命令类似，vi命令会占用整个 Terminal 空间来显示文件内容。打开后，在“command模式”，vi 会等你输入一些预定义字符来告诉 vi 你想做什么。你也可以使用键盘上的箭头键单纯地浏览文件。你想编辑时，按A开始（会进入编辑模式）。文字会插入到光标处。如果你想保存，需要先退出编辑模式进入 command 模式。方法是按下esc键。回到 command 模式后，按住shift同时按两次Z来保存并退出。如果你不想保存，在 command 模式输入:quit!并按enter
return直接退出。



#### 管理用户
sudo

#### 小技巧
- 输入命令open .可以用 Finder 打开当前的位置。
- 在 Terminal 的偏好里面可以设定它的外观和风格。
- 中止一个错误的或者发疯的命令，可以使用组合键control + C。
- 你可以在执行前编辑命令，只需要使用箭头和键盘上的其他字母。
- 没有输入任何命令时，你可以用▲和▼来浏览历史命令。同样可以编辑和再次执行。
- 你 也可以使用history命令查看历史记录。
-  你可以使用组合键control + L清屏

#### 日志处理

```shell
tail -f <file name> // 查看日志文件内容
grep 'keyWord' <file name> // 根据关键字搜索文件中的内容
zgrep 'keyWord' <file name> // 根据关键字搜索压缩文件内容
```

#### 端口进程
查看进程占用，获取进程PID
` lsof -i tcp:3000`
杀死进程，杀死对应PID
`kill pid`

### 2、MAC APP
* MindNode  思维导图 XMind ZEN 
* Scroll Reverser 鼠标反向
* Switch hosts 切换host
* React Native Debugger 
* sublime 文本编辑
* Charlse 抓包
* Typora md
* postman 
* [JSUI]([https://github.com/kitze/JSUI/releases/tag/v0.0.18](applewebdata://4A1BB12E-133D-4895-8CCE-CD8BA797EBC9/aa))
* 

### 3、搜狗输入法 繁体简体切换
* 快捷键 shift + ctrl + f 切换

### 4、zan-proxy 使用指南
* 切记一定要配置 host；(至少添加一条：localhost 127.0.0.1)
* http 转发规则中，可以使用正则表达式、对应的捕获列表、环境变量

### 5、VScode chrome debugger
```
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
```

view = f(data) ，框架做了一件事情，就是把 数据data 显示到页面上 view上；现在写的应用页面，包含两部分，一是data 二是view。你处理data，然后把data交给vue去渲染成页面。vue不知道渲染成什么页面，所一页面最终渲染成什么样子是你所写的模板所决定的

