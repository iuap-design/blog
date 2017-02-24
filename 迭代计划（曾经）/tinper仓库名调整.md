# tinper仓库名调整

#### 已完成调整仓库

目前已对以下仓库做了调整：

* **neoui-polyfill**  ->  tinper-neoui-polyfill
* **neoui** ->  tinper-neoui
* **neoui-grid** -> tinper-neoui-grid
* **neoui-tree** -> tinper-neoui-tree
* **sparrow** -> tinper-sparrow

以下仓库名未做调整，但需要更改依赖

* **kero**

* **kero-adapter**

* tinper.org

* iuap-design.github.io

* generate-uui

建议迁移步骤

1.本地删除以下仓库

* neoui-polyfill
* neoui
* neoui-grid
* neoui-tree
* sparrow
* kero
* kero-adapter

2.升级`utip`至`1.3.5`

```
npm install -g utip@1.3.5
```
3.执行`utip pull`可`clone`并自动执行`cnpm install`更新

```
utip pull
```
4.以下三仓库tinper.org,iuap-design.github.io,generate-uui.删除`node_modules`，执行`npm install`

```
cd tinper.org
rm -rf node_modules/
npm install
```
备注：

如本地不删除仓库，可自行更新远程地址，更改远程地址方法。更改远程地址后，重复以上第4步

```shell
$ git remote set-url origin *new path*
```




***

以下为本次仓库调整概述：


| 原仓库                | 新仓库                   | 配套更改                                     | 初始版本号 |
| ------------------ | --------------------- | ---------------------------------------- | ----- |
| **generate-uui**   | generate-uui          | 原定cdn仓库名，暂不更改                            | -     |
| **neoui-polyfill** | tinper-neoui-polyfill | utip,tinper.org,iuap-design.org,kero-adapter | 0.1.0 |
| **neoui**          | tinper-neoui          | utip,kero-adapter                        | 0.1.0 |
| **neoui-grid**     | tinper-neoui-grid     | utip,kero-adapter                        | 0.1.0 |
| **neoui-tree**     | tinper-neoui-tree     | utip,kero-adapter                        | 0.1.0 |
| **sparrow**        | tinper-sparrow        | neoui,kero,polyfill, adapter,utip,定制     | 0.1.0 |
| kero               | kero                  |                                          | 3.5.0 |
| kero-adapter       | kero-adapter          |                                          | 1.6.0 |



neoui-polyfill

* package发包,更改版本号
* *依赖： sparrow未更改*
* iuap-design.org
  * package.son 版本号 + 依赖更改
  * gitbook-build.sh 依赖更改
* tinper.org
  * package.json 修改polyfill依赖
* kero-adapter
  * package.json
  * gulp file.json
* utip
  * build
  * check
  * checkdist
  * publish
  * pull


neoui

* 关键点：kero-adapter中的源文件依赖由neoui改为tinder-neoui，注意
* *定制下载的依赖还没有更改*tinper & iuap-design
* utip build/publish 依赖


定制下载

* category.js -> tinper-neoui
* neoui.json
* pack.js
* page/package.js



#### 推进计划

- 确认修改后仓库名
- 进一步确认仓库依赖关系
- 重新发包测试

#### 推进时间

- 仓库名依赖关系核查 1day
- 重新发包测试 2day（周末）
- 上线发现问题随时处理

#### 命名更改

| 原仓库名                                     | 新仓库名                  | 原npm           |
| ---------------------------------------- | --------------------- | -------------- |
| [kero-adapter](https://github.com/iuap-design/kero-adapter) | xxx                   | kero-adapter   |
| [neoui-grid](https://github.com/iuap-design/neoui-grid) | tinper-neoui-grid     | neoui-grid     |
| [generate-uui](https://github.com/iuap-design/generate-uui) | cdn                   | -              |
| [neoui](https://github.com/iuap-design/neoui) | tinper-neoui          | neoui          |
| [neoui-polyfill](https://github.com/iuap-design/neoui-polyfill) | tinper-neoui-polyfill | neoui-polyfill |
| [neoui-tree](https://github.com/iuap-design/neoui-tree) | tinper-neoui-tree     | neoui-tree     |
| [kero](https://github.com/iuap-design/kero) | xxx                   | kero           |
| [sparrow](https://github.com/iuap-design/sparrow) | tinper-sparrow        | neoui-sparrow  |
| [neoui-datetimepicker](https://github.com/iuap-design/neoui-datetimepicker) | 删除                    | -              |
| [neoui-knockout](https://github.com/iuap-design/neoui-knockout) | -                     | neoui-knockout |
| [templates](https://github.com/iuap-design/templates) | iuap-design-templates | -              |
| tinper-bee                               | -                     | -              |
| tinper-uba                               | -                     | -              |

#### 依赖关系

| 仓库                        | 依赖                                       | 依赖方法      |
| ------------------------- | ---------------------------------------- | --------- |
| neoui                     | sparrow                                  | npm       |
| kero                      | sparrow                                  | npm       |
| kero-adapter              | sparrow,neoui,kero,neoui-polyfill,neoui-grid,neoui-tree | npm,tip   |
| tinper.org/iuap-design.io | kero-adapter,neoui-polyfill              | shell定制下载 |
| generate-uui              | kero-adapter                             | shell下载   |
| utip                      | sparrow,neoui,kero,neoui-polyfill,neoui-grid,neoui-tree,kero-adapter | npm&shell |


