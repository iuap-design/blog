# iuapdesign持续集成

iuapdesign通过运维平台一键发布，实现官网预发布环境部署，可用于上线前测试&官网最终部署准备。

#### 流程图解

![iuap design持续集成全流程](https://cloud.githubusercontent.com/assets/11772494/20378437/1aab7752-acd1-11e6-917f-cbb226b3454f.png)

1. 本地开发测试
   * 开发人员在github仓库develop分支进行开发
   * 开发人员在本地环境测试
   * 测试完成提交合并develop分支到release分支
2. 预发布
   * 产品开发管理部门定时同步github仓库至gitlab仓库
   * 产品开发管理部门定时创建release分支镜像
   * 运维平台发布最新镜像
   * 线上测试修改
3. 正式上线
   * 提交可支持上线的docker镜像至最终环境




#### 流程概述

* Github仓库提交
* 代码同步
* docker镜像构建
* docker镜像预发布
* 项目正式上线



#### GitHub仓库提交

| 仓库名              | 仓库地址                                     | git拉取地址                                  | 说明                  | 端口号  |
| ---------------- | ---------------------------------------- | ---------------------------------------- | ------------------- | ---- |
| tinper.org       | https://github.com/iuap-design/tinper.org | git@github.com:iuap-design/tinper.org.git | tinper官网            | 8001 |
| generate-uui     | https://github.com/iuap-design/generate-uui | git@github.com:iuap-design/generate-uui.git | cdn资源               | -    |
| design.yyuap.com | https://github.com/iuap-design/design.yyuap.com | git@github.com:iuap-design/design.yyuap.com.git | design.yyuap.com 官网 | 8080 |
| designer         | https://github.com/iuap-design/designer  | git@github.com:iuap-design/designer.git  | 设计器                 | 9000 |
| mall             | http://git.yonyou.com/iuap-design/mall   | git@git.yonyou.com:iuap-design/mall.git  | 模板商城                | 4000 |



#### 代码同步

目前为产品管理部每天自动拉取同步代码，构建镜像。

*需求： 增加手动同步代码脚本*



#### docker镜像构建

通过`Build with Parameters`手动构建镜像。

目前输出镜像命名规则为时间戳

| 镜像             | 地址                                       | 备注   |
| -------------- | ---------------------------------------- | ---- |
| 设计器            | [design构建](http://ci.yonyou.com/jenkins/view/GF-iUAP/job/iUAP_design_release_Build_Docker/) |      |
| design.yyuap官网 | [yyuap构建](http://ci.yonyou.com/jenkins/view/GF-iUAP/job/iUAP_design.yyuap.com_release_Build_Docker/) |      |
| 商城             | [mall构建](http://ci.yonyou.com/jenkins/view/GF-iUAP/job/iUAP_design_mall_release_Build_Docker/) |      |
| tinper官网       | [tinper构建](http://ci.yonyou.com/jenkins/view/GF-iUAP/job/iUAP_design_tinper_release_Build_Docker/) |      |
| cdn            | [cdn构建](http://ci.yonyou.com/jenkins/view/GF-iUAP/job/iUAP_design_cdn_release_Build_Docker/) |      |
|                |                                          |      |



#### docker镜像预发布

预发布环境可在公司内网进行测试

通过登录运维平台，进入`发布管理`，选择对应项目，`执行构建`,等待预发布执行结果。

*log： design官网测试容器可查看日志记录*

| 名称       | IP地址                   | 备注               |
| -------- | ---------------------- | ---------------- |
| design   | 172.20.15.65           | design.yyuap.com |
| mall     | 172.20.15.65/mall      | 模板商城             |
| designer | 172.20.15.65/designer/ | 设计器              |
| tinper   | 172.20.15.66           | tinper官网         |
| 数据库      | 172.20.15.54           | 账号密码需查询邮件        |
| 运维环境     | 172.20.15.55           | 账号密码需查询邮件        |



#### 项目正式上线

预发布上线后，提交修改，创建新的镜像确认后，由运维部门根据稳定版镜像发布线上环境

正式环境信息

| 名称       | IP            | 域名（暂未解析）         |
| -------- | ------------- | ---------------- |
| design官网 | 123.56.25.92  | design.yyuap.com |
| tinper官网 | 123.56.28.142 | tinper.org       |





#### 后续工作及讨论

* 为什么不直接使用github仓库，还需要代码同步？

  同步原因：github拉取，公司存在网络问题，使用gitlab多次拉取，确保代码可完整拉取

  后续希望能还是直接采用github代码直接拉取更新。

* 需求：手动同步脚本(薛文)

* 需求：编译镜像自动发布(薛文，胡斌)

* 需求：构建成功,失败,发送邮件提醒（薛文）

* 需求：构建优化，基础镜像增加npm包（卫东，赵宇，胡斌）

* **后续：上线后切换CDN资源 & 域名解析**



#### 注意事项

* 仓库有如下更新：

  * 数据库
  * 配置文件等

  均需要联系运维部门，更新docker环境，确保产品正常运营

* 新版本上线需要提供：

  * 更改内容
  * 版本号等信息

  邮件发送给运维负责人员，安排上线