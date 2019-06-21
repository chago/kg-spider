# kugou-spider
从酷狗网下载音乐的简单爬虫

<strong>设计思路：</strong></br>
1.循环访问https://www.kugou.com/yy/rank/home/{PAGE_NUM}-8888.html?from=homepage，每次将{PAGE_NUM}替换为具体的页码，一共循环23次
</br>
2.获取具体某页所有的歌曲列表（含具体url、hash值、album_id），将hash和album_id分别作为key和value放入ehcache中</br>
3.逐个访问具体音乐的url，获取页面里面的hash，到缓存中获取album_id，然后替换掉下请求中的{HASHCODE}和{ALBUMID}，然后{TIME}用System.currentTimeMillis()</br>
替换，然后访问替换后的请求</br>
https://wwwapi.kugou.com/yy/index.php?r=play/getdata&callback=jQuery19108318842169864549_1558160178250&
hash={HASHCODE}&album_id={ALBUMID}&dfid=4Vyhka0JsPzT0DLMy10TfJPj&mid=122dc1e8e26152d6ec1aca669ca448d3&platid=4&_={TIME}</br>
4.根据第3步的返回结果json，解析出MP3真实的url；如果第3步返回err_code不为0，说明爬虫被识别了，需要重新获取新的代理ip，再次访问</br>
5.下载到本地磁盘，如果是重复歌曲不再下载</br>

<strong>用到的技术：</strong></br>
1.HttpClient抓包</br>
2.Jsoup解析html</br>
3.FastJson解析json报文</br>
4.ehcache缓存用来识别是否为重复歌曲、识别代理IP是否使用过、记录歌曲的hash和alum_id</br>
5.log4j记录日志</br>
6.commons-io执行下载，不用自己写流了</br>

<strong>遗留问题：</strong></br>
1.只能抓取到免费歌曲，对于收费歌曲不能抓取，其实我们也不该抓取</br>
2.代码中为了方便用了很多static，不能支持多线程或并发抓取</br>
</br>
成功的路上，你永远不是一个人！欢迎加入我们：</br>

![](./qq.jpg)

<strong>声明：</strong>
本爬虫小程序仅限个人学习交流用。本程序和程序抓取到的歌曲均不可用于商业用途，否则后果自负！！！</br>
本爬虫小程序仅限个人学习交流用。本程序和程序抓取到的歌曲均不可用于商业用途，否则后果自负！！！</br>
本爬虫小程序仅限个人学习交流用。本程序和程序抓取到的歌曲均不可用于商业用途，否则后果自负！！！</br>
