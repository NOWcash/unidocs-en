## 介绍

**uts 是什么**

uts 是一门跨平台的、高性能的、强类型的现代编程语言。它可以被翻译为不同平台的原生编程语言。如：JavaScript、Kotlin、Swift 等。

uts 采用了与 ts 基本一致的语法规范，支持绝大部分 ES6 API。因此前端工程师可以快速的掌握 uts 开发

## 快速入门
### 基本语法
#### 声明

uts 有两种声明方式

1. let

    声明一个可重新赋值的变量。语法 `let [变量名] : [类型] = 值;`。

    > 相当于 TypeScript 中的 let，kotlin 中的 var

```ts
let str = "hello"; // 声明一个字符串变量
str = "hello world"; // 重新赋值
```

2. const

    声明一个只读常量，只能为其赋值一次。语法 `const [变量名] : [类型] = 值;`。

    > 相当于 TypeScript 中的 const, kotlin 中的 val

```ts
const str = "hello"; // 声明一个字符串变量
str = "hello world"; // 报错，不允许重新赋值
```

#### 变量

在 uts 中，使用变量名需要遵守一定的规则。

-   变量名称可以包含数字和字母。

-   除了下划线 \_ 外，不能包含其他特殊字符，包括空格。

-   变量名不能以数字开头。

> 注意：与 TypeScript 不同的是，uts 不允许以 $ 开头命名变量

#### 操作符

##### 赋值运算符(Assignment operators)

| 名字                                              | 简写的操作符 | 含义        |
| ------------------------------------------------- | ------------ | ----------- | ---------- |
| 赋值(Assignment)                                  | x = y        | x = y       |
| 加法赋值(Addition assignment)                     | x += y       | x = x + y   |
| 减法赋值(Subtraction assignment)                  | x -= y       | x = x - y   |
| 乘法赋值(Multiplication assignment)               | x \*= y      | x = x \* y  |
| 除法赋值(Division assignment)                     | x /= y       | x = x / y   |
| 求余赋值(Remainder assignment)                    | x %= y       | x = x % y   |
| 左移位赋值(Left shift assignment)                 | x <<= y      | x = x << y  |
| 右移位赋值(Right shift assignment)                | x >>= y      | x = x >> y  |
| 无符号右移位赋值(Unsigned right shift assignment) | x >>>= y     | x = x >>> y |
| 按位与赋值(Bitwise AND assignment)                | x &= y       | x = x & y   |
| 按位异或赋值(Bitwise XOR assignment)              | x ^= y       | x = x ^ y   |
| 按位或赋值(Bitwise OR assignment)                 | x \|= y      | x \|= y     | x = x \| y |

##### 比较运算符(Comparison operators)

| 运算符                              | 描述                                        | 返回 true 的示例 |
| ----------------------------------- | ------------------------------------------- | ---------------- |
| 等于 Equal (==)                     | 如果两边操作数相等时返回 true。             | var1==var2       |
| 不等于 Not equal (!=)               | 如果两边操作数不相等时返回 true             | var1!=var2       |
| 全等 Strict equal (===)             | 两边操作数相等且类型相同时返回 true。       | var1===var2      |
| 不全等 Strict not equal (!==)       | 两边操作数不相等或类型不同时返回 true。     | var1!==var2      |
| 大于 Greater than (>)               | 左边的操作数大于右边的操作数返回 true       | var1>var2        |
| 大于等于 Greater than or equal (>=) | 左边的操作数大于或等于右边的操作数返回 true | var1>=var2       |
| 小于 Less than (<)                  | 左边的操作数小于右边的操作数返回 true       | var1<var2        |
| 小于等于 Less than or equal (<=)    | 左边的操作数小于或等于右边的操作数返回 true | var1<=var2       |

##### 算数运算符(Arithmetic operators)

| 运算符   | 范例 | 描述                                                                                                                                     |
| -------- | ---- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 求余(%)  |      | 二元运算符. 返回相除之后的余数.                                                                                                          |
| 自增(++) |      | 一元运算符. 将操作数的值加一. 如果放在操作数前面 (++x), 则返回加一后的值; 如果放在操作数后面 (x++), 则返回操作数原值,然后再将操作数加一. |
| 自减(--) |      | 一元运算符. 将操作数的值减一. 前后缀两种用法的返回值类似自增运算符.                                                                      |

