### 统一使用

- 在虚拟机中安装manjaro使用v2ray时总是错误的原因，应该看一下时间对不对，v2ray有严格的时间限制，时间不对的情况下就不能正确使用了，所以要调整时间，调整完时间就能正确使用了目前来看。

##### Linux好玩的命令

###### figlet

- 艺术字生成器，由ASCII字符组成
- 有许多字体和格式选项，可以使用showfigfonts命令查看可用字体：
- 然后，您可以使用-f选项指定要使用的字体：

###### cowsay

- 用ASCII字符打印牛，羊等动物，还有个cowthink，这个是奶牛想，那个是奶牛说
- cowsay -l 查看其它动物的名字，然后 -f 跟上动物名

### Mac

- 环境变量也是一个变量，而且是全局变量，除非在shell中写入export，只在当前shell中有用，重新启用shell就没用了，如果想一直起作用，只需要写入配置文件中，但是在linux环境下有好几个可以设置环境变量，有的是对所有用户有作用，有的是对当前用户有作用。在需要的时候可以使用它，变量的使用就是为了方便，可以将很长的一串当做一个我们定义的变量，然后通过变量来使用，简化了使用。例如PATH，我们执行程序的路径去里面寻找，然后去执行。环境变量的使用USER=lyl，HOME=/home/lyl，如果在程序中使用到当前用户，直接调用USER环境变量就可以了。环境变量的命名在程序中一般都有体现，要不然找不到。例如PATH是程序运行时的路径，在程序中要调用PATH才行，不能调用其他的环境变量，也不在其他的环境变量中寻找。
- mac终端里面没有走代理，所以curl不能使用，其他的app默认自动走代理，走的是系统的代理，所以需要设置环境变量http_proxy和https_proxy来使终端使用代理。原理是终端没有走代理，在环境中没有找到，此时设置环境变量，此环境变量在v2ray里面直接调用来使用，所以走了代理。
- proxy就是代理，前面可以设置不同的例如http，https，查看ubuntu上env可以看到有很多的proxy
- [代理的讲解](https://sites.google.com/site/2018pk/222)
- 代理服务器设置本地代理即127.0.0.1:8889意思是访问请求不直接发送出去，而是通过当前主机进行各种加密设置伪装成http发送出去
- http和socks代理的区别，http是一种协议，SOCKS是一种网络传输协议，主要用于客户端与外网服务器之间通讯的中间传递。SOCKS是"SOCKet Secure"的缩写，http代理是用来浏览网页用的，socks代理可以看成是一种全能的代理，不管是telnet、ftp还是其他被墙的网站都可以进行代理。
- SOCKS工作在比HTTP代理更低的层次：SOCKS使用握手协议来通知代理软件其客户端试图进行的连接SOCKS，然后尽可能透明地进行操作，而常规代理可能会解释和重写报头（例如，使用另一种底层协议，例如FTP；然而，HTTP代理只是将HTTP请求转发到所需的HTTP服务器）。虽然HTTP代理有不同的使用模式，CONNECT方法允许转发TCP连接；然而，SOCKS代理还可以转发UDP流量和反向代理，而HTTP代理不能。HTTP代理通常更了解HTTP协议，执行更高层次的过滤。代理是转发请求，没有加密解密过程也不需要。
- http是一种网络通信协议，当不能直接访问服务器时，通过客户端与代理服务器之间的http连接进行请求，然后代理服务器将请求发送出去，请求的数据放到代理服务器上，然后客户端从代理服务器通过http连接拿取数据。翻墙的原理是通过代理服务器将客户端的请求通过加密算法伪装成其他的http请求，翻墙涉及到加密解密过程，而且涉及到使用哪种协议进行加密解密，国外的VPS服务器返回的http请求是进过加密的，客户端不能直接使用，所以要经过本地进行解密，所以本地也相当于一个代理服务器，安装了v2ray之后有一个端口，通过这个127.0.0.1和这个端口进行通信，出来的数据就是解密完成的就可以使用了。本地的请求通过本地代理服务器来说明使用哪种加密算法，访问到VPS，VPS进行解密然后访问。长城防火墙的原理是封IP地址，比如google服务器的地址，我们自己购买的VPS地址是没有被封的。本地的请求一般不需要加密，因为封的是IP，而我们的IP是自己的可以直接连接。
- 翻墙设置代理地址为127.0.0.1，不同的协议有不同的端口，所有的请求数据通过127.0.0.1和端口跟本机进行通信，本机就相当于一个服务器，而我们安装的翻墙软件就相当于安装在服务器上的软件，软件一直在监听端口，然后获取数据，根据协议拿到数据后代理服务器也即是本机安装的软件进行加解密，然后发送出去。
- 将本机也看作一个服务器，本机是通过127.0.0.1进行通信的，本机上的软件就相当于安装在服务器上的软件。一些请求通过127.0.0.1发送到本机，本机上的软件通过加密然后发送出去，然后发送回来的数据也是先经过代理服务器然后解密，在通过127.0.0.1返还回去。安装的翻墙软件能直接经过tcp，udp发送数据，软件就直接有这个功能，服务器只是一个载体，各种功能是通过其上的软件来实现的。
- 翻墙是需要本地代理的，因为其要加密解密。代理服务器一些其他的功能例如隐藏IP，作为防火墙隔离内网与外网等不需要使用本地代理。
- http和socks一样只是一种通讯协议，http只是请求http，而socks可以响应各种请求。例如telnet、ftp等。两种在osi模型中的位置不一样，所用的技术也不一样。这两种都是放在代理服务器上的。协议就是协议，客户端将数据包装成这个协议，代理服务器使用协议得到数据，然后进行转发代理功能。
- Http工作在应用层上，而Socks工作在会话层上，且Socks代理只是简单地传递数据包，并且不必关心是何种应用协议，所以Socks5代理服务器比应用层代理服务器要快得多。 两者支持协议不同，工作环境也不同，因此也不能直接替换使用。
- http和socks代理使用的端口一般是不一样的，本地代理也是不一样的。端口的意思是找一个通道进行连接。如果使用的是http则使用一个端口，使用的是socks则使用其他端口。通过设置本地代理设置export 环境变量。设置环境变量就可以让程序通过这个环境变量调用本地端口传进来的数据进行加密解密工作。
- ubuntu设置里面网络代理关闭后，或者在软件上进行断开连接，env查看环境变量，就没有了proxy环境变量。
- mac下使用软件qv2ray设置了代理，在设置里面，但是环境变量里面没有，说明mac终端没有走代理，可以手动设置。使用export写进配置文件中。
- mac下没有ubuntu下自动设置自动取消环境变量。但是软件里面有断开连接。

---
- [mac下shell配置文件的讲解](https://zhuanlan.zhihu.com/p/34110025)
- mac下终端使用代理，但是其没有ubuntu上自动断开，所以使用命令来让终端使用代理，想要使用代理时就是proxy打开，平常没事使用unproxy关闭。
```shell
alias proxy='export all_proxy=socks5://127.0.0.1:1089 && export http_proxy=http://127.0.0.1:8889 && \
	export https_proxy=http://127.0.0.1:8889'
alias unproxy='unset all_proxy && unset http_proxy && unset https_proxy'
```
- /bin/bash -c ""其中的-c的含义是给bash shell 输入的命令，命令在双引号里面。
- mac下shell配置文件的加载有顺序/etc/profile /etc/paths ~/.bash_profile ~/.bash_login ~/.profile ~/.bashrc，/etc/profile和/etc/paths是系统级别的，系统启动就会加载，后面几个是当前用户级的环境变量，后面3个按照从前往后的顺序读取，如果~/.bash_profile文件存在，则后面的几个文件就会被忽略不读了，如果~/.bash_profile文件不存在，才会以此类推读取后面的文件。~/.bashrc没有上述规则，它是bash shell打开的时候载入的。.bash_profile这个文件在系统里面没有，没有就自己创建。zsh加载后面的几个不一样，zsh有.zprofile，相当于.bash_profile，修改的方法一样。zsh没有加载.bashrc，所以需要在.zshrc里面输入命令source ~/.bashrc
---
- mac下lyl目录在/Users/lyl，linux在/home/lyl，两者不一样，cd ～直接切换到lyl目录

#### homebrew

##### 术语

```
formula
    Homebrew package definition built from upstream sources
cask
    Homebrew package definition that installs macOS native applications
keg
    installation destination directory of a given formula version e.g. /usr/local/Cellar/foo/0.1
rack
    directory containing one or more versioned kegs e.g. /usr/local/Cellar/foo
keg-only
    a formula is keg-only if it is not symlinked into Homebrew´s prefix (e.g. /usr/local)
cellar
    directory containing one or more named racks e.g. /usr/local/Cellar
Caskroom
    directory containing one or more named casks e.g. /usr/local/Caskroom
external command
    brew subcommand defined outside of the Homebrew/brew GitHub repository
tap
    directory (and usually Git repository) of formulae, casks and/or external commands
bottle
    pre-built keg poured into the cellar/rack instead of building from upstream sources
```

- formula就是那些需要下载源文件编译的程序，一般为命令行的程序
- cask就是本地应用程序，带界面的，例如tabby就是cask
- key就是在/opt/homebrew/Cellar/fzf/0.29.0每一个程序里面都有一个版本号
- Caskroom和cellar在同一级目录，Caskroom放的是cask，例如tabby就在caskroom里面
- tap就是第三方仓库
- bottle就是提前编译好的二进制程序。

##### 命令

###### brew list

```
list
   List all installed formulae.   包括cask

brew list
==> Formulae
berkeley-db	cscope		gettext		libev		libssh2		lua		node		perl		ranger		rtmpdump	tmux		xz
brotli		fd		icu4c		libevent	libunistring	mpdecimal	openldap	python-tk@3.9	readline	ruby		universal-ctags	zstd
c-ares		fzf		jansson		libidn2		libuv		ncurses		openssl@1.1	python@3.10	rename		sqlite		utf8proc
ca-certificates	gdbm		jemalloc	libnghttp2	libyaml		nghttp2		pcre2		python@3.9	ripgrep		tcl-tk		vim

==> Casks
font-hack-nerd-font	tabby
```

###### brew install

```
install [options] formula|cask [...]
       Install a formula or cask. Additional options specific to a formula may be appended to the command.

--formula  Treat all named arguments as formulae.
--cask Treat all named arguments as casks.
```

- brew install命令可以不带任何参数安装formula或者cask，但是也可以带参数，--formula表示后面安装的都是formula，--cask表示后面跟的都是cask

###### brew tap

```
tap [options] [user/repo] [URL]
   Tap a formula repository.
   If no arguments are provided, list all installed taps.
   With URL unspecified, tap a formula repository from GitHub using HTTPS. Since so many taps are hosted on GitHub, this command is a shortcut for brew tap user/repo   https://github.com/user/homebrew-repo.
```

- brew tap可以为brew的软件的 跟踪,更新,安装添加更多的的tap formulae

- 如果你在核心仓库没有找到你需要的软件,那么你就需要安装第三方的仓库去安装你需要的软件

- tap命令的仓库源默认来至于Github

- `brew tap <user>/<repo>` 在本地对这个 `https://github.com/user/repo` 仓库上做了一个浅度的克隆，完成之后 `brew`就可以在这个仓库包含的`formulae`上工作,好比就在`Homebrew`规范的仓库,你可使用`brew install` 或者`brew uninstall `安装或者卸载这个仓库上的软件。当你执行`brew update`这个命令时，`tap` 和 `formulae` 就会自定更新

- `brew untap <user>/<repo> [<user>/<repo> <user>/<repo> ...]` 移除已经安装的`tap`.这个仓库被删除,`brew`就不在可用在这个仓库的`formulae`.可以同时删除几个仓库

- 仓库命令的规范

  - 在 `Github`上,你的仓库名称必须是`homebrew-something`,为了使用一个参数的`brew tap`命令,`homebrew-`这个前缀不是可选的,是必须的。
  - 当你在命令行使用`brew tap`时，你可以省略`homebrew-`这个前缀的
  - 也就是说:`brew tap username/foobar`是作为长版本`brew tap username/homebrew-foobar`使用的一个简写
  - 也就是说在github仓库上的名字是需要有homebrew-这个前缀的，而在命令行brew tap命令是不需要的，brew程序会自己加上的
  - username是不用管大小写的，只要字母一样，brew就会找到正确的仓库。

  ```
  brew tap homebrew/cask-fonts
  brew install --cask font-hack-nerd-font
  
  https://github.com/Homebrew/homebrew-cask-fonts
  
  从这可以看出，仓库是有homebrew前缀的，而且username是可以不用管大小写的。
  ```

###### brew update

```
update [options]
       Fetch the newest version of Homebrew and all formulae from GitHub using git(1) and perform any necessary migrations.
```

- Homebrew 经常会在执行命令的时候触发更新，不过如果你想要主动检查更新，可以执行 `brew update` 来唤起 Homebrew 的更新。

###### brew upgrade

- 使用 `brew upgrade` 来更新所有的软件，或者是使用 `brew upgrade [软件名]`来更新单个软件。

### manjaro

- manjaro报错缺少运行库libcrypt.so.1时解决办法

  ```shell
  yay -S libxcrypt-compat
  ```

- manjaro删除不需要的依赖包的命令

  ```
  sudo pacman -R $(pacman -Qdtq)
  ```

  - -Q查询的时候会将版本号都输出出来，这样删除的时候就会出错，因为其将版本号也当作软件包的一部分。-q选项可以将版本号这些信息都隐藏掉。这样就能正确删除。-d是列出所有作为依赖关系安装的软件包 [过滤器]。-t选项列出不被任何软件包(可选)要求的软件包(-tt 忽略可选依赖)，这样就是不被依赖的被选出来了。-d选出依赖包-t选出不被依赖的选项包。

##### manjaro软件源

- pacman -Sy命令更新源时会输出

  ```
  core 已经是最新版本
  extra 已经是最新版本
  community 已经是最新版本
  multilib 已经是最新版本
  ```

  - 说明manjaro配置了四个软件源，我们也可以配置自己的软件源，配置文件/etc/pacman.conf

    ```
    [core]
    SigLevel = PackageRequired
    Include = /etc/pacman.d/mirrorlist
    
    [extra]
    SigLevel = PackageRequired
    Include = /etc/pacman.d/mirrorlist
    
    [community]
    SigLevel = PackageRequired
    Include = /etc/pacman.d/mirrorlist
    
    # If you want to run 32 bit applications on your x86_64 system,
    # enable the multilib repositories as required here.
    
    [multilib]
    SigLevel = PackageRequired
    Include = /etc/pacman.d/mirrorlist
    
    ```

    - 这是系统配置的软件源

  - 配置自己的软件源

    ```
    Arch Linux 中文社区仓库 是由 Arch Linux 中文社区驱动的非官方用户仓库。包含中文用户常用软件、工具、字体/美化包等。
    [archlinuxcn]
    Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
    
    我们也可以配置多个源，然后放在文件里面，用Include表示那个文件，将所有的源都加进来
    [archlinuxcn]
    SigLevel = Optional TrustedOnly
    Include = /etc/pacman.d/archlinuxcn
    其中archlinuxcn是一个文件，里面是各种服务器，一行一行的由Server带头显示
    Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
    Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
    Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
    ```


##### fcitx

- 安装输入法

  ```
  sudo pacman -S fcitx-im
  sudo pacman -S fcitx-configtool
  sudo pacman -S fcitx-sogoupinyin
  ```

- 添加输入法配置文件 `sudo vim ~/.xprofile`

  ```
  export GTK_IM_MODULE=fcitx
  export QT_IM_MODULE=fcitx
  export XMODIFIERS="@im=fcitx"
  ```

- 打开配置页面进行配置输入法

  - 输入法全局配置时注意事项
    - 输入法界面第一个输入法为非激活输入法，其余的为激活输入法。
    - 输入法配置界面切换激活/非激活输入法，就是切换第一个非激活输入法与激活输入法的第一个
    - 输入法切换键就是在循环切换激活的输入法，并不会切换第一个非激活输入法
    - 输入法快捷键自定义的时候要注意按键抬起的顺序，例如设置为ctrl+space，此时自定义的时候要先按ctrl在按space，然后先抬起space在抬起ctrl，这样就能设置成功。


##### python

- 安装tkinter，运行idle3时报错无法导入tkinter

  ```
  sudo pacman -S tk
  ```

- 安装pip

  ```
  sudo pacman -S python-pip   #此时安装的是python3的pip，pip版本跟python版本挂钩，python是3.10版本的，pip也是3.10版本的，如果想安装其他版本的pip，需要先安装其他版本的python，然后安装对应的pip版本，这样通过pip下载的py包就会放到对应版本的site-packages目录里面
  ```

  - 官网上寻找安装方法，打开python官网，点击最上面一行pypl，打开的界面上搜寻pip，点进去就能看到pip的介绍，然后可以看到安装方法。

###### 安装不同版本的python

- 在manjaro中启用AUR，启用过程在添加/删除软件->三个点->首选项->第三方->启用AUR支持

  - 在软件仓库中搜索python版本，例如python3.6搜寻python36，此时就能看到搜索结果，如果搜寻到，使用yay安装

    ```
    yay -S python36
    ```

  - 其是编译安装的，要注意提前安装make，gcc等工具

- 源码安装python

  - python官网下载源码tar.gz或者tar.xz文件，或者wget、curl下载源码

  - 解压缩文件

    ```
    tar -zxvf  gz文件
    tar -Jxvf  xz文件
    ```

  - 进入解压缩后的文件夹

    ```
    cd Python-3.8.13
    ```

  - 配置安装路径

    ```
    ./configure --prefix=/usr/lib/python3.8
    ```

    - manjaro下所有的都安装在/usr/lib下，其他版本的安装路径应该也在这里，最好看一下和其他版本的放在一起，容易管理。

    - manjaro下lib64和lib目录是一个，软连接过去的，其他的linux版本lib和lib64是不同的，manjaro有一个lib32目录是存的32位的，其他的linux 发行版没有lib32目录，lib目录就是32位的，这个有些区别

      ```shel
      ls -l                                                      
      总用量 312
      drwxr-xr-x   6 root root  90112  4月  6 17:04 bin
      drwxr-xr-x 506 root root  36864  4月  6 16:46 include
      drwxr-xr-x 240 root root 159744  4月  6 17:50 lib
      drwxr-xr-x   2 root root   4096  3月 14 17:39 lib32
      lrwxrwxrwx   1 root root      3 12月 18 23:21 lib64 -> lib
      drwxr-xr-x  11 root root   4096  3月 14 17:32 local
      lrwxrwxrwx   1 root root      3 12月 18 23:21 sbin -> bin
      drwxr-xr-x 278 root root  12288  4月  6 16:41 share
      drwxr-xr-x   2 root root   4096 12月 18 23:21 src
      ```

  - 编译和安装

    ```
    make && make install
    ```

  - 添加环境变量

    - 因为yay和pacman安装的python，其可执行程序都放在了/usr/bin下面，这样就不用自己管理配置环境变量了，因为/usr/bin就在PATH下，但是用源码安装的python可执行程序并没有放到/usr/bin下面。而是在/usr/lib/python3.8/bin下面，即自己配置的安装路径里面，这样就需要将环境变量添加上，这样才能找到可执行程序。

      ```
      export PATH=$PATH:/usr/lib/python3.8/bin
      ```

      - 这样是在此次终端中有效，如果在所有终端中有效，就需要将上面这句话放到配置文件中。~/.zshrc

- 为不同版本的python安装对应版本的pip

  ```
  python3.6 -m ensurepip --upgrade
  ```

  - 其中python是哪个版本的，前面就写python几点几

  - 这样使用pip就可以使用对应版本的pip3.6，使用pip3.6安装的py包放在python3.6目录里面，这样就隔离了不同版本的影响

    ```
    /usr/lib/python3.6/site-packages/numpy
    ```

  - 到时候使用import引入包，使用不同的python解释器去解释，就能区分开不同版本的包。

  - 注意，系统自己安装的python版本，例如我用的manjaro安装的是python3.10，其python安装在/usr/lib/python3.10里面，但是其通过pip安装的包在/home/lyl/.local/lib/python3.10/site-packages里面，这是系统自带的安装的，如果我们安装了其他版本的python，其都是在/usr/lib里面以不同版本的python来做目录区分的。例如上面的python3.6，但是源码安装的python在manjaro下也是在/home下，yay安装的在/usr/lib下，这个到时候使用的时候直接用find查找一下看一下具体在哪里就可以了，没有固定的具体的位置，不是死的。

##### vim

- 安装nodejs和npm

  ```
  sudo pacman -S nodejs
  sudo pacman -S npm
  ```

  - 临时使用配置源，不会影响到本地配置，在 npm install XXX 时加入--registry URL即可

    ```
    npm --registry https://registry.npm.taobao.org install express
    ```

  - 永久修改本地npm配置源

    ```
    npm config set registry https://registry.npm.taobao.org
    ```

  - 查看npm源地址有没有换成功：

    ```
    npm config get registry
    ```

  - 重置为官方源

    ```
    npm config set registry https://registry.npmjs.org/
    ```

  - coc.nvim用的是nodejs，其中coc的插件用的是npm来下载的，所以需要配置npm的源，如果可以翻墙就不需要配置了，如果翻不出去就配置成淘宝的源。

    - Node.js 是一个JavaScript 运行时，它让JavaScript 脱离了浏览器环境，可以直接在计算机上运行，极大地拓展了JavaScript 用途。

  - npm(Node.js Package Manager)是一个Node.js的包管理工具，用来解决Node.js代码部署问题。在安装Node.js时会自动安装相应的npm版本,不需要单独安装。使用npm包管理工具可以解决如下场景的需求。

    (1）从npm服务器下载别人编写的第三方包到本地使用。

    (2）从npm服务器下载并安装别人编写的命令程序到本地使用。

    (3）将自己编写的包或命令行程序上传到npm服务器供别人使用。

- 安装clang

  ```
  sudo pacman -S clang
  ```

- 安装ripgrep，文本搜索神器

  ```
  sudo pacman -S ripgrep
  ```

- 安装universal-ctags

  ```
  sudo pacman -S universal-ctags
  ```


##### 快捷键

- super键就是win键。

- 快速打开终端在gnome下没有设置，自己设置快捷键Ctrl+Alt+t

  ```
  其中命令为gnome-terminal，bin目录下有这个程序，是打开一个终端
  ```


###### 多任务和多窗口

- manjaro下有多任务（工作空间）的概念，类似于mac下可以设置窗口放到哪个任务里面，这样我们可以切换任务来达到操作不同窗口的概念。
  - 多任务的设置在设置->多任务->工作空间，里面有一个动态工作空间和固定数量的工作空间可以设置
  - 快捷键为super+数字键1234，来切换不同的任务，shift+super+数字键1234，来将窗口移动到不同的任务。这些在设置->键盘里面都可以设置。super+PgDn来切换到下一个任务，super+PgUp切换到上一个任务；shift+super+上下左右来将窗口切换到不同的显示器。除了上面shift+super+数字键将窗口移动到固定的任务，还可以直接将窗口向左向右切换到任务shift+super+PgDn，shift+super+PgUp，这样就不用切换到固定的任务了，因为在设置为动态工作空间下任务是不固定的。
  
- 多窗口的概念就是在一个任务上可以打开多个窗口，其中的快捷键为
  - super+左右来切换窗口分屏到左侧和右侧，super+q来关闭窗口，super+f用来切换全屏状态。这种是对于所有的窗口来说的。还有对于终端terminal来说的如下面
  
  - 在终端下有特殊的设置，我们可以来操作终端，这只是对终端有效
  
    ```
    新建窗口 shift+ctrl+n
    关闭窗口 shift+ctrl+q
    新建标签页 shift+ctrl+t
    关闭标签页 shift+ctrl+w
    复制 shift+ctrl+c
    粘贴 shift+ctrl+v
    ```
  
    ```
    切换到上一个标签页 ctrl+PgUp
    切换到下一个标签页 ctrl+PgDn
    移动标签页到左端 shift+ctrl+PgUp
    移动标签页到右端 shift+ctrl+PgDn
    切换到标签页1 Alt+1
    切换到标签页2 Alt+2
    ...... Alt+数字键
    ```
  
    
