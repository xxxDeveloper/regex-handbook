<h1 align="center">
  <samp>正则手册</samp>
</h1>

## 量词
|   模式   |                 说明                 |                 示例                 |
| :------: | :----------------------------------: | :----------------------------------- |
|   `*`    |      重复 0 次或更多次，等价于 `{0,}`。 `贪婪模式`      |      表达式：`你好.*`<br />测试文本：<br />1：`你好`<br />2：`你好，世界`      |
|   `*?`    |      重复 0 次或更多次，等价于 `{0,}?`。 `惰性模式`      |      表达式：`你好.*?`<br />测试文本：<br />1：`你好`<br />2：`你好`，世界      |
|   `+`    |      重复 1 次或更多次，等价于 `{1,}`。 `贪婪模式`      |      表达式：`你好.+`<br />测试文本：<br />1：你好<br />2：`你好，世界`      |
|   `+?`    |      重复 1 次或更多次，等价于 `{1,}?`。 `惰性模式`      | 表达式：`你好.+?`<br />测试文本：<br />1：你好<br />2：`你好，`世界 |
|   `?`    |     重复 0 次或 1 次，等价于 `{0,1}` 。 `贪婪模式`     |     表达式：`你好.?`<br />测试文本：<br />1：`你好`<br />2：`你好，`世界     |
|   `??`    |     重复 0 次 或 1 次，等价于 `{0,1}?` 。 `惰性模式`     | 表达式：`你好.??`<br />测试文本：<br />1：`你好`<br />2：`你好`，世界 |
|  `{n}`   |     重复出现 `n` 次。 `贪婪模式`，匹配指定 `n` 次     | 表达式：`0\d{2}-\d{8}`<br />测试文本：<br />1：012-123456<br />2：`012-12345678`9 |
|  `{n}?`   |     重复出现 `n` 次。 `惰性模式`，与 `{n}` 一样，没啥区别     | 表达式：`0\d{2}-\d{8}?`<br />测试文本：<br />1：012-123456<br />2：`012-12345678`9 |
|  `{n,}`  |  至少重复出现 `n` 次。 `贪婪模式` ，优先匹配 `, ` >>> 更多次  | 表达式：`0\d{2}-\d{7,}`<br />测试文本：<br />1：012-123456<br />2：`012-123456789` |
|  `{n,}?`  |   至少重复出现 `n` 次。 `惰性模式`，优先匹配 `n`   | 表达式：`0\d{2}-\d{7,}?`<br />测试文本：<br />1：012-123456<br />2：`012-1234567`89 |
| `{n,m}`  | 重复出现 `n` 到 `m`  次。 `贪婪模式` ，优先匹配 `m` | 表达式：`0\d{2}-\d{7,8}`<br />测试文本：<br />1：012-123456<br />2：`012-12345678`9 |
| `{n,m}?`  | 重复出现 `n` 到 `m`  次。 `惰性模式` ，优先匹配 `n`  | 表达式：`0\d{2}-\d{7,8}?`<br />测试文本：<br />1：012-123456<br />2：`012-1234567`89 |

## 位置

|    模式    |                             说明                             | 示例                                                         |
| :--------: | :----------------------------------------------------------: | ------------------------------------------------------------ |
|    `^`     | 匹配字符串 `开头的位置`，当正则有修饰符 `m` 时，表示匹配行开头位置 | 表达式：`^0\d{6}`<br />测试文本：`0123456`7                  |
|    `$`     | 匹配 字符串`结尾的位置` ，当正则有修饰符 `m` 时，表示匹配行结尾位置 | 表达式：`^0\d{6}xxx$`<br />测试文本：<br />1：0123456xxxyyy<br />2：`0123456xxx` |
|    `\b`    |             匹配 `单词边界` ，既单词的开始和结束             | 表达式：`\bxxx\w*\b`<br />测试文本：`xxx666yyy`              |
|    `\B`    |        匹配 `非单词边界` ，既不是单词开头或结束的位置        | 表达式：`\Bxxx\w*\B`<br />测试文本：xxx666`xxx66`6           |
| `(?=xxx)`  | 匹配 `xxx` 前面的位置，`零宽断言` 也叫 `零宽度正预测先行断言` | 表达式：`/\b\w+(?=ing\b)/g`<br />测试文本：I'm `singing` while you're `dancing` |
| `(?<=xxx)` | 匹配 `xxx` 后面的位置，`零宽断言 ` 也叫`零宽度正回顾后发断言` | 表达式：`(?<=\bre)\w+\b`<br />测试文本：re`ading` a book     |
| `(?!xxx)`  | 匹配后面跟的不是 `xxx` 的位置，`负向零宽断言` 也叫`零宽度负预测先行断言` | 表达式：`\d{3}(?!\d)`<br />测试文本：123`456`xxx             |
| `(?<!xxx)` | 匹配前面不是 `xxx` 的位置，`负向零宽断言` 也叫`零宽度负回顾后发断言` | 表达式：`(?<![a-z])\d{7}`<br />测试文本：xxx0`1234567`89     |

