# Lofter2Hexo

## 【Lofter迁移指南】
！！！恳请扩散！！！

首先务必保存好导出的xml，切勿遗失，也别删除。
其次红心蓝手热度数据不在里面，喜欢、粉丝、关注也不在里面，只有文章内容和评论。

之前写过lofter导出到xml的方法（乐乎网页版-更多-导入导出，下载到的xml就是你的乐乎文章的备份）和xml转换为markdown的脚本，当时脚本其实已考虑到图片下载和图床迁移，自用效果不错，但未及详写，也没来得及打包成软件。

现在打包成exe了，完全不懂代码也可以用。下载地址在最后。

xml文件和程序放在同一文件夹下即可，会自动识别。

Mac系统直接运行脚本，不提供打包，因为wxPython打包的程序不能识别当前目录具体位置。

以下是迁移科普，包括图床和静态博客相关：

我自己是写乐乎的同时也写Hexo博客，重要的内容基本两边都有，这个迁移程序我大概也不怎么用得上，但是帮人迁移时发现Hexo博客入门门槛略高（是一次性的难度，搭好环境就简单了）。而且虽然markdown作为标记语言非常简单明了，也会有人因不习惯而头疼。所以，实在搞不懂怎么写markdown的话，可以试试继续写乐乎然后及时备份，单纯用导出xml+迁移程序来写markdown。我之后会增加多个xml文件合并导出和去除重复日志的功能。目前已支持多个xml文件分别导出为markdown文件到对应文件夹，如果有一个或多个xml文件（多个号或多个子博客的情况），但其中没有重复日志，现在就可以用了。

乐乎图床是有防盗链的，之前我没怎么研究这点，但是微博图床也已经开始防盗链了，简单来说就是你在微博站内发微博图可以看到图，在其他站发图的话，如果是https会因为安全性带上当前网址的referer，微博知道请求不是来自微博站内就不会显示图片，本地markdown预览因为不带referer往往是可以正常查看图片的，Coding Pages因为是http不带s也不发送referer也能看到图片，但GitHub Pages是强制https，试过一些曲线救国方法，效果不灵光，所以必须迁移图床。

我使用的批量下载方法是用Selenium控制Chrome然后用Python脚本在前台控制键盘不断打开链接再Ctrl+S保存图片。这个不好做图形界面并且还在修改以适配Windows（目前的版本只能给Mac用），适配完成后会以Python脚本形式分享，需要懂怎么运行Python和安装相关库才能用。届时可以委托能够运行脚本的人代下图片。

图片需要上传到其他不限制外链的图床才算迁移完毕。如果你上传到了自己的GitHub的库中，填好GitHub用户名和图片库名重新运行一遍软件生成markdown再更新博客即可。为了博客生成速度考虑，图片不建议放在GitHub Pages库里，保持图文分开，也避免Git信息冗余导致博客文件夹占用地方过大。

GitHub作为图床的话，不限制图片大小，不缩尺寸不二压，也没啥其他限制。个人使用，量不大，也符合使用规则。

GitHub之外，当前能用的图床有七牛、腾讯、SM.MS等几个，免费能用的数量和流量有限，还有其他限制。

乐乎应该以前迁移过图床服务器的网址，所以xml里面有些图片地址不对，需要按失效地址中的服务器前缀生成新地址。这点脚本中已考虑。

乐乎已删除的文章中的图片链接大多并未失效，这点和微博类似。但不确定这种状态会保持多久，再加上防外链过严，还是建议尽快迁移图床。

非礼勿视图片没救了，请自己手动补档。

乐乎文章评论区内容默认会放在markdown文件底部，不需要显示这些评论的话可以在脚本中关掉。

关于博客迁移去向，GitHub Pages静态博客是最优选。自建Wordpress（Wordpress.org）和Wordpress.com（在线博客网站，和前面那个不是一回事）也有xml导入导出功能，但字段不同的地方很多，必须写转换脚本，我用得很少并且还没搞清楚格式，所以，放到以后。

生成静态博客的引擎有好几种：
功能丰富的Hexo（基于Nodejs，安装步骤较长，中文教程多）；
生成网页速度极快的Hugo（基于Go，只需下载一个exe）；
GitHub原生支持的Jekyll（这个的话什么都不用装只上传markdown文件也行，GitHub会生成网页）。

迁移程序目前版本生成的markdown是为Hexo准备的。Hugo和Jekyll所需要的markdown文件的头部信息有所不同，之后会在程序中添加支持。建议都试一遍，哪个成功用上了就用哪个。

