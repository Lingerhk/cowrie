# Cowrie

##Noite:

From https://github.com/micheloosterhof/cowrie/blob/master/README.md.
For more details information see: http://www.micheloosterhof.com/cowrie/.

Cowrie 是一个中度交互式的SSH蜜罐系统，它旨在通过攻击者的shell交互，进行log采集与安全分析。
[Cowrie](http://github.com/micheloosterhof/cowrie/) 由Michel Oosterhof开发，并且基于Upi Tamminen的[Kippo](http://github.com/desaster/kippo/)蜜罐原型改进。

## Cowrie特点

一些有趣的特点：

* 该虚拟文件系统能够增加／移动文件。一个完备的虚拟文件系统颇似Debian 5.0的完整版。
* 可以添加虚拟文件中的内容，让攻击者通过'cat'命令显示，例如'/etc/passwd'文件。
* Session日志存储在于[UML Compatible](http://user-mode-linux.sourceforge.net/) 的兼容格式（二进制／JSON），并且很容易基于原始时间戳回放。回放shell真是交互过程。
* Cowrie可以顺便下载攻击这通过wget/curl或者通过sftp/scp上传的文件，以便后期分析。

基于kippo添加的新功能:

* 支持SFTP和SCP命令文件上传
* 支持SSH命令执行，如:ssh user@ip 'ls'
* 可记录SSH代理连接的tcp/ip连接记录
* 支持重定向SMTP连接到指定的SMTP蜜罐服务器Honeypot(e.g. [mailoney](https://github.com/awhitehatter/mailoney))
* 日志记录支持JSON格式，便于一些日志分析管理工具处理分析(e.g. 开源的ELK日志分析套件)
* 添加了许多新命令的支持

## 第三方包依赖

Software required:

* Python 2.7+
* Zope Interface 3.6.0+
* Twisted 8.0+
* python-crypto
* python-cryptography
* python-pyasn1
* python-gmpy2 (recommended)
* python-mysqldb (for MySQL output)
* python-OpenSSL

## Cowrie文件结构:

* `cowrie.cfg` - Cowrie的配置文件，默认原始文件是`cowrie.cfg.dist`
* `data/fs.pickle` - 虚拟文件系统
* `data/userdb.txt` - ssh登录凭证（采用黑／白名单方式，灵活配置）
* `dl/` - 攻击者在蜜罐中传输的文件存储在此
* `honeyfs/` - 虚拟文件系统的文件内容（可以将真实系统中的文件copy到此或者使用`bin/fsctl`创建文件）
* `log/cowrie.json` - 输出的JSON格式的日志
* `log/cowrie.log` - log/debug输出
* `log/tty/*.log` - session会话日志
* `txtcmds/` - 虚拟命令时回显的文件内容
* `bin/createfs` - 使用此命令在虚拟文件系统中创建文件
* `bin/playlog` - 很实用的一个回话日志回放的工具

## Is it secure?

Maybe. See [FAQ](https://github.com/desaster/kippo/wiki/FAQ)

## I have some questions!

Please visit https://github.com/micheloosterhof/cowrie/issues
