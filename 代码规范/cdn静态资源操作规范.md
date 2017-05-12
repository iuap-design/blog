# 提交一个库

## Step 1

需要新建库目录及其版本目录，并将文件放在相应目录下，最后补全*package.json*文件。

```
├── backbone.js               # ... library
│   ├── 1.1.0                 # ... version
│   |   └── backbone.js       # ... fileanme
│   └── 1.1.1
│       └── backbone.js
└── package.json              # ... package.json

			
```


## Step 2

编辑*package.json*描述文件，这个文件描述最新版本的信息。

```
// 项目名必须与文件夹名一致
{
  "name": "项目名",
  "filename": "主文件名，比如 abc.js",
  "version": "1.0",
  "description": "项目简介",
  "homepage": "项目主页/网站地址",
  "keywords": ["关键字1", "关键字2", "关键字3"],
  "maintainers": [
	{
	  "name": "作者/维护者",
	  "web": "作者/维护者个人主页",
	  "mail": "作者/维护者邮件"
	}
  ],
  "repositories": [
	{
	  "type": "git",
	  "url": "开源库地址"
	}
  ]
}

			
```

## Step 3

将新建库的文件夹打包，然后将打包好的zip文件，发送给我。qq：1062887235，邮箱：huyueb@yonyou.com