如果实在搞不定在线迁移，生成的markdown仍可以本地查看。

我的主要操作系统是Mac，Python仅是看书自学的水平，在Windows上遇到的部分问题我不一定能提供解答。

可以委托我或者其他会使用迁移脚本的人进行迁移。委托需要提供你的【用户名.GitHub.io】库的协作权限（如果彻底不会用就给我一个你新注册的GitHub用户名和密码），和对应的一个或多个乐乎导出的xml文件。如果要迁移的图片较多，会花较长时间。

个人博客可以使用以下免费评论系统：
来必力livere，韩国公司，支持国内如微博贴吧等社交平台登陆；
Valine，基于LeanCloud的无后端评论系统；
Gitalk等，基于Github账户的评论系统；
畅言，必须备案。

Hexo推荐使用主题theme-next，经常增加新功能。

此外，Hexo本身的插件有包括加密日志、看板萌娘、统计字数、一键更新等等有用功能。

不过，乐乎的日志瀑布流和Tag广场，暂时没有方法做到。

GitHub项目地址：
https://github.com/alicewish/Lofter2Hexo

其中wxPython-Lofter2Hexo.py是图形界面的python脚本，wxPython-Lofter2Hexo.exe是此脚本打包的可执行程序，效果是一样的。

整个迁移过程会略长，markdown的基础知识、Hexo的搭建、图床迁移，都有数是最好的，如果遇到问题，善用搜索和求助。

支援群912760241，可以找我问相关。

最后吼一句，女孩子们去学编程吧，我们能写得出美好得多的东西，即使是笨拙的。

## 【Lofter2Hexo 1.2版更新】

①lofter导出到xml方法：乐乎网页版-更多-导入导出。
下载到的xml就是你的乐乎文章的备份。

②xml文件和程序放在同一文件夹下即可，会按后缀名自动识别。

③Mac系统直接运行脚本，不提供打包，因为wxPython在Mac上打包的程序不能识别当前目录具体位置，无法使用。

④提供四种迁出类型：
Hexo（http://hexo.io）
Hugo（http://gohugo.io）
Jekyll（https://jekyllrb.com）
Gridea（https://gridea.dev）
其中Gridea是软件，Jekyll不需要安装环境也可以，Hugo需按说明安装一个对应软件且速度很快，Hexo稍麻烦但对应中文教程很多。

⑤GitHub项目地址：
https://github.com/alicewish/Lofter2Hexo

⑥主程序是`wxPython-Lofter2Hexo.py`，其打包版为`wxPython-Lofter2Hexo.exe`，运行效果是一样的。
这个程序的效果是把xml转换为对应的markdown文件。

⑦`wxPython-Lofter2Hexo-图片下载器.py`是配套图片下载器，不提供打包版，因为打包不成功。
原理是使用Selenium控制Chrome，使用脚本控制键盘按`ctrl`+`s`和`enter`，需保持被控制的Chrome在前台。

⑧下载完图片以后上传到GitHub，同时保证本地有对应图片库，再次运行主程序，如果在本地GitHub库找到对应图片即假设对应GitHub网址也有图片，将乐乎图片地址替换为对应新图床并生成markdown。

⑨`Lofter2Hexo.py`是早期的原型脚本，会Python且不需要图形界面的可以自己修改成需要的。

⑩支援群`912760241`，可以找我问相关。

## 【Lofter2Hexo 1.3版更新】

【Lofter迁移到Wordpress】

①主程序为wxPython-Lofter2Hexo.exe，下载地址 https://github.com/alicewish/Lofter2Hexo/raw/master/wxPython-Lofter2Hexo.exe

②lofter导出xml的方法：【乐乎网页版】-【更多】-【导入导出】。 下载到的xml就是你的乐乎文章的备份。

③lofter的xml文件和程序放在同一文件夹下即可，会按后缀名自动识别。

④程序提供五种迁移类型：
Hexo（http://hexo.io）
Hugo（http://gohugo.io）
Jekyll（https://jekyllrb.com
Gridea（https://gridea.dev）
Wordpress（https://wordpress.com/） 
选择最后一种，将生成适用于Wordpress的xml。

⑤登陆Wordpress，选择【我的站点】-【工具】-【导入】，上传刚才转换后的适用于Wordpress的xml。

⑥等待日志导入完成。如果觉得有用，可以给我的项目 https://github.com/alicewish/Lofter2Hexo 加个star。

⑦支援群【912760241】，可以找我问相关。

## 【Lofter2Hexo 4.47版更新】

图形界面改用PyQt5重写，修正了一些bug。

