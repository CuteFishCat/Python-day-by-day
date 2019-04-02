## 第一章 Linux 环境下Python开发环境搭建

### 第三节 CentOS7系统 下使用Pyenv 安装Python 环境

#### 1.3.1 Pyenv 介绍
&emsp;&emsp; Pyenv 是一款解决 Python 多版本环境使用的管理工具，它源自 rbenv 和  
ruby-build 。通过 pyenv 我们可以同时编译安装部署多个 Python 环境，方便  
多 python 版本开发调试项目。详细介绍可以访问 pyenv 项目主页:  
https://github.com/pyenv/pyenv  

#### 1.3.2 Linux 环境下安装 Pyenv
&emsp;&emsp; 安装 pyenv 比较简单 仅需将 pyenv 项目下载到当前用户家目录，然后配置  
指定的环境变量后即可使用。由于 pyenv 项目存放在 github 上，因此我们可以  
使用 git 命令 clone 到用户家目录。下面我们在 CentOS7 系统上用 python 用户  
演示一下安装的具体过程:
```bash
[python@localhost ~]$ su -l root
Password: 
Last login: Tue Apr  2 16:07:47 CST 2019 on pts/0
[root@localhost ~]# yum install git
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.163.com
 * extras: mirrors.cn99.com
 * updates: mirrors.cn99.com
Package git-1.8.3.1-20.el7.x86_64 already installed and latest version
Nothing to do
[root@localhost ~]# exit
logout
[python@localhost ~]$ git clone https://github.com/pyenv/pyenv.git .pyenv
Cloning into '.pyenv'...
remote: Enumerating objects: 81, done.
remote: Counting objects: 100% (81/81), done.
remote: Compressing objects: 100% (45/45), done.
remote: Total 16818 (delta 37), reused 61 (delta 28), pack-reused 16737
Receiving objects: 100% (16818/16818), 3.29 MiB | 463.00 KiB/s, done.
Resolving deltas: 100% (11379/11379), done.
[python@localhost ~]$ 
[python@localhost ~]$ ls -adl .pyenv
drwxrwxr-x. 11 python python 4096 Apr  2 16:13 .pyenv
[python@localhost ~]$ 
[python@localhost ~]$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
[python@localhost ~]$
[python@localhost ~]$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
[python@localhost ~]$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile 
[python@localhost ~]$ pyenv
bash: pyenv: command not found...
[python@localhost ~]$
[python@localhost ~]$ source .bash_profile 
[python@localhost ~]$ pyenv
pyenv 1.2.9-35-gb610909
Usage: pyenv <command> [<args>]

Some useful pyenv commands are:
   commands    List all available pyenv commands
   local       Set or show the local application-specific Python version
   global      Set or show the global Python version
   shell       Set or show the shell-specific Python version
   install     Install a Python version using python-build
   uninstall   Uninstall a specific Python version
   rehash      Rehash pyenv shims (run this after installing executables)
   version     Show the current Python version and its origin
   versions    List all Python versions available to pyenv
   which       Display the full path to an executable
   whence      List all Python versions that contain the given executable

See `pyenv help <command>' for information on a specific command.
For full documentation, see: https://github.com/pyenv/pyenv#readme
[python@localhost ~]$ 
```
上图中成功安装完成 Pyenv 

#### 1.3.3 使用 pyevn 编译安装 Python 环境

&emsp;&emsp; pyenv 的基础功能就是安装不同版本的 Python ，具体的选项为 `install`  
除了 install 选项以外，还有其他选项，详情可参考 [Pyevn 选项文档](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md) 。使用  
pyenv install --list 可以列出当前 pyenv 工具支持的 Python 版本，将 --list 改为  
具体的版本号后，可以完成具体 Python 环境的安装， 下面我们演示一下: 
```bash
[python@localhost ~]$ pyenv install --list
Available versions:
  2.1.3
  2.2.3
  2.3.7
  2.5.5
  2.5.6
  2.6.6
  2.6.7
  2.6.8
  2.6.9
  2.7.0
  2.7-dev
  2.7.1
  2.7.2
  2.7.3
  2.7.4
  2.7.5
  2.7.6
  2.7.7
  2.7.8
  2.7.9
  2.7.10
  2.7.11
  2.7.12
  2.7.13
  2.7.14
  2.7.15
  2.7.16
  3.0.1
  3.1.0
  3.4.2
  3.4.3
  3.4.4
  3.4.5
  3.4.6
  3.4.7
  3.4.8
  3.4.9
  3.5.0
  3.5-dev
  3.5.1
  3.5.2
  3.5.3
  3.5.4
  3.5.5
  3.5.6
  3.5.7
  3.6.0
  3.6-dev
  3.6.1
  3.6.2
  3.6.3
  3.6.4
  3.6.5
  3.6.6
  3.6.7

  .
  .省略部分具体版本......
  .

  pypy-2.1-src
  pypy-2.1
  pypy-5.3-src
  pypy-5.3
  stackless-2.7.10
  stackless-2.7.11