##### 位运算符(Bitwise operators)

| Operator                        | Usage   | Description                                                                                                      |
| ------------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------- |
| 按位与 AND                      | a & b   | 在 a,b 的位表示中，每一个对应的位都为 1 则返回 1， 否则返回 0.                                                   |
| 按位或 OR                       | a \| b  | 在 a,b 的位表示中，每一个对应的位，只要有一个为 1 则返回 1， 否则返回 0.                                         |
| 按位异或 XOR                    | a ^ b   | 在 a,b 的位表示中，每一个对应的位，两个不相同则返回 1，相同则返回 0.                                             |
| 按位非 NOT                      | ~ a     | 反转被操作数的位。                                                                                               |
| 左移 shift                      | a << b  | 将 a 的二进制串向左移动 b 位,右边移入 0.                                                                         |
| 算术右移                        | a >> b  | 把 a 的二进制表示向右移动 b 位，丢弃被移出的所有位.(译注:算术右移左边空出的位是根据最高位是 0 和 1 来进行填充的) |
| 无符号右移(左边空出位用 0 填充) | a >>> b | 把 a 的二进制表示向右移动 b 位，丢弃被移出的所有位，并把左边空出的位都填充为 0                                   |

##### 逻辑运算符(Logical operators)

| 运算符       | 范例             | 描述     |
| ------------ | ---------------- | -------- |
| 逻辑与(&&)   | expr1 && expr2   | (逻辑与) |
| 逻辑或(\|\|) | expr1 \|\| expr2 | (逻辑或) |
| 逻辑非(!)    | !expr            | (逻辑非) |

##### 字符串运算符(String operators)

除了比较操作符，它可以在字符串值中使用，连接操作符（+）连接两个字符串值相连接，返回另一个字符串，它是两个操作数串的结合。

```ts
console.log("my " + "string"); // console logs the string "my string".
```

##### 条件（三元）运算符(Conditional operator)

条件运算符是 uts 中唯一需要三个操作数的运算符。运算的结果根据给定条件在两个值中取其一。语法为：

`条件 ? 值1 : 值2`

```ts
const status = age >= 18 ? "adult" : "minor";
```

### 基本类型

#### 布尔值（Boolean）

    有 2 个值分别是：true 和 false。

#### 数字（Number）

    整数或浮点数，例如： 42 或者 3.14159。

#### 字符串（String）

    字符串是一串表示文本值的字符序列，例如："hello" 。

#### null

    一个表明 null 值的特殊关键字。

### 字面量

字面量是由语法表达式定义的常量；或，通过由一定字词组成的语词表达式定义的常量

在 uts 中，你可以使用各种字面量。这些字面量是按字面意思给出的固定的值，而不是变量

#### 数组字面量

数组字面值是一个封闭在方括号对 ([]) 中的包含有零个或多个表达式的列表，其中每个表达式代表数组的一个元素。当你使用数组字面值创建一个数组时，该数组将会以指定的值作为其元素进行初始化，而其长度被设定为元素的个数。

下面的示例用 3 个元素生成数组coffees，它的长度是 3。

```ts
const coffees = ["French Roast", "Colombian", "Kona"]
const a=[3]
console.log(a.length) // 1
console.log(a[0]) // 3
```

数组字面值同时也是数组对象。

#### 布尔字面量

布尔类型有两种字面量：true和false。

#### 数字字面量

数字字面量包括多种基数的整数字面量和以 10 为基数的浮点数字面量

##### 整数字面量

整数可以用十进制（基数为 10）、十六进制（基数为 16）、二进制（基数为 2）表示。

- 十进制整数字面量由一串数字序列组成，且没有前缀 0。如：`0, 117, -345`

- 十六进制整数以 0x（或 0X）开头，可以包含数字（0-9）和字母 a~f 或 A~F。如：`0x1123, 0x00111 , -0xF1A7`

- 二进制整数以 0b（或 0B）开头，只能包含数字 0 和 1。如：`0b11, 0b0011 , -0b11`

