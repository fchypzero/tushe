# TUSHE

图社（TUSHE）是基于 FLask 的图床和图片浏览网站源码，也可以用作套图网站。网站采用 Mongodb 作为数据库，图片也储存于 GridFS。
采用 lask—Login 做用户认证，采用 Flask-Admin 做后台。

还用到了 Flask-Mongoengine, Flask-Bcrypt 等。见`requirements.txt`。

## 部署

### 要求

1. Python3.3+
1. pip install -r requirements.txt (Pillow 相关的支持见：[http://pillow.readthedocs.org/installation.html#linux-installation](http://pillow.readthedocs.org/installation.html#linux-installation))

### 部署方法
提供了uwsgi supervisor 配合 nginx 的配置文件。具体请参考他们的文档。

## 已知问题和解决方式

由于引用了 Flask-Login 和 GridFs，所有的请求会插入 Set-Cookie 的 Header。

目前的解决方式是在 Nginx 里面对对应的目录设置 uwsgi_hide_header Set-Cookie。

另外，为了不让每次请求都从数据库读取，可以再引入 Flask-Cache 和在 Nginx 里面设置 uwsgi_cache 相关参数。