[python@localhost ~]$
[python@localhost ~]$ pyenv install -v 3.6.3
/tmp/python-build.20190402172510.109803 ~
Downloading Python-3.6.3.tar.xz...
-> https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tar.xz
/tmp/python-build.20190402172510.109803/Python-3.6.3 /tmp/python-build.20190402172510.109803 ~
Installing Python-3.6.3...
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for python3.6... no
checking for python3... no
checking for python... python
checking for --enable-universalsdk... no
checking for --with-universal-archs... no
checking MACHDEP... linux
checking for --without-gcc... no
checking for --with-icc... no
checking for gcc... no
checking for cc... no
checking for cl.exe... no
configure: error: in `/tmp/python-build.20190402172510.109803/Python-3.6.3':
configure: error: no acceptable C compiler found in $PATH
See `config.log' for more details

BUILD FAILED (CentOS Linux 7 using python-build 1.2.9-35-gb610909)

Inspect or clean up the working tree at /tmp/python-build.20190402172510.109803
Results logged to /tmp/python-build.20190402172510.109803.log

Last 10 log lines:
checking for --with-universal-archs... no
checking MACHDEP... linux
checking for --without-gcc... no
checking for --with-icc... no
checking for gcc... no
checking for cc... no
checking for cl.exe... no
configure: error: in `/tmp/python-build.20190402172510.109803/Python-3.6.3':
configure: error: no acceptable C compiler found in $PATH
See `config.log' for more details
[python@localhost ~]$ 
```


&emsp;&emsp;上图中使用 `pyevn install -v 3.6.3` 提示编译安装的错误信息，这是因为 pyevn  
底层安装 Python 环境是通过编译安装实现的，而我的系统中并未提供编译安装所依赖的软  
件包。那好，下面我们先在系统中安装完成编译 python 所依赖的所有软件包，如图:
```bash
[python@localhost ~]$ su -l root
Password: 
Last login: Tue Apr  2 16:24:02 CST 2019 on :0
[root@localhost ~]#
[root@localhost ~]# yum install -y gcc make patch gdbm-devel openssl-devel sqlite-devel readline-devel zlib-devel bzip2-devel ncurses-devel libffi-devel
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.163.com
 * extras: mirrors.cn99.com
 * updates: mirrors.cn99.com
Package gcc-4.8.5-36.el7_6.1.x86_64 already installed and latest version
Package 1:make-3.82-23.el7.x86_64 already installed and latest version
Package patch-2.7.1-10.el7_5.x86_64 already installed and latest version
Package gdbm-devel-1.10-8.el7.x86_64 already installed and latest version
Package 1:openssl-devel-1.0.2k-16.el7_6.1.x86_64 already installed and latest version
Package sqlite-devel-3.7.17-8.el7.x86_64 already installed and latest version
Package readline-devel-6.2-10.el7.x86_64 already installed and latest version
Package zlib-devel-1.2.7-18.el7.x86_64 already installed and latest version
Package bzip2-devel-1.0.6-13.el7.x86_64 already installed and latest version
Package ncurses-devel-5.9-14.20130511.el7_4.x86_64 already installed and latest version
Package libffi-devel-3.0.13-18.el7.x86_64 already installed and latest version
Nothing to do
[root@localhost ~]# exit
logout
[python@localhost ~]$
[python@localhost ~]$ pyenv install -v 3.6.3
/tmp/python-build.20190402174323.1818 ~
Downloading Python-3.6.3.tar.xz...
-> https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tar.xz
.
.省略编译安装具体过程
.
fi
rm -f /home/python/.pyenv/versions/3.6.3/share/man/man1/python3.1
(cd /home/python/.pyenv/versions/3.6.3/share/man/man1; ln -s python3.6.1 python3.1)
if test "xupgrade" != "xno"  ; then \
	case upgrade in \
		upgrade) ensurepip="--upgrade" ;; \
		install|*) ensurepip="" ;; \
	esac; \
	 ./python -E -m ensurepip \
		$ensurepip --root=/ ; \
