参考地址：https://juejin.cn/post/7119401211471609886
## let const的暂时性死区

let const 也存在变量提升  也可以说是不存在变量提升

当程序的控制流程在新的作用域（`module` `function` 或 `block` 作用域）进行实例化时，**在此作用域中用let/const声明的变量会先在作用域中被创建出来**，但因此时还未进行词法绑定，所以是不能被访问的，如果访问就会抛出错误。因此，在这运行流程进入作用域创建变量，到变量可以被访问之间的这一段时间，就称之为暂时死区。

*ES6规定，`let/const` 命令会使区块形成封闭的作用域。若在声明之前使用变量，就会报错。*
*总之，在代码块内，使用 `let` 命令声明变量之前，该变量都是不可用的。*
*这在语法上，称为 **“暂时性死区”**（ temporal dead zone，简称 **TDZ**）*

## 字符串扩展方法
1. includes() ：返回布尔值  表示找到了参数字符串
``` javascript

let s = 'hello world !'

s.includes('o') // true
```
`startsWith()` ：返回布尔值，表示参数字符串是否在原字符串的头部。

```js
s.startsWith('Hello') // true
复制代码
```

`endsWith()` ：返回布尔值，表示参数字符串是否在原字符串的尾部。

```js
s.endsWith('!') // true
```

`repeat()` ： 返回一个新字符串，表示将原字符串重复`n`次。

```js
'hello'.repeat(2) // "hellohello"
```

`padStart()` ： 字符串不够指定长度，将头部补全

```js
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'
```

`padEnd()` ： 字符串不够指定长度，将尾部补全。

```js
'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
复制代码
```

`trimStart()` ： 消除字符串头部的空格(返回的都是新字符串，不会修改原始字符串)

```js
const s = '  abc  ';
s.trimStart() // "abc  "
复制代码
```

`trimEnd()` ： 消除尾部的空格 (返回的都是新字符串，不会修改原始字符串)

```js
s.trimEnd() // "  abc"
复制代码
```

`matchAll()` ： 返回一个正则表达式在当前字符串的所有匹配  
`replaceAll()` ： 可以一次性替换所有匹配。

```js
'aabbcc'.replaceAll('b', '_') // 'aa__cc'
复制代码
```

`at()` ：接受一个整数作为参数，返回参数指定位置的字符，支持负索引

```js
const str = 'hello';
str.at(1) // "e"
```

  