##### 浮点数字面量

浮点数字面值可以有以下的组成部分：

- 一个十进制整数，可以带正负号（即前缀“+”或“ - ”），
- 小数点（“.”），
- 小数部分（由一串十进制数表示），
- 指数部分。

指数部分以“e”或“E”开头，后面跟着一个整数，可以有正负号（即前缀“+”或“-”）。浮点数字面量至少有一位数字，而且必须带小数点或者“e”（大写“E”也可）。

简言之，其语法是：

```
[(+|-)][digits][.digits][(E|e)[(+|-)]digits]
```

例如：

```ts
3.14
-.2345789 // -0.23456789
-3.12e+12  // -3.12*10^12
.1e-23    // 0.1*10^(-23)=10^(-24)=1e-24
```

#### RegExp字面量

正则表达式是字符被斜线围成的表达式。下面是一个正则表达式文字的一个例子。

```ts
const re = /ab+c/;
```

#### 字符串字面量

字符串字面量是由双引号（"）对或单引号（'）括起来的零个或多个字符。字符串被限定在同种引号之间；也即，必须是成对单引号或成对双引号。下面的例子都是字符串字面值：

```ts
"foo"
'bar'
"1234"
"one line \n another line"
"John's cat"
```

你可以在字符串字面值上使用字符串对象的所有方法，你也能用对字符串字面值使用类似 String.length 的属性：

```ts
console.log("John's cat".length)
// 将打印字符串中的字符个数（包括空格）
// 结果为：10
```

##### 模板字符串

模板字面量 是允许嵌入表达式的字符串字面量。你可以使用多行字符串和字符串插值功能。也被称为“模板字符串”。

```ts
// Basic literal string creation
`In uts '\n' is a line-feed.`

// Multiline strings
`In uts this is
 not legal.`

// String interpolation
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```
##### 转义特殊字符

|字符	|意思		|
|--		|--			|
|`\b`	|退格符		|
|`\f`	|换页符		|
|`\n`	|换行符		|
|`\r`	|回车符		|
|`\t`	|制表符		|
|`\'`	|单引号		|
|`\"`	|双引号		|
|`\\`	|反斜杠字符	|

### 控制流程

#### 条件

##### If 语句

当一个逻辑条件为真，用 if 语句执行一个语句。当这个条件为假，使用可选择的 else 从句来执行这个语句。if 语句如下所示：

```ts
if (condition_1) {
    statement_1;
} else if (condition_2) {
    statement_2;
} else if (condition_n_1) {
    statement_n;
} else {
    statement_last;
}
```

> 注意：if 和 else if 中的条件表达式必须为布尔值

##### switch 语句

switch 语句允许一个程序求一个表达式的值并且尝试去匹配表达式的值到一个 case 标签。如果匹配成功，这个程序执行相关的语句。switch 语句如下所示：

```ts
switch (expression) {
   case label_1:
      statements_1
      [break;]
   case label_2:
      statements_2
      [break;]
   default:
      statements_def
      [break;]
}
```

程序首先查找一个与 expression 匹配的 case 语句，然后将控制权转移到该子句，执行相关的语句。如果没有匹配值， 程序会去找 default 语句，如果找到了，控制权转移到该子句，执行相关的语句。如果没有找到 default，程序会继续执行 switch 语句后面的语句。default 语句通常出现在 switch 语句里的最后面，当然这不是必须的。

可选的 break 语句与每个 case 语句相关联， 保证在匹配的语句被执行后程序可以跳出 switch 并且继续执行 switch 后面的语句。如果 break 被忽略，则程序将继续执行 switch 语句中的下一条语句。

##### 三元表达式

uts 支持使用三元表达式。一个条件后面会跟一个问号（?），如果条件为 true ，则问号后面的表达式 A 将会执行；表达式 A 后面跟着一个冒号（:），如果条件为 false ，则冒号后面的表达式 B 将会执行。本运算符经常作为 if 语句的简捷形式来使用。

```ts
function getFee(isMember: boolean): string {
    return isMember ? "$2.00" : "$10.00";
}

console.log(getFee(true));
// expected output: "$2.00"

console.log(getFee(false));
// expected output: "$10.00"

console.log(getFee(null));
// expected output: "$10.00"
```

