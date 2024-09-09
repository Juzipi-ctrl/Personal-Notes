# 40个超有趣的Linux命令行彩蛋和游戏

## 一键下载安装配置本文全部命令所需环境

```shell
sudo apt-get update
git clone https://github.com/TommyZihao/linux-funny-command.git
cd linux-funny-command
sudo chmod 777 1.sh
./1.sh
```

运行这个脚本文件大概需要十几分钟时间，如果你不想安装全部命令，可以按后文的介绍手动安装相应的命令。

如果你运行完了这个脚本，只需输入每条命令代码框中最后的运行命令就可以执行命令啦。

## 1、黑客帝国字节数据流——假装自己是黑客高手，无孔不入

在命令行中输入以下命令安装并运行。

```text
sudo apt-get install cmatrix
cmatrix
```

![动图封面](https://pic3.zhimg.com/v2-775943b4bcd25d2f161521146793fb5e_b.jpg)

还可输入参数控制颜色。

```text
cmatric -C red
```

![动图封面](https://pic1.zhimg.com/v2-45918babd64fa21a5f4758fc9fc03080_b.jpg)

按`ctrl`+`c`退出。

> 在《黑客帝国》电影里的字节流其实是该片美术指导Simon Whitley的日本妻子菜谱上的片假名。

## 2、高大上仪表盘blessed-contrib——假装自己指点江山，纵横捭阖

```text
sudo apt-get install npmsudo apt install nodejs-legacy
sudo apt install nodejs-legacy
git clone https://github.com/yaronn/blessed-contrib.git
cd blessed-contrib
npm install
node ./examples/dashboard.js
```

![动图封面](https://pic3.zhimg.com/v2-bd7d743f210165ea9e954a1ac351bc02_b.jpg)

> [blessed-contrib项目主页](https://link.zhihu.com/?target=https%3A//github.com/yaronn/blessed-contrib)
> 建议在云服务器或虚拟机上运行这个命令，在树莓派上运行可能会出问题。

## 3、高大上仪表盘hollywood——假装自己日理万机，宵衣旰食

Dustin Kirkland 利用一个长途飞行的时间，编写了这个炫酷、有趣但也没什么实际作用的软件。

Ubuntu操作系统可以直接通过以下命令安装并运行。

```text
sudo apt install hollywood
hollywood
```

在其它Linux发行版中，可以通过以下命令安装并运行。

```text
sudo apt-add-repository ppa:hollywood/ppa
sudo apt-get install hollywood
sudo apt-get install byobu
hollywood
```

![动图封面](https://pic4.zhimg.com/v2-b0bbec742c00ffab3cd0f506610c4293_b.jpg)

![动图封面](https://pic1.zhimg.com/v2-a743d132ed462e55eeb356abbdb51f28_b.jpg)

> [hollywood项目主页](https://link.zhihu.com/?target=https%3A//github.com/dustinkirkland/hollywood)

## 4、追逐鼠标的小猫oneko

在桌面的命令行界面输入

```text
sudo apt-get install oneko
oneko
```

然后输入`oneko`，即可看到效果。

按`ctrl`+`c`退出。

> 注意，本命令只能在桌面所在的命令行界面输入，在远程ssh界面会显示“oneko:Can't open display”

![动图封面](https://pic1.zhimg.com/v2-7939d9bdfe02e2c521883796abe1f9a4_b.jpg)

## 5、ASCII艺术框：box命令

```text
sudo apt-get install boxes
echo "Tongji Univerisity" | boxes
echo "Tongji Univerisity" | boxes -d dog
fortune | boxes -d cat | lolcat
```

![img](https://pic4.zhimg.com/80/v2-6eaf4f0938f6455647d574c7f0390c67_1440w.webp)

## 6、燃起字符串大火aafire

在命令行界面输入

```text
sudo apt-get install libaa-bin  
aafire
```

然后输入 `aafire`，即可看到效果

按`ctrl`+`c`退出。

![动图封面](https://pic1.zhimg.com/v2-3092a0356f16e9841494c1b28e095470_b.jpg)

## 7、火车：Strem Locomotive

在命令行界面输入

```text
sudo apt-get install sl
```

然后输入 `sl`，即可看到效果。

![动图封面](https://pic1.zhimg.com/v2-c2e424a29e7a093a7107ff656ef23998_b.jpg)

输入`sl-h`可以看到彩蛋（没有空格）

![动图封面](https://pic2.zhimg.com/v2-749ac76e83a697312d06163cadbd894d_b.jpg)

> 这个命令其实是在用户把ls命令输错成sl命令的时候准备的彩蛋。

## 8、盯着鼠标看的大眼睛

在命令行界面输入

```text
sudo apt-get install x11-apps
```

然后输入 `xeyes`，回车，即可看到效果：一双紧盯着鼠标所在位置的大眼睛。

按`ctrl`+`c`退出。

![动图封面](https://pic2.zhimg.com/v2-1f6049ad93063415cf809e3bd8062b59_b.jpg)

## 9、艺术字生成器toilet

在命令行界面输入

```text
sudo apt-get install toilet
```

然后输入下面任意一行命令，通过在命令中加-f更换字体或滤镜，你可以把命令里的`Tongji University`换成你想要转换的字符。

案例1

```text
toilet Tongji University
```

![img](https://pic4.zhimg.com/80/v2-eb60e42d4bb0e77a335420351bb7b1d7_1440w.webp)

案例2 双色字：

```text
toilet -f mono12 -F metal Tongji University
```

![img](https://pic4.zhimg.com/80/v2-d523379da079534a038787cbc8724a77_1440w.webp)

案例3 彩色字：

```text
toilet -f mono12 -F gay Tongji University
```

输入`man toilet`查看更多帮助，按`q`退出。

![img](https://pic2.zhimg.com/80/v2-4914744e497c4b0326776fbcc78ba5ed_1440w.webp)

## 10、艺术字生成器figlet

在命令行界面输入

```text
sudo apt-get install figlet
```

然后输入下面任意一行命令，通过在命令中加-f更换字体或滤镜，你可以把命令里的`Tongji University`换成你想要转换的字符。

```text
figlet Tongji University
```

![img](https://pic2.zhimg.com/80/v2-36ce06062bb64bde15dcc7ac8be568dd_1440w.webp)

## 11、字符串视频——回归计算机的上古时代

在命令行界面输入

```text
sudo apt-get install bb
```

然后输入 `bb`，选择`y`加音乐，选择`8`继续，即可看到一段用字符串制作的视频，讲述了视频作者的生涯和使用Linux操作系统的历程，这段视频制作于1997年，基于AAlib平台制作。

按`ctrl`+`c`退出。

> 这段视频的音乐很带感哦\~

![动图封面](https://pic1.zhimg.com/v2-cd79ec479a23bdf204a990dbc6f1e764_b.jpg)



## 12、输出名人名言、古诗词

在命令行界面输入

```text
sudo apt-get install fortune fortune-zh
```

然后输入 `fortune`，即可看到效果。

![img](https://pic2.zhimg.com/80/v2-9742107015950d4d7499eec969f2ec31_1440w.webp)

> 可以把这个程序设置成每次开机自动启动，每次你登陆的时候就能看到一条新的名人名言或唐诗宋词了。

## 13、字符串水族馆：ASCIIquarium

第一步：安装各种依赖

```text
sudo apt-get install libcurses-perl
cd /tmp

wget http://search.cpan.org/CPAN/authors/id/K/KB/KBAUCOM/Term-Animation-2.4.tar.gz

tar -zxvf Term-Animation-2.4.tar.gz
cd Term-Animation-2.4/

sudo perl Makefile.PL &&  make &&   make test

sudo make install
```

第二步：安装软件

```text
cd /tmp
sudo wget https://robobunny.com/projects/asciiquarium/asciiquarium.tar.gz
```

如果显示文件下载失败，可以点击`https://robobunny.com/projects/asciiquarium/asciiquarium.tar.gz`下载压缩包，然后通过FileZilla等文件远程传输软件传输到/tmp文件夹中。

然后继续执行下列命令。

```text
tar -zxvf asciiquarium.tar.gz
cd asciiquarium_1.1/
sudo cp asciiquarium /usr/local/bin
sudo chmod 0755 /usr/local/bin/asciiquarium
asciiquarium
```

![动图封面](https://pic2.zhimg.com/v2-eb466b724a3503797d123698e46a029d_b.jpg)

> [ASCIIquarium项目主页](https://link.zhihu.com/?target=https%3A//robobunny.com/projects/asciiquarium/html/%3Fpage%3D0)

## 14、会说话的牛

在命令行界面输入

```text
sudo apt-get install cowsay
```

然后输入 `cowsay “Hello Tongji Univerisity”`。

![img](https://pic1.zhimg.com/80/v2-aa41236b0150207377f3e9610695d0dc_1440w.webp)

只需用 `-l`参数就能看到它能提供的所有动物。

```text
cowsay -l
```

会输出如下人物，你可以通过`-f`参数加人物名字来更换说话人物：

```text
# Cow files in /usr/share/cowsay/cows:
apt beavis.zen bong bud-frogs bunny calvin cheese cock cower daemon default
dragon dragon-and-cow duck elephant elephant-in-snake eyes flaming-sheep
ghostbusters gnu head-in hellokitty kiss kitty koala kosh luke-koala
mech-and-cow meow milk moofasa moose mutilated pony pony-smaller ren sheep
skeleton snowman sodomized-sheep stegosaurus stimpy suse three-eyes turkey
turtle tux unipony unipony-smaller vader vader-koala www
```

比如更换成hellokitty：

```text
cowsay -f dragon 'Hello Tongji Univerisity'
```

![img](https://pic1.zhimg.com/80/v2-01b0fe0fc940c401c8e66fcb058dc838_1440w.webp)

也可以利用管道命令，将fortune生成的名人名言在cowsay中输出

```text
fortune | cowsay
```

加个颜色

```text
sudo apt install lolcat
```

利用管道命令，让彩色的恐龙大哥说彩色的唐诗：

```text
fortune | cowsay -f stegosaurus | lolcat
```

![img](https://pic4.zhimg.com/80/v2-c4b303d6d05f6ac33e5c8a7fa5644493_1440w.webp)

## 15、会说话的牛2

> 注意，本命令只能在桌面所在的命令行界面输入，在远程ssh命令行界面输入会显示“Can't open display”

在命令行界面输入

```text
sudo apt-get install xcowsay
```

然后输入: `xcowsay “Hello Tongji Univerisity欢迎来同济大学”`

![img](https://pic3.zhimg.com/80/v2-2796e057fcd41b4dd319b7b63ac2414a_1440w.webp)

## 16、日历

直接在命令行界面输入

```text
cal 12 2018
```

即可看到2018年12月的日历。

![img](https://pic2.zhimg.com/80/v2-67644b1b6a03f6f1080723c7139bf975_1440w.webp)

有趣的是，如果你输入。

```text
cal 9 1752
```

你会发现这个月少了11天，这是因为当时大英帝国美洲殖民地的历法从凯撒历法换成了格里高利历法，凯撒历法要迟11天，所以这11天成了日历上的空白期。

[1752年9月为什么少了11天？](https://link.zhihu.com/?target=http%3A//blog.sina.com.cn/s/blog_8713f2c501013md6.html)

## 17、yes命令

直接在命令行界面输入

```text
yes Tongji University
yes Tongji University | lolcat
```

就会看到无穷无尽输出的Tongji University

按`ctrl`+`c`退出。

![动图封面](https://pic3.zhimg.com/v2-5d011cc9b100d9e510d457844a7fb37e_b.jpg)

## 18、分解因数

在命令行界面输入

```text
factor 60
```

即可看到60的分解质因数的结果

![img](https://pic1.zhimg.com/80/v2-f6d54cfef34330f882a6e4ebb4d8af48_1440w.webp)

## 19、screenfetch:显示系统、主题信息

```text
sudo apt install screenfetch
screenfetch
```

在开源社区或程序员社区提问时，可以通过这条命令，直接截图，就能很清晰地描述自己的系统环境。

在Ubuntu云服务器上运行：

![img](https://pic1.zhimg.com/80/v2-b24106e14e5b7dc2bebc2c9eea7b710c_1440w.webp)

在树莓派上运行：

![img](https://pic4.zhimg.com/80/v2-234bc1c59665b7057bc979a8dd6ec163_1440w.webp)

## 20、linux各发行版logo图片及系统信息

```text
sudo apt install linuxlogo
linux_logo
linux_logo -f -L list
sudo apt-get install neofetch
neofetch
```

在ubuntu云服务器上运行linux_logo

![img](https://pic3.zhimg.com/80/v2-4e03d610e30f323ccdfc695686593b96_1440w.webp)

在树莓派上运行linux_log

![img](https://pic4.zhimg.com/80/v2-d2a47e42d7c876500eaf89d647aa0f3f_1440w.webp)

![img](https://pic3.zhimg.com/80/v2-b6bfe5478e780e0da845ddde0a12e8ee_1440w.webp)

循环打印所有支持打印的图标

```text
for i in {1..30};do linux_logo -f -L $i;sleep 0.5;done
```

![动图封面](https://pic2.zhimg.com/v2-27f6d02d58918fd0b1eb8c051994ae55_b.jpg)

## 21、图片转ASCII画风

> 这条命令在树莓派上运行会出问题，建议在云主机或虚拟机上运行。

```text
sudo apt-get install aview imagemagick

wget http://labfile.oss.aliyuncs.com/courses/1/Linus.png

asciiview Linus.png
```



![img](https://pic3.zhimg.com/80/v2-75190b52f7495a3cfe47442f052d0d2a_1440w.webp)

你可以把wget后面的链接换成任意图片的URL。

比如

```text
wget http://www.shumeipai.wang/bingbingbing.jpg
asciiview bingbingbing.jpg
```



![img](https://pic4.zhimg.com/80/v2-9ce9a91ed26861c6715b089fd6a776eb_1440w.webp)

## 22、反转字符命令

在命令行中输入`rev`，打开rev界面，然后输入任意字符，比如

```text
I am a student in Tongji Univerisity
```

按回车，即可看到字符反转之后的结果

按`ctrl`+`c`退出rev界面回到命令行界面。

```text
echo "I am a student in Tongji Univerisity" | rev
```

将一句话中所有单词的顺序反转,但在单词内部字母顺序不变

```text
echo "I am a student in Tongji University" | rev | tr ' ' '\n' | tac | tr '\n' ' '| rev
```

![img](https://pic3.zhimg.com/80/v2-5c90fe129516e8461615059c4dd858de_1440w.webp)

## 23、打字机pv命令：字幕一个个匀速显示出来

```text
sudo apt-get install pv
echo "Tongji Opensource" | pv -qL 10
cal | pv -qL 10
```

![动图封面](https://pic3.zhimg.com/v2-989776aeada572bc91514e193bd46fe2_b.jpg)

## 24、从删库到跑路 sudo rm -rf /*



![img](https://pic2.zhimg.com/80/v2-0228069227129493387461738bb59529_1440w.webp)



> 友情提示：千万不要轻易尝试这个命令，特别是在运行有网站服务器、数据库的Linux主机上

```text
sudo rm -rf /*
```

- sudo：获取root管理员权限
- rm：remove，即删除
- -rf：r表示递归删除，即删除所有的子目录，f表示不需要再进行确认
- /：home目录
- *：所有文件

**也就是说，这条命令是删除这台Linux主机上的所有文件，甚至包括开机文件**

关于这条命令的一些有趣的图片：

![动图封面](https://pic2.zhimg.com/v2-3614565ebc86aa30872f9908f63a5bd5_b.jpg)



![动图封面](https://pic1.zhimg.com/v2-5ce9a42ec770536691222370fecaa904_b.jpg)

![动图封面](https://pic1.zhimg.com/v2-0e0b877c3cd96a7cf38c3a75c16069fc_b.jpg)

![动图封面](https://pic1.zhimg.com/v2-c43f1a2451e41a9087ae2f383f21f908_b.jpg)

## 25、播放星球大战

这条命令在windows上都可以运行

1、打开控制面板，找到”启动或关闭Windows功能“，然后打开Telnet客户端。



![img](https://pic3.zhimg.com/80/v2-0391f01c256e1243d29b2c0749a0e5b2_1440w.webp)





![img](https://pic3.zhimg.com/80/v2-410624794145cf6d6dd58eb80766a2b6_1440w.webp)



2、用管理员模式打开DOS命令行界面，输入以下命令，回车。



![img](https://pic3.zhimg.com/80/v2-b4d245f59bc25135835861638cc6154e_1440w.webp)

```text
telnet towel.blinkenlights.nl
```

![动图封面](https://pic1.zhimg.com/v2-ea240c2ec2492b1c211d510e3119cbdc_b.jpg)

![动图封面](https://pic2.zhimg.com/v2-07e8329b4201d99a32cdf42cdebae541_b.jpg)

## 26、让命令行说话

> 运行这个命令不能通过远程连接，必须通过音响

```text
sudo apt install espeak
espeak 'Hello my dariling'
```

## 27、随机产生人名与地址

```text
sudo apt-get install rig
rig
```

![img](https://pic4.zhimg.com/80/v2-bf1c1d1fa47bbbb4bdda8a6e2d7e43d3_1440w.webp)

## 28、超级牛力——包管理器的彩蛋

在Ubuntu和Debian上，apt-get包管理器内嵌着一个彩蛋。 如果你在命令行界面输入

```text
apt-get help
```

在最后一行能找到

This APT has Super Cow Powers。

本APT具有超级牛力。

则说明你的系统可以运行这个菜单。

![img](https://pic2.zhimg.com/80/v2-946ff7e64e0f97d21043dd47b86fb6d5_1440w.webp)

在命令行界面输入

```text
apt-get moo
```

即可看到这个彩蛋。

aptitiude包管理器也有类似的彩蛋

```text
aptitude moo
aptitude moo -vv
aptitude moo -vvv
aptitude moo -vvvv
aptitude moo -vvvvv
aptitude moo -vvvvvv
```

![img](https://pic2.zhimg.com/80/v2-674f455eeb283523225480e7a9ff7689_1440w.webp)

> 这个彩蛋的灵感来自于法国作家安托万·德·圣·埃克苏佩里童话小说《小王子》的第一章



![img](https://pic1.zhimg.com/80/v2-8882c86333eea320266c9d2377bd9718_1440w.webp)



## 29、命令行游戏bastet：俄罗斯方块

```text
sudo apt install bastet
bastet
```

左右键控制方块移动，上键控制方块旋转。

![动图封面](https://pic4.zhimg.com/v2-ecbcd9d59e1ba0cfd0e4c725341928fb_b.jpg)

## 30、命令行游戏ninvaders：太空入侵者

```text
sudo apt-get install ninvaders
ninvaders
```

按空格键发射子弹。

![动图封面](https://pic4.zhimg.com/v2-ec7b1f5649deda39c21be633efe9267b_b.jpg)





## 31、命令行游戏pacman4console：吃豆人

```text
sudo apt-get install pacman4console
pacman4console
```

使用方向键控制移动。



![动图封面](https://pic3.zhimg.com/v2-a29d43b582352818de011eb1c9ab49a6_b.jpg)





## 32、命令行游戏nSnake：贪吃蛇

```text
sudo apt-get install nsnake
nsnake
```

使用方向键控制。



![动图封面](https://pic3.zhimg.com/v2-184cad0b108704e9d6a24eec84ee924a_b.jpg)





## 33、命令行游戏Greed：赢者通吃

```text
sudo apt-get install greed
greed
```

数字表示下一步可前进的步数，游戏的目标是在咬到自己尾巴之前尽可能多走几步。



![动图封面](https://pic4.zhimg.com/v2-e433936037fd535cf24304e4367bc76f_b.jpg)





## 34、命令行游戏Air Traffic Controller：空中塔台控制

```text
sudo apt-get install bsdgames
atc
```

在玩之前，你可以先输入`man atc`查看这个游戏的说明文档。游戏的目标是通过一系列命令输入，引导飞机起飞和降落，进行空中塔台调度。



![动图封面](https://pic2.zhimg.com/v2-7842ac92f3d66c9808aa568719fb6635_b.jpg)





## 35、命令行游戏backgammon：双陆棋

```text
sudo apt-get install bsdgames
backgammon
```

这是一款1997年制作的老游戏，游戏开始的时候可以阅读相关规则介绍。



![img](https://pic3.zhimg.com/80/v2-74f26ae2ef01cde46313d7cdd4ffec1a_1440w.webp)



## 36、命令行游戏moonbuggy：月球战车

```text
sudo apt-get install moon-buggy
moon-buggy
```



![动图封面](https://pic3.zhimg.com/v2-690e5bfc682f602f99f12271f7314312_b.jpg)





## 37、命令行游戏2048

```text
wget https://raw.githubusercontent.com/mevdschee/2048.c/master/2048.c
gcc -o 2048 2048.c
./2048
```



![动图封面](https://pic2.zhimg.com/v2-227d258ddd1402f1334fc608155c0ea9_b.jpg)





## 38、命令行也能联机玩网游：Tron

```text
ssh sshtron.zachlatta.com
```

使用wasd四个键控制蛇的移动，游戏的目标是既不要咬到别人也不要咬到自己，活着的时间越长分数越高。



![动图封面](https://pic4.zhimg.com/v2-c85e30b610225e8bb7185e927fc89a07_b.jpg)





## 39、命令行游戏：巨洞冒险

巨洞冒险Colossal Cave Adventure，又名 ADVENT、Clossal Cave 或 Adventure，是八十年代初到九十年代末最受欢迎的基于文字的冒险游戏。在 1976 年，一个叫 Will Crowther 的程序员开发了这款游戏的一个早期版本，之后另一位叫 Don Woods 的程序员改进了这款游戏，为它添加了许多新元素，包括计分系统以及更多的幻想角色和场景。这款游戏最初是为 PDP-10 开发的，这是一种历史悠久的大型计算机。后来，它被移植到普通家用台式电脑上，比如 IBM PC 和 Commodore 64。游戏的最初版使用 Fortran 开发，之后在八十年代初它被微软加入到 MS-DOS 1.0 当中。

游戏的主要目标是找到一个传言中藏有大量宝藏和金子的洞穴并活着离开它。这款游戏的灵感主要来源于原作者 Will Crowther 丰富的洞穴探索的经历。他曾经经常在洞穴中冒险，特别是肯塔基州的猛犸洞Mammoth Cave。因为游戏中的洞穴结构大体基于猛犸洞，你也许会注意到游戏中的场景和现实中的猛犸洞的相似之处。

```text
sudo apt-get install python3-yaml libedit-dev
sudo pip3 install PyYAML
git clone https://gitlab.com/esr/open-adventure.git
cd open-adventure
make
make check
advent
```



![img](https://pic1.zhimg.com/80/v2-ea8983b35f483aad9ea6b7bfdf170630_1440w.webp)



## 40、打印圆周率后小数点若干位

```text
sudo apt-get install pi
pi 50
```

打印小数点后若干位的圆周率。



![img](https://pic2.zhimg.com/80/v2-5ffc3bfd58b4cb3ac668d5e76b65be1d_1440w.webp)

