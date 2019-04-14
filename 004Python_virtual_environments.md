## 第一章 Linux 环境下Python开发环境搭建

### 第四节 Python 虚拟环境

#### 1.4.1 虚拟环境和 virtualenv 概述

&emsp;&emsp; 上一节中我们可以使用 pyenv 完成不同 python 版本的安装和切换，极大  
的提升了环境部署的效率。但是在 python 软件开发的过程中，还有一个问题需  
要解决`----软件包依赖`。 默认情况下，我们使用 pip 会将新安装的 python 软件  
包安装到指定路径下，但是实际情况是每个项目所用到的软件包和具体的软件包  
版本一般不相同，有的时候会产生冲突。出于解决软件包依赖管理和软件工程项  
目管理的目的，我们希望每个项目都有一个单独的目录存放自己依赖的软件包，  
这时候，虚拟环境的概念就产生了。我们需要一个工具可以完成上面的需求，即  
可以使用具体 python 版本，同时将软件包依赖单独放置特定文件系统路径下，而  
非 python 的默认路径下。 virtualenv 就可以完成这个功能。virtualenv 本身是一个  
python 软件包，我们可以访问 [pypi](https://pypi.org) 获取相关信息。


#### 1.4.2 pip 和 virtualenv 安装
&emsp;&emsp;上文中说过，virtualenv 是一个 python 的软件包，我们使用 pip 直接安装即可，  
那么我们使用哪个 python 版本安装 virtualenv 呢，一般建议使用平时主要使用的  
python 版本即可，也可使用系统默认的 python 版本。这里我们使用 CentOS7 自带  
的 python2.7.5 来安装，如图:
```bash
[python@localhost ~]$ python -V
Python 2.7.5
[python@localhost ~]$ pip install virtualenv
bash: pip: command not found...
[python@localhost ~]$ 
[python@localhost ~]$ 
[python@localhost ~]$ su -l root
Password: 
Last login: Tue Apr  9 16:13:52 CST 2019 on :0
[root@localhost ~]# wget https://files.pythonhosted.org/packages/ed/69/c805067de1feedbb98c53174b0f2df44cc05e0e9ee73bb85eebc59e508c6/setuptools-41.0.0.zip
--2019-04-09 16:17:24--  https://files.pythonhosted.org/packages/ed/69/c805067de1feedbb98c53174b0f2df44cc05e0e9ee73bb85eebc59e508c6/setuptools-41.0.0.zip
Resolving files.pythonhosted.org (files.pythonhosted.org)... 151.101.109.63, 2a04:4e42:1a::319
Connecting to files.pythonhosted.org (files.pythonhosted.org)|151.101.109.63|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 848208 (828K) [binary/octet-stream]
Saving to: ‘setuptools-41.0.0.zip’

100%[=====================================================================================>] 848,208      992KB/s   in 0.8s   

2019-04-09 16:17:26 (992 KB/s) - ‘setuptools-41.0.0.zip’ saved [848208/848208]

[root@localhost ~]# unzip setuptools-41.0.0.zip 
Archive:  setuptools-41.0.0.zip
  inflating: setuptools-41.0.0/bootstrap.py  
  inflating: setuptools-41.0.0/README.rst  
  inflating: setuptools-41.0.0/setup.py  
  inflating: setuptools-41.0.0/msvc-build-launcher.cmd  
  inflating: setuptools-41.0.0/towncrier_template.rst  
  .
  .省略解压过程。。。。。。
  .
  inflating: setuptools-41.0.0/setuptools.egg-info/dependency_links.txt  
  inflating: setuptools-41.0.0/setuptools.egg-info/entry_points.txt  
  inflating: setuptools-41.0.0/setuptools.egg-info/SOURCES.txt  
[root@localhost ~]# ll
total 876
-rw-------. 1 root root   1866 Jan  4 22:24 anaconda-ks.cfg
drwxr-xr-x. 2 root root   4096 Jan  4 22:30 Desktop
drwxr-xr-x. 2 root root   4096 Jan  4 22:30 Documents
drwxr-xr-x. 2 root root   4096 Jan  4 22:30 Downloads
-rw-r--r--. 1 root root   1914 Jan  4 22:27 initial-setup-ks.cfg
drwxr-xr-x. 2 root root   4096 Jan  4 22:30 Music
drwxr-xr-x. 2 root root   4096 Jan  4 22:30 Pictures
drwxr-xr-x. 2 root root   4096 Jan  4 22:30 Public
drwxr-xr-x. 7 root root   4096 Apr  9 16:17 setuptools-41.0.0
-rw-r--r--. 1 root root 848208 Apr  6 01:33 setuptools-41.0.0.zip
drwxr-xr-x. 2 root root   4096 Jan  4 22:30 Templates
drwxr-xr-x. 2 root root   4096 Jan  4 22:30 Videos
[root@localhost ~]#
[root@localhost ~]# cd setuptools-41.0.0/
[root@localhost ~]#
[root@localhost setuptools-41.0.0]# python setup.py install
running install
running bdist_egg
running egg_info
writing requirements to setuptools.egg-info/requires.txt
writing setuptools.egg-info/PKG-INFO
writing top-level names to setuptools.egg-info/top_level.txt
writing dependency_links to setuptools.egg-info/dependency_links.txt
writing entry points to setuptools.egg-info/entry_points.txt
reading manifest file 'setuptools.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
warning: no previously-included files found matching 'pyproject.toml'
writing manifest file 'setuptools.egg-info/SOURCES.txt'
installing library code to build/bdist.linux-x86_64/egg
running install_lib
running build_py
creating build
creating build/lib
copying easy_install.py -> build/lib
creating build/lib/pkg_resources
copying pkg_resources/__init__.py -> build/lib/pkg_resources
copying pkg_resources/py31compat.py -> build/lib/pkg_resources
creating build/lib/setuptools
copying setuptools/version.py -> build/lib/setuptools
copying setuptools/py33compat.py -> build/lib/setuptools
copying setuptools/msvc.py -> build/lib/setuptools
copying setuptools/extension.py -> build/lib/setuptools

creating build/bdist.linux-x86_64/egg/EGG-INFO
copying setuptools.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying setuptools.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying setuptools.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying setuptools.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying setuptools.egg-info/requires.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying setuptools.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying setuptools.egg-info/zip-safe -> build/bdist.linux-x86_64/egg/EGG-INFO
creating dist
creating 'dist/setuptools-41.0.0-py2.7.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing setuptools-41.0.0-py2.7.egg
Copying setuptools-41.0.0-py2.7.egg to /usr/lib/python2.7/site-packages
Adding setuptools 41.0.0 to easy-install.pth file
Installing easy_install script to /usr/bin
Installing easy_install-2.7 script to /usr/bin
.
.省略安装过程。。。。
.
Installed /usr/lib/python2.7/site-packages/setuptools-41.0.0-py2.7.egg
Processing dependencies for setuptools==41.0.0
Finished processing dependencies for setuptools==41.0.0
[root@localhost setuptools-41.0.0]# cd ..
[root@localhost ~]# 
[root@localhost ~]# 
[root@localhost ~]# wget https://files.pythonhosted.org/packages/36/fa/51ca4d57392e2f69397cd6e5af23da2a8d37884a605f9e3f2d3bfdc48397/pip-19.0.3.tar.gz
--2019-04-09 16:18:50--  https://files.pythonhosted.org/packages/36/fa/51ca4d57392e2f69397cd6e5af23da2a8d37884a605f9e3f2d3bfdc48397/pip-19.0.3.tar.gz
Resolving files.pythonhosted.org (files.pythonhosted.org)... 151.101.109.63, 2a04:4e42:36::319
Connecting to files.pythonhosted.org (files.pythonhosted.org)|151.101.109.63|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1324617 (1.3M) [binary/octet-stream]
Saving to: ‘pip-19.0.3.tar.gz’

100%[=====================================================================================>] 1,324,617    915KB/s   in 1.4s   

2019-04-09 16:18:57 (915 KB/s) - ‘pip-19.0.3.tar.gz’ saved [1324617/1324617]

[root@localhost ~]# ls
anaconda-ks.cfg  Documents  initial-setup-ks.cfg  Pictures           Public             setuptools-41.0.0.zip  Videos
Desktop          Downloads  Music                 pip-19.0.3.tar.gz  setuptools-41.0.0  Templates
[root@localhost ~]# tar xf pip-19.0.3.tar.gz 
[root@localhost ~]# ll
total 2176
-rw-------. 1 root root     1866 Jan  4 22:24 anaconda-ks.cfg
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Desktop
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Documents
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Downloads
-rw-r--r--. 1 root root     1914 Jan  4 22:27 initial-setup-ks.cfg
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Music
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Pictures
drwxr-xr-x. 4  501 games    4096 Feb 21 01:14 pip-19.0.3
-rw-r--r--. 1 root root  1324617 Feb 21 01:23 pip-19.0.3.tar.gz
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Public
drwxr-xr-x. 9 root root     4096 Apr  9 16:18 setuptools-41.0.0
-rw-r--r--. 1 root root   848208 Apr  6 01:33 setuptools-41.0.0.zip
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Templates
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Videos
[root@localhost ~]# 
[root@localhost ~]# cd pip-19.0.3/
[root@localhost pip-19.0.3]# python setup.py install
/usr/lib64/python2.7/distutils/dist.py:267: UserWarning: Unknown distribution option: 'python_requires'
  warnings.warn(msg)
running install
running bdist_egg
running egg_info
writing src/pip.egg-info/PKG-INFO
writing top-level names to src/pip.egg-info/top_level.txt
writing dependency_links to src/pip.egg-info/dependency_links.txt
writing entry points to src/pip.egg-info/entry_points.txt
reading manifest file 'src/pip.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
warning: no files found matching 'docs/docutils.conf'
warning: no previously-included files found matching '.coveragerc'
.
.安装过程省略。。。。。
.
byte-compiling build/bdist.linux-x86_64/egg/pip/_internal/build_env.py to build_env.pyc
creating build/bdist.linux-x86_64/egg/EGG-INFO
copying src/pip.egg-info/PKG-INFO -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/pip.egg-info/SOURCES.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/pip.egg-info/dependency_links.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/pip.egg-info/entry_points.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/pip.egg-info/not-zip-safe -> build/bdist.linux-x86_64/egg/EGG-INFO
copying src/pip.egg-info/top_level.txt -> build/bdist.linux-x86_64/egg/EGG-INFO
creating dist
creating 'dist/pip-19.0.3-py2.7.egg' and adding 'build/bdist.linux-x86_64/egg' to it
removing 'build/bdist.linux-x86_64/egg' (and everything under it)
Processing pip-19.0.3-py2.7.egg
creating /usr/lib/python2.7/site-packages/pip-19.0.3-py2.7.egg
Extracting pip-19.0.3-py2.7.egg to /usr/lib/python2.7/site-packages
Adding pip 19.0.3 to easy-install.pth file
Installing pip script to /usr/bin
Installing pip2.7 script to /usr/bin
Installing pip2 script to /usr/bin

Installed /usr/lib/python2.7/site-packages/pip-19.0.3-py2.7.egg
Processing dependencies for pip==19.0.3
Finished processing dependencies for pip==19.0.3
[root@localhost pip-19.0.3]# cd
[root@localhost ~]# pwd
/root
[root@localhost ~]# pip install virtualenv
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won’t be maintained after that date. A future version of pip will drop support for Python 2.7.
Collecting virtualenv
  Downloading https://files.pythonhosted.org/packages/33/5d/314c760d4204f64e4a968275182b7751bd5c3249094757b39ba987dcfb5a/virtualenv-16.4.3-py2.py3-none-any.whl (2.0MB)
    100% |████████████████████████████████| 2.0MB 3.9MB/s 
Installing collected packages: virtualenv
Successfully installed virtualenv-16.4.3
[root@localhost ~]# exit
logout
[python@localhost ~]$ whereis virtualenv
virtualenv: /usr/bin/virtualenv
[python@localhost ~]$ 
```
上图中因为 CentOS7 系统自带的 python2.7.5 没有 pip 命令，所以我们先手动下  
载依赖的软件包并完成 pip 的安装工作。安装完 pip 后，使用 pip 再安装 virtualenv  

&emsp;&emsp;除了手动安装 pip 以外，我们还可以使用 yum 安装 epel 仓库中的 python2-pip 软件  
包，由于手动安装默认会安装到 /usr/bin 下，所以如果使用 CentOS7 默认的 python2.7.5  
版本，建议还是使用 yum 完成 pip 的安装工作。下面我们恢复虚拟机快照，重新再来一  
次，如图:
```bash
[python@localhost ~]$ 
[python@localhost ~]$ su -l root
Password: 
Last login: Tue Apr  9 17:30:26 CST 2019 on :0
[root@localhost ~]#
[root@localhost ~]# yum install python2-pip
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.huaweicloud.com
 * epel: mirror.premi.st
 * extras: mirror.jdcloud.com
 * updates: mirror.jdcloud.com
Resolving Dependencies
--> Running transaction check
---> Package python2-pip.noarch 0:8.1.2-8.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=============================================================================================================================
 Package                         Arch                       Version                           Repository                Size
=============================================================================================================================
Installing:
 python2-pip                     noarch                     8.1.2-8.el7                       epel                     1.7 M

Transaction Summary
=============================================================================================================================
Install  1 Package

Total download size: 1.7 M
Installed size: 7.2 M
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/x86_64/7/epel/packages/python2-pip-8.1.2-8.el7.noarch.rpm: Header V3 RSA/SHA256 Signature, key ID 352c64e5: NOKEY
Public key for python2-pip-8.1.2-8.el7.noarch.rpm is not installed
python2-pip-8.1.2-8.el7.noarch.rpm                                                                    | 1.7 MB  00:00:01     
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Importing GPG key 0x352C64E5:
 Userid     : "Fedora EPEL (7) <epel@fedoraproject.org>"
 Fingerprint: 91e9 7d7c 4a5e 96f1 7f3e 888f 6a2f aea2 352c 64e5
 Package    : epel-release-7-11.noarch (@extras)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : python2-pip-8.1.2-8.el7.noarch                                                                            1/1 
  Verifying  : python2-pip-8.1.2-8.el7.noarch                                                                            1/1 

Installed:
  python2-pip.noarch 0:8.1.2-8.el7                                                                                           

Complete!
[root@localhost ~]# rpm -ql python2-pip
/usr/bin/pip
/usr/bin/pip2
/usr/bin/pip2.7
/usr/lib/python2.7/site-packages/pip
.
.省略部分显示信息。。。。。。
.
/usr/share/doc/python2-pip-8.1.2/docs/usage.rst
/usr/share/doc/python2-pip-8.1.2/docs/user_guide.rst
/usr/share/licenses/python2-pip-8.1.2
/usr/share/licenses/python2-pip-8.1.2/LICENSE.txt
[root@localhost ~]#
[root@localhost ~]# pip --version
pip 8.1.2 from /usr/lib/python2.7/site-packages (python 2.7)
[root@localhost ~]# pip2 --version
pip 8.1.2 from /usr/lib/python2.7/site-packages (python 2.7)
[root@localhost ~]# 
[root@localhost ~]# pip install --upgrade pip
Collecting pip
  Downloading https://files.pythonhosted.org/packages/d8/f3/413bab4ff08e1fc4828dfc59996d721917df8e8583ea85385d51125dceff/pip-19.0.3-py2.py3-none-any.whl (1.4MB)
    100% |████████████████████████████████| 1.4MB 973kB/s 
Installing collected packages: pip
  Found existing installation: pip 8.1.2
    Uninstalling pip-8.1.2:
      Successfully uninstalled pip-8.1.2
Successfully installed pip-19.0.3
[root@localhost ~]# ls -al /usr/bin/pip*
-rwxr-xr-x. 1 root root 215 Apr  9 17:01 /usr/bin/pip
-rwxr-xr-x. 1 root root 215 Apr  9 17:01 /usr/bin/pip2
-rwxr-xr-x. 1 root root 215 Apr  9 17:01 /usr/bin/pip2.7
[root@localhost ~]# pip --version
pip 19.0.3 from /usr/lib/python2.7/site-packages/pip (python 2.7)
[root@localhost ~]# 
[root@localhost ~]# pip2 --version
pip 19.0.3 from /usr/lib/python2.7/site-packages/pip (python 2.7)
[root@localhost ~]# 
[root@localhost ~]# pip install virtualenv
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won‘t be maintained after that date. A future version of pip will drop support for Python 2.7.
Collecting virtualenv
  Downloading https://files.pythonhosted.org/packages/33/5d/314c760d4204f64e4a968275182b7751bd5c3249094757b39ba987dcfb5a/virtualenv-16.4.3-py2.py3-none-any.whl (2.0MB)
    100% |████████████████████████████████| 2.0MB 1.3MB/s 
Installing collected packages: virtualenv
Successfully installed virtualenv-16.4.3
[root@localhost ~]# whereis virtualenv
virtualenv: /usr/bin/virtualenv
[root@localhost ~]# exit
logout
[python@localhost ~]$ 
```

#### 1.4.3 virtualenv 基本使用

&emsp;&emsp;上一小节中我们成功的在 CentOS7 中安装了 pip 和 virtualenv，下面  
我们介绍一下 virtualenv 使用方法。下面我们直接使用 virtualenv 命令创  
建 python2.7.5 的环境目录 venv，如图:
```bash
[python@localhost ~]$ ll
total 32
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Desktop
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Documents
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Downloads
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Music
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Pictures
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Public
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Templates
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Videos
[python@localhost ~]$ mkdir project
[python@localhost ~]$ cd project/
[python@localhost project]$ virtualenv venv
  No LICENSE.txt / LICENSE found in source
New python executable in /home/python/project/venv/bin/python2
Also creating executable in /home/python/project/venv/bin/python
Installing setuptools, pip, wheel...
done.
[python@localhost project]$ ll
total 4
drwxrwxr-x. 5 python python 4096 Apr  9 17:55 venv
[python@localhost project]$ source venv/bin/activate
(venv) [python@localhost project]$ python -V
Python 2.7.5
(venv) [python@localhost project]$
(venv) [python@localhost project]$ deactivate
[python@localhost project]$ 
[python@localhost project]$
```
上图中我们使用 python2.7.5 中的 virtualenv 工具成功的在 project 目录中创建  
了 venv 虚拟环境目录，然后使用 venv 目录中 bin 下的 activate 脚本，将当前  
系统 python 切换到 venv 目录 bin 的 python 解析器，当不想使用这个 venv 时  
可以使用 deactivate 命令取消当前 venv 中的 python 环境，回到系统目录的  
python 环境下。



下面我们使用刚才创建好的 venv 虚拟环境目录，用 pip 安装 jupyter，如图:
```bash
[python@localhost ~]$ source project/venv/bin/activate
(venv) [python@localhost ~]$ pip install jupyter
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 wontt be maintained after that date. A future version of pip will drop support for Python 2.7.
Collecting jupyter
  Downloading https://files.pythonhosted.org/packages/83/df/0f5dd132200728a86190397e1ea87cd76244e42d39ec5e88efd25b2abd7e/jupyter-1.0.0-py2.py3-none-any.whl
.
.省略部分安装信息。。。。。
.
Successfully installed MarkupSafe-1.1.1 Send2Trash-1.5.0 attrs-19.1.0 backports-abc-0.5 backports.shutil-get-terminal-size-1.0.0 bleach-3.1.0 configparser-3.7.4 decorator-4.4.0 defusedxml-0.5.0 entrypoints-0.3 enum34-1.1.6 functools32-3.2.3.post2 futures-3.2.0 ipaddress-1.0.22 ipykernel-4.10.0 ipython-5.8.0 ipython-genutils-0.2.0 ipywidgets-7.4.2 jinja2-2.10.1 jsonschema-3.0.1 jupyter-1.0.0 jupyter-client-5.2.4 jupyter-console-5.2.0 jupyter-core-4.4.0 mistune-0.8.4 nbconvert-5.4.1 nbformat-4.4.0 notebook-5.7.8 pandocfilters-1.4.2 pathlib2-2.3.3 pexpect-4.7.0 pickleshare-0.7.5 prometheus-client-0.6.0 prompt-toolkit-1.0.15 ptyprocess-0.6.0 pygments-2.3.1 pyrsistent-0.14.11 python-dateutil-2.8.0 pyzmq-18.0.1 qtconsole-4.4.3 scandir-1.10.0 simplegeneric-0.8.1 singledispatch-3.4.0.3 six-1.12.0 terminado-0.8.2 testpath-0.4.2 tornado-5.1.1 traitlets-4.3.2 wcwidth-0.1.7 webencodings-0.5.1 widgetsnbextension-3.4.2
(venv) [python@localhost ~]$
(venv) [python@localhost ~]$ jupyter notebook
[I 21:30:32.365 NotebookApp] Writing notebook server cookie secret to /run/user/1001/jupyter/notebook_cookie_secret
[I 21:30:32.604 NotebookApp] Serving notebooks from local directory: /home/python
[I 21:30:32.604 NotebookApp] The Jupyter Notebook is running at:
[I 21:30:32.604 NotebookApp] http://localhost:8888/?token=10306e5c41c7a8782acd73c40e702f49420ccff741ee86b1
[I 21:30:32.604 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 21:30:32.609 NotebookApp] 
    
    To access the notebook, open this file in a browser:
        file:///run/user/1001/jupyter/nbserver-53736-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=10306e5c41c7a8782acd73c40e702f49420ccff741ee86b1
^C[I 21:30:44.634 NotebookApp] interrupted
Serving notebooks from local directory: /home/python
0 active kernels
The Jupyter Notebook is running at:
http://localhost:8888/?token=10306e5c41c7a8782acd73c40e702f49420ccff741ee86b1
Shutdown this notebook server (y/[n])? y
[C 21:30:46.373 NotebookApp] Shutdown confirmed
[I 21:30:46.374 NotebookApp] Shutting down 0 kernels
(venv) [python@localhost ~]$
(venv) [python@localhost ~]$ deactivate
[python@localhost ~]$ 
[python@localhost ~]$ jupyter notebook
bash: jupyter: command not found...
[python@localhost ~]$
```
上图中，我们在 venv 环境目录内安装了 jupyter 并且成功运行，退出 venv 环境后，再次  
运行 jupyter notebook 报错，说明 jupyter 确实安装到了 venv 的环境目录中，系统自带的   
python2.7.5 中并没有安装，所以无法运行。

&emsp;&emsp;之前我们创建的 venv 是根据系统中 python2.7.5 创建的，目前大家使用的都是 python3  
版本，下面我们使用第一章编译安装的方式，手动编译安装一个 python3.7.3 版本，如图:
```bash
[python@localhost ~]$ su -l root
Password: 
Last login: Tue Apr  9 21:45:23 CST 2019 on pts/0
[root@localhost ~]# yum install -y gcc make patch gdbm-devel openssl-devel sqlite-devel readline-devel zlib-devel bzip2-devel ncurses-devel libffi-devel
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.nwsuaf.edu.cn
 * epel: mirrors.tuna.tsinghua.edu.cn
 * extras: mirrors.nwsuaf.edu.cn
 * updates: mirrors.njupt.edu.cn
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
[root@localhost ~]# yum install lftp
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.nwsuaf.edu.cn
 * epel: mirrors.tuna.tsinghua.edu.cn
 * extras: mirrors.nwsuaf.edu.cn
 * updates: mirrors.njupt.edu.cn
Package lftp-4.4.8-11.el7.x86_64 already installed and latest version
Nothing to do
[root@localhost ~]# lftp 172.20.0.1/pub
cd ok, cwd=/pub                                  
lftp 172.20.0.1:/pub> cd software/
lftp 172.20.0.1:/pub/software> mget Python-3.7.3.tar.xz 
17108364 bytes transferred in 2 seconds (9.33M/s)                        
lftp 172.20.0.1:/pub/software> exit
[root@localhost ~]# ll
total 16748
-rw-------. 1 root root     1866 Jan  4 22:24 anaconda-ks.cfg
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Desktop
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Documents
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Downloads
-rw-r--r--. 1 root root     1914 Jan  4 22:27 initial-setup-ks.cfg
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Music
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Pictures
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Public
-rw-r--r--. 1 root root 17108364 Mar 26 04:59 Python-3.7.3.tar.xz
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Templates
drwxr-xr-x. 2 root root     4096 Jan  4 22:30 Videos
[root@localhost ~]# tar xf Python-3.7.3.tar.xz 
[root@localhost ~]# ll
total 16752
-rw-------.  1 root root     1866 Jan  4 22:24 anaconda-ks.cfg
drwxr-xr-x.  2 root root     4096 Jan  4 22:30 Desktop
drwxr-xr-x.  2 root root     4096 Jan  4 22:30 Documents
drwxr-xr-x.  2 root root     4096 Jan  4 22:30 Downloads
-rw-r--r--.  1 root root     1914 Jan  4 22:27 initial-setup-ks.cfg
drwxr-xr-x.  2 root root     4096 Jan  4 22:30 Music
drwxr-xr-x.  2 root root     4096 Jan  4 22:30 Pictures
drwxr-xr-x.  2 root root     4096 Jan  4 22:30 Public
drwxr-xr-x. 18  501  501     4096 Mar 26 04:59 Python-3.7.3
-rw-r--r--.  1 root root 17108364 Mar 26 04:59 Python-3.7.3.tar.xz
drwxr-xr-x.  2 root root     4096 Jan  4 22:30 Templates
drwxr-xr-x.  2 root root     4096 Jan  4 22:30 Videos
[root@localhost ~]# cd Python-3.7.3/
[root@localhost Python-3.7.3]# 
[root@localhost Python-3.7.3]# 
[root@localhost Python-3.7.3]# ./configure --prefix=/usr/local/python3.7.3
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for python3.7... no
checking for python3... no
checking for python... python
checking for --enable-universalsdk... no
.
.省略安装过程信息。。。。。
.
config.status: creating pyconfig.h
creating Modules/Setup
creating Modules/Setup.local
creating Makefile


If you want a release build with all stable optimizations active (PGO, etc),
please run ./configure --enable-optimizations


[root@localhost Python-3.7.3]#
[root@localhost Python-3.7.3]# make
.
.省略编译过程信息。。。。。
.
renaming build/scripts-3.7/2to3 to build/scripts-3.7/2to3-3.7
renaming build/scripts-3.7/pyvenv to build/scripts-3.7/pyvenv-3.7
/bin/install -c -m 644 ./Tools/gdb/libpython.py python-gdb.py
gcc -pthread -c -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall    -std=c99 -Wextra -Wno-unused-result -Wno-unused-parameter -Wno-missing-field-initializers -Werror=implicit-function-declaration   -I. -I./Include    -DPy_BUILD_CORE -o Programs/_testembed.o ./Programs/_testembed.c
gcc -pthread     -Xlinker -export-dynamic -o Programs/_testembed Programs/_testembed.o libpython3.7m.a -lcrypt -lpthread -ldl  -lutil   -lm  
sed -e "s,@EXENAME@,/usr/local/python3.7.3/bin/python3.7m," < ./Misc/python-config.in >python-config.py
LC_ALL=C sed -e 's,\$(\([A-Za-z0-9_]*\)),\$\{\1\},g' < Misc/python-config.sh >python-config
[root@localhost Python-3.7.3]# 
[root@localhost Python-3.7.3]# make install
.
.省略编译安装过程信息。。。。。
.
if test "x" != "x" ; then \
	rm -f /usr/local/python3.7.3/bin/python3-32; \
	(cd /usr/local/python3.7.3/bin; ln -s python3.7-32 python3-32) \
fi
rm -f /usr/local/python3.7.3/share/man/man1/python3.1
(cd /usr/local/python3.7.3/share/man/man1; ln -s python3.7.1 python3.1)
if test "xupgrade" != "xno"  ; then \
	case upgrade in \
		upgrade) ensurepip="--upgrade" ;; \
		install|*) ensurepip="" ;; \
	esac; \
	 ./python -E -m ensurepip \
		$ensurepip --root=/ ; \
fi
Looking in links: /tmp/tmp_tgoyekn
Collecting setuptools
Collecting pip
Installing collected packages: setuptools, pip
Successfully installed pip-19.0.3 setuptools-40.8.0
[root@localhost Python-3.7.3]# 
[root@localhost Python-3.7.3]#
[root@localhost Python-3.7.3]# cd
[root@localhost ~]# 
[root@localhost ~]# rm -rf ./Python*
[root@localhost ~]# ll
total 40
-rw-------. 1 root root 1866 Jan  4 22:24 anaconda-ks.cfg
drwxr-xr-x. 2 root root 4096 Jan  4 22:30 Desktop
drwxr-xr-x. 2 root root 4096 Jan  4 22:30 Documents
drwxr-xr-x. 2 root root 4096 Jan  4 22:30 Downloads
-rw-r--r--. 1 root root 1914 Jan  4 22:27 initial-setup-ks.cfg
drwxr-xr-x. 2 root root 4096 Jan  4 22:30 Music
drwxr-xr-x. 2 root root 4096 Jan  4 22:30 Pictures
drwxr-xr-x. 2 root root 4096 Jan  4 22:30 Public
drwxr-xr-x. 2 root root 4096 Jan  4 22:30 Templates
drwxr-xr-x. 2 root root 4096 Jan  4 22:30 Videos
[root@localhost ~]#
[root@localhost ~]# /usr/local/python3.7.3/bin/python3.7 -V
Python 3.7.3
[root@localhost ~]#
[root@localhost ~]# exit
logout
[python@localhost ~]$
[python@localhost ~]$ /usr/local/python3.7.3/bin/python3.7 -V
Python 3.7.3
[python@localhost ~]$ 
[python@localhost ~]$ mkdir myproject
[python@localhost ~]$ 
[python@localhost ~]$ ll
total 40
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Desktop
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Documents
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Downloads
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Music
drwxrwxr-x. 3 python python 4096 Apr 11 14:18 myproject
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Pictures
drwxrwxr-x. 3 python python 4096 Apr  9 17:55 project
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Public
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Templates
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Videos
[python@localhost ~]$
[python@localhost ~]$ virtualenv -p /usr/local/python3.7.3/bin/python3.7 myproject/venv3.7
Running virtualenv with interpreter /usr/local/python3.7.3/bin/python3.7
Using base prefix '/usr/local/python3.7.3'
New python executable in /home/python/myproject/venv3.7/bin/python3.7
Also creating executable in /home/python/myproject/venv3.7/bin/python
Installing setuptools, pip, wheel...
done.
[python@localhost ~]$
[python@localhost ~]$ cd myproject/
[python@localhost myproject]$ ls
venv3.7
[python@localhost myproject]$ ll
total 4
drwxrwxr-x. 5 python python 4096 Apr 11 14:18 venv3.7
[python@localhost myproject]$ source venv3.7/bin/activate
(venv3.7) [python@localhost myproject]$ python -V
Python 3.7.3
(venv3.7) [python@localhost myproject]$ deactivate
[python@localhost myproject]$
[python@localhost myproject]$ cd
[python@localhost ~]$ python -V
Python 2.7.5
[python@localhost ~]$
```
上图中我们使用 python2.7.5 中的 virtualenv 创建了一个新的虚拟环境，位置在 myproject   
目录下的 venv3.7 目录内，激活后 python3.7.3 环境生效。  

由于虚拟目录是基于 shell 环境变量和具体的文件系统目录，因此使用 deactivate 命令后直  
接删除对应目录就可以完成虚拟目录的彻底删除工作，如下图:
```bash
[python@localhost ~]$ source project/venv/bin/activate
(venv) [python@localhost ~]$ python -V
Python 2.7.5
(venv) [python@localhost ~]$ deactivate
[python@localhost ~]$ hash
hash: hash table empty
[python@localhost ~]$ 
[python@localhost ~]$ ll
total 40
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Desktop
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Documents
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Downloads
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Music
drwxrwxr-x. 3 python python 4096 Apr 11 14:18 myproject
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Pictures
drwxrwxr-x. 3 python python 4096 Apr  9 17:55 project
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Public
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Templates
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Videos
[python@localhost ~]$ rm -rf project/
[python@localhost ~]$ ll
total 36
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Desktop
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Documents
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Downloads
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Music
drwxrwxr-x. 3 python python 4096 Apr 11 14:18 myproject
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Pictures
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Public
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Templates
drwxr-xr-x. 2 python python 4096 Apr  9 17:36 Videos
[python@localhost ~]$
```
上图中我们彻底删除了之前在 project 目录中创建的 venv 目录。virtualenv 的基础使用已经  
介绍完成了，一些不太常用的高级用法大家可以自行研究一些官方文档。还有一个 virtualenv  
的管理工具 virtualenvwrapper ，感兴趣的同学可以直接使用 pip 安装一下。  

#### 1.4.4  venv 介绍和使用
&emsp;&emsp; python3.3 版本开始，默认提供了一个 venv 模块，用以完成创建虚拟环境  
的工作，可以使用 python -m 或者 pyvenv 命令完成虚拟环境管理，下面我们演  
示一下:  
```bash
[python@localhost ~]$ python -V
Python 2.7.5
[python@localhost ~]$ 
[python@localhost ~]$ python3.7 -V
bash: python3.7: command not found...
[python@localhost ~]$ 
[python@localhost ~]$ su -l root
Password: 
Last login: Thu Apr 11 15:28:52 CST 2019 on pts/0
[root@localhost ~]# vi /etc/profile.d/python3.7.3
[root@localhost ~]# 
[root@localhost ~]# cat /etc/profile.d/python3.7.3
#!/bin/bash

export PATH=$PATH:/usr/local/python3.7.3/bin/
[root@localhost ~]# 
[root@localhost ~]# exit
logout
[python@localhost ~]$ source /etc/profile.d/python3.7.3 
[python@localhost ~]$ python3.7 -V
Python 3.7.3
[python@localhost ~]$
[python@localhost ~]$ mkdir project/{webprojec,aiproject}
mkdir: cannot create directory ‘project/webprojec’: No such file or directory
mkdir: cannot create directory ‘project/aiproject’: No such file or directory
[python@localhost ~]$  
[python@localhost ~]$ mkdir project/{webprojec,aiproject}
mkdir: cannot create directory ‘project/webprojec’: No such file or directory
mkdir: cannot create directory ‘project/aiproject’: No such file or directory
[python@localhost ~]$ 
[python@localhost ~]$ 
[python@localhost ~]$ mkdir -pv project/{webprojec,aiproject}
mkdir: created directory ‘project’
mkdir: created directory ‘project/webprojec’
mkdir: created directory ‘project/aiproject’
[python@localhost ~]$ cd project/
[python@localhost project]$ ls
aiproject  webprojec
[python@localhost project]$ pyvenv webprojec/webenv
WARNING: the pyenv script is deprecated in favour of `python3.7 -m venv`
[python@localhost project]$ python3 -m venv aiproject/aienv
[python@localhost project]$
[python@localhost ~]$ mkdir -pv project/{webprojec,aiproject}
mkdir: created directory ‘project’
mkdir: created directory ‘project/webprojec’
mkdir: created directory ‘project/aiproject’
[python@localhost ~]$ cd project/
[python@localhost project]$ ls
aiproject  webprojec
[python@localhost project]$ pyvenv webprojec/webenv
WARNING: the pyenv script is deprecated in favour of `python3.7 -m venv`
[python@localhost project]$ python3 -m venv aiproject/aienv
[python@localhost project]$
[python@localhost project]$ cd aiproject/
[python@localhost aiproject]$ ls
aienv
[python@localhost aiproject]$ cd aienv/
[python@localhost aienv]$ ll
total 16
drwxrwxr-x. 2 python python 4096 Apr 11 16:34 bin
drwxrwxr-x. 2 python python 4096 Apr 11 16:34 include
drwxrwxr-x. 3 python python 4096 Apr 11 16:34 lib
lrwxrwxrwx. 1 python python    3 Apr 11 16:34 lib64 -> lib
-rw-rw-r--. 1 python python   87 Apr 11 16:34 pyvenv.cfg
[python@localhost aienv]$ cd ../../webprojec/webenv/
[python@localhost webenv]$ ll
total 16
drwxrwxr-x. 2 python python 4096 Apr 11 16:12 bin
drwxrwxr-x. 2 python python 4096 Apr 11 16:12 include
drwxrwxr-x. 3 python python 4096 Apr 11 16:12 lib
lrwxrwxrwx. 1 python python    3 Apr 11 16:12 lib64 -> lib
-rw-rw-r--. 1 python python   87 Apr 11 16:12 pyvenv.cfg
[python@localhost webenv]$ 
[python@localhost webenv]$ source bin/activate
(webenv) [python@localhost webenv]$ python -V
Python 3.7.3
(webenv) [python@localhost webenv]$ hash
hits	command
   1	/home/python/project/webprojec/webenv/bin/python
(webenv) [python@localhost webenv]$
(webenv) [python@localhost webenv]$ deactivate
[python@localhost webenv]$ 
[python@localhost webenv]$ hash
hash: hash table empty
[python@localhost webenv]$ cd ../../aiproject/aienv/bin/
[python@localhost bin]$
[python@localhost bin]$ source activate
(aienv) [python@localhost bin]$ python -V
Python 3.7.3
(aienv) [python@localhost bin]$
(aienv) [python@localhost bin]$ hash
hits	command
   1	/home/python/project/aiproject/aienv/bin/python
(aienv) [python@localhost bin]$ deactivate
[python@localhost bin]$ hash
hash: hash table empty
[python@localhost bin]$
[python@localhost bin]$ cd
[python@localhost ~]$ 
```
上图我将之前安装的 python3.7.3 配置到 PATH 环境中使之生效。然后在 python 用户家目  
录创建了 project 文件夹，并在该文件夹下创建两个项目目录，分别是 webproject 和  
aiprojec。然后使用 pyvenv 命令在 webproject 下创建了 webenv 虚拟环境目录，创建该目录  
时，提示 pyvenv命令已经废弃，建议我们使用 python3.7 -m venv 方式创建虚拟环境。最  
后我们根据建议，使用 python3.7 -m 方式在 aiproject 项目下创建了 aienv 虚拟环境目录。  
和 virtualenv 使用方式一样，使用某个环境时 source 对应虚拟环境 bin 目录下的 activate 文  
件即可，退出时使用 deactivate 命令，需要删除虚拟环境目录时，直接删除虚拟环境目录即  
可。


#### 1.4.5  使用 pyenv-virtualenv 插件
&emsp;&emsp; 第一章第三节我们讲解过 pyenv ，当时我们使用 pyenv 完成了不同 python 版本的安装  
和环境的切换。但是当时并没有解决虚拟环境的问题，我们可以使用上面讲解的 virtualenv  
和 venv 完成虚拟目录创建管理的工作。为了方便使用，pyenv 提供了一个 pyenv-virtualenv  
的插件,可以替代 virtualenv 或者 venv 完成虚拟目录的管理工作。下面我们演示一下这个插  
件的安装和基本使用:
```bash
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.7
  3.6.8
[python@localhost ~]$
[python@localhost ~]$ git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
Cloning into '/home/python/.pyenv/plugins/pyenv-virtualenv'...
remote: Enumerating objects: 30, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (24/24), done.
remote: Total 2064 (delta 14), reused 13 (delta 6), pack-reused 2034
Receiving objects: 100% (2064/2064), 592.75 KiB | 296.00 KiB/s, done.
Resolving deltas: 100% (1403/1403), done.
[python@localhost ~]$ 
[python@localhost ~]$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
[python@localhost ~]$ 
[python@localhost ~]$ source .bashrc 
[python@localhost ~]$ 
[python@localhost ~]$ pyenv virtualenv 3.6.8 spenv
Looking in links: /tmp/tmpi3ljzthj
Requirement already satisfied: setuptools in /home/python/.pyenv/versions/3.6.8/envs/spenv/lib/python3.6/site-packages (40.6.2)
Requirement already satisfied: pip in /home/python/.pyenv/versions/3.6.8/envs/spenv/lib/python3.6/site-packages (18.1)
[python@localhost ~]$ 
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.7
  3.6.8
  3.6.8/envs/spenv
  spenv
[python@localhost ~]$ cd .pyenv/versions/
[python@localhost versions]$ ll
total 8
drwxr-xr-x. 6 python python 4096 Apr 11 18:27 3.5.7
drwxr-xr-x. 7 python python 4096 Apr 11 18:31 3.6.8
lrwxrwxrwx. 1 python python   45 Apr 11 18:31 spenv -> /home/python/.pyenv/versions/3.6.8/envs/spenv
[python@localhost versions]$ cd
[python@localhost ~]$
[python@localhost ~]$ python -V
Python 2.7.5
[python@localhost ~]$
[python@localhost ~]$ pyenv activate spenv
pyenv-virtualenv: prompt changing will be removed from future release. configure ‘export PYENV_VIRTUALENV_DISABLE_PROMPT=1’ to simulate the behavior.
(spenv) [python@localhost ~]$
(spenv) [python@localhost ~]$ pyenv versions
  system
  3.5.7
  3.6.8
  3.6.8/envs/spenv
* spenv (set by PYENV_VERSION environment variable)
(spenv) [python@localhost ~]$
(spenv) [python@localhost ~]$ pyenv virtualenvs
  3.6.8/envs/spenv (created from /home/python/.pyenv/versions/3.6.8)
* spenv (created from /home/python/.pyenv/versions/3.6.8)
(spenv) [python@localhost ~]$
(spenv) [python@localhost ~]$ 
(spenv) [python@localhost ~]$ python -V
Python 3.6.8
(spenv) [python@localhost ~]$ pip install jupyter
Collecting jupyter
  Using cached https://files.pythonhosted.org/packages/83/df/0f5dd132200728a86190397e1ea87cd76244e42d39ec5e88efd25b2abd7e/jupyter-1.0.0-py2.py3-none-any.whl
  .
  .省略安装信息。。。。。。
  .
  Running setup.py install for prometheus-client ... done
  Running setup.py install for tornado ... done
  Running setup.py install for backcall ... done
  Running setup.py install for pandocfilters ... done
  Running setup.py install for pyrsistent ... done
Successfully installed MarkupSafe-1.1.1 Send2Trash-1.5.0 attrs-19.1.0 backcall-0.1.0 bleach-3.1.0 decorator-4.4.0 defusedxml-0.5.0 entrypoints-0.3 ipykernel-5.1.0 ipython-7.4.0 ipython-genutils-0.2.0 ipywidgets-7.4.2 jedi-0.13.3 jinja2-2.10.1 jsonschema-3.0.1 jupyter-1.0.0 jupyter-client-5.2.4 jupyter-console-6.0.0 jupyter-core-4.4.0 mistune-0.8.4 nbconvert-5.4.1 nbformat-4.4.0 notebook-5.7.8 pandocfilters-1.4.2 parso-0.4.0 pexpect-4.7.0 pickleshare-0.7.5 prometheus-client-0.6.0 prompt-toolkit-2.0.9 ptyprocess-0.6.0 pygments-2.3.1 pyrsistent-0.14.11 python-dateutil-2.8.0 pyzmq-18.0.1 qtconsole-4.4.3 six-1.12.0 terminado-0.8.2 testpath-0.4.2 tornado-6.0.2 traitlets-4.3.2 wcwidth-0.1.7 webencodings-0.5.1 widgetsnbextension-3.4.2
You are using pip version 18.1, however version 19.0.3 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
(spenv) [python@localhost ~]$ 
(spenv) [python@localhost ~]$ 
(spenv) [python@localhost ~]$ jupyter notebook
[I 18:41:41.192 NotebookApp] Serving notebooks from local directory: /home/python
[I 18:41:41.192 NotebookApp] The Jupyter Notebook is running at:
[I 18:41:41.192 NotebookApp] http://localhost:8888/?token=c36aa6e3d3928b8c4bdbe9bdb5f6e8e631290808d49fbe60
[I 18:41:41.192 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 18:41:41.234 NotebookApp] 
    
    To access the notebook, open this file in a browser:
        file:///run/user/1001/jupyter/nbserver-110650-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=c36aa6e3d3928b8c4bdbe9bdb5f6e8e631290808d49fbe60
^C[I 18:41:57.029 NotebookApp] interrupted
Serving notebooks from local directory: /home/python
0 active kernels
The Jupyter Notebook is running at:
http://localhost:8888/?token=c36aa6e3d3928b8c4bdbe9bdb5f6e8e631290808d49fbe60
Shutdown this notebook server (y/[n])? y
[C 18:41:59.773 NotebookApp] Shutdown confirmed
[I 18:41:59.774 NotebookApp] Shutting down 0 kernels
(spenv) [python@localhost ~]$ pyenv deactivate
[python@localhost ~]$
[python@localhost ~]$
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.7
  3.6.8
  3.6.8/envs/spenv
  spenv
[python@localhost ~]$
[python@localhost ~]$ jupyter notebook
pyenv: jupyter: command not found

The ’jupyter‘ command exists in these Python versions:
  3.6.8/envs/spenv
  spenv

[python@localhost ~]$
[python@localhost ~]$
```
上图中我们先在 pyenv 中安装了 pyenv-virtualenv，然后使用 pyenv 的 virtualenv 选项创  
建一个 python 版本为 3.6.8 的虚拟环境 spenv。根据 pyenv 的提示信息，我们发现新创  
建的虚拟环境 spenv 的实际存放路径为 pyenv 的 versions 目录下的具体版本的 envs 路径  
下。之后我们可以使用 pyenv 的 activate 选项来生效一个我们制定的具体虚拟环境。上  
图中我们可以使用 pyenv versions 查看当前所使用的虚拟环境，也可以使用 pyenv virtualenvs  
查看。虚拟环境的生效范围为当前 shell ，最后要想退出虚拟环境，我们需要使用 pyenv  
的 deactivate 选项完成，或者直接退出当前 shell 即可。 pyenv 的 virtualenv 插件除了提  
供专有的管理命令选项外，我们还可以使用之前 pyenv 的 global local shell 的环境指定方  
式来指定当前生效的 python 版本或者虚拟环境。pyenv 的 activate 选项的实际效果和 pyenv  
的 shell 选项功能一样。

&emsp;&emsp;上面的演示步骤没有讲解删除虚拟环境的方法，下面我们演示一下:
```bash
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.7
  3.6.8
  3.6.8/envs/spenv
  spenv
[python@localhost ~]$
[python@localhost ~]$ pyenv virtualenv-delete spenv
pyenv-virtualenv: remove /home/python/.pyenv/versions/3.6.8/envs/spenv? y
[python@localhost ~]$
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.7
  3.6.8
[python@localhost ~]$ pyenv virtualenv 3.5.7 aienv
Requirement already satisfied: setuptools in /home/python/.pyenv/versions/3.5.7/envs/aienv/lib/python3.5/site-packages
Requirement already satisfied: pip in /home/python/.pyenv/versions/3.5.7/envs/aienv/lib/python3.5/site-packages
[python@localhost ~]$ pyenv virtualenv 3.6.8 webenv
Looking in links: /tmp/tmpat6xc4mn
Requirement already satisfied: setuptools in /home/python/.pyenv/versions/3.6.8/envs/webenv/lib/python3.6/site-packages (40.6.2)
Requirement already satisfied: pip in /home/python/.pyenv/versions/3.6.8/envs/webenv/lib/python3.6/site-packages (18.1)
[python@localhost ~]$
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.5.7
  3.5.7/envs/aienv
  3.6.8
  3.6.8/envs/webenv
  aienv
  webenv
[python@localhost ~]$
[python@localhost ~]$ pyenv virtualenvs
  3.5.7/envs/aienv (created from /home/python/.pyenv/versions/3.5.7)
  3.6.8/envs/webenv (created from /home/python/.pyenv/versions/3.6.8)
  aienv (created from /home/python/.pyenv/versions/3.5.7)
  webenv (created from /home/python/.pyenv/versions/3.6.8)
[python@localhost ~]$ 
[python@localhost ~]$ pyenv uninstall 3.5.7
pyenv-virtualenv: remove /home/python/.pyenv/versions/3.5.7/envs/aienv? y
pyenv: remove /home/python/.pyenv/versions/3.5.7? y
[python@localhost ~]$ 
[python@localhost ~]$
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.6.8
  3.6.8/envs/webenv
  webenv
[python@localhost ~]$ pyenv virtualenvs
  3.6.8/envs/webenv (created from /home/python/.pyenv/versions/3.6.8)
  webenv (created from /home/python/.pyenv/versions/3.6.8)
[python@localhost ~]$ 
[python@localhost ~]$
[python@localhost ~]$ pyenv uninstall webenv
pyenv-virtualenv: remove /home/python/.pyenv/versions/3.6.8/envs/webenv? y
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.6.8
[python@localhost ~]$ pyenv virtualenvs
[python@localhost ~]$ 
[python@localhost ~]$ 
```

上图我们演示了使用 pyenv 的 virtualenv-delete 选项完成删除虚拟环境的操作，之后又使用了  
uninstall 选项进行删除，由于虚拟环境创建的路径是在具体的 python 版本目录下，所有不建议  
直接删除指定的 python 版本，但是可以直接使用 pyenv uninstall 删除对应的虚拟目录。


&emsp;&emsp; pyenv-virtualenv 插件底层对虚拟环境的管理是通过 python 的 venv 模块实现的，但是python3.3 之前的版本没有该模块，所以使用 virtualenv 模块虚拟环境的管理工作。
```bash
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.6.8
[python@localhost ~]$
[python@localhost ~]$ pyenv virtualenv 3.6.8 webenv
Looking in links: /tmp/tmpkdi7_a4q
Requirement already satisfied: setuptools in /home/python/.pyenv/versions/3.6.8/envs/webenv/lib/python3.6/site-packages (40.6.2)
Requirement already satisfied: pip in /home/python/.pyenv/versions/3.6.8/envs/webenv/lib/python3.6/site-packages (18.1)
[python@localhost ~]$
[python@localhost ~]$
[python@localhost ~]$ pyenv virtualenv system aienv
  No LICENSE.txt / LICENSE found in source
New python executable in /home/python/.pyenv/versions/aienv/bin/python2
Also creating executable in /home/python/.pyenv/versions/aienv/bin/python
Installing setuptools, pip, wheel...
done.
Installing pip from https://bootstrap.pypa.io/get-pip.py...
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won’t be maintained after that date. A future version of pip will drop support for Python 2.7.
Collecting pip
  Downloading https://files.pythonhosted.org/packages/d8/f3/413bab4ff08e1fc4828dfc59996d721917df8e8583ea85385d51125dceff/pip-19.0.3-py2.py3-none-any.whl (1.4MB)
    100% |████████████████████████████████| 1.4MB 7.6MB/s 
Installing collected packages: pip
  Found existing installation: pip 19.0.3
    Uninstalling pip-19.0.3:
      Successfully uninstalled pip-19.0.3
Successfully installed pip-19.0.3
[python@localhost ~]$ 
[python@localhost ~]$
[python@localhost ~]$ pyenv versions
* system (set by /home/python/.pyenv/version)
  3.6.8
  3.6.8/envs/webenv
  aienv
  webenv
[python@localhost ~]$
[python@localhost ~]$ cd .pyenv/versions/webenv/
[python@localhost webenv]$ ll
total 16
drwxrwxr-x. 2 python python 4096 Apr 12 11:37 bin
drwxrwxr-x. 2 python python 4096 Apr 12 11:37 include
drwxrwxr-x. 3 python python 4096 Apr 12 11:37 lib
lrwxrwxrwx. 1 python python    3 Apr 12 11:37 lib64 -> lib
-rw-rw-r--. 1 python python   99 Apr 12 11:37 pyvenv.cfg
[python@localhost webenv]$ 
[python@localhost webenv]$ cd
[python@localhost ~]$ 
[python@localhost ~]$ cd .pyenv/versions/aienv/
[python@localhost aienv]$ ll
total 12
lrwxrwxrwx. 1 python python   34 Apr 12 11:39 aienv -> /home/python/.pyenv/versions/aienv
drwxrwxr-x. 2 python python 4096 Apr 12 11:39 bin
drwxrwxr-x. 2 python python 4096 Apr 12 11:39 include
drwxrwxr-x. 3 python python 4096 Apr 12 11:39 lib
lrwxrwxrwx. 1 python python    3 Apr 12 11:39 lib64 -> lib
[python@localhost aienv]$ 
[python@localhost aienv]$ cd
[python@localhost ~]$ 
[python@localhost ~]$
```
上图中我们分别创建了 python2.7 和 python3.6 版本的虚拟环境，发现对应目录下的结构不一样，  
python3.6 版本的虚拟环境内容有 pyven配置文件，证明是使用 venv 模块创建的该虚拟环境。 

#### 1.4.6  Pycharm 中虚拟环境的管理

&emsp;&emsp;Pycharm 是 python 软件开发的集成开发环境，他具备 python 项目创建管理、python 解析器  
和虚拟环境管理功能；作为 python 代码编辑器，他具备代码高亮，语法提示，错误提示，代码补  
全等功能，方便程序员快速高效的编写项目；作为调试环境，方便运行、测试、debug程序；内含  
git、svn 等版本控制客户端，方便项目代码管理，是广大 Python 程序员首选的 IDE。

&emsp;&emsp;下面我们集中介绍一下 Pycharm 的项目创建管理与 python 虚拟环境的设置功能。在前几节中  
我们已经安装过了 pycharm 这个工具，今天我们再来操作复习一遍。首先我们从 pycharm 官网下  
载 Linux 版的压缩包，然后解压到一个软件安装的路径下。Pycharm 是用 Java 开发出来的图形化  
集成开发工具，压缩包内包含 Java 运行环境，因此不需要提前安装 Java 运行环境就可以直接运行  
在它 bin 目录内的启动程序 pycharm.sh。

```bash
[python@localhost ~]$ ls
Desktop    Music      project                            Templates
Documents  myproject  Public                             Videos
Downloads  Pictures   pycharm-community-2019.1.1.tar.gz
[python@localhost ~]$ mkdir software
[python@localhost ~]$ tar xf pycharm-community-2019.1.1.tar.gz -C software/
[python@localhost ~]$
[python@localhost ~]$ ls
Desktop    Music      project                            software
Documents  myproject  Public                             Templates
Downloads  Pictures   pycharm-community-2019.1.1.tar.gz  Videos
[python@localhost ~]$
[python@localhost ~]$ cd software/
[python@localhost software]$ 
[python@localhost software]$ mv pycharm-community-2019.1.1 pycharm
[python@localhost software]$ 
[python@localhost software]$ cd pycharm/bin/
[python@localhost bin]$ ./pycharm.sh 
OpenJDK 64-Bit Server VM warning: Option UseConcMarkSweepGC was deprecated in version 9.0 and will likely be removed in a future release.
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by com.intellij.ide.ClassUtilCore to field sun.net.www.protocol.jar.JarFileFactory.fileCache
WARNING: Please consider reporting this to the maintainers of com.intellij.ide.ClassUtilCore
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
```
上图我们又演示了 pycharm 的安装过程并在 shell 终端中启动了 pycharm。

&emsp;&emsp;下面我们通过图片给大家介绍一下常用的选项和功能，如下：  

1. 启动画面  
![启动画面](pycharm01.png)

2. 项目选择页面  
![项目选择页面](pycharm02.png)

3. 点击设置Configure，创建一个快捷方程式，方便下次启动，不用再手动创建桌面图标  
![创建快捷方程式](pycharm03.png)

4. 在项目选择页面，可以选择通过版本管理工具下载对应的项目  
![版本管理工具创建项目](pycharm04.png)

5. 在项目选择页面，可以选择 Open 打开本地文件系统中保存的 python 项目  
![打开本地的项目](pycharm05.png)

6. 在项目选择页面，点击 Create New Project 可以创建一个新项目  
![创建新项目](pycharm06.png)

6.1. 点击创建项目后进行项目设置:  
Location: 填写项目在文件系统中的路径，最后是项目文件夹名称，如图我创建了 aiproject 项目  
New environment using: 选择Virtualenv  
&emsp;&emsp;Location: 默认的就可以，在项目文件夹内  
&emsp;&emsp;Base interpreter: 要指定系统中的一个具体的 Python 版本，不要写成虚拟环境的路径  
&emsp;&emsp;&emsp;&emsp;Inherit global site-packages:&ensp;不勾选  
&emsp;&emsp;&emsp;&emsp;Make available to all projects: 不勾选  
然后点击 Create 创建即可项目  
![创建新项目设置页面](pycharm061.png)

6.2. 上图是使用新创建的虚拟环境，我们也可以使用系统中已创建过的虚拟环境来创建项目  
Location: 填写项目在文件系统中的路径，最后是项目文件夹名称，如图我创建了 aiproject 项目  
New environment using: 选择 Existing Interpreter  
&emsp;&emsp;Interpreter: 要指定系统中的一个具体的虚拟环境的路径   
然后点击 Create 创建即可项目  
`*** 一般建议使用 6.1 中的方式，每个项目单独创建一个虚拟环境 ***`     
![创建新项目设置页面](pycharm062.png)


7. 项目主界面  
上面是 pycharm 的菜单栏: 可以完成各种设置功能  
左面是项目文件显示窗口: 可以创建删除项目文件，了解项目目录结构等  
右面是代码编辑窗口: 点击项目文件显示窗口中的具体文件，即可再右面的编辑区域进行代码文件的编辑  
下面是代码运行标准交互窗口: 在代码编辑窗口或者项目显示窗口选中具体的 python 文件后鼠标右键点击运行即可
![创建新项目设置页面](pycharm07.png)