三元操作符是右结合的，也就是说你可以像这样把它链接起来， 和 if … else if … else if … else 链类似:

```ts
function example(): string {
    return condition1
        ? value1
        : condition2
        ? value2
        : condition3
        ? value3
        : value4;
}

// Equivalent to:

function example(): string {
    if (condition1) {
        return value1;
    } else if (condition2) {
        return value2;
    } else if (condition3) {
        return value3;
    } else {
        return value4;
    }
}
```

#### 循环

##### for

一个 for 循环会一直重复执行，直到指定的循环条件为 false。 一个 for 语句是这个样子的：

```ts
for ([initialExpression]; [condition]; [incrementExpression]) {
    statement;
}
```

当一个 for 循环执行的时候，会发生以下过程：

1. 如果有初始化表达式 initialExpression，它将被执行。这个表达式通常会初始化一个或多个循环计数器。
2. 计算 condition 表达式的值。如果 condition 的值是 true，循环中的语句会被执行。如果 condition 的值是 false，for 循环终止。如果 condition 表达式整个都被省略掉了，3. condition 的值会被认为是 true。
3. 循环中的 statement 被执行。如果需要执行多条语句，可以使用块（{ ... }）来包裹这些语句。
4. 如果有更新表达式 incrementExpression，执行更新表达式。
5. 回到步骤 2。

举例：

```ts
for (let i = 0; i < 10; i++) {
    //...
}
```
##### do...while

do...while 语句一直重复直到指定的条件求值得到假值（false）。 一个 do...while 语句看起来像这样：

```ts
do {
    statement;
} while (condition);
```

statement 在检查条件之前会执行一次。要执行多条语句（语句块），要使用块语句（{ ... }）包括起来。 如果 condition 为真（true），statement 将再次执行。 在每个执行的结尾会进行条件的检查。当 condition 为假（false），执行会停止并且把控制权交回给 do...while 后面的语句。

举例：

```ts
let i = 0;
do {
    i += 1;
} while (i < 10);
```

##### while

一个 while 语句只要指定的条件求值为真（true）就会一直执行它的语句块。一个 while 语句看起来像这样：

```ts
while (condition) {
    statement;
}
```

如果这个条件变为假，循环里的 statement 将会停止执行并把控制权交回给 while 语句后面的代码。

条件检测会在每次 statement 执行之前发生。如果条件返回为真， statement 会被执行并紧接着再次测试条件。如果条件返回为假，执行将停止并把控制权交回给 while 后面的语句。

要执行多条语句（语句块），要使用语句块 ({ ... }) 包括起来。

举例：

```ts
let n = 0;
let x = 0;
while (n < 3) {
    n++;
    x += n;
}
```

##### break

使用 break 语句来终止循环，switch。

举例：

```ts
for (let i = 0; i < 10; i++) {
    if (i > 5) {
        break;
    }
}
let x = 0;
while (true) {
    x++;
    if (x > 5) {
        break;
    }
}
```

##### continue

使用 continue 语句来终止当前循环，并在下一次迭代时继续执行循环。

举例：

```ts
for (let i = 0; i < 10; i++) {
    if (i > 5) {
        continue;
    }
}
let x = 0;
while (true) {
    x++;
    if (x > 5) {
        continue;
    }
}
```

#### 异常

你可以用 throw 语句抛出一个异常并且用 try...catch 语句捕获处理它。

使用 throw 表达式来抛出异常：

```ts
throw new Error("Hi There!");
```

使用 try……catch 表达式来捕获异常：

```ts

try {
    // 一些代码
} catch (e: Error) {
    // 处理程序
} finally {
    // 可选的 finally 块
}

```

### 函数

函数是 uts 中的基本组件之一。 一个函数是 uts 过程 — 一组执行任务或计算值的语句。要使用一个函数，你必须将其定义在你希望调用它的作用域内。

一个 uts 函数用 function 关键字定义，后面跟着函数名和圆括号。

#### 定义函数

##### 函数声明

一个函数定义（也称为函数声明，或函数语句）由一系列的 function 关键字组成，依次为：

