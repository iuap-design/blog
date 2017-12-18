# JavaScript 编码规范

此为前端开发团队遵循和约定的 JavaScript 编码规范，意在提高代码的规范性和可维护性。

## <a name='types'>类型</a>

-   **原始值**: 相当于传值

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var foo = 1,
        bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
-   **复杂类型**: 相当于传引用

    + `object`
    + `array`
    + `function`

    ```javascript
    var foo = [1, 2],
        bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```


## <a name='objects'>对象</a>

- 使用字面值创建对象

  ```javascript
  // bad
  var item = new Object();

  // good
  var item = {};
  ```

- 不要使用保留字 [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) 作为键

  ```javascript
  // bad
  var superman = {
    class: 'superhero',
    default: { clark: 'kent' },
    private: true
  };

  // good
  var superman = {
    klass: 'superhero',
    defaults: { clark: 'kent' },
    hidden: true
  };
  ```

## <a name='arrays'>数组</a>

- 使用字面值创建数组

  ```javascript
  // bad
  var items = new Array();

  // good
  var items = [];
  ```

- 如果你不知道数组的长度，使用push

  ```javascript
  var someStack = [];

  // bad
  someStack[someStack.length] = 'abracadabra';
    
  // good
  someStack.push('abracadabra');
  ```

- 当你需要拷贝数组时使用slice

  ```javascript
  var len = items.length,
      itemsCopy = [],
      i;

  // bad
  for (i = 0; i < len; i++) {
    itemsCopy[i] = items[i];
  }

  // good
  itemsCopy = items.slice();
  ```

- 使用slice将类数组的对象转成数组.

  ```javascript
  function trigger() {
    var args = Array.prototype.slice.call(arguments);
    ...
  }
  ```



## <a name='strings'>字符串</a>

-   对字符串使用单引号 `''`

    ```javascript
    // bad
    var name = "Bob Parr";

    // good
    var name = 'Bob Parr';

    // bad
    var fullName = "Bob " + this.lastName;

    // good
    var fullName = 'Bob ' + this.lastName;
    ```

-   超过80个字符的字符串应该使用字符串连接换行
    - 注: 如果过度使用，长字符串连接可能会对性能有影响.

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that \
    was thrown because of Batman. \
    When you stop to think about \
    how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    var errorMessage = 'This is a super long error that ' +
    'was thrown because of Batman.' +
    'When you stop to think about ' +
    'how Batman had anything to do ' +
    'with this, you would get nowhere ' +
    'fast.';
    ```


- 编程时使用join而不是字符串连接来构建字符串，特别是IE

  ```javascript
  var items,
      messages,
      length, i;

  messages = [{
    state: 'success',
    message: 'This one worked.'
  },{
    state: 'success',
    message: 'This one worked as well.'
  },{
    state: 'error',
    message: 'This one did not work.'
  }];

  length = messages.length;

  // bad
  function inbox(messages) {
    items = '<ul>';

    for (i = 0; i < length; i++) {
      items += '<li>' + messages[i].message + '</li>';
    }

    return items + '</ul>';
  }

  // good
  function inbox(messages) {
    items = [];

    for (i = 0; i < length; i++) {
      items[i] = messages[i].message;
    }

    return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
  }
  ```



## <a name='functions'>函数</a>

-   函数表达式:

    ```javascript
    // 匿名函数表达式
    var anonymous = function() {
      return true;
    };

    // 有名函数表达式
    var named = function named() {
      return true;
    };

    // 立即调用函数表达式
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

