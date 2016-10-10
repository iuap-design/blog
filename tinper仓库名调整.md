# tinper仓库名调整

> 备注：tin per.org缺少自动更新polyfill,kero-adapter脚本
>
> 文本还未更新

#### 目前更改进度

更改远程地址方法：

```shell
$ git remote set-url origin *new path*
```

| 原仓库                | 新仓库                   | 配套更改                                     |
| ------------------ | --------------------- | ---------------------------------------- |
| **generate-uui**   | cdn                   | 本地，远程服务器更新                               |
| **neoui-polyfill** | tinper-neoui-polyfill | utip,tinper.org,iuap-design.org,kero-adapter |
| **neoui**          | tinper-neoui          | utip,kero-adapter                        |
| **neoui-grid**     | tinper-neoui-grid     | utip,kero-adapter                        |
| **neoui-tree**     | tinper-neoui-tree     | utip,kero-adapter                        |
| **sparrow**        |                       |                                          |
|                    |                       |                                          |



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