-   函数的名称。
-   函数参数列表，包围在括号中并由逗号分隔。
-   函数返回值类型。
-   定义函数的 uts 语句，用大括号{}括起来。

> 注意：函数必须明确标明返回值类型

例如，以下的代码定义了一个简单的 add 函数：

```ts
function add(x: string, y: string): string {
    return x + y;
}
```

##### 函数表达式

虽然上面的函数声明在语法上是一个语句，但函数也可以由函数表达式创建。这样的函数可以是匿名的；它不必有一个名称。例如，函数 add 也可这样来定义：

```ts
const add = function (x: string, y: string): string {
    return x + y;
};
```

> 注意：函数表达式不支持使用函数名，比如`const add = function add(){}`是不允许的。

#### 调用函数

定义一个函数并不会自动的执行它。定义了函数仅仅是赋予函数以名称并明确函数被调用时该做些什么。调用函数才会以给定的参数真正执行这些动作。例如，一旦你定义了函数 add，你可以如下这样调用它：

```ts
add("hello", "world");
```

上述语句通过提供参数 "hello" 和 "world" 来调用函数。函数执行完它的语句会返回值 "hello world"。

#### 函数作用域

在函数内定义的变量不能在函数之外的任何地方访问，因为变量仅仅在该函数的域的内部有定义。相对应的，一个函数可以访问定义在其范围内的任何变量和函数。

```ts
const hello = "hello";
const world = "world";

function add(): string {
    return hello + world; // 可以访问到 hello 和 world
}
```

##### 嵌套函数

你可以在一个函数里面嵌套另外一个函数。嵌套（内部）函数对其容器（外部）函数是私有的。它自身也形成了一个闭包。一个闭包是一个可以自己拥有独立的环境与变量的表达式（通常是函数）。

既然嵌套函数是一个闭包，就意味着一个嵌套函数可以”继承“容器函数的参数和变量。换句话说，内部函数包含外部函数的作用域。

可以总结如下：

-   内部函数只可以在外部函数中访问。
-   内部函数形成了一个闭包：它可以访问外部函数的参数和变量，但是外部函数却不能使用它的参数和变量。

举例：

```ts
function addSquares(a: number, b: number): number {
    function square(x: number): number {
        return x * x;
    }
    return square(a) + square(b);
}
addSquares(2, 3); // returns 13
addSquares(3, 4); // returns 25
addSquares(4, 5); // returns 41
```

##### 命名冲突

当同一个闭包作用域下两个参数或者变量同名时，就会产生命名冲突。更近的作用域有更高的优先权，所以最近的优先级最高，最远的优先级最低。这就是作用域链。链的第一个元素就是最里面的作用域，最后一个元素便是最外层的作用域。

举例：

```ts
function outside(): (x: number) => number {
    let x = 5;
    const inside = function (x: number): number {
        return x * 2;
    };
    return inside;
}

outside()(10); // 返回值为 20 而不是 10
```

命名冲突发生在 return x 上，inside 的参数 x 和 outside 变量 x 发生了冲突。这里的作用链域是{inside, outside}。因此 inside 的 x 具有最高优先权，返回了 20（inside 的 x）而不是 10（outside 的 x）。

#### 闭包

闭包是 uts 中最强大的特性之一。uts 允许函数嵌套，并且内部函数可以访问定义在外部函数中的所有变量和函数，以及外部函数能访问的所有变量和函数。

但是，外部函数却不能够访问定义在内部函数中的变量和函数。这给内部函数的变量提供了一定的安全性。

此外，由于内部函数可以访问外部函数的作用域，因此当内部函数生存周期大于外部函数时，外部函数中定义的变量和函数的生存周期将比内部函数执行时间长。当内部函数以某一种方式被任何一个外部函数作用域访问时，一个闭包就产生了。

举例：

```ts
const pet = function (name: string): () => string {
    //外部函数定义了一个变量"name"
    const getName = function (): string {
        //内部函数可以访问 外部函数定义的"name"
        return name;
    };
    //返回这个内部函数，从而将其暴露在外部函数作用域
    return getName;
};
const myPet = pet("Vivie");
myPet(); // 返回结果 "Vivie"
```
#### 函数参数

