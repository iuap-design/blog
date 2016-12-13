#tinper-bee demo开发规范指南



###目录结构说明

* demo 根目录
* demolist  （Demo存放的根目录）
* index-demo-base.js （Demo父组件js，用来装载demo子组件）

###demolist下创建Demo@.js (@为整数，如0，1)

* 格式如下：

```javascript
/**
 *
 * @title 默认按钮
 *
 */
class Demo1 extends Component {
    constructor(props){
        super(props);
        this.state = {
            open: false
        }
    }
    render () {
        return (
            <div className="demoPadding">
                <Button>Default</Button>
                <Button disabled>disabled</Button>
            </div>
        )
    }
}
```
*  class Demo1 要求跟文件命名一致，首字母大写
*  @title 定义标题内容，长度截取后面20个字符
*  Demo1.js 文件命名要求首字母大写，后面添加整数


###生成规则

* demolist下的*.js会跟index-demo-base.js合并，
* 命名为index.js,发布到demo目录下
* 编译成demo.js,发布到dist目录下