## 括号

|      模式       |                             说明                             | 示例 |
| :-------------: | :----------------------------------------------------------: | ---- |
|     `(xxx)`     |           匹配 `xxx` ，并捕获文本到自动命名的组里            | 表达式：`\d{3}(xxx)\d{3}`<br />测试文本：`666xxx888` |
|    `(?:xxx)`    |      匹配 `xxx` ，不捕获匹配的文本，也不给此分组分配组号      | 表达式：`(?:xxx)\d{3}`<br />测试文本：666`xxx888` |
|  `(xxx\|yyy)`  |           匹配 `xxx` 或 `yyy` ，并捕获文本到自动命名的组里。`捕获型分支结构`           | 表达式：`(xxx\|yyy)\d{3}`<br />测试文本：666`yyy888` |
| `(?:xxx\|yyy)` | 匹配 `xxx` 或 `yyy`  ，不捕获匹配的文本，也不给此分组分配组号。`非捕获型分支结构`。 | 表达式：`(?:xxx\|yyy)\d{3}`<br />测试文本：666`xxx888` |
|     `\num`      | `后向引用` ，用于重复搜索前面某个分组匹配的文本。比如 `\1` ，表示引用的是第一个括号里的捕获的数据 | 表达式：`(?<=<(\w+)>)(.*?)(?=<\/(\1)>)`<br />测试文本：\<div\>`我是div标签`\<\/div\>\<span\>`我是span标签`\<\/span\> |

## 字符组

|    模式    |                            说明                             |
| :--------: | :---------------------------------------------------------: |
|  `[abc]`   |             匹配`a`、`b`、`c`中其中任何一个字符             |
| `[a-d1-4]` | 匹配 `a`、`b`、`c`、`d`、`1`、`2`、`3`、`4`其中任何一个字符 |
|  `[^abc]`  |       匹配 `除了` `a`、 `b`、 `c` 之外的任何一个字符        |
|    `.`     |     `通配符`，匹配除了少数字符（ `\n` ）之外的任意字符      |
|    `\d`    |                匹配  `数字`，等价于 `[0-9]`                 |
|    `\D`    |               匹配 `非数字`，等价于 `[^0-9]`                |
|    `\w`    |           匹配 `单词字符`，等价于 `[a-zA-Z0-9_]`            |
|    `\W`    |         匹配 `非单词字符` ，等价于 `[^a-zA-Z0-9_]`          |
|    `\s`    |            匹配 `空白符`，等价于 `[ \t\v\n\r\f]`            |
|    `\S`    |          匹配 `非空白符` ，等价于 `[^ \t\v\n\r\f]`          |


## 字面量

|    模式    |                             说明                             |
| :--------: | :----------------------------------------------------------: |
| 字面、数字 |          匹配字面量本身。比如 `/f/`  匹配字母 `"f"`          |
|    `\0`    |                        匹配 `NUL字符`                        |
|    `\t`    |                      匹配 `水平制表符`                       |
|    `\v`    |                      匹配 `垂直制表符`                       |
|    `\n`    |                        匹配 `换行符`                         |
|    `\r`    |                        匹配 `回车符`                         |
|    `\f`    |                        匹配 `换页符`                         |
|   `\xnn`   |          匹配  `拉丁字符` 。比如 `\xOA` 等价与 `\n`          |
|  `\uxxxx`  | 匹配  `Unicode字符` 。比如 `\u2028` 匹配 `行终止符`， `\u2029` 匹配 `段终止符` |
|   `\cX`    |    匹配 `ctrl+X` 。比如  `cI` 匹配  `ctrl+I`,等价于 `\t`     |
|   `[\b]`   |               匹配  `Backspace键（特殊记忆）`                |


