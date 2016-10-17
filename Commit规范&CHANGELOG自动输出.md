# CHANGELOG规范

项目版本调整后，手动发布CHANGELOG.md.为规范`commit`提交，便于自动生成文档，现提供规范流程.

**0.规范**

参考AngularJS规范：[AngularJS's commit message convention](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#-git-commit-guidelines) 

### 提交Commit流程

**1.安装**

```
$ npm install -g commitizen
```

**2.进入仓库，配置Angular规范**

```
commitizen init cz-conventional-changelog --save-dev --save-exact
```

**3.提交commit**

```
git cz
```

使用`git cz`替换`git commit`，会有以下选项供选择：

```
feat：新功能（feature）
fix：修补bug
docs：文档（documentation）
style： 格式（不影响代码运行的变动）
refactor：重构（即不是新增功能，也不是修改bug的代码变动）
perf: 优化代码
test：增加测试
chore：构建过程或辅助工具的变动
revert：回退commit
```

针对目前流程，对fix提交说明进行规范如下：

* 项目问题

```

fix: 'pro-' + jira编号 + ':'  + 项目名称 + ':'+ 问题描述

```
每个项目问题都必须有对应的jira，并在jira描述中体现出项目名称。问题描述可直接拷贝jira描述。

* 其他问题

内部发现及修改项目问题中的额外提交，直接进行问题描述，保证每个jira问题只会有一个对应的提交。

其中，提交的`feat`,`fix`以后会生成到changelog.md文档中

```
* New feature
* Bug fix
```

选择对应的内容提交后，提示

* Denote the scope of this change ($location, $browser, $compile, etc.):需要输入作用域，此部分不做要求，直接回车进入下一步

* Write a short, imperative tense description of the change:**此部分输入本次提交内容**，回车

* Provide a longer description of the change:此部分不做要求，回车

* List any breaking changes or issues closed by this change:**如此次修改有修改issue，可输入关闭issue**

  ```
  Closes #234
  Closes #123, #245, #992
  ```

  ​

### 生成CHANGELOG.md文档流程

**安装输出**

```
$ npm install -g conventional-changelog-cli
$ cd my-project
$ conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

**简化命令**

在neoui仓库已配置了`package.json`，安装可直接执行

```
$ npm run changelog
```