##### 默认参数

函数参数可以有默认值，当省略相应的参数时使用默认值。

```ts
function multiply(a:number, b:number = 1):number {
  return a*b;
}
multiply(5); // 5
```
#### 箭头函数

箭头函数表达式（也称胖箭头函数）相比函数表达式具有较短的语法。箭头函数总是匿名的。

```ts
const arr = ["Hydrogen", "Helium", "Lithium", "Beryllium"];
const a2 = arr.map(function (s): number {
    return s.length;
});
console.log(a2); // logs [ 8, 6, 7, 9 ]
const a3 = arr.map((s): number => s.length);
console.log(a3); // logs [ 8, 6, 7, 9 ]
```

### 类

uts 中使用关键字 class 声明类

```ts
class Person {
    /*……*/
}
```

类声明由类名以及由花括号包围的类体构成。

#### 构造函数

constructor 是一种用于创建和初始化 class 创建的对象的特殊方法。

-   语法：

```ts
constructor([arguments]) { ... }
```

-   描述：

在一个类中只能有一个名为 “constructor” 的特殊方法。 一个类中出现多次构造函数 (constructor)方法将会抛出一个 SyntaxError 错误。

在一个构造方法中可以使用 super 关键字来调用一个父类的构造方法。

如果没有显式指定构造方法，则会添加默认的 constructor 方法。

如果不指定一个构造函数(constructor)方法, 则使用一个默认的构造函数(constructor)。

-   示例：

```ts
class Polygon {
    constructor() {
        this.name = "Polygon";
    }
}

class Square extends Polygon {
    constructor() {
        super();
    }
}
```

#### 继承

uts 允许使用继承来扩展现有的类。

-   语法：

```ts
class ChildClass extends ParentClass { ... }
```

-   描述：

extends 关键字用来创建一个类的子类。

-   示例：

```ts
class Polygon {}

class Square extends Polygon {}
```

##### 覆盖方法

uts 对于可覆盖的成员以及覆盖后的成员需要显式修饰符：

```ts
class Polygon {
    name(): string {
        return "Polygon";
    }
}

class Square extends Polygon {
    override name(): string {
        return "Square";
    }
}
```

Square.name 函数上必须加上 override 修饰符。如果没写，编译器会报错。

##### 覆盖属性

属性与方法的覆盖机制相同。在超类中声明然后在派生类中重新声明的属性必须以 override 开头，并且它们必须具有兼容的类型。

```ts
 class Shape {
     vertexCount: Int = 0
}

class Rectangle extends Shape {
    override  vertexCount = 4
}
```

##### 调用超类实现

派生类中的代码可以使用 super 关键字调用其超类的函数实现：

```ts
class Rectangle {
    draw() {}
}
class FilledRectangle extends Rectangle {
    override draw() {
        super.draw();
    }
}

```

#### 实例属性

uts 中实例属性存在于类的每一个实例中。

##### 声明实例属性

uts 可以在类中声明属性，默认可读，可写。

```ts
class Address {
    city: String = "beijing";
}
```

使用一个实例属性，以类实例引用它即可：

```ts
function copyAddress(address: Address): Address {
    const result = new Address();
    result.city = address.city; // 访问 city 属性
    return result;
}
```

##### Getter 与 Setter

uts 支持通过 getters/setters 来截取对对象成员的访问。 它能帮助你有效的控制对对象成员的访问。

```ts
const passcode = "secret passcode";
class Employee {
    private _fullName: string = "";

    get fullName(): string {
        return this._fullName;
    }

    set fullName(newName: string) {
        if (passcode === "secret passcode") {
            this._fullName = newName;
        } else {
            console.log("Error: Unauthorized update of employee!");
        }
    }
}
```

##### readonly

uts 可以使用 readonly 关键字将属性设置为只读的。 只读属性必须在声明时或构造函数里被初始化。

```ts
class Octopus {
    readonly name: string;
    readonly numberOfLegs: number = 8;
    constructor (theName: string) {
        this.name = theName;
    }
}
let dad = new Octopus("Man with the 8 strong legs");
dad.name = "Man with the 3-piece suit"; // 错误! name 是只读的.
```

