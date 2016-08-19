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

## 目前进展

* [neoui-datetimepicker](https://github.com/iuap-design/neoui-datetimepicker)组件仓库并入`neoui`组件
* 完成`sparrow`,`neoui`,`kero`,`kero-adapter`es6重构，输出第一版重构后的`u.js`,
* 各仓库已切换到正式的开发分支release
* 提供自动化构建，见[utip](https://github.com/iuap-design/utip/blob/master/README.md)

## 输出测试流程

以下介绍为输出u.js流程。

* 依赖关系

  各仓库之间，通过npm install对应的包进行依赖。下图为仓库信息

  | 目录           | 依赖                 | 压缩前  | 压缩后  | 备注              |
  | ------------ | ------------------ | ---- | ---- | --------------- |
  | sparrow      | -                  | 125  | 52   |                 |
  | neoui        | sparrow            | 532  | 244  | 含datetimepicker |
  | kero         | sparrow            | 219  | 86   |                 |
  | kero-adapter | sparrow,neoui,kero | 506  | 242  |                 |
  | u.js         | 以上所有               | 747  | 348  |                 |

* 仓库源码

  各仓库源码在根目录的`js`文件

* 输出u.js

  为规避npm发包繁琐流程，建议采用以下方式输出`u.js `进行测试

  1. 各仓库完成源码修改后，请在`kero-adapter`仓库中`node_modules`下找到同名文件包，用修改后的`js`目录替换对应同名文件下的对应目录

     > 注意1）sparrow在node_modules中名为neoui-sparrow; 2) 如包管理器有不同层级的node_modules,请注意将下一级中对应的文件目录进行相应替换

  2. kero-adapter 仓库执行`npm run product`即可在`dist`产出最终的`u.js`

  ​