## 修饰符
| 符号 |                             说明                             | 示例                                                         |
| :--: | :----------------------------------------------------------: | ------------------------------------------------------------ |
| `g`  |         `global - 全局匹配` ，找到所有满足匹配的子串         | 表达式：`/你好/g`<br />测试文本：<br />1：`你好`，世界，`你好`我好大家好 |
| `i`  |     `ignore - 忽略大小写` , 匹配过程中 `忽略字母大小写`      | 表达式：`/halo/gi`<br />测试文本：<br />1：`halo`，world、`HaLo`，`HALO`，WORLD |
| `m`  | `multi line - 多行匹配` ，把 `^` 和 `$` 变成  行开头  和  行结尾 | 表达式：`/halo/gm`<br />测试文本：<br />1：`halo`<br/>`halo`，world<br/>world，`halo` |
| `s`  | `single line - 单行匹配` ，更改 `.` 的含义，使它与每一个字符匹配（包括换行符 \n ） | 表达式：`/halo./gs`<br />测试文本：<br />1：`halo`<br/>world |
| `d`  |   `indices - 指数`，返回正则表达式在目标字符串中匹配的索引   | 表达式：`/halo./gd`<br />测试文本：world，`halo`<br/><br />使用 `exec` 会返回一个 `indices` 的数组，代表正则表达式在目标字符串中开始到结束的索引 |
| `y`  |       `sticky - 粘性`，匹配从目标字符串的当前位置开始        | 表达式#1：`/x+/y`<br />测试文本#1：`xxx`_xx_x<br /><br />表达式#2：`/x+/g`<br />测试文本#2：`xxx`_`xx`_`x` |
| `u`  |          `unicode ` ，使用 unicode 码的模式进行匹配          | 表达式#1：`/^\uD83D/.test('\uD83D\uDC2A')` <br />// >>> true <br /><br />表达式#2：`/^\uD83D/.test('\uD83D\uDC2A')` <br />// >>> false |

## RegExp

|  属性  |                        说明                        | 示例                                                         |
| :----: | :------------------------------------------------: | ------------------------------------------------------------ |
| `test` |    检索目标字符串中指定的值，返回 true 或 false    | /halo/g.test('world,halo.')<br/><br />// >>> true            |
| `exec` | 检索目标字符串中指定值，返回找到的值，并确定其位置 | /halo/g.exec('world,halo.')<br/><br />// >>> ['halo', index: 6, input: 'world,halo.', groups: undefined] |


## String
|    方法    |                             说明                             | 示例                                                         |
| :--------: | :----------------------------------------------------------: | ------------------------------------------------------------ |
|  `search`  |      返回匹配到的第一个子串在目标字符串中的 `位置索引`       | const str = 'world,halo'<br/>str.search(/halo/)<br /><br />// >>> 6 |
|  `split`   |    以匹配到的子串，对目标字符串 `进行切分` 。返回一个数组    | const str = 'world,halo.'<br/>str.split(/halo/)<br /><br />// >>> ['world,', '.'] |
|  `match`   |      返回匹配到的子串的结果数组，其中包含具体的匹配信息      | const str = 'world,halo.'<br/>str.match(/halo/)<br /><br />// >>> ['halo', index: 6, input: 'world,halo.', groups: undefined] |
| `matchAll` | 返回匹配到的所有子串的结果数组，其中包含具体的匹配信息，返回值是一个迭代器 | [...'world,halo.halo,world'.matchAll(/halo/g)]<br /><br />// >>> [<br />['halo', index: 6, input: 'world,halo.halo,world', groups: undefined],['halo', index: 11, input: 'world,halo.halo,world', groups: undefined]<br />] |
| `replace`  | 对目标字符串进行 `替换操作` 。正则是其第一个参数。返回替换后的字符串 | const str = 'world,halo.'<br/>str.replace(/halo/, 'hello')<br /><br />// >>> 'world,hello.' |

## Replace

> 这里是对第二个参数的说明汇总


|      字符      |             说明             |             示例             |
| :-------------: | :--------------------------: | ---------------------------- |
| `$1,$2,...,$99` | 匹配第1-99个分组里捕获的文本 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$1\_xxx\_")<br/><br />// >>> 'halo\_xxx\_.world,hello' |
|      `$&`       | 匹配到的子串文本 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$&\_xxx\_")<br/><br />// >>> 'world,halo\_xxx\_.world,hello' |
|      `$`\`      | 匹配到的子串的左边文本 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$`\_xxx\_")<br/><br />// >>> '\_xxx\_.world,hello' |
|       `$'`        | 匹配到子串的右边文本 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$'\_xxx\_")<br/><br />// >>> '.world,hello\_xxx\_.world,hello' |
|       `$$`        | 美元符号 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$$")<br/><br />// >>> '$.world,hello' |

### 参考
- [MDN Regexp](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
- [Regular 30-minute tutorial](https://deerchao.cn/tutorials/regex/regex.htm#howtouse)
- [JS Regex Mini Book](https://github.com/qdlaoyao/js-regex-mini-book)