#### 静态属性

使用关键字 static 来将一个属性声明为静态属性。静态属性不会在实例中被调用，而只会被类本身调用。

```ts
class ClassWithStaticField {
    static staticField = "static field";
}

console.log(ClassWithStaticField.staticField);
```

#### 实例方法

uts 中实例方法存在于类的每一个实例中。

##### 声明实例方法

uts 可以在类中声明实例方法。

```ts
class Rectangle {
    private height:number;
    private width:number;
    constructor(height: number, width: number) {
        this.height = height;
        this.width = width;
    }
    calcArea(): number {
        return this.height * this.width;
    }
}
```

使用一个实例方法，以类实例调用它即可：

```ts
const square = new Rectangle(10, 10);
square.calcArea();
```

#### 静态方法

使用关键字 static 来将一个方法声明为静态方法。静态方法不会在实例中被调用，而只会被类本身调用。它们经常是工具函数，比如用来创建或者复制对象。

```ts
class ClassWithStaticMethod {
    static staticMethod(): string {
        return "static method has been called.";
    }
}
ClassWithStaticMethod.staticMethod();
```

#### 可见性修饰符

类的方法与属性都可以有可见性修饰符。

在 uts 中有三个可见性修饰符：private、 protected、 和 public。 默认可见性是 public。

##### public

在 uts 中可以自由的访问程序里定义的 public 成员，这也是 uts 的默认行为。

##### private

当成员被标记成 private 时，它就不能在声明它的类的外部访问。比如：

```ts
class Cat {
    private name: string = "Cat";
}

new Cat().name; // 错误: 'name' 是私有的.
```

##### protected

protected 修饰符与 private 修饰符的行为很相似，但有一点不同，protected 成员在派生类中仍然可以访问。比如：

```ts
class Person {
    protected name: string;
    constructor(name: string) {
        this.name = name;
    }
}

class Employee extends Person {
    private department: string;

    constructor(name: string, department: string) {
        super(name);
        this.department = department;
    }

    public getElevatorPitch(): string {
        return `Hello, my name is ${this.name} and I work in ${this.department}.`;
    }
}
const howard = new Employee("Howard", "Sales");
console.log(howard.getElevatorPitch());
console.log(howard.name); // 错误
```

注意，我们不能在 Person 类外使用 name，但是我们仍然可以通过 Employee 类的实例方法访问，因为 Employee 是由 Person 派生而来的。

### 模块

uts 支持将程序拆分为可按需导入的单独模块，模块中可以导入和导出各种类型的变量，如函数，字符串，数字，布尔值，类等。

#### 导出

export 语句可以将一个文件中的函数，类等导出。比如：

```ts
export const name: string = "square";
export function draw() {}
export default class Canvas {} // default 关键词支持默认导出
```

- 导出的函数声明与类声明必须要有名称。
- export 命令可以出现在模块的任何位置，但必需处于模块顶层。
- 在一个文件中，export、import 可以有多个，export default 仅有一个。
- 通过 export 方式导出，在导入时要加{ }，export default 则不需要。

#### 导入

import 语句可以将另一个文件中的函数，类等导入到当前文件。比如：

```ts
import { name as name1, draw } from "./canvas.uts" // 支持 as 语法做别名导入
import * as Utils from "./utils.uts" // Test 包含所有 export 的导出
import Canvas from "./canvas.uts" // 对应 export default 的导出
```

示例

```ts
/*-----export [test.js]-----*/
export const name = 'test'
export function test(){
    console.log('test')
}
export default class Test{
    test(){
        console.log('Test.test')
    }
}
```

```ts
import { name } from './test.uts'
import * as testModule from './test.uts'
import Test from './test.uts'
console.log(name)
testModule.test()
const test = new Test()
test.test()
```

### 内置对象
#### Array

Array 对象是用于构造数组的全局对象，数组是类似于列表的高阶对象。

##### 实例属性

###### length

数组中的元素个数

##### 实例方法

###### concat

用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组

###### copyWithin

浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度

###### every

测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值

###### fill

用一个固定值填充一个数组中从起始索引到终止索引内的全部元素

