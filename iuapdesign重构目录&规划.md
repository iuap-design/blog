## iuap design重构规划

## 仓库目录结构

整体项目`neoui组件`通过适配器`kero-adapter`，结合数据绑定`kero`，完成整套企业前端应用解决方案。

iuap design整体由以下多个仓库组成：

其中`NeoUI组件`,`kero-adapter适配器`,`kero数据绑定`,`generate打包输出`为目前主要维护部分。

**1.NeoUI组件**

包含所有UI组件

* [neoui](https://github.com/iuap-design/neoui):主要ui组件
* [neoui-grid](https://github.com/iuap-design/neoui-grid):grid表单相关组件
* [neoui-tree](https://github.com/iuap-design/neoui-tree):tree列表相关组件
* [neoui-datetimepicker](https://github.com/iuap-design/neoui-datetimepicker):datetimepicker日期相关组件


**2.kero-adapter适配器**

`NeoUI组件`和`kero数据绑定`的适配器

* [kero-adapter](https://github.com/iuap-design/kero-adapter):关联ui组件和kero数据绑定

**3.kero数据绑定**

用于进行数据绑定

* [kero](https://github.com/iuap-design/kero):组件数据绑定

**4.generate打包输出**

打包`NeoUI组件`、`kero-adapter适配器`、`kero数据绑定`，输出完整文件

* [generate-uui](https://github.com/iuap-design/generate-uui):打包输出完整文件,包含`u.js`,`u.css`(暂用之前打包名称)


**5.polyfill**

针对ie8提供polyfill脚本支持实现基本特性

* [neoui-polyfill](https://github.com/iuap-design/neoui-polyfill):针对低版本ie8的polyfill

**6.uba完整构建方案**

* 后续推出，目前使用`gulp+webpack+babel`方案

##  重构进行

重构思路如下：

* 功能拆分：`NeoUI组件`及`kero-adapter适配器`，根据插件功能进行拆分解，实现功能独立，方便后期维护
* 功能依赖：使用`es6`的`import`，`export`将独立功能进行模块化管理
* 自动化构建：目前为`gulp + webpack + babel`进行自动化构建输出，后续提供`uba`完整构建方案
* 发布：各仓库均通过`npm publish`进行发布
* 插件拆分：完成整体输出测试后，拆分各插件，建立各仓库实现从ui渲染，事件绑定，数据绑定的完整插件效果

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


