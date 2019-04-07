# CuteOne

**不是OneIndex 不是PyOne，不是 不是 不是**   
**不是OneIndex 不是PyOne，不是 不是 不是**   
**不是OneIndex 不是PyOne，不是 不是 不是**   
重要的事情说三遍，我都觉得都不够。。因为他们很多功能都木有。木有。木有  


**CuteOne**是一款OneDrive多网盘挂载程序。
> 多盘负载、在线查看、在线上传、下载、多盘同步、主从同步、在线分享、文件夹权限管理、
  会员功能、等级制度、付费查看、密码查看、支付模块、主题切换、极速缓存、  
**欢迎捐赠，QQ群：8331213**

* 首页
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t22hd8kwj21gs0qwdo4.jpg)

* 弹出层
![](http://ww1.sinaimg.cn/large/a096a6bfly1g19wsm3vzvj21gr0qogpi.jpg)

* 后台 - 首页
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t21bb8e8j21hc0qv0u9.jpg)

* 后台 - 驱动列表
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t23cy43oj21hc0qyq62.jpg)

* 后台 - 主从网盘列表
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t23d4lhkj21hc0qvdht.jpg)

* 后台 - 网盘管理
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t23cye5cj21hc0qwjts.jpg)

* 后台 - 权限管理
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t23cy2i7j21hc0qwmz5.jpg)

* 后台 - 群组权限
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t23cxhlaj21hc0qxgnl.jpg)

* 后台 - 用户管理
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t23cyc3gj21hc0qvwhm.jpg)

* 后台 - 网站设置
![](http://ww1.sinaimg.cn/large/a096a6bfgy1g1t23d4vecj21hc0qx772.jpg)



# 环境需求
* Linux
* Nginx
* Python3  ——[如何安装Python3](https://www.cnblogs.com/s-seven/p/9105973.html)
* Mysql >= 5.5
* MongoDB


# 安装流程
* 前言
> 初次安装真的，我自己都觉得繁琐，但是一劳永逸；  
  如果没有python3的，先安装python3 再执行下面的流程。  
  具体安装图文教程  ——[Gitbook](https://wiki.cuteone.cn/)
* 第一步，拉取代码  
```
git clone https://github.com/Hackxiaoya/CuteOne.git  
```
* 第二步，安装需求的库和创建uwsgi软连
```
cd CuteOne
pip3 install -r requirements.txt
> 如果出现pip install --upgrade pip的字样，就执行更新一下，没有就跳过
> pip3 install --upgrade pip

ln -s /usr/local/python3/bin/uwsgi /usr/bin/uwsgi
```
* 第三步，修改根目录。启动网站后台运行   
```
vi uwsgi.ini
> 里面有一个chdir，把路径改成你自己的路径
nohup uwsgi --ini uwsgi.ini &
> 忽略显示的错误
```
* 第四步，Nginx反代一下，端口是5000

* 第五步，访问安装路径
```
http://你的域名/install/
```
* 第六步，根据流程安装呗
```
等出现安装完成的字样就可以了
如果访问不行，你就执行：pgrep -f uwsgi 看看有没有运行起来
如果没有返回ID，你就执行一下： nohup uwsgi --ini uwsgi.ini &
就行了。
```
* 第七步，添加驱动，不然你访问首页会报错
```
http://你的域名/admin/
> 到驱动的位置添加个驱动，然后添加个网盘，然后更新一下缓存就可以了
> 如果后台账号密码不对，就用默认账号密码，都是admin
> 如果报错502，就是网站没启动
```


# 功能简述
* 驱动列表
> 其实驱动列表你们把他当成一个分类即可，可是为啥里面可以添加很多网盘呢？  
  那么重点来了，因为有负载切换的功能，当你一个网盘很多人在看这个网盘的同一个视频  
  可能会变慢，我猜的；  所以可以切换到另外一个网盘里面的相同资源看，实现切换线路；  
  然后这么设计是也是为了资源备份用的，意思就是这个驱动列表下的所有网盘内容需要保持一致；  
  如果不一致，那么久没办法切换负载；  所以我们看一条；  
* 主从备份
> 主从备份的功能就是给驱动下的所有网盘进行同步，但是前提是驱动下只能有一个主盘，别的都是从盘；  
  因为主从备份是拉取主盘的内容，备份到从盘里的； 所以你们可以在主盘里面看到上传按钮，而从盘没有；  
  这个功能是预防你们网盘被封，然后有备份盘当做备用；这也是一个卖资源盘的办法；  
* 权限管理
> 权限管理其实就是给文件夹设置密码啦；  
  然后你们可以看到还有群组管理，这个是干啥的呢？嗯，就是设置VIP的意思，就是这个群组可以免密查看你加密的文件路径；  
* 会员管理
> 会员管理顾名思义啦，他还有一个功能是和权限管理的群组是挂钩的，意思就是会员你可以给他分配群组，  
  也就是所谓的VIP制度，让会员可以免密查看一些加密的文件夹；  
* 文件管理
> 因为有了会员，所以想给会员也能上传文件，然后分享，所以出了这个会员的文件管理，这里可以单独给会员设置存储盘，会员上传的文件就会在这个里面；  
* 任务管理
> 这个就是你在驱动列表的网盘里面上传了文件，这里可以看到那个文件当前的同步状态而已；  
-----------
* 开始同步 和 更新缓存
> 开始同步只有你点击管理了之后 进入驱动下的网盘列表，你才看到这个按钮，因为他是用来主从备份的，你不需要主从备份，你就别按他；  
  
> 更新缓存，如果你不更新缓存，你会发现你前端没有文件，这个其实就是拉取一下最新的数据而已；  
----------
* 文件地址的缓存周期
> OneDrive的文件地址是有时效性的，大概五分钟这样吧，所以我这边使用里类推模式来更新地址缓存，什么是类推，就是当这个文件五分钟内有人访问一次，  
  数据库就会是最新文件的地址，以此类推，如果文件热度很高，地址是一直是最新的，如果热度低，只要有一个人访问，地址就会缓存到最新的到数据库；  







# 常见问题
* 出现500
> 大概是数据库有问题，你看看数据库是否创建了表
* 出现502 
> 大概是因为CuteOne没运行,输入一下启动网站的命令
* 首次安装，访问报错
> 首次安装之后需要在后台先添加一个网盘才行。
* 启动了之后，访问报错
> 你大概是首次安装启动，请查看安装流程。
* 添加网盘的时候获取code的时候，code在url里，注意看浏览器的url
* 重装网站程序
> 执行ls -a 会看到有一个.install的文件，rm .install 删除他即可。


# 常见命令
* 查看uwsgi
```
pgrep -f uwsgi
```
* kill所有uwsgi
```
killall -9 uwsgi
```
* 启动网站
```
nohup uwsgi --ini uwsgi.ini &
> 忽略显示的错误
```



# 未来可能收费的功能列表：
* Offie系列产品的在线修改功能；
* 付费查看功能；
* 采集功能；；
* 压缩包上传解压同步功能；
* 文件夹上传同步功能；  

**好吧，这只是我YY的收费功能，其实也已开源，去TM的收费**