###### filter

创建一个新数组，其包含通过所提供函数实现的测试的所有元素

###### find

返回数组中满足提供的测试函数的第一个元素的值

###### findIndex

返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回 -1

###### flat

按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回

###### flatMap

使用映射函数映射每个元素，然后将结果压缩成一个新数组

###### forEach

对数组的每个元素执行一次给定的函数

###### includes

判断一个数组是否包含一个指定的值，如果包含则返回 true，否则返回 false

###### indexOf

返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回 -1

###### join

将一个数组的所有元素连接成一个字符串并返回这个字符串

###### lastIndexOf

返回指定元素在数组中的最后一个的索引，如果不存在则返回 -1

###### map

返回一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值

###### pop

从数组中删除最后一个元素，并返回该元素的值

###### push

将一个或多个元素添加到数组的末尾，并返回该数组的新长度

###### reduce

对数组中的每个元素执行一个由您提供的 reducer 函数（升序执行），将其结果汇总为单个返回值

###### reduceRight

接受一个函数作为累加器（accumulator）和数组的每个值（从右到左）将其减少为单个值

###### shift

从数组中删除第一个元素，并返回该元素的值

###### slice

提取源数组的一部分并返回一个新数组

###### some

测试数组中是不是至少有一个元素通过了被提供的函数测试

###### splice

通过删除或替换现有元素或者原地添加新的元素来修改数组，并以数组形式返回被修改的内容

###### unshift

将一个或多个元素添加到数组的头部，并返回该数组的新长度

##### 常见操作

- 创建数组
```ts
const fruits = ['Apple', 'Banana']
console.log(fruits.length)
```
- 通过索引访问数组元素
```ts
const first = fruits[0]
// Apple
const last = fruits[fruits.length - 1]
// Banana
```
- 遍历数组
```ts
fruits.forEach(function(item, index, array) {
  console.log(item, index)
})
// Apple 0
// Banana 1
```
- 添加元素到数组的末尾
```ts
const newLength = fruits.push('Orange')
// ["Apple", "Banana", "Orange"]
```
- 删除数组末尾的元素
```ts
const last = fruits.pop() // remove Orange (from the end)
// ["Apple", "Banana"]
```
- 删除数组头部元素
```ts
const first = fruits.shift() // remove Apple from the front
// ["Banana"]
```
- 添加元素到数组的头部
```ts
const newLength = fruits.unshift('Strawberry') // add to the front
// ["Strawberry", "Banana"]
```
- 找出某个元素在数组中的索引
```ts
fruits.push('Mango')
// ["Strawberry", "Banana", "Mango"]
const pos = fruits.indexOf('Banana')
// 1
```
- 通过索引删除某个元素
```ts
const removedItem = fruits.splice(pos, 1) // this is how to remove an item
// ["Strawberry", "Mango"]
```
- 从一个索引位置删除多个元素
```ts
const vegetables = ['Cabbage', 'Turnip', 'Radish', 'Carrot']
console.log(vegetables)
// ["Cabbage", "Turnip", "Radish", "Carrot"]
const pos = 1
const n = 2
const removedItems = vegetables.splice(pos, n)
// this is how to remove items, n defines the number of items to be removed,
// starting at the index position specified by pos and progressing toward the end of array.
console.log(vegetables)
// ["Cabbage", "Carrot"] (the original array is changed)
console.log(removedItems)
// ["Turnip", "Radish"]
```
- 复制一个数组
```ts
const shallowCopy = fruits.slice() // this is how to make a copy
// ["Strawberry", "Mango"]
```
##### 访问数组元素

数组的索引是从 0 开始的，第一个元素的索引为 0，最后一个元素的索引等于该数组的 长度 减 1。

如果指定的索引是一个无效值，将会抛出 IndexOutOfBoundsException 异常

下面的写法是错误的，运行时会抛出 SyntaxError 异常，而原因则是使用了非法的属性名：

```ts
console.log(arr.0) // a syntax error
```

#### Date
#### Error
#### JSON
#### Map
#### Promise
#### RegExp
#### Set

## 学习资料

### JavaScript 开发者快速上手 uts
### Android 开发者快速上手 uts