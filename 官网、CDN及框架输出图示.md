* 官网输出机制

<img width="1214" alt="default" src="https://cloud.githubusercontent.com/assets/11772494/17814686/963404fc-6663-11e6-96d1-e2d3f9c64c02.png">

* CDN机制

目前官网cdn均存储在generate-uui仓库的dist目录下，通过在服务器部署，可直接用在页面链接使用。如静态资源jquery存放于dist/jquery/jquery-1.9.1.min.js，可通过引用以下路径获取到http://design.yyuap.com/static/jquery/jquery-1.9.1.min.js.
<img width="914" alt="2016-08-19 11 30 40" src="https://cloud.githubusercontent.com/assets/11772494/17815071/478f90e4-6665-11e6-98c5-fdc98deb17d4.png">

* 框架机制

框架包含以下5个仓库，他们之间的关系见下
<img width="1098" alt="2016-08-19 11 43 47" src="https://cloud.githubusercontent.com/assets/11772494/17815467/032339d6-6667-11e6-9770-16fe1de0be3a.png">

延伸：
[utip介绍](https://github.com/iuap-design/utip):用于自动化输出u.js，省去中间发包等依赖环节
[重构目录及规划](https://github.com/iuap-design/blog/blob/master/iuapdesign%E9%87%8D%E6%9E%84%E7%9B%AE%E5%BD%95%26%E8%A7%84%E5%88%92.md):重构进展及介绍
