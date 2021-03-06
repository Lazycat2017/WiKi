# 如何使用 RSS 脚本

请完整阅读本文档！本人不予回答本文档已经涵盖的问题……  

## 原理
我的 RSS 的脚本的原理是使用 `curl` 命令抓取 PT 站种子浏览页面，并根据需求下载种子，比如 Free 种、置顶种等。  
因此，在 PT 站来看，当你在盒子上使用 RSS 脚本时，就约等于你使用盒子 IP 去访问 PT 站点。这在大多数情况下没什么问题，但是有一些对于代理限制比较严格的站点，比如 GGN／BTN（我只是举个例子，这两个站不需要脚本，AutoDL-Irssi 就行），就需要告知管理，登记代理的使用情况。  





## 使用须知

1. `#` 这个符号，也就是井号，开头的是注释
注释内容对脚本的运行毫无影响，不需要删除，我只是写给你看作为指导的  

2. 在某些站点，使用 RSS 脚本可能需要备案  
注意：备案时是备案使用盒子 IP 的代理，而不是备案要使用 RSS 脚本  

3. 不建议把 RSS 的频率设定得过高  
太高的频率可能会被站点认为是在做太高的频率可能会被站点认为是在做 DDoS 或者恶意使用脚本。至于多少时间执行一次 RSS 算频率高，这个是站点管理说了算的，不同的管理看法不同。我个人不建议把 RSS 间隔设定在 5 分钟以内，因为在站点既不提供 RSS 又没有 AutoDL-Irssi 支持的站，或者在 RSS 约等于没有的站（比如 ADC、Cinematik），没有多少人会 RSS，稍微晚上车几分钟影响一般不是很大  

4. 注意正确填写 Cookies  
用不正确的 Cookies 访问站点约等于输错密码、登陆失败，次数多了可能导致你盒子的 IP 被 ban  





## 脚本参数

脚本需要修改的设置项一般就以下几个：

- `Cookie` 站点的 Cookies，如何获取、填写请看[这篇教程](https://github.com/Aniverse/WiKi/blob/master/How.to.use.RSS.md#2-获取-cookies)  
```
Cookie="lognnI=XXXXXXXXX ;loggnA=XXXXXXXXX ; loggnB=XXXXXXXXX ; navpreferences=XXXXXXXXX"
```

- `WatchFolder` BT 客户端的监控文件夹的路径，脚本会把种子下载到这个路径  
我这个路径只是给你举个例子，你实际上的监控文件夹路径不一定是这个（尤其是共享盒子），具体路径在哪里自己找
```
WatchFolder="/home/用户名/下载软件/监控文件夹"
```

- `LogFile` 脚本运行的日志文件，记录脚本曾经 RSS 到过哪些种子  
脚本里默认用的是有 root 权限才有权限访问的路径，如果你不用 root 运行脚本，请修改这个路径，否则脚本无法运行！  
```
LogFile="/log/HDSpain_record.txt"
```

- `RSSType` 脚本的 RSS 模式，不同的脚本有不同的模式可供选择，也有的脚本只提供了一种模式因此没得选  
```
RSSType=B
```

还有两项一般不需要修改的参数：

- `UA` UserAgent。脚本是模拟成 UA 对应的浏览器去访问 PT 站的，如果不懂的话就不要改这个项目  
```
UA="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36"
```

- `URL` 脚本 RSS 的站点种子浏览页面的网址。 大多数情况下不需要修改  
比如在 Route，我的脚本给的 URL 是 `browse.php?s=&action=s`，也就是默认的种子浏览页面去除置顶种子的页面，脚本是抓取这个网页里的全部种子。如果你只想 RSS 蓝光原盘，你把 URL 改成 `browse.php?s=&action=s&c1=1&m1=1` 即可  
```
URL="https://www.hd-spain.com/index.php?sec=listado"
```




## 如何使用

### 1. 填写好脚本各项的参数

### 2. 把脚本上传到盒子上  
可以用 FTP/SFTP/ZMODEM 等方式上传到盒子上，但其实也可以直接把脚本文本复制粘贴到盒子上  

### 3. 赋予脚本执行权限
```
chmod +x /脚本/的/路/径
```

### 4. 测试脚本
```
/脚本/的/路/径 --test
```

输入这个命令测试脚本能否正常运行，正常运行的话会输出应该被 RSS 到的种子的下载链接


### 5. 设定定期运行

比较常见的做法是使用 cron，SSH 输入：

```
crontab -e
```

如果出现类似这个界面让你选编辑器的，哪个用得顺手你用哪个。  
如果你都不会用的话，推荐你敲回车选择默认的 `nano`，最易于上手，[教程见此](http://man.linuxde.net/nano)  

```
*/5 * * * * /脚本/的/完整/路径
```

这里的 `5` 是 5 分钟执行一次脚本的意思。
**注意**：这里要填写的是完整的路径，FTP 下的路径是不完整的，比如说 `/home/aniverse/script/rss.tik` 是完整路径，`/script/rss.tik` 和 `~/script/rss.tik` 就不是完整路径  




### FAQ
1. 以后再写
2. 以后再写
3. 以后再写
