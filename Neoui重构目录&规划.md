## Neoui重构规划

## 仓库目录结构

整体项目`UI组件`通过适配器`kero-adapter`，结合数据绑定`kero`，完成整套企业前端应用解决方案。

Neoui整体由以下几个仓库组成：

**1.组件仓库**

包含所有UI组件

* [neoui](https://github.com/iuap-design/neoui):主要ui组件
* [neoui-grid](https://github.com/iuap-design/neoui-grid):grid表单相关组件
* [neoui-tree](https://github.com/iuap-design/neoui-tree):tree列表相关组件
* [neoui-datetimepicker](https://github.com/iuap-design/neoui-datetimepicker):datetimepicker日期相关组件

**2.适配器仓库**

`组件仓库`和`数据绑定仓库`的连接器

* [kero-adapter](https://github.com/iuap-design/kero-adapter):关联ui组件和kero数据绑定

**3.数据绑定仓库**

用于进行数据绑定

* [kero](https://github.com/iuap-design/kero):组件数据绑定

**4.打包输出仓库**

打包`组建仓库`、`适配器仓库`、`数据绑定仓库`，输出完整文件

* [generate-uui](https://github.com/iuap-design/generate-uui):打包输出完整Neoui文件


##  重构进行

重构思路如下：

* 功能拆分：UI及适配器仓库，根据插件功能进行拆分解，实现功能独立，方便后期维护


* 功能依赖：使用`es6`的`import`，`export`将独立功能进行模块化管理
* 自动化构建：`gulp + webpack + babel`进行自动化构建输出
* 发布：各仓库均通过`npm publish`进行发布
* 插件拆分：完成整体输出测试后，拆分各插件，建立各仓库实现从ui渲染，事件绑定，数据绑定的完整独立效果

## 仓库基本目录结构

├── dist 文件最终输出

├── example 测试用例

├── gulpfile.js 配置文件

├── js 原始js目录

├── lib es6转es5输出目录

├── package.json 

├── scss 原始样式文件目录

├── vendor 第三方依赖库

├── version.js 头部添加注释文件

└── webpack.config.js 配置文件


## 目前规划

* [neoui-datetimepicker](https://github.com/iuap-design/neoui-datetimepicker)组件仓库并入`neoui`组件


