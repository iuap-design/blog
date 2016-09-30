# tinper仓库名调整

#### 推进计划

- 确认修改后仓库名
- 进一步确认仓库依赖关系
- 重新发包测试

#### 推进时间

- 仓库名依赖关系核查 1day
- 重新发包测试 2day（周末）
- 上线发现问题随时处理

#### 命名更改

| 原仓库名                                     | 新仓库名                | 原npm           | 新npm                |
| ---------------------------------------- | ------------------- | -------------- | ------------------- |
| [kero-adapter](https://github.com/iuap-design/kero-adapter) | tinper-kero-adapter | kero-adapter   | tinper-kero-adapter |
| [neoui-grid](https://github.com/iuap-design/neoui-grid) | tinper-ui-grid      | neoui-grid     | tinper-grid         |
| [generate-uui](https://github.com/iuap-design/generate-uui) | tinper-cdn          | -              | -                   |
| [neoui](https://github.com/iuap-design/neoui) | tinper-ui           | neoui          | tinper-ui           |
| [neoui-polyfill](https://github.com/iuap-design/neoui-polyfill) | tinper-ui-polyfill  | neoui-polyfill | tinper-ui-polyfill  |
| [neoui-tree](https://github.com/iuap-design/neoui-tree) | tinper-ui-tree      | neoui-tree     | tinper-ui-tree      |
| [kero](https://github.com/iuap-design/kero) | tinper-kero         | kero           | tinper-kero         |
| [sparrow](https://github.com/iuap-design/sparrow) | tinper-sparrow      | neoui-sparrow  | tinper-sparrow      |
| [neoui-datetimepicker](https://github.com/iuap-design/neoui-datetimepicker) | 删除                  | -              | -                   |
| [neoui-knockout](https://github.com/iuap-design/neoui-knockout) |                     | neoui-knockout |                     |
| [templates](https://github.com/iuap-design/templates) | tinper-templates    | -              | -                   |

#### 依赖关系

| 仓库                        | 依赖                                       | 依赖方法      |
| ------------------------- | ---------------------------------------- | --------- |
| neoui                     | sparrow                                  | npm       |
| kero                      | sparrow                                  | npm       |
| kero-adapter              | sparrow,neoui,kero,neoui-polyfill,neoui-grid,neoui-tree | npm,tip   |
| tinper.org/iuap-design.io | kero-adapter,neoui-polyfill              | shell定制下载 |
| generate-uui              | kero-adapter                             | shell下载   |
| utip                      | sparrow,neoui,kero,neoui-polyfill,neoui-grid,neoui-tree,kero-adapter | npm&shell |

