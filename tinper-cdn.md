# `tinper-cdn` 公共静态资源库

## 代码仓库和维护流程

### 官网代码

1、 `http://tinper.org/dist/cdn/index.html` 官网展示页面，以及其对应的代码：`https://github.com/iuap-design/tinper.org/tree/release/src/cdn`；

### 爬取资源并上传oss

2、 `https://github.com/iuap-design/NodeSpider` 爬取第三方公共静态资源；<br />
3、 通过阿里 OSS 客户端将资源上传，key 和 secret 内部邮件有说明；<br />
4、 需要分别更新：cdnconfig目录，以及对应的资源目录。

### 【出现缓存问题的时候】更新cdn资源

5、 `http://git.yonyou.com/iuap-design/cdn-refresh` 刷新 `design.yyuap.com/static` 和 `design.yonyoucloud.com` 的 CDN 资源


## 维护和交接

guoyff@yonyou.com && yangchenchen6@yonyou.com
