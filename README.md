# 江南大学校园网信息爬虫

## 简介

这是针对江南大学校园网各网站的信息采集爬虫, 爬取各类校园网站信息入江南听雨数据库, 作为江南听雨其他产品的数据源.

这个爬虫是采用 [Python][py] 语言的 [Scrapy][scrapy] 框架开发的应用.

[py]: http://python.org/
[scrapy]: http://scrapy.org/


## 覆盖范围

如无说明, 都默认为只爬取相应栏目首页上的链接, 不深入抓取. 对应的爬虫名非单独说明即为相应网站的二级域名 (如 `jw`).


### 院系

* [江南大学数字媒体学院](http://dm.jiangnan.edu.cn/cn/)
* [江南大学研究生院](http://gs.jiangnan.edu.cn/)

### 党群/行政机构

* [江南大学教务处](http://jw.jiangnan.edu.cn/)
* [江南大学新闻网](http://xinwen.jiangnan.edu.cn/)的信息公告栏目
* [江南大学就业信息网](http://scc.jiangnan.edu.cn/)
* [大学生创业网](http://jdcy.jiangnan.edu.cn/)的通知公告栏目 (起点为[此页面][jdcy-startpoint], 并非首页上相应栏目的 "更多" 链接)
* [江南大学后勤信息网](http://hq.jiangnan.edu.cn/)通知公告栏目的站内新闻, 不包括外链内容 (已由对应相关站点的爬虫负责)
* [江南大学信息化建设与管理中心](http://nic.jiangnan.edu.cn/)的通知公告栏目
* [江南大学后勤管理处](http://hqc.jiangnan.edu.cn/)的通知公告栏目
* [江南大学保卫处](http://bwch.jiangnan.edu.cn/)的通知公告栏目

[jdcy-startpoint]: http://jdcy.jiangnan.edu.cn/newsclass_%E9%80%9A%E7%9F%A5%E5%85%AC%E5%91%8A_%E9%80%9A%E7%9F%A5%E5%85%AC%E5%91%8A.html


## 部署方法

*TODO: 完善这一部分的细节*

简略的草稿:

* 部署前提条件是有一个 Redis 服务器, 并且假定你已经准备好并且进入了一个 virtualenv 管理这个项目的依赖关系. `pip install -r requirements.txt` 就不用教了吧
* 首先定制 `Rainfile.yml` 中的数据库配置部分
* 然后部署爬虫附带的 Celery 服务: `celery -A campuspiders.tasks worker`, 这一步可以用 supervisord 之类的服务管理工具实现
* 设置 cronjob 按一定时间段分别触发各个爬虫的抓取任务
* 起 API 服务, 可以用 uWSGI 或者 gunicorn 这些东西做容器, 服务进程管理也用 supervisord 就行


## 授权

* GPLv3+


<!-- vim:set ai et ts=4 sw=4 sts=4 fenc=utf-8: -->
