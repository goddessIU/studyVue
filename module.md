# es6中module相关知识总结
之前有在红宝书上和一个小案例中，简单学习过module；这次，系统的学习了下，为后面深入学习vue打下基础；
主要依靠阮一峰老师的[es6入门](https://www.bookstack.cn/read/es6-3rd/docs-module.md),主要记录下主要知识点，方便日后复习

## export相关
```js
1.一次export一个变量
export var firstName = 'george';

2.export多个变量
let firstName = 'george';
let lastName = 'wang';
export { firstName, lastName };

3.export时重命名
function v1() {}
function v2() {}
export { v1 as s1, v2 as s2 };
//在import之后，就可以使用s1或者s2

```

## import相关
```js
1.一次引入一个
import { firstName, lastName } from 'util';
//然后就可以使用firstName和lastName了

2.改名引入
import { firstName as surname } from 'util';

3.仅仅执行加载的模块
import 'lodash';

4.整体载入
import * as circle from 'util';
//现在所有载入变量，都在circle这个对象上，成为其属性
```
import语句会执行加载的模块


## 默认导出
```js
//导出
export default function() {

}

//导入
import customName from 'util';//直接命名，无需{}
customName();


//导出的时候命名为default
function add() {

}
export {add as default}


//导入的时候改名
import { default as foo } from 'util';

//默认导入和其他导入同时import
import _, { a, b, c } from 'util'; 
```

## export与import符合写法
```js
export { foo, bar } from 'module';
直接转发接口，并未导入当前模块
```

## module加载实现
es6中module是动态加载的，所以在导入之后，使用某个值，是根据它当时的值。
```js
//导出
export var foo = 'var';
setTimeout(() => foo = 'bar', 1000);

//导入
import { foo } from 'util';
console.log(foo);
setTimeout(() => console.log(foo, 2000))
//var
//bar
一秒之后，foo值为bar
```

## 循环加载
教程中有循环加载一节（不直接抄了，不太好意思），从这里可以看出，是先把import导入的内容全部完成，才能继续执行导入模块后边的内容
```js
import {foo} from 'util';//把util中的导出引入完成后
console.log(foo)//在执行后面的内容
```

## 一个小栗子
一直困惑，若是a import b中的一个变量，就要把b都执行了？
写了个小栗子，如下：（原创的）
```html
<!-- 省去没用的，就留了个这个 -->
</body>
<script type='module' src='a.js'></script>
</html>
```

```js
//a.js
import {bar} from './b.js';
console.log('this is a.js');
console.log(bar);
```

```js
//b.js
console.log('this is b.js 1');
export var bar = 'abc';
console.log('this is b.js 2');
```

结果如下：
this is b.js 1
b.js:3 this is b.js 2
a.js:2 this is a.js
a.js:3 abc

好了，确实是执行了b全部


收工
如果哪里不对，请您指正，我会的还比较少，谢谢

