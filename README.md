# meeko
![Build Stat](https://api.travis-ci.org/kongnet/meeko.svg?branch=master)
[![Coverage Status](https://coveralls.io/repos/github/kongnet/meeko/badge.svg?branch=master)](https://coveralls.io/github/kongnet/meeko?branch=master)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/fb7f44bf54b742ec97db7c17f49ceb4c)](https://www.codacy.com/app/9601698/meeko?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=kongnet/meeko&amp;utm_campaign=Badge_Grade)

[![NPM](https://nodei.co/npm/meeko.png?downloads=true&stars=true)](https://nodei.co/npm/meeko/)

[![Standard - JavaScript Style Guide](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/kongnet/meeko)

## 开始你的征途
``` js
let $ = require('meeko')
```
## 数学函数
``` js
$.math.linearFitting(xArray,yArray) 线性拟合
```
## 颜色基本函数
``` js
$.log($.c.dimr('dimred', backGroundColor[41-47], isUnderline))
```
## json color format
``` js
* $.dir(object)
* 内部10行代码实现 注意字符串下标数组无法显示
```

![JSON color format](https://github.com/kongnet/meeko/raw/master/screenShot/jsonFormat.png)

## $.compare
``` js
let cnDictObj = {items:[{'name':'a',lev:1},{name:'b',lev:2}]}
$.log(cnDictObj.items.sort(compare('lev', 'desc'))) //默认升序
```
## Array原型扩展
* *remove (idx = 0, len = 1)*
``` js
[1, 2, 3, 4, 5].remove(1,2) => [1,4,5]
```
* *count()* 
``` js
 ['A', 'B', 'B', 'C', 'A', 'D'].count() => {"A":2,"B":2,"C":1,"D":1}
```
* *flatten()* 
``` js
[1, [2, [3, [4, 5], 6], 7], 8].flatten() => [1,2,3,4,5,6,7,8]
```
* *orderBy()* 
``` js
[{ name: 'A', age: 48 }, { name: 'B', age: 36 }, { name: 'C', age: 26 }]
.orderBy(['age'],['asc']) 
=> [{"name":"C","age":26},{"name":"B","age":36},{"name":"A","age":48}] 默认升序
```

## String原型扩展
* *upperFirst()* 将首字母变成大写,其他小写
* *String.render(o)* 字符串模板渲染
* *fillStr(str, len, pos = 1)* 填入什么字符多少位,中文算2个字符,pos 1右面填，-1左面填

## Notice
``` js
$.tools.checkParam(obj)
* obj 如果为日期格式,日期格式为UTC日期
* 请在前端写入mysql之前 date.date2Str()一下
* 否则需要主动调用mysql的转换utc时间的函数
```
## 正则发生器
``` js
r = '(你|我|他)'
console.log($.reg.gen(r))
```
## 日期格式化
``` js
yyyy/YYYY mm/MM ww/WW dd/DD hh/HH mm ss SS(毫秒) q(季度) X(unix秒)
$.now().format('X')
```
## 路径下所有js文件全加载
``` js
$.requireAll() //加载某个目录下的所有对象，默认 __dirname
```
## 分布式雪花碎片算法 每秒可以产生超过200万 不重复id
``` js
new $.Snowflake(workId, dataCenterId, sequence) // 工作进程id ，服务器id，开始序号
```
## pipe 一个函数的输出是另一个函数的输入
``` js
 let r = $.pipe(x => x.toUpperCase(), // 单词变大写
      a => a.split(''), // -----------------分成数组
      a => a[3], // ------------------------取下标3
      s => s.charCodeAt(0).toString(16), // 变为16进制
      s => s.fillStr('0', 4, -1), // -------不足4位部分左边填0
      s => `\\u${s}` // --------------------转成\uxxxx 形式
    )('Test') // ----------------------- => \u0054
```
```mermaid
sequenceDiagram
    participant 用户A
    participant 用户B
    participant Bot
    用户A->>Bot: 你好啊？

    Bot-->>用户A: 你好!
    Note right of Bot: 人工智能核心代码
    用户B->>Bot: 在吗？
    Bot-->>用户B: 在!
    Note right of Bot: 去除[啊吗嘛]等<br/>语气助词,?换成! 
```