-   绝对不要在一个非函数块里声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但是它们解析不同。
    - **注:** ECMA-262定义把`块`定义为一组语句，函数声明不是一个语句。[阅读ECMA-262对这个问题的说明](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    if (currentUser) {
      var test = function test() {
        console.log('Yup.');
      };
    }
    ```

    - 绝对不要把参数命名为 `arguments`, 这将会逾越函数作用域内传过来的 `arguments` 对象.

    ```javascript
    // bad
    function nope(name, options, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, options, args) {
      // ...stuff...
    }
    ```



## <a name='properties'>属性</a>

- 当使用变量访问属性时使用中括号.

  ```javascript
  var luke = {
    jedi: true,
    age: 28
  };

  function getProp(prop) {
    return luke[prop];
  }

  var isJedi = getProp('jedi');
  ```



## <a name='variables'>变量</a>

-   总是使用 `var` 来声明变量，如果不这么做将导致产生全局变量，我们要避免污染全局命名空间。

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

-   使用一个 `var` 以及新行声明多个变量，缩进4个空格。

    ```javascript
        // bad
        var items = getItems();
        var goSportsTeam = true;
        var dragonball = 'z';

        // good
        var items = getItems(),
            goSportsTeam = true,
            dragonball = 'z';
    ```

    - 最后再声明未赋值的变量，当你想引用之前已赋值变量的时候很有用。

    ```javascript
    // bad
    var i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    var i, items = getItems(),
        dragonball,
        goSportsTeam = true,
        len;

    // good
    var items = getItems(),
        goSportsTeam = true,
        dragonball,
        length,
        i;
    ```

    - 在作用域顶部声明变量，避免变量声明和赋值引起的相关问题。

    ```javascript
    // bad
    function() {
      test();
      console.log('doing stuff..');

      //..other stuff..

      var name = getName();

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // good
    function() {
      var name = getName();

      test();
      console.log('doing stuff..');

      //..other stuff..

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // bad
    function() {
      var name = getName();

      if (!arguments.length) {
        return false;
      }

      return true;
    }

    // good
    function() {
      if (!arguments.length) {
        return false;
      }

      var name = getName();

      return true;
    }
    ```



## <a name='conditionals'>条件表达式和等号</a>

-   适当使用 `===` 和 `!==` 以及 `==` 和 `!=`.
-   条件表达式的强制类型转换遵循以下规则：

    + **对象** 被计算为 **true**
    + **Undefined** 被计算为 **false**
    + **Null** 被计算为 **false**
    + **布尔值** 被计算为 **布尔的值**
    + **数字** 如果是 **+0, -0, or NaN** 被计算为 **false** , 否则为 **true**
    + **字符串** 如果是空字符串 `''` 则被计算为 **false**, 否则为 **true**

    ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

-   使用快捷方式.

    ```javascript
        // bad
        if (name !== '') {
          // ...stuff...
        }

        // good
        if (name) {
          // ...stuff...
        }

        // bad
        if (collection.length > 0) {
          // ...stuff...
        }

        // good
        if (collection.length) {
          // ...stuff...
        }
    ```

    - 阅读 [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) 了解更多



## <a name='blocks'>块</a>

- 给所有多行的块使用大括号

  ```javascript
  // bad
  if (test)
    return false;

  // good
  if (test) return false;

  // good
  if (test) {
    return false;
  }

  // bad
  function() { return false; }

  // good
  function() {
    return false;
  }
  ```



## <a name='comments'>注释</a>

-   使用 `/** ... */` 进行多行注释，包括描述，指定类型以及参数值和返回值

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param <String> tag
    // @return <Element> element
    function make(tag) {

      // ...stuff...

      return element;
    }

    // good
    /**
    * make() returns a new element
    * based on the passed in tag name
    * @param <String> tag
    * @return <Element> element
    */
    function make(tag) {
        // ...stuff...
        return element;
    }
    ```


-   使用 `//` 进行单行注释，在评论对象的上面进行单行注释，注释前放一个空行.

    ```javascript
    // bad
    var active = true;  // is current tab

    // good
    // is current tab
    var active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }
    ```

    - 如果你有一个问题需要重新来看一下或如果你建议一个需要被实现的解决方法的话需要在你的注释前面加上 `FIXME` 或 `TODO` 帮助其他人迅速理解

    ```javascript
    function Calculator() {

      // FIXME: shouldn't use a global here
      total = 0;

      return this;
    }
    ```

    ```javascript
    function Calculator() {

      // TODO: total should be configurable by an options param
      this.total = 0;

      return this;
    }
    ```




## <a name='whitespace'>空白</a>

-   将tab设为4个空格

    ```javascript
    // bad
    function() {
      ∙∙var name;
    }

    // bad
    function() {
      ∙var name;
    }

    // good
    function() {
      ∙∙∙∙var name;
    }
    ```
-   大括号前放一个空格

    ```javascript
        // bad
        function test(){
          console.log('test');
        }

        // good
        function test() {
          console.log('test');
        }

        // bad
        dog.set('attr',{
          age: '1 year',
          breed: 'Bernese Mountain Dog'
        });

        // good
        dog.set('attr', {
          age: '1 year',
          breed: 'Bernese Mountain Dog'
        });
    ```

    - 在做长方法链时使用缩进.

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // good
    $('#items')
      .find('.selected')
      .highlight()
      .end()
      .find('.open')
      .updateCount();

    // bad
    var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
        .attr('width',  (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);

    // good
    var leds = stage.selectAll('.led')
        .data(data)
      	.enter().append('svg:svg')
        .class('led', true)
        .attr('width',  (radius + margin) * 2)
      	.append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);
    ```


## <a name='commas'>逗号</a>

- 不要将逗号放前面

  ```javascript
  // bad
  var once
    , upon
    , aTime;

  // good
  var once,
      upon,
      aTime;

  // bad
  var hero = {
      firstName: 'Bob'
    , lastName: 'Parr'
    , heroName: 'Mr. Incredible'
    , superPower: 'strength'
  };

  // good
  var hero = {
    firstName: 'Bob',
    lastName: 'Parr',
    heroName: 'Mr. Incredible',
    superPower: 'strength'
  };
  ```

- 不要加多余的逗号，这可能会在IE下引起错误，同时如果多一个逗号某些ES3的实现会计算多数组的长度。

  ```javascript
  // bad
  var hero = {
    firstName: 'Kevin',
    lastName: 'Flynn',
  };

  var heroes = [
    'Batman',
    'Superman',
  ];

  // good
  var hero = {
    firstName: 'Kevin',
    lastName: 'Flynn'
  };

  var heroes = [
    'Batman',
    'Superman'
  ];
  ```



## <a name='semicolons'>分号</a>

- 语句结束一定要加分号

  ```javascript
  // bad
  (function() {
    var name = 'Skywalker'
    return name
  })()

  // good
  (function() {
    var name = 'Skywalker';
    return name;
  })();

  // good
  ;(function() {
    var name = 'Skywalker';
    return name;
  })();
  ```



## <a name='type-coercion'>类型转换</a>

-   在语句的开始执行类型转换.
-   字符串:

    ```javascript
        //  => this.reviewScore = 9;

        // bad
        var totalScore = this.reviewScore + '';

        // good
        var totalScore = '' + this.reviewScore;

        // bad
        var totalScore = '' + this.reviewScore + ' total score';

        // good
        var totalScore = this.reviewScore + ' total score';
    ```

    -  对数字使用 `parseInt` 并且总是带上类型转换的基数.

```javascript
   var inputValue = '4';

   // bad
   var val = new Number(inputValue);

   // bad
   var val = +inputValue;

   // bad
   var val = inputValue >> 0;

   // bad
   var val = parseInt(inputValue);

   // good
   var val = Number(inputValue);

   // good
   var val = parseInt(inputValue, 10);

   // good
   /**
   * parseInt was the reason my code was slow.
   * Bitshifting the String to coerce it to a
   * Number made it a lot faster.
   */
   var val = inputValue >> 0;
```

    - 布尔值:

    ​```javascript
    var age = 0;
    
    // bad
    var hasAge = new Boolean(age);
    
    // good
    var hasAge = Boolean(age);
    
    // good
    var hasAge = !!age;
    ​```



## <a name='naming-conventions'>命名约定</a>

-   避免单个字符名，让你的变量名有描述意义。

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

-   当命名对象、函数和实例时使用驼峰命名规则

    ```javascript
        // bad
        var OBJEcttsssss = {};
        var this_is_my_object = {};
        var this-is-my-object = {};
        function c() {};
        var u = new user({
          name: 'Bob Parr'
        });

        // good
        var thisIsMyObject = {};
        function thisIsMyFunction() {};
        var user = new User({
          name: 'Bob Parr'
        });
    ```

    - 当命名构造函数或类时使用驼峰式大写

      ```javascript
      // bad
      function user(options) {
        this.name = options.name;
      }

      var bad = new user({
        name: 'nope'
      });

      // good
      function User(options) {
        this.name = options.name;
      }

      var good = new User({
        name: 'yup'
      });
      ```

    - 命名私有属性时前面加个下划线 `_`

      ```javascript
      // bad
      this.__firstName__ = 'Panda';
      this.firstName_ = 'Panda';

      // good
      this._firstName = 'Panda';
      ```

    - 当保存对 `this` 的引用时使用 `_this`.

      ```javascript
      // bad
      function() {
        var self = this;
        return function() {
          console.log(self);
        };
      }

      // bad
      function() {
        var that = this;
        return function() {
          console.log(that);
        };
      }

      // good
      function() {
        var _this = this;
        return function() {
          console.log(_this);
        };
      }
      ```



## <a name='accessors'>存取器</a>

-   属性的存取器函数不是必需的
-   如果你确实有存取器函数的话使用getVal() 和 setVal('hello')

    ```javascript
        // bad
        dragon.age();

        // good
        dragon.getAge();

        // bad
        dragon.age(25);

        // good
        dragon.setAge(25);
    ```

    - 如果属性是布尔值，使用isVal() 或 hasVal()

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

    - 可以创建get()和set()函数，但是要保持一致

    ```javascript
    function Jedi(options) {
      options || (options = {});
      var lightsaber = options.lightsaber || 'blue';
      this.set('lightsaber', lightsaber);
    }

    Jedi.prototype.set = function(key, val) {
      this[key] = val;
    };

    Jedi.prototype.get = function(key) {
      return this[key];
    };
    ```



## <a name='constructors'>构造器</a>

- 给对象原型分配方法，而不是用一个新的对象覆盖原型，覆盖原型会使继承出现问题。

  ```javascript
  function Jedi() {
    console.log('new jedi');
  }

  // bad
  Jedi.prototype = {
    fight: function fight() {
      console.log('fighting');
    },

    block: function block() {
      console.log('blocking');
    }
  };

  // good
  Jedi.prototype.fight = function fight() {
    console.log('fighting');
  };

  Jedi.prototype.block = function block() {
    console.log('blocking');
  };
  ```

- 方法可以返回 `this` 帮助方法可链。

  ```javascript
  // bad
  Jedi.prototype.jump = function() {
    this.jumping = true;
    return true;
  };

  Jedi.prototype.setHeight = function(height) {
    this.height = height;
  };

  var luke = new Jedi();
  luke.jump(); // => true
  luke.setHeight(20) // => undefined

  // good
  Jedi.prototype.jump = function() {
    this.jumping = true;
    return this;
  };

  Jedi.prototype.setHeight = function(height) {
    this.height = height;
    return this;
  };

  var luke = new Jedi();

  luke.jump()
    .setHeight(20);
  ```


- 可以写一个自定义的toString()方法，但是确保它工作正常并且不会有副作用。

  ```javascript
  function Jedi(options) {
    options || (options = {});
    this.name = options.name || 'no name';
  }

  Jedi.prototype.getName = function getName() {
    return this.name;
  };

  Jedi.prototype.toString = function toString() {
    return 'Jedi - ' + this.getName();
  };
  ```



## <a name='events'>事件</a>

- 当给事件附加数据时，传入一个哈希而不是原始值，这可以让后面的贡献者加入更多数据到事件数据里而不用找出并更新那个事件的事件处理器

  ```js
  // bad
  $(this).trigger('listingUpdated', listing.id);

  ...

  $(this).on('listingUpdated', function(e, listingId) {
    // do something with listingId
  });
  ```

    更好:

  ```js
  // good
  $(this).trigger('listingUpdated', { listingId : listing.id });

  ...

  $(this).on('listingUpdated', function(e, data) {
    // do something with data.listingId
  });
  ```



## <a name='modules'>模块</a>

-   模块应该以 `!` 开始，这保证了如果一个有问题的模块忘记包含最后的分号在合并后不会出现错误
-   这个文件应该以驼峰命名，并在同名文件夹下，同时导出的时候名字一致
    - 加入一个名为noConflict()的方法来设置导出的模块为之前的版本并返回它
    - 总是在模块顶部声明 `'use strict';`

    ```javascript
    // fancyInput/fancyInput.js

    !function(global) {
      'use strict';

      var previousFancyInput = global.FancyInput;

      function FancyInput(options) {
        this.options = options || {};
      }

      FancyInput.noConflict = function noConflict() {
        global.FancyInput = previousFancyInput;
        return FancyInput;
      };

      global.FancyInput = FancyInput;
    }(this);
    ```



## <a name='jquery'>jQuery</a>

-   缓存jQuery查询

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...stuff...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // good
    function setSidebar() {
      var $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

-   对DOM查询使用级联的 `$('.sidebar ul')` 或 `$('.sidebar ul')`
    - 对有作用域的jQuery对象查询使用 `find`

    ```javascript
    // bad
    $('.sidebar', 'ul').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good (slower)
    $sidebar.find('ul');

    // good (faster)
    $($sidebar[0]).find('ul');
    ```



## <a name='es5'>ECMAScript 5兼容性</a>

- 参考Kangax的 ES5 [compatibility table](http://kangax.github.com/es5-compat-table/)






## 合理的组织js代码

#### 纯函数式

```
/**
 * [task description]
 * @param  {[type]}  [description]
 */
function Init(){
    domRneder();
    handleEvent();
}

/**
 * [task description]
 * @param  {[type]}  [description]
 */
function domRneder(){
    console.log('domRneder.....')
}

/**
 * [task description]
 * @param  {[type]}  [description]
 */
function handleEvent(){
    console.log('handleEvent......')
}


```

#### 单例模式

```
var Index = {
    /**
     * [task description]
     * @param  {[type]}  [description]
     */
    init: function (){
        this.domRender();
        this.handleEvent();
    },
    /**
     * [task description]
     * @param  {[type]}  [description]
     */
    domRneder: function(){
        console.log('domRender');
    },
    /**
     * [task description]
     * @param  {[type]}  [description]
     */
    handleEvent: function(){
        console.log('handleEvent');
        this.otherFn();
    },
    /**
     * [task description]
     * @param  {[type]}  [description]
     */
    otherFn: function(){
        console.log('todo....')
    }
};

Index.init();

```

#### 构造函数加原型

- 3.1第一种

```
/**
 * [task description]
 * @param  {[type]}  [description]
 */
var Robot = function(){
    this.a = 'a';
    this.b = 'b';
    this.init();
 }

/**
 * [task description]
 * @param  {[type]}  [description]
 */
Robot.prototype.init = function(){
    this.say();
    this.work();
}

/**
 * [task description]
 * @param  {[type]}  [description]
 */
Robot.prototype.say = function(){
    console.log('say...')
}

/**
 * [task description]
 * @param  {[type]}  [description]
 */
Robot.prototype.work = function(){
    console.log('work...')
}

new Robot();

```

- 3.2第二种

```
/**
 * [task description]
 * @param  {[type]}  [description]
 */
function Detail(){
    this.init();
};

/**
 * [task description]
 * @param  {[type]}  [description]
 */
Detail.view = {
    "PRICE_BTN" : $("._price_btn a")
}

/**
 * [task description]
 * @param  {[type]}  [description]
 */
Detail.prototype = {
    init : function(){
        this.initUrl();
    },
    initUrl : function(){
        console.log('handle.....')
    }
}

new Detail();

```

#### ES6 Module

```
class Person {
    constructor(){
        this.a = 'a';
        this.b = 'b'
    }
    say(){
        console.log('say.....')
    }
}

new Person();



```

### 代码间隙

```
// 1
if ( a > 0 ) { }

// 2
var x = 20;

// 3
for ( var i = 0, len = arr.length; i < len; i++ ) {

}

```

### 注释

```
/**
 * [task description]
 * @param  {[type]}  [description]
 */
function Detail(){
    this.init();

    // 变量定义
    var a = 'xx';
};

```

### 公共的方法进行抽离

### 4个空格缩进

```
// bad
function a ( ) {

    if () { }
  for () {}

        if () { }
}

// good
function a ( ) {

    if () { }
    for () {}
    if () { }
}


```

### 命名

- 名副其实，见名知意
- 小驼峰

```
// bad
var x1 = 0, a_77 = b;

// good
var newFeature = [];

```

### 断行

```
// bad
$.a().b({a: b}).c().dd()

// good
$.a()
 .b({a: b})
 .c()

```

### json格式

```
// bad
var a = {a: 9,c:0,cccc:'9409043'}

// good

var a = {
    a: 9,
    c: 0,
    cccc: '9409043'
}

```

## 5.git的使用和提交信息规范

1. 合理使用分支
2. 习惯用命令行，图形化工具可以作为辅助
3. 提交的信息要有意义，说明解决了什么bug，添加了什么feature功能
4. 习惯用 `git status`，时刻知道你当前在什么分支，当前的文件处于什么样的状态







## <a name='performance'>性能</a>

-   [On Layout & Web Performance](http://kellegous.com/j/2013/01/26/layout-performance/)
-   [String vs Array Concat](http://jsperf.com/string-vs-array-concat/2)
    - [Try/Catch Cost In a Loop](http://jsperf.com/try-catch-in-loop-cost)
    - [Bang Function](http://jsperf.com/bang-function)
    - [jQuery Find vs Context, Selector](http://jsperf.com/jquery-find-vs-context-sel/13)
    - [innerHTML vs textContent for script text](http://jsperf.com/innerhtml-vs-textcontent-for-script-text)
    - [Long String Concatenation](http://jsperf.com/ya-string-concat)
    - Loading...



## <a name='resources'>资源</a>

**Read This**

- [Annotated ECMAScript 5.1](http://es5.github.com/)

**其它规范**

- [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
- [jQuery Core Style Guidelines](http://docs.jquery.com/JQuery_Core_Style_Guidelines)
    - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwldrn/idiomatic.js/)

**其它风格**

- [Naming this in nested functions](https://gist.github.com/4135065) - Christian Johansen
- [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52)

**阅读更多**

- [Understanding JavaScript Closures](http://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll

**书籍**

- [JavaScript: The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
- [JavaScript Patterns](http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
    - [Pro JavaScript Design Patterns](http://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
    - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](http://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
    - [Maintainable JavaScript](http://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
    - [JavaScript Web Applications](http://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
    - [Pro JavaScript Techniques](http://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
    - [Smashing Node.js: JavaScript Everywhere](http://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch

**博客**

-   [Adam Lu](http://adamlu.com/)
-   [DailyJS](http://dailyjs.com/)
    - [JavaScript Weekly](http://javascriptweekly.com/)
    - [JavaScript, JavaScript...](http://javascriptweblog.wordpress.com/)
    - [Bocoup Weblog](http://weblog.bocoup.com/)
    - [Adequately Good](http://www.adequatelygood.com/)
    - [NCZOnline](http://www.nczonline.net/)
    - [Perfection Kills](http://perfectionkills.com/)
    - [Ben Alman](http://benalman.com/)
    - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
    - [Dustin Diaz](http://dustindiaz.com/)
    - [nettuts](http://net.tutsplus.com/?s=javascript)


# 声明


> 本规范由`github`上`adamlu`同学翻译自`airbnb`出品的前端代码规范，[点这里查看原文](https://github.com/GuoYongfeng/javascript)