fi
Collecting setuptools
Collecting pip
Installing collected packages: setuptools, pip
Successfully installed pip-9.0.1 setuptools-28.8.0
Installed Python-3.6.3 to /home/python/.pyenv/versions/3.6.3

/tmp/python-build.20190402174323.1818 ~
~
[python@localhost ~]$
```
>上图中顺利完成 python3.6.3 这个版本的安装工作。



&emsp;&emsp;上面我们演示了通过 pyenv 成功的安装了 python3.6.3，那我们如何  
查看刚安装完成的 python 呢 ？下面介绍一下 pyevn 的 versions 选项:
```bash
[python@localhost ~]$ pyenv  versions --help
Usage: pyenv versions [--bare] [--skip-aliases]

Lists all Python versions found in `$PYENV_ROOT/versions/*'.

[python@localhost ~]$
```
versions 可以列出 pyenv 安装的所有 python 版本，具体位置在 pyenv 的 versions  
文件夹下，我们可以进入该文件里查看一下，如图:
```bash
[python@localhost ~]$ pwd
/home/python
[python@localhost ~]$ cd .pyenv/
[python@localhost .pyenv]$ ll
total 204
drwxrwxr-x. 2 python python   4096 Apr  2 16:27 bin
-rw-rw-r--. 1 python python  25848 Apr  2 16:27 CHANGELOG.md
-rw-rw-r--. 1 python python   7522 Apr  2 16:27 COMMANDS.md
drwxrwxr-x. 2 python python   4096 Apr  2 16:27 completions
-rw-rw-r--. 1 python python   3390 Apr  2 16:27 CONDUCT.md
drwxrwxr-x. 2 python python   4096 Apr  2 16:27 libexec
-rw-rw-r--. 1 python python   1092 Apr  2 16:27 LICENSE
-rw-rw-r--. 1 python python    406 Apr  2 16:27 Makefile
drwxrwxr-x. 3 python python   4096 Apr  2 16:27 plugins
drwxrwxr-x. 4 python python   4096 Apr  2 16:27 pyenv.d
-rw-rw-r--. 1 python python  15752 Apr  2 16:27 README.md
drwxrwxr-x. 2 python python   4096 Apr  2 17:46 shims
drwxrwxr-x. 2 python python   4096 Apr  2 16:27 src
-rw-rw-r--. 1 python python 104764 Apr  2 16:27 terminal_output.png
drwxrwxr-x. 3 python python   4096 Apr  2 16:27 test
drwxrwxr-x. 3 python python   4096 Apr  2 17:43 versions
[python@localhost .pyenv]$ cd versions/
[python@localhost versions]$ ll
total 4
drwxr-xr-x. 6 python python 4096 Apr  2 17:46 3.6.3
[python@localhost versions]$ cd 3.6.3/
[python@localhost 3.6.3]$ ll
total 16
drwxr-xr-x. 2 python python 4096 Apr  2 17:46 bin
drwxr-xr-x. 3 python python 4096 Apr  2 17:46 include
drwxr-xr-x. 4 python python 4096 Apr  2 17:46 lib
drwxr-xr-x. 3 python python 4096 Apr  2 17:46 share
[python@localhost 3.6.3]$ cd bin/
[python@localhost bin]$ ll
total 24808
lrwxrwxrwx. 1 python python        8 Apr  2 17:46 2to3 -> 2to3-3.6
-rwxrwxr-x. 1 python python      125 Apr  2 17:46 2to3-3.6
lrwxrwxrwx. 1 python python       16 Apr  2 17:46 easy_install -> easy_install-3.6
-rwxrwxr-x. 1 python python      266 Apr  2 17:46 easy_install-3.6
lrwxrwxrwx. 1 python python        7 Apr  2 17:46 idle -> idle3.6
lrwxrwxrwx. 1 python python        7 Apr  2 17:46 idle3 -> idle3.6
-rwxrwxr-x. 1 python python      123 Apr  2 17:46 idle3.6
lrwxrwxrwx. 1 python python        6 Apr  2 17:46 pip -> pip3.6
-rwxrwxr-x. 1 python python      238 Apr  2 17:46 pip3
-rwxrwxr-x. 1 python python      238 Apr  2 17:46 pip3.6
lrwxrwxrwx. 1 python python        8 Apr  2 17:46 pydoc -> pydoc3.6
lrwxrwxrwx. 1 python python        8 Apr  2 17:46 pydoc3 -> pydoc3.6
-rwxrwxr-x. 1 python python      108 Apr  2 17:46 pydoc3.6
lrwxrwxrwx. 1 python python        9 Apr  2 17:46 python -> python3.6
lrwxrwxrwx. 1 python python        9 Apr  2 17:46 python3 -> python3.6
-rwxr-xr-x. 2 python python 12650352 Apr  2 17:45 python3.6
lrwxrwxrwx. 1 python python       17 Apr  2 17:46 python3.6-config -> python3.6m-config
-rwxr-xr-x. 1 python python    63994 Apr  2 17:46 python3.6-gdb.py
-rwxr-xr-x. 2 python python 12650352 Apr  2 17:45 python3.6m
-rwxr-xr-x. 1 python python     3141 Apr  2 17:46 python3.6m-config
lrwxrwxrwx. 1 python python       16 Apr  2 17:46 python3-config -> python3.6-config
lrwxrwxrwx. 1 python python       16 Apr  2 17:46 python-config -> python3.6-config
lrwxrwxrwx. 1 python python       10 Apr  2 17:46 pyvenv -> pyvenv-3.6
-rwxrwxr-x. 1 python python      465 Apr  2 17:46 pyvenv-3.6
[python@localhost bin]$ cd
[python@localhost ~]$ 
```
通过上图，我们发现，pyenv 将编译安装的具体版本 python 程序直接安装到了 pyenv 的  
versions 目录下。 下面我们使用 pyenv 的 versions 选项命令 查看 pyenv 下都安装了哪些  
具体的版本，如图:
```bash
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.6.3
[python@localhost ~]$ 
[python@localhost ~]$ python -V
Python 2.7.5
[python@localhost ~]$
```
上图中 pyenv versions 命令执行后返回了两个 python 版本，system 代表 CentOS7 系统自带  
的 python2.7 版本， 3.6.3 代表我们之前通过 pyenv 安装的 python3.6.3 版本。system 前面的  
`*` 代表当前 shell 环境生效的 python 版本。

&emsp;&emsp; 现在我们可以方便的使用 pyenv 安装各种版本，当然之后也可以使用 uninstall 选项删除之  
前安装的具体版本，比如我们先安装一个 python3.6.6 然后再使用 `pyenv uninstall 3.6.3` ,  
演示过程如下:
```bash
[python@localhost ~]$ pyenv install 3.6.6
Downloading Python-3.6.6.tar.xz...
-> https://www.python.org/ftp/python/3.6.6/Python-3.6.6.tar.xz
Installing Python-3.6.6...
Installed Python-3.6.6 to /home/python/.pyenv/versions/3.6.6

[python@localhost ~]$ 
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.6.3
  3.6.6
[python@localhost ~]$ pyenv uninstall 3.6.3
pyenv: remove /home/python/.pyenv/versions/3.6.3? y
[python@localhost ~]$ 
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.6.6
[python@localhost ~]$
```

#### 1.3.4 使用 Pyenv 管理的指定 python 版本

