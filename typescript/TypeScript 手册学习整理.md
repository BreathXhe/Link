## 序

TypeScript是JavaScript语言的一个类型化超集，是由微软开发的免费、开源编程语言。其本质上是向JavaScript添加了一些可选的静态类型和基于类的面向对象编程特性，可编译为原生JavaScript语言。目前为止笔者仍认为学TypeScript是非必须的，但不可否认有很多`npm`模块都在使用或转为使用TypeScript开发，因此有必要学习和掌握这一语言扩展。

本文是非官方的TypeScript中文文档，基于[TypeScript 3.9](http://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-9.html)翻译和整理，请结合[官方文档](http://www.typescriptlang.org/)及相关版本参阅本文。

1. [快速上手](# 1. 快速上手)
2. [语言手册（Handbook）](# 2. 语言手册（Handbook）)
3. [手册引用（Handbook Reference）](# 3. 手册引用（Handbook Reference）)


## 1. 快速上手

- [1.1 安装](# 1.1 安装)
- [1.2 构建第一个TypeScript文件](# 1.2 构建第一个TypeScript文件)
- [1.3 编译代码](# 1.3 编译代码)
- [1.4 类型注释](# 1.4 类型注释)
- [1.5 接口](# 1.5 接口)
- [1.6 类](#1.6 类)
- [1.7 运行TypeScript Web应用](#1.7 运行TypeScript Web应用)

让我们使用TypeScript来构建一个简单的Web应用程序。

### 1.1 安装

可以使用以下两种方式来获取TypeScript工具：

- 通过[`npm`](https://www.npmjs.com/)(Node.js包管理器)
- 通过在Visual Studio中安装TypeScript插件

Visual Studio 2017和Visual Studio 2015 Update 3默认包含了TypeScript。如果你所使用版本的Visual Studio还没有安装TypeScript，你可以[下载它](http://www.typescriptlang.org/#download-links)。

对于`NPM`用户来说，可以：

```
$ npm install -g typescript
```



### 1.2 构建第一个TypeScript文件

在你的编辑器中输入以下代码，并保存到`greeter.ts`文件中：

```
function greeter(person) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```



### 1.3 编译代码

虽然使用了`.ts`扩展名，但是这段代码只是JavaScript。可以直接复制/粘贴此内容到现有的JavaScript应用中。

在命令行中，运行TypeScript编译器：

```
$ tsc greeter.ts
```

这会生成一个`greeter.js`文件，其会包含与你输入文件相同的JavaScript代码。然后，就可以运行这个使用TypeScript编写的JavaScript应用了。

现在，我们开始使用TypeScript提供的一些新工具。在*"person"*函数的参数中添加`:string`类型注释，如下所示：

```
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```



### 1.4 类型注释

在TypeScript中，类型注释是记录函数或变量预期约定的轻量级方法。在本示例中，我们打算用单个字符串参数来调用*greeter*函数。可以尝试修改调用方式，并传递一个数组：

```
function greeter(person: string) {
    return "Hello, " + person;
}

let user = [0, 1, 2];

document.body.textContent = greeter(user);
```

重新编译后，会看到一个错误：

```
error TS2345: Argument of type 'number[]' is not assignable to parameter of type 'string'.
```

同样，可以试着删除*greeter*调用的所有参数。TypeScript会告诉你使用意外数量的参数调用了此函数。这两种情况，TypeScript都可以基于代码的结构和所提供的类型注释提供静态分析。

请注意，尽管有错误，但仍然会创建`greeter.js`文件。即使代码中有错误，仍可以使用TypeScript，但这种情况下，TypeScript会警告你的代码可能不会按预期运行。



### 1.5 接口

接下来进一步开发这个示例。在这里，我们将使用接口来描述一个有*firstName*和*lastName*字段的对象。在TypeScript中，如果两个类型的内部结构兼容，则它们是兼容的。这使我们可以通过接口所需的结构来描述接口，而无需显式的实现子句。

```
interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "Jane", lastName: "User" };

document.body.textContent = greeter(user);
```



### 1.6 类

最后，让我们用类来扩展示例。TypeScript支持JavaScript中的新特性，例如：对基于类的面向对象编程的支持。

在这里，我们将创建一个带有构造函数和一些公共字段的`Student`类。注意，类和接口可以很好地配合使用，从而使开发者可以正确的决定抽象级别。

还要注意，在构造函数的参数上使用`public`是一种快捷方式，它使我们能够自动创建具有该名称的属性。

```
class Student {
    fullName: string;
    constructor(public firstName: string, public middleInitial: string, public lastName: string) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = new Student("Jane", "M.", "User");

document.body.textContent = greeter(user);
```

重新运行`tsc greeter.ts`，可以看到所生成的JavaScript与先前的代码相同。TypeScript中的类只是JavaScript中经常使用的基于原型（*prototype-based*）的OO的简写。



### 1.7 运行TypeScript Web应用

现在，在`greeter.html`中输入以下内容：

```
<!DOCTYPE html>
<html>
    <head><title>TypeScript Greeter</title></head>
    <body>
        <script src="greeter.js"></script>
    </body>
</html>
```

在浏览器中打开`greeter.html`，就可以看到我们首个TypeScript Web应用了。



**附录**

如果在Visual Studio中打开`greeter.ts`，或将代码复制到TypeScript 练习场（*playground*）。就可以将鼠标悬停在标识符上以查看其类型、根据DOM元素的类型查看完成列表和参数帮助、将光标放在对*greeter*函数的引用上然后按F12键转到其定义等。



## 2. 语言手册（Handbook）

- [2.1 TypeScript手册](#2.1 TypeScript手册)
- [2.2 基本类型（Basic Types）](#2.2 基本类型（Basic Types)
- [2.3 接口（Interfaces）](#2.3 接口（Interfaces）)
- [2.4 函数（Functions）](#2.4 函数（Functions）)
- [2.5 字面量类型（Literal Types）](#2.5 字面量类型（Literal Types）)
- [2.6 联合与交叉类型（Unions and Intersection Types）](2.6 联合与交叉类型（Unions and Intersection Types）)
- [2.7 类（Classes）](2.7 类（Classes）)
- [2.8 枚举（Enums）](2.8 枚举（Enums）)
- [2.9 泛型（Generics）](2.9 泛型（Generics）)

### 2.1 TypeScript手册

- [1. 关于本手册](#1. 关于本手册)
- [2. 本手册的结构](#2. 本手册的结构)
- [3. 开始使用](#3. 开始使用)

#### 1. 关于本手册

在进入编程社区20多年后，JavaScript现已成为有史以来使用最广泛的跨平台语言之一。JavaScript最初是一种用于向网页添加交互的小型脚本语言，如今已成长为各种规模的前端和后端应用程序的首选语言。虽然用JavaScript编写的程序的大小、范围和复杂性呈指数级增长，但JavaScript语言却缺乏表达不同代码单元之间的关系的能力。加上JavaScript特有的运行时语义，语言和代码复杂性之间的不匹配使JavaScript开发成为难以大规模管理的任务。

程序员写代码最常见的错误可以描述为类型错误：在期望使用某种类型值的情况下，使用了其它类型的值。这可能由简单的输入错误、未知库的API、关于运行时行为的错误假设或其它错误所致。TypeScript的目标是成为JavaScript程序的静态类型检查器-换句话说，一种在代码运行之前运行的工具（静态），并通过类型检查确保程序类型的正确。

假如你是在没有JavaScript背景的情况下使用TypeScript的，TypeScript是你的第一语言，那么我们建议你首先从[Mozilla Web Docs的JavaScript文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)开始阅读。如果你有其他语言的经验，就可以通过阅读手册快速掌握JavaScript语法。



#### 2. 本手册的结构

本手册分为两部分：

- 语言手册

  《TypeScript手册》旨在向程序员提供对TypeScript介绍的全面性文档。你可以根据本文索引结构从上至下阅读手册。

  通过对每一章或每一页阅读，都可以使你对相关概念有更深刻的理解。《 TypeScript手册》不是完整的语言规范，但可作为该语言所有功能和行为的全面指南。

  完成学习的读者应该能够：

  - 阅读并了解常用的TypeScript语法和模式
  - 解释重要的编译器选项的作用
  - 大多数情况下可以正确预测类型系统的行为
  - 为简单的函数、对象或类编写`.d.ts`声明

  出于清楚和简洁起见，本手册的主要内容不会探讨所涵盖功能的每一个极端情况或细节。但可以在参考文章中找到相关概念的更多详细信息。

- 手册引用

  手册参考旨在提供对TypeScript指定部分如何工作的深层次介绍。你可以从上到下阅读，但是每个部分的目的都是提供对单个概念的更深入的说明-也就是说并没有连续性的关系。



##### **非目标**

本手册的目标还包括成为简洁的语言文档，可以在几个小时内轻松阅读。为了简短起见，将不会涉及某些主题。

也就是说，本手册并没有完全介绍诸如函数、类和闭包之类的JavaScript核心基础知识。在适当的地方，我们将提供指向相关资料查看链接，可用于阅读理解相关概念。

本手册也不能替代语言规范。在某些情况下，将跳过一些极端情况或对行为的具体描述，而转而使用更高的级、易于理解的解释。但会有单独的参考页，它们可以更准确、更正式地TypeScript行为描述。参考页不适合不熟悉TypeScript的读者，因此可能使用高级术语或你尚未读到的参考主题。

最后，非必要情况下本手册不会介绍TypeScript与其它工具的交互方式。像如何通过*webpack*、*rollup*、*parcel*、*react*、*babel*、*closure*、*lerna*、*rush*、*bazel*、*preact*、*vue*、*angular*、*svelte*、*jquery*、*yarn*、或*npm*来配置TypeScript，都不在的介绍主题范围内-可以在其它相关网站找到这些资源的介绍。



#### 3. 开始使用

在开始[基本类型](#2.2基本类型)之前，建议阅读以下介绍性页面之一。这些介绍旨在强调TypeScript与你喜欢的编程语言之间的主要异同，并消除针对这些语言的常见误解。

- [TypeScript for New Programmers](https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html)
- [TypeScript for JavaScript Programmers](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)
- [TypeScript for OOP Programmers](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html)
- [TypeScript for Functional Programmers](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html)



### 2.2 基本类型（Basic Types）

- [1. 介绍](#1. 介绍)
- [2. Boolean](#2. Boolean)
- [3. Number](#3. Number)
- [4. String](#4. String)
- [5. Array](#5. Array)
- [6. Tuple](#6. Tuple)
- [7. Enum](#7. Enum)
- [8. Any](#8. Any)
- [9. Void](#9. Void)
- [10. Null与Undefined]#10. Null与Undefined)
- [11. Never](#11. Never)
- [12. Object](#12. Object)
- [13. 类型断言](#13. 类型断言)
- [14. 关于`'let'`](#14. 关于`'let'`)

#### 1. 介绍

为了使程序有用，我们需要能够使用一些最简单的数据单元：数字、字符串、结构、布尔值等。在TypeScript中，支持与JavaScript中几乎相同的类型，并提供了枚举类型以方便处理。



#### 2. Boolean

最基本的数据类型是简单的`true`/`false`值，JavaScript和TypeScript中都将该值称为布尔(`boolean`)值。

```
let isDone: boolean = false;
```



#### 3. Number

与JavaScript中一样，TypeScript中的所有数字都是浮点值。这些浮点数的类型为`number`。除了十六进制和十进制字面量外，TypeScript还支持ECMAScript 2015中引入的二进制和八进制字面量。

```
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```



#### 4. String

用JavaScript为网页和服务器创建程序的另一个基本部分是使用文本数据。与其他语言一样，使用`string`类型来表示这些文本数据类型。与JavaScript一样，TypeScript也使用双引号（`"`）或单引号（`'`）包围字符串数据。

```
let color: string = "blue";
color = 'red';
```

同样也可使用“模板字符串”（[*template strings*](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/template_strings)），模板字符串可以跨多行并可以嵌入式表达式。模板字符串通过反引号（```）字符包围，嵌入式表达式的格式为：`${ expr }`。

```
let fullName: string = `Bob Bobbington`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ fullName }.

I'll be ${ age + 1 } years old next month.`;
```

这相当于像这样声明`sentence`：

```
let sentence: string = "Hello, my name is " + fullName + ".\n\n" +
    "I'll be " + (age + 1) + " years old next month.";
```



#### 5. Array

像JavaScript一样，TypeScript允许使用值数组。数组类型可以用以下两种方式编写。首先，可以使用`[]`来包裹指定类型的元素以表示该元素类型的数组：

```
let list: number[] = [1, 2, 3];
```

第二，可以使用普通的数组类型：`Array<elemType>`

```
let list: Array<number> = [1, 2, 3];
```



#### 6. Tuple

元组类型允许你用固定数量的元素表示数组，这些元素的类型是已知的，但不必相同。例如，你可能希望将值表示为一对字`string`和一个`array`：

```
// 声明元组类型
let x: [string, number];
// 初始化
x = ["hello", 10]; // OK
// 错误的初始化
x = [10, "hello"]; // Error
Type 'number' is not assignable to type 'string'.
Type 'string' is not assignable to type 'number'.
```

当访问已知索引的元素时，将获取正确的类型：

```
console.log(x[0].substring(1)); // OK
console.log(x[1].substring(1)); // Error, 'number' does not have 'substring'
Property 'substring' does not exist on type 'number'.
```

访问一组已知索引之外的元素会失败，并显示相关错误：

```
x[3] = "world"; // Error, Property '3' does not exist on type '[string, number]'.

console.log(x[5].toString()); // Error, Property '5' does not exist on type '[string, number]'.
Object is possibly 'undefined'.
Tuple type '[string, number]' of length '2' has no element at index '5'.
label type '[string, number]' of length '2' has no element at index '3'.
Object is possibly 'undefined'.
Tuple type '[string, number]' of length '2' has no element at index '5'.
```





#### 7. Enum

对标准JavaScript数据类型集的一个有益补充是`enum`。与C#等语言一样，枚举是一种为数字值集赋予更友好名称的方法。

```
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green;
```

默认情况下，枚举开始从`0`开始对其成员编号。也可以通过手工设置其成员之一的值来对其进行更改。例如，我们可以将前面示例设置为从`1`而不是`0`：

```
enum Color {
  Red = 1,
  Green,
  Blue,
}
let c: Color = Color.Green;
```

或者也可以设置所有枚举成员：

```
enum Color {
  Red = 1,
  Green = 2,
  Blue = 4,
}
let c: Color = Color.Green;
```

枚举的一个方便功能是，可以在枚举中从数字值转为该值的名称。例如，如果我们有值`2`，但不确定前面的`Color`枚举中所映射到的值，这时可以查找对应的名称：

```
enum Color {
  Red = 1,
  Green,
  Blue,
}
let colorName: string = Color[2];

console.log(colorName); // Displays 'Green' as its value is 2 above
```



#### 8. Any

我们可能需要描述在编写应用程序时不知道的变量类型，这些值可能来自动态内容，如：用户或第三方库。这时，我们需要退出类型检查，并让值通过编译。为此，我们可以将其标记为`any`类型：

```
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

`any`类型是使用现有JavaScript的强大方法，可让你在编译过程中逐步选择加入或退出类型检查。你可能希望通过`Object`扮演相似的角色，但是，`Object`类型的变量仅允许你为其分配任何值，并不能在它们上调用任意方法，即使是实际存在的方法：

```
let notSure: any = 4;
notSure.ifItExists(); // okay, ifItExists might exist at runtime
notSure.toFixed(); // okay, toFixed exists (but the compiler doesn't check)

let prettySure: Object = 4;
prettySure.toFixed(); // Error: Property 'toFixed' doesn't exist on type 'Object'.
Property 'toFixed' does not exist on type 'Object'.
```

如果你知道该类型的某些部分，但可能不是全部，那么`any`类型也很方便。例如，你可能有一个数组，但是该数组混合了不同的类型：

```
let list: any[] = [1, true, "free"];

list[1] = 100;
```



#### 9. Void

`void`有点像`any`反意词：不是任何类型。通常，可能会将其视为不返回值的函数的返回类型：

```
function warnUser(): void {
    console.log("This is my warning message");
}
```

声明`void`类型的变量通常没什么用，因为你只能为其分配`null`（仅`--strictNullChecks`未指定时可以，参见下节）或`undefined`值。

```
let unusable: void = undefined;
unusable = null; // OK if `--strictNullChecks` is not given
```



#### 10. Null与Undefined

在TypeScript中，`undefined`和`null`实际上都有自己的类型，分别名为`undefined`和`null`。像`void`一样，它们本身并不是非常有用：

```
// 我们能为这些变量分配的值并不多
let u: undefined = undefined;
let n: null = null;
```

默认情况下，`null`和`undefined`是所有其他类型的子类型。这意味着你可以将`null`和`undefined`分配给`number`。

但是，当使用`--strictNullChecks`标志时，`null`和`undefined`仅可分配给`and`类型及其各自的类型（一个例外是`undefined`也可分配给`void`）。这有助于避免许多常见错误。如果要传递`string`或`null`或`undefined`，则可以使用联合类型`string|null|undefined`。

关于联合类型，请参见：[高级类型](#3.1 高级类型（Advanced Types）)章节。

*注意：我们鼓励尽可能的使用`--strictNullChecks`，但出于本手册的目的，我们假定它已关闭。*



#### 11. Never

`never`类型表示永不出现的值的类型。 例如，`never`是始终会抛出异常或永远不会返回异常的函数表达式或箭头函数表达式的返回类型； 当变量被任何永远不会为真的类型窄化时，变量也将获得`never`类型。

`never`类型是每个类型的子类型，并且可以分配给每种类型；但是，任何类型都不是`never`的子类型或可分配给`never`的子类型（`never`本身除外）。甚至`any`都不可分配给`never`。

函数返回`never`的一些示例：

```
// 返回“never”的函数必须有无法到达的终点
function error(message: string): never {
    throw new Error(message);
}

// 推断的返回类型为“never”
function fail() {
    return error("Something failed");
}

// 返回“never”的函数必须具有不可达的端点
function infiniteLoop(): never {
    while (true) {
    }
}
```



#### 12. Object

`object`是代表非原始类型的类型，即`number`、`string`、`boolean`、`bigint`、`symbol`、`null`或`undefined`的任何类型。

通过`object`类型，可以更好地表示`Object.create`之类的API。例如：

```
declare function create(o: object | null): void;

create({ prop: 0 }); // OK
create(null); // OK

create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
Argument of type '42' is not assignable to parameter of type 'object | null'.
Argument of type '"string"' is not assignable to parameter of type 'object | null'.
Argument of type 'false' is not assignable to parameter of type 'object | null'.
Argument of type 'undefined' is not assignable to parameter of type 'object | null'.
```



#### 13. 类型断言

有时，你会遇到比TypeScript更了解值的情况。通常，当你知道某个实体的类型可能比其当前类型更具体时，就会发生这种情况。

*类型断*言是一种告诉编译器应该使用什么类型的方法。类型断言就像其他语言中的类型转换，但是不执行数据的特殊检查或重组。它对运行时没有影响，仅由编译器使用。TypeScript会假定你已经执行了所需的任何特殊检查。

类型断言有两种形式。 一种是“尖括号”语法：

```
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

另一种是使用`as`语法：

```
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

这两个方式是等效的。但是，将TypeScript与JSX一起使用时，仅允许使用`as`式断言



#### 14. 关于let

你可能已经注意到，到目前为止，我们一直在使用`let`关键字，而不是JavaScript中的`var`关键字。`let`关键字是在ES2015中引入到JavaScript的，由于它比`let`更安全，因此现在被视为标准关键字。使用`let`可以缓解JavaScript中的许多常见问题，因此你应尽可能使用它而不是`var`。



### 2.3 接口（Interfaces）

- [1. 第一个接口](#1. 第一个接口)
- [2. 可选属性](#2. 可选属性)
- [3. 只读属性](#3. 只读属性)
  - [readonly与const]
- [4. 多余属性检查](#4. 多余属性检查)
- [5. 函数类型](#5. 函数类型)
- [6. 可索引类型](#6. 可索引类型)
- [7. 类类型](#7. 类类型)
- [8. 扩展接口](#8. 扩展接口)
- [9. 混合类型](#9. 混合类型)
- [10. 接口扩展类](#10. 接口扩展类)

TypeScript的核心原则之一是：类型检查重点在于值的形状。有时将其称为“鸭子类型”(duck typing)或“结构子类型”(structural subtyping)。在TypeScript中，接口充当命名这些类型的角色，并且是在代码内定义协议以及与项目外代码定义协议的有效方法

#### 1. 第一个接口

可以通过以下简单示例查看接口如何工作的：

```
function printLabel(labeledObj: { label: string }) {
    console.log(labeledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```

类型检查器会检查对`printLabel`的调用。`printLabel`函数有一个参数，该参数要求传入的对象有类型为`string`的名为`label`的属性。请注意，我们的对象实际上有比这更多的属性，但是编译器仅检查是否存在必须的属性并与所需的类型匹配。在某些情况下，TypeScript不太宽松，我们将在稍后介绍。

接下来再次编写相同的示例，这一次使用*接口*来描述必须有字符串类型的`label`属性：

```
interface LabeledValue {
    label: string;
}

function printLabel(labeledObj: LabeledValue) {
    console.log(labeledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```

接口`LabeledValue`是一个名称，我们现在可以通过它来描述前面示例中需求。它仍然表示具有一个名为`label`的属性，该属性的类型为`string`。请注意，我们不必再明确的告诉传递给`LabeledValue`的对象，而可以像使用其他语言一样实现此接口。在这里，只关心形状。如果我们传给函数的对象满足列出的要求，则可以使用。

值得指出的是，类型检查器不关心这些属性出现的顺序，而仅需要接口所需的属性存在并且满足所需的类型。



#### 2. 可选属性

并不是说接口的所有属性都是必须的，有些属性可以在某些条件下存在或不存在。当创建诸如“可选包”(option bags)之类的模式时，这些可选属性很常用，在该模式中可以将仅填充了几个属性的对象传递给的函数。

以下是这种模式的一个示例：

```
interface SquareConfig {
    color?: string;
    width?: number;
}

function createSquare(config: SquareConfig): {color: string; area: number} {
    let newSquare = {color: "white", area: 100};
    if (config.color) {
        newSquare.color = config.color;
    }
    if (config.width) {
        newSquare.area = config.width * config.width;
    }
    return newSquare;
}

let mySquare = createSquare({color: "black"});
```

有可选属性的接口与其他接口的编写方式相似，其中的可选属性以`?`表示，并添加在所声明属性名称的末尾。

可选属性的优点在于，可以描述这些可能的可用属性，同时仍然可以防止使用不属于接口的属性。例如，如果我们在`createSquare`中错误的输入了`color`属性的名称，就会收到一条错误消息：

```
interface SquareConfig {
    color?: string;
    width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
    let newSquare = {color: "white", area: 100};
    if (config.clor) {
        // Error: Property 'clor' does not exist on type 'SquareConfig'
        newSquare.color = config.clor;
    }
    if (config.width) {
        newSquare.area = config.width * config.width;
    }
    return newSquare;
}

let mySquare = createSquare({color: "black"});
Property 'clor' does not exist on type 'SquareConfig'. Did you mean 'color'?
```



#### 3. 只读属性

有些属性仅在首次创建对象时可修改，这时可以通过在属性名前添加`readonly`来指定：

```
interface Point {
    readonly x: number;
    readonly y: number;
}
```

我们可以用字面量的形式创建一个`Point`对象，其被分配值后`x`和`y`将不可修改。

```
let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error!
Cannot assign to 'x' because it is a read-only property.
```

TypeScript有与`Array<T>`相同的`ReadonlyArray<T>`类型，并且删除了所有变种方法，因此可以确保创建后不更改数组。

```
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error!
ro.push(5); // error!
ro.length = 100; // error!
a = ro; // error!
Index signature in type 'readonly number[]' only permits reading.
Property 'push' does not exist on type 'readonly number[]'.
Cannot assign to 'length' because it is a read-only property.
The type 'readonly number[]' is 'readonly' and cannot be assigned to the mutable type 'number[]'.
```

在上面代码段的最后一行可以看到，即使将整个`ReadonlyArray`分配回普通数组也是非法的。但是，仍然可以使用类型断言来覆盖它：

```
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;

a = ro as number[];
```



##### **readonly与const**

可以通过一个简单的方式来判断是该使用`readonly`还是`const`，如果是变量则使用`const`，而属性则使用`readonly`。



#### 4. 多余属性检查

在前面的接口示例中，在只需要`{ label: string; }`时，TypeScript让我们可以传递`{ size: number; label: string; }`。并且还可以通过“可选包”添加可选属性。

但是，将两者简单的结合起来可能会引发错误。例如，前面使用`createSquare`的示例：

```
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
  return { color: config.color || "red", area: config.width || 20 };
}

let mySquare = createSquare({ colour: "red", width: 100 });
Argument of type '{ colour: string; width: number; }' is not assignable to parameter of type 'SquareConfig'.
  Object literal may only specify known properties, but 'colour' does not exist in type 'SquareConfig'. Did you mean to write 'color'?
```

请注意，`createSquare`的指定参数名是`color`而不是`colour`。在原生JavaScript中，这种情况会自动失败。

你可能会说该程序的类型是正确的，因为`width`属性兼容，没有`color`属性，多余的`colour`属性无关紧要。

但是，TypeScript会认为此代码中可能存在一个错误。将对象字面量分配给其他变量或将其作为参数传递时，将对其进行特殊处理并进行多余属性检查。如果对象字面量有“目标类型”所没有的任何属性，则会出现错误：

```
// error: Object literal may only specify known properties, but 'colour' does not exist in type 'SquareConfig'. Did you mean to write 'color'?
let mySquare = createSquare({ colour: "red", width: 100 });
```

要处理这些检查实际上非常容易，最简单的方法是只使用类型断言：

```
let mySquare = createSquare({ width: 100, opacity: 0.5 } as SquareConfig);
```

但是，如果你确定对象可以有某些以特殊方式使用的额外属性，更好的方法可能是添加字符串索引签名。例如，如果`SquareConfig`可以有上述类型的`color`和`width`属性，但是也可以有任意数量的其他属性，那么我们可以这样定义它：

```
interface SquareConfig {
    color?: string;
    width?: number;
    [propName: string]: any;
}
```

我们稍微讨论一下索引签名，但是这里说的是`SquareConfig`可以有任意数量的属性，并且只要它们不是颜色或宽度，它们的类型就无关紧要。

解决这些检查的最后一种方法（可能有点意外）是将对象分配给另一个变量：由于`squareOptions`不会进行多余属性检查，因此编译器不会报错。

```
let squareOptions = { colour: "red", width: 100 };
let mySquare = createSquare(squareOptions);
```

只要`squareOptions`和`SquareConfig`之间有一个公共属性，上述变通方法就可用。在此示例中，它是`width`属性。但是，如果变量没有任何公共对象属性，则将会失败。 例如：

```
let squareOptions = { colour: "red" };
let mySquare = createSquare(squareOptions);
```

请记住，对于上述示例代码，应尽可能不要试图“绕开”这些检查。对于有方法和状态保持的更复杂的对象字面量，你可能需要牢记这些技术，但大多数情况下对有多余属性实际上是错误的。也就是说，如果遇到诸如选项包之类的多余的属性检查问题，则可能需要修改一些类型声明。



#### 5. 函数类型

接口能够描述JavaScript对象可能采用的各种形状。除了使用可以用属性描述对象外，接口还可以描述函数类型。

为了在接口中描述函数类型，我们给接口一个调用签名。这就像只声明参数列表和返回类型的函数声明。参数列表中的每个参数都需要名称和类型。

```
interface SearchFunc {
    (source: string, subString: string): boolean;
}
```

定义后，就可以像使用其他接口一样使用此函数类型接口。在这里，我们展示了如何创建函数类型的变量并为其分配相同类型的函数值。

```
let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
    let result = source.search(subString);
    return result > -1;
}
```

为了使函数类型正确通过检查，参数名称不需要匹配。例如，我们可以这样编写上面的示例：

```
let mySearch: SearchFunc;
mySearch = function(src: string, sub: string): boolean {
    let result = src.search(sub);
    return result > -1;
}
```

函数参数会同时进行检查，会检查每个参数的位置及类型。如果不想指定类型，那么TypeScript会跟据上下文类型推断参数类型，因为函数值会直接分配给`SearchFunc`类型的变量。同样，函数表达式的返回类型也会由其返回的值（此处为`false`和`true`）所隐含。

```
let mySearch: SearchFunc;
mySearch = function(src, sub) {
    let result = src.search(sub);
    return result > -1;
}
```

如果函数表达式返回数字或字符串，则类型检查器会抛出一个错误，表示返回类型与`SearchFunc`接口中描述的返回类型不匹配。

```
let mySearch: SearchFunc;

// error: Type '(src: string, sub: string) => string' is not assignable to type 'SearchFunc'.
// Type 'string' is not assignable to type 'boolean'.
mySearch = function(src, sub) {
  let result = src.search(sub);
  return "string";
};
```



#### 6. 可索引类型

与使用接口来描述函数类型相似，也可以用接口描述可“索引”到的类型，例如`a[10]`或`ageMap["daniel"]`。可索引类型有索引签名，该签名描述了用于索引对象的类型以及建立索引时所对应的返回类型。举个例子：

```
interface StringArray {
    [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];
```

以上，我们的`StringArray`接口有索引签名。此索引签名描述，当用`number`对`StringArray`进行索引时，它将返回一个`string`。

支持两种类型的索引签名：`string`和`number`。可以同时支持两种类型的索引器，但是从`number`索引器返回的类型必须是从`string`索引器返回的类型的子类型。这是因为使用`number`索引时，JavaScript实际上会在其索引到对象之前将其转换为字符串。这意味着使用`100`（一个数字）进行索引与使用`"100"`（一个字符串）进行索引是一回事，因此两者必须保持一致。

```
class Animal {
    name: string;
}
class Dog extends Animal {
    breed: string;
}

// Error: indexing with a numeric string might get you a completely separate type of Animal!
interface NotOkay {
    [x: number]: Animal;
    [x: string]: Dog;
}
Numeric index type 'Animal' is not assignable to string index type 'Dog'.
```

尽管字符串索引签名在描述“字典”模式上强大，但它还强制所有属性与其返回类型匹配。因为字符串索引声明`obj.property`也可以作为`obj["property"]`使用。在以下示例中，`name`的类型与字符串索引的类型不匹配，并且类型检查器提示错误：

```
interface NumberDictionary {
    [index: string]: number;
    length: number;    // ok, length is a number
    name: string;      // error, the type of 'name' is not a subtype of the indexer
}
Property 'name' of type 'string' is not assignable to string index type 'number'.
```

但是，如果索引签名是属性类型的并集，则可以接受不同类型的属性：

```
interface NumberOrStringDictionary {
    [index: string]: number | string;
    length: number;    // ok, length is a number
    name: string;      // ok, name is a string
}
```

最后，可以将索引签名设为`readonly`，以防止给它们的索引分配值：

```
interface ReadonlyStringArray {
    readonly [index: number]: string;
}
let myArray: ReadonlyStringArray = ["Alice", "Bob"];
myArray[2] = "Mallory"; // error!
Index signature in type 'ReadonlyStringArray' only permits reading.
```

不能为`myArray[2]`设置值，因为它是只读的.



#### 7. 类类型

##### **实现接口**

在TypeScript中，还可以像使用C#和Java等语言中的接口一样，显式强制类满足特定协定。

```
interface ClockInterface {
    currentTime: Date;
}

class Clock implements ClockInterface {
    currentTime: Date = new Date();
    constructor(h: number, m: number) { }
}
```

还可以描述在类中实现的接口中描述的方法，就像在下面示例中的`setTime`一样：

```
interface ClockInterface {
    currentTime: Date;
    setTime(d: Date): void;
}

class Clock implements ClockInterface {
    currentTime: Date = new Date();
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
```

接口描述了类的公有端，而不是公有和私有端。这就禁止使用它们来检查类是否还具有针对该类实例的私有部分的指定类型。

##### **类的静态端与实例端之间的区别**

当使用类和接口时，请记住一个类有两种类型：静态端的类型和实例端的类型。你可能会注意到，如果使用构造签名创建接口并尝试创建实现该接口的类，则会出现错误：

```
interface ClockConstructor {
    new (hour: number, minute: number);
}

class Clock implements ClockConstructor {
    currentTime: Date;
    constructor(h: number, m: number) { }
}
Class 'Clock' incorrectly implements interface 'ClockConstructor'.
  Type 'Clock' provides no match for the signature 'new (hour: number, minute: number): any'.
```

这是因为当类实现接口时，仅检查该类的实例端。由于构造函数位于静态端，因此它不会包含在检查中。

相反，如果需要直接使用类的静态端时。在以下示例中，我们定义了两个接口，用于构造函数的`ClockConstructor`和用于实例方法的`ClockInterface`。然后，为方便起见，我们定义了一个构造函数`createClock`，该函数会创建传递给它的类型的实例：

```
interface ClockConstructor {
  new (hour: number, minute: number): ClockInterface;
}

interface ClockInterface {
  tick(): void;
}

function createClock(
  ctor: ClockConstructor,
  hour: number,
  minute: number
): ClockInterface {
  return new ctor(hour, minute);
}

class DigitalClock implements ClockInterface {
  constructor(h: number, m: number) {}
  tick() {
    console.log("beep beep");
  }
}

class AnalogClock implements ClockInterface {
  constructor(h: number, m: number) {}
  tick() {
    console.log("tick tock");
  }
}

let digital = createClock(DigitalClock, 12, 17);
let analog = createClock(AnalogClock, 7, 32);
```

因为`createClock`的首个参数是`ClockConstructor`类型，所以在`createClock(AnalogClock, 7, 32)`中，会检查`AnalogClock`是否有正确的构造函数签名。

另一个简单的方式是使用类表达式：

```
interface ClockConstructor {
  new (hour: number, minute: number);
}

interface ClockInterface {
  tick();
}

const Clock: ClockConstructor = class Clock implements ClockInterface {
  constructor(h: number, m: number) {}
  tick() {
      console.log("beep beep");
  }
}
```



#### 8. 扩展接口

像类一样，接口可以互相扩展。这使你可以将一个接口的成员复制到另一个接口中，从而可以将接口拆分为可重用组件，以提供更大的灵活性。

```
interface Shape {
    color: string;
}

interface Square extends Shape {
    sideLength: number;
}

let square = {} as Square;
square.color = "blue";
square.sideLength = 10;
```

一个接口还可以扩展多个接口，从而创建所有接口的组合。

```
interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

interface Square extends Shape, PenStroke {
    sideLength: number;
}

let square = {} as Square;
square.color = "blue";
square.sideLength = 10;
square.penWidth = 5.0;
```



#### 9. 混合类型

如前所述，接口可以描述现实世界JavaScript中存在的丰富类型。由于JavaScript具有动态和灵活的特性，因此有时可能会遇到一个对象，该对象可能是上述某些类型的组合。

以下示例中是一个既具有函数又具有对象特性的对象，它还有其他属性：

```
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}

function getCounter(): Counter {
    let counter = (function (start: number) { }) as Counter;
    counter.interval = 123;
    counter.reset = function () { };
    return counter;
}

let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```

与第三方JavaScript交互时，你可能会需要使用上述模式来完全描述类型的形状。



#### 10. 接口扩展类

当接口类型扩展类类型时，它会继承该类的成员，但不继承其实现。好像该接口声明了该类的所有成员而没有提供实现。接口甚至继承基类的私有成员和受保护成员。这意味着，当你创建一个扩展带有私有或受保护成员的类的接口时，该接口类型只能由该类或其子类实现。

如果你有较大的继承层次结构，但要指定你的代码仅适用于有某些属性的子类时，这会很有用。子类除了从基类继承外，不必有其它关联。例如：

```
class Control {
    private state: any;
}

interface SelectableControl extends Control {
    select(): void;
}

class Button extends Control implements SelectableControl {
    select() { }
}

class TextBox extends Control {
    select() { }
}

// Error: Property 'state' is missing in type 'Image'.
class Image implements SelectableControl {
    private state: any;
    select() { }
}

class Location {

}
Class 'ImageControl' incorrectly implements interface 'SelectableControl'.
  Types have separate declarations of a private property 'state'.
```

在上面示例中，`SelectableControl`包含`Control`的所有成员，包括私有`state`属性。由于`state`是私有成员，因此`Control`的后代只能实现`SelectableControl`。这是因为只有`Control`的后代才会有源自同一声明的`state`私有成员，这是私有成员必须是兼容。

在`Control`类中，可以通过`SelectableControl`的实例访问`state`私有成员。 实际上，`SelectableControl`的行为类似于已知有`select`方法的`Control`。`Button`和`TextBox`类是`SelectableControl`的子类型（因为它们都继承自`Control`并且有`select`方法），而`Image`和`Location`类不是。



### 2.4 函数（Functions）

- [1. 介绍](#1. 介绍)

- [2. 函数](#2. 函数)

- [3. 函数类型](#3. 函数类型)

- - [类型函数](#函数类型)
  - [编写函数类型](#编写函数类型)
  - [推断类型](#推断类型)

- [4. 可选及默认参数](#4. 可选及默认参数)

- [5. 剩余参数](#5. 剩余参数)

- [6. `this`](#6. `this`)

- - [`this`与箭头函数](#`this`与箭头函数)
  - [`this`参数](#`this`参数)
  - [回调中的`this`参数](#回调中的`this`参数)

- [7. 重载](#7. 重载)

#### 1. 介绍

函数是JavaScript中所有应用程序的基本构建模块。它们是你构建抽象层、模仿类、信息隐藏和模块的方式。在TypeScript中，虽然有类、命名空间和模块，但是函数仍然在描述操作中起着关键作用。TypeScript还向标准JavaScript函数添加了一些新功能，以使其更易于使用。

#### 2. 函数

首先，就像在JavaScript中一样，可以将TypeScript函数创建为*命名函数*或*匿名函数*。无论是要构建API中的函数列表，还是创建一次性函数以交给另一个函数，都可以为你的应用提供最合适的方法。

快速回顾一下这两种方法在JavaScript中的样子：

```
// Named function
function add(x, y) {
    return x + y;
}

// Anonymous function
let myAdd = function(x, y) { return x + y; };
```

和JavaScript中一样，函数可以引用函数主体外部的变量。当这样做时，称之为*捕获*了这些变量。详细工作原理（以及使用此技术时的取舍）不在本文讨论的范围之内，但是深刻理解该机制的工作原理是使用JavaScript和TypeScript的重中之重。

```
let z = 100;

function addToZ(x, y) {
    return x + y + z;
}
```



#### 2. 函数类型

##### **类型函数**

让我们向前面示例添加类型：

```
function add(x: number, y: number): number {
    return x + y;
}

let myAdd = function(x: number, y: number): number { return x + y; };
```

我们可以为每个参数中添加类型，然后为函数本身添加返回类型。TypeScript可以通过`return`语句来确认返回类型，在许多情况下，我们也可以选择不使用返回类型。

##### **编写函数类型**

现在，我们已经添加了函数类型，接下来，通过查看函数类型的每一部分来编写函数的完整类型：

```
let myAdd: (x: number, y: number) => number = function(
  x: number,
  y: number
): number {
  return x + y;
};
```

函数的类型有两个相同的部分：*参数类型*及*返回类型*。如果写了函数类型时，两个部分都是必需的。我们像参数列表一样写了参数类型，为每个参数指定了名称和类型。该名称只是为了提高可读性。相反，我们还可以这样写：

```
let myAdd: (baseValue: number, increment: number) => number = function(
  x: number,
  y: number
): number {
  return x + y;
};
```

只要参数类型位置对应，就被认为是该函数的有效类型，无论在函数类型中指定的参数名是什么。

第二部分是返回类型。我们通过在参数和返回类型之间使用箭头（`=>`）以清楚哪里是返回类型。如前所述，这是函数类型的必需部分，因此，如果函数不返回值，则可以使用`void`而不是将其保留。

值得注意的是，只有参数和返回类型构成函数类型，而所捕获的变量并不会反映在类型中。实际上，捕获的变量是所有函数的“隐藏状态”的一部分，但并不构成其API。

##### **类型推断**

在处理示例时，你可能会注意到即使在等式的一侧只有类型，TypeScript编译器也可以找出类型：

```
// myAdd has the full function type
let myAdd = function(x: number, y: number): number { return  x + y; };

// The parameters 'x' and 'y' have the type number
let myAdd: (baseValue: number, increment: number) => number =
    function(x, y) { return x + y; };
```

这称为“上下文类型化”，是一种类型推断，有助于减少程序输入的工作量。



#### 3. 可选及默认参数

在TypeScript中，函数假定每个参数都是必需的。这并不意味着不能将其指定为`null`或`undefined`，在调用该函数时，编译器将检查用户是否已为每个参数提供了值。编译器还会假设这些参数是唯一将传给函数的参数，也就是说，传给函数的参数数量必须与函数期望的参数数量匹配。

```
function buildName(firstName: string, lastName: string) {
    return firstName + " " + lastName;
}

let result1 = buildName("Bob");                  // error, too few parameters
let result2 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result3 = buildName("Bob", "Adams");         // ah, just right
```

在JavaScript中，每个参数都是可选的，用户可以根据需要将其保留。当这样做时，它们的值会是`undefined`。 我们可以通过向参数末尾添加`?`，在TypeScript中实现相同的功能。例如，假设我们希望上面的`lastName`是可选的：

```
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}

let result1 = buildName("Bob");                  // works correctly now
let result2 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result3 = buildName("Bob", "Adams");         // ah, just right
```

所有可选参数必须跟在必选参数之后。如果我们想使成为可选的，而非`lastName`，就需要修改函数中参数的顺序，将`firstName`放在列表的最后。

在TypeScript中，我们还可以设置一个默认值，如果用户不提供参数，或者用户在其位置传递了`undefined`，则将分配一个参数值。这称为默认初始化参数。修改前面示例，并将`lastName`默认为`"Smith"`：

```
function buildName(firstName: string, lastName = "Smith") {
    return firstName + " " + lastName;
}

let result1 = buildName("Bob");                  // works correctly now, returns "Bob Smith"
let result2 = buildName("Bob", undefined);       // still works, also returns "Bob Smith"
let result3 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result4 = buildName("Bob", "Adams");         // ah, just right
```

所有必选参数之后的默认初始化参数都被视为可选参数，也与可选参数一样，可以在调用它们各自的函数时将其省略。这意味着可选参数和尾随默认参数将在其类型上共享通用性，因此两者：

```
function buildName(firstName: string, lastName?: string) {
    // ...
}
```

和：

```
function buildName(firstName: string, lastName = "Smith") {
    // ...
}
```

共享类型`(firstName: string, lastName?: string) => string`。`lastName`的默认值会被省略，仅将参数标记为可选的。

与普通可选参数不同，默认初始化参数不需要在必选参数之后出现。如果默认初始化参数位于必选参数之前，则用户需要显式传递`undefined`以获取默认初始化值。例如，我们可以在`firstName`上仅使用默认初始化来编写最后一个示例：

```
function buildName(firstName = "Will", lastName: string) {
    return firstName + " " + lastName;
}

let result1 = buildName("Bob");                  // error, too few parameters
let result2 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result3 = buildName("Bob", "Adams");         // okay and returns "Bob Adams"
let result4 = buildName(undefined, "Adams");     // okay and returns "Will Adams"
```



#### 4. 剩余参数

必需参数、可选参数和默认参数都有一个共同点：它们都只表示一个参数。有时，想将多个参数作为一组来使用，或者可能不知道一个函数最终将使用多少个参数。在JavaScript中，可以直接用在每个函数体内可见的`arguments`变量来处理参数。

而在TypeScript中，可以将这些参数集合到一个变量中：

```
function buildName(firstName: string, ...restOfName: string[]) {
    return firstName + " " + restOfName.join(" ");
}

// employeeName will be "Joseph Samuel Lucas MacKinzie"
let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");
```

剩余参数(`rest parameters`)被视为不限数量的可选参数。在为剩余参数传递参数时，可以使用任意数量的参数。编译器将构建一个用省略号（`...`）后面的名称传递的参数数组，使你可以在函数中使用它。

省略号还用于带有剩余参数的函数类型：

```
function buildName(firstName: string, ...restOfName: string[]) {
    return firstName + " " + restOfName.join(" ");
}

let buildNameFun: (fname: string, ...rest: string[]) => string = buildName;
```



#### 5. this

学习如何在JavaScript中使用`this`是一`this`，并知道未正确使用它的地方。幸运的是，TypeScript使你可以通过两种技术来捕获`this`的当使用。如果你需要了解`this`在JavaScript中的工作方式，可以阅读Yehuda Katz的：[“理解JavaScript函数调用与*this*”](http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)一文。其中很好地解释了`this`的内部工作原理，在此我们仅做简单的基础介绍。

##### **this与箭头函数**

在JavaScript中，`this`是在调用函数时设置的变量。这使其成为一个非常强大且灵活的功能，但是必须始终知道函数在其中执行的上下文。这是令人困惑的，尤其是在返回函数或将函数作为参数传递时。

让我们看一个例子：

```
let deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    createCardPicker: function() {
        return function() {
            let pickedCard = Math.floor(Math.random() * 52);
            let pickedSuit = Math.floor(pickedCard / 13);

            return {suit: this.suits[pickedSuit], card: pickedCard % 13};
        }
    }
}

let cardPicker = deck.createCardPicker();
let pickedCard = cardPicker();

alert("card: " + pickedCard.card + " of " + pickedCard.suit);
```

请注意，`createCardPicker`是一个函数，它本身也返回一个函数。如果尝试运行该示例，则会收到错误消息，而不是预期的警告框。因为我们单独调用`cardPicker()`，在`createCardPicker`中创建的函数中所使用的`this`将被设置为`window`而不是`deck`对象。这样的顶级非方法语法调用将对`this`使用`window`。（注意：在严格模式下，`this`将是`undefined`而不是`window`）。

我们可以通过在返回箭头函数的方式，确保函数绑定正确的`this`以解决这一问题。这样，无论之后怎么用，它仍然可以绑定到`deck`对象。为此，我们将函数表达式修改为使用ECMAScript 6中的箭头函数。箭头函数会在函数创建位置而不是在调用位置捕获`this`：

```
let deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    createCardPicker: function() {
        // NOTE: the line below is now an arrow function, allowing us to capture 'this' right here
        return () => {
            let pickedCard = Math.floor(Math.random() * 52);
            let pickedSuit = Math.floor(pickedCard / 13);

            return {suit: this.suits[pickedSuit], card: pickedCard % 13};
        }
    }
}

let cardPicker = deck.createCardPicker();
let pickedCard = cardPicker();

alert("card: " + pickedCard.card + " of " + pickedCard.suit);
```

更好的是，如果将`--noImplicitThis`标志传递给编译器，犯此错误时，TypeScript会发出警告。它会指出`this.suits[pickedSuit]`中的`this`类型为`any`。

##### **this参数**

`this.suits[pickedSuit]`的类型仍然是`any`，这是因为`this`来自对象字面量内部的函数表达式。要解决此问题，可以提供一个明确的`this`参数。`this`参数是一个伪参数，它们会首先出现在函数的参数列表中：

```
function f(this: void) {
    // make sure `this` is unusable in this standalone function
}
```

然后我们为上面的示例中的`Card`和`Deck`添加几个接口，以使类型更清晰和易于重用：

```
interface Card {
    suit: string;
    card: number;
}
interface Deck {
    suits: string[];
    cards: number[];
    createCardPicker(this: Deck): () => Card;
}
let deck: Deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    // NOTE: The function now explicitly specifies that its callee must be of type Deck
    createCardPicker: function(this: Deck) {
        return () => {
            let pickedCard = Math.floor(Math.random() * 52);
            let pickedSuit = Math.floor(pickedCard / 13);

            return {suit: this.suits[pickedSuit], card: pickedCard % 13};
        }
    }
}

let cardPicker = deck.createCardPicker();
let pickedCard = cardPicker();

alert("card: " + pickedCard.card + " of " + pickedCard.suit);
```

现在，TypeScript知道可以在`Deck`对象上调用`createCardPicker`。这意味着`this`现在是`Deck`类型，而不是`any`，所以`--noImplicitThis`不会引起任何错误。

##### **回调中的this参数**

当你将函数传递给以后会调用它们的库时，也可能在回调中遇到`this`错误。因为调用你的回调的库将像普通函数一样调用它，所以`this`将是`undefined`。通过一些处理，也可以使用`this`参数来防止回调错误。首先，库作者需要使用`this`注释回调类型：

```
interface UIElement {
    addClickListener(onclick: (this: void, e: Event) => void): void;
}
```

`this: void`表示`addClickListener`期望`onclick`是不需要`this`类型的函数。其次，用`this`注释您的调用代码：

```
class Handler {
    info: string;
    onClickBad(this: Handler, e: Event) {
        // oops, used `this` here. using this callback would crash at runtime
        this.info = e.message;
    }
}
let h = new Handler();
uiElement.addClickListener(h.onClickBad); // error!
```

通过`this`注释，使你明确必须在`Handler`的实例上调用`onClickBad`。然后TypeScript将检测到`addClickListener`需要具有`this: void`的函数。要解决该错误，就修改`this`的类型：

```
class Handler {
    info: string;
    onClickGood(this: void, e: Event) {
        // can't use `this` here because it's of type void!
        console.log('clicked!');
    }
}
let h = new Handler();
uiElement.addClickListener(h.onClickGood);
```

因为`onClickGood`指定了`this`的类型是`void`，其传递给`addClickListener`是合法的。当然，这也意味着它不能使用`this.info`。如果两者都需要，则必须使用箭头函数：

```
class Handler {
  info: string;
  onClickGood = (e: Event) => {
    this.info = e.message;
  };
}
```

之所以可行，是因为箭头函数使用的是外部`this`(即：箭头函数本身没有`this`)，因此始终可以将它们传递给期望`this: void`的对象。 不利的一面是，每个`Handler`类型的对象都会创建一个箭头函数。另一方面，方法只能创建一次并附加到`Handler`的原型中，并会在`Handler`类型的所有对象之间共享。



#### 6. 重载

JavaScript本质上是一种非常动态的语言。一个JavaScript函数根据传入参数的形状返回不同类型的对象的情况并不少见。

```
let suits = ["hearts", "spades", "clubs", "diamonds"];

function pickCard(x): any {
  // Check to see if we're working with an object/array
  // if so, they gave us the deck and we'll pick the card
  if (typeof x == "object") {
    let pickedCard = Math.floor(Math.random() * x.length);
    return pickedCard;
  }
  // Otherwise just let them pick the card
  else if (typeof x == "number") {
    let pickedSuit = Math.floor(x / 13);
    return { suit: suits[pickedSuit], card: x % 13 };
  }
}

let myDeck = [
  { suit: "diamonds", card: 2 },
  { suit: "spades", card: 10 },
  { suit: "hearts", card: 4 }
];
let pickedCard1 = myDeck[pickCard(myDeck)];
alert("card: " + pickedCard1.card + " of " + pickedCard1.suit);

let pickedCard2 = pickCard(15);
alert("card: " + pickedCard2.card + " of " + pickedCard2.suit);
```

在这里，`pickCard`函数将根据用户传入的内容返回两个不同的东西。如果用户传入了代表*deck*的对象，则该函数将选用*card*。如果用户选择了*card*，我们会告诉他们选择了哪个*card*。但是我们如何用类型系统来描述呢？

答案是，为同一函数提供多种函数类型，以作为重载列表。该列表是编译器来于解析函数调用的列表。我们来创建一个重载列表，以描述`pickCard`接受和返回的内容。

```
let suits = ["hearts", "spades", "clubs", "diamonds"];

function pickCard(x: { suit: string; card: number }[]): number;
function pickCard(x: number): { suit: string; card: number };
function pickCard(x): any {
  // Check to see if we're working with an object/array
  // if so, they gave us the deck and we'll pick the card
  if (typeof x == "object") {
    let pickedCard = Math.floor(Math.random() * x.length);
    return pickedCard;
  }
  // Otherwise just let them pick the card
  else if (typeof x == "number") {
    let pickedSuit = Math.floor(x / 13);
    return { suit: suits[pickedSuit], card: x % 13 };
  }
}

let myDeck = [
  { suit: "diamonds", card: 2 },
  { suit: "spades", card: 10 },
  { suit: "hearts", card: 4 }
];
let pickedCard1 = myDeck[pickCard(myDeck)];
alert("card: " + pickedCard1.card + " of " + pickedCard1.suit);

let pickedCard2 = pickCard(15);
alert("card: " + pickedCard2.card + " of " + pickedCard2.suit);
```

通过这一修改，重载现在为我们提供了对`pickCard`函数的类型检查调用。

为了使编译器选择正确的类型检查，它遵循与基础JavaScript相似的过程。它会查看重载列表，并在第一次重载之前尝试使用所提供的参数调用该函数。如果找到匹配项，它将选择此重载作为正确的重载。因此，习惯上按从最具体到最不具体的顺序对重载进行排序。

请注意，`function pickCard(x): any`不属于重载列表，因此它只有两个重载：一个是重载一个对象、另一个重载一个数字。使用任何其他参数类型调用`pickCard`都会引发错误。



### 2.5 字面量类型（Literal Types）

- [1. 字面量窄化](#1. 字面量窄化)
- [2. 字符串字面量类型](#2. 字符串字面量类型)
- [3. 数字字面量类型](#3. 数字字面量类型)

*字面量*是集合类型的更具体的子类型。也就是说类型系统内部的`"Hello World"`是一个`string`，但`string`不是`"Hello World"`。

当前TypeScript中提供了两种字面量类型：字符串和数字。通过字面量类型，你可以对字符串或数字指定确切的值。

#### 1. 字面量窄化

当通过`var`或`let`声明变量时，你是在告诉编译器该变量可能会修改其内容。相反，使用`const`声明变量时会通知TypeScript该对象永远不会改变。

```
// We're making a guarantee that this variable
// helloWorld will never change, by using const.

// So, TypeScript sets the type to be "Hello World" not string
const helloWorld = "Hello World";

// On the other hand, a let can change, and so the compiler declares it a string
let hiWorld = "Hi World";
```

从的无限数量的可能性（有无限数量的可能性的字符串值），到较具体的、有限数量的潜在情况（在`helloWorld`的示例中为*1*）的过程称为*窄化*。



#### 2. 字符串字面量类型

字符串字面量类型允许你指定的字符串中必须具有的确切值。在实践中，字符串字面量类型可以与联合类型、类型保护和类型别名很好地结合在一起。可以将这些功能组合使用，以获得类似于字符串的枚举行为。

```
type Easing = "ease-in" | "ease-out" | "ease-in-out";

class UIElement {
  animate(dx: number, dy: number, easing: Easing) {
    if (easing === "ease-in") {
      // ...
    } else if (easing === "ease-out") {
    } else if (easing === "ease-in-out") {
    } else {
      // It's possible that someone could reach this
      // by ignoring your types though.
    }
  }
}

let button = new UIElement();
button.animate(0, 0, "ease-in");
button.animate(0, 0, "uneasy");
Argument of type '"uneasy"' is not assignable to parameter of type 'Easing'.
```

你可以传递三个允许的字符串中的任意一个，但是任何其他字符串都会抛出错误。

```
Argument of type '"uneasy"' is not assignable to parameter of type '"ease-in" | "ease-out" | "ease-in-out"'
```

可以使用相同的方式通过字符串字面量来区分重载：

```
function createElement(tagName: "img"): HTMLImageElement;
function createElement(tagName: "input"): HTMLInputElement;
// ... more overloads ...
function createElement(tagName: string): Element {
    // ... code goes here ...
}
```



#### 3. 数字字面量类型

TypeScript同样有数字字面量类型，其作用与上面的字符串字面量相同。

```
function rollDice(): 1 | 2 | 3 | 4 | 5 | 6 {
  return (Math.floor(Math.random() * 5) + 1) as 1 | 2 | 3 | 4 | 5 | 6;
}

const result = rollDice();
```

使用它们的情况常见于描述配置值：

```
interface MapConfig {
  lng: number;
  lat: number;
  tileSize: 8 | 16 | 32;
}

setupMap({ lng: -73.935242, lat: 40.73061, tileSize: 16 });
```



### 2.6 联合与交叉类型（Unions and Intersection Types）

- [1. 联合类型（Union Types）](#1. 联合类型（Union Types）)

- - [公用字段联合](#公用字段联合)
  - [区分性联合](#区分性联合)

- [2. 交叉类型（Intersection Types）](#2. 交叉类型（Intersection Types）)

- - [通过交集混合](#通过交集混合)

到目前为止，本手册涵盖了原子对象的类型。但是，当对更多类型进行建模时，你会发现需要工具来组成或组合现有类型，而不是从头开始创建它们。

类型交叉与联合是组合类型的一种方法。

#### 1. 联合类型（Union Types）

并集类型与交集类型紧密相关，但是它们的用法却大不相同。有时，你会遇到一个期望参数为`number`和`string`的库。例如以下函数：

```
/**
 * Takes a string and adds "padding" to the left.
 * If 'padding' is a string, then 'padding' is appended to the left side.
 * If 'padding' is a number, then that number of spaces is added to the left side.
 */
function padLeft(value: string, padding: any) {
    if (typeof padding === "number") {
        return Array(padding + 1).join(" ") + value;
    }
    if (typeof padding === "string") {
        return padding + value;
    }
    throw new Error(`Expected string or number, got '${padding}'.`);
}

padLeft("Hello world", 4); // returns "    Hello world"
```

`padLeft`的问题在于其`padding`参数输入为`any`。这意味着我们可以使用既不是数字也不是字符串的参数来调用它，但是TypeScript可以使用它。

```
// passes at compile time, fails at runtime.
let indentedString = padLeft("Hello world", true);
```

在传统的面向对象的代码中，我们可能会通过创建类型的层次结构来抽象这两种类型。虽然这更为明确，但也有些过度。关于`padLeft`原始版本的一点好处是，我们能够只传递原始类型，这样用法就简单明了了。如果我们只是尝试使用其他地方已经存在的函数，这种新方法也不可用。

可以通过*联合类型*代替`padding`参数来代替`any`：

```
/**
 * Takes a string and adds "padding" to the left.
 * If 'padding' is a string, then 'padding' is appended to the left side.
 * If 'padding' is a number, then that number of spaces is added to the left side.
 */
function padLeft(value: string, padding: string | number) {
  // ...
}

let indentedString = padLeft("Hello world", true);
Argument of type 'true' is not assignable to parameter of type 'string | number'.
```

联合类型描述的值可以是几种类型之一。我们用竖线（`|`）来分隔每种类型，所以`number | string | boolean`可以是`number`、`string`或`boolean`。



##### **公用字段联合**

如果我们拥有一个有联合类型的值，则我们只能访问该联合中所有类型都通用的成员。

```
interface Bird {
  fly(): void;
  layEggs(): void;
}

interface Fish {
  swim(): void;
  layEggs(): void;
}

declare function getSmallPet(): Fish | Bird;

let pet = getSmallPet();
pet.layEggs();

// Only available in one of the two possible types
pet.swim();
Property 'swim' does not exist on type 'Bird | Fish'.
  Property 'swim' does not exist on type 'Bird'.
```

联合类型在这里可能会有些棘手，但要习惯它需要一些直觉。如果值的类型为`A|B`，我们只能肯定地知道它有`A`和`B`都有的成员。在此示例中，`Bird`有一个名为`fly`的成员。我们无法确定变量类型为`Bird | Fish`有`fly`的方法。 如果变量在运行时确实是`Fish`，则调用`pet.fly()`将失败。



##### **区分性联合**

使用联合的一种常用技术是拥有一个使用文字类型的字段，可以通过该字段使TypeScript窄化可能的当前类型。例如，我们创建三种类型的联合，它们共享一个字段。

```
type NetworkLoadingState = {
  state: "loading";
};

type NetworkFailedState = {
  state: "failed";
  code: number;
};

type NetworkSuccessState = {
  state: "success";
  response: {
    title: string;
    duration: number;
    summary: string;
  };
};

// Create a type which represents only one of the above types
// but you aren't sure which it is yet.
type NetworkState =
  | NetworkLoadingState
  | NetworkFailedState
  | NetworkSuccessState;
```

以上所有类型都有一个名为`state`的字段，它们也有自己的字段：

| NetworkLoadingState | NetworkFailedState | NetworkSuccessState |
| :------------------ | :----------------- | :------------------ |
| state               | state              | state               |
|                     | code               | response            |

由于`state`字段在`NetworkState`内部的每种类型中都有，所以无需进行存在性检查即可安全地访问代码。

使用`state`作为字面量类型，可以将`state`的值与等效字符串进行比较，TypeScript会知道当前正在使用哪种类型。

| NetworkLoadingState | NetworkFailedState | NetworkSuccessState |
| :------------------ | :----------------- | :------------------ |
| "loading"           | "failed"           | "success"           |

在这种情况下，可以使用`switch`语句来缩小运行时表示的类型：

```
type NetworkState =
  | NetworkLoadingState
  | NetworkFailedState
  | NetworkSuccessState;

function networkStatus(state: NetworkState): string {
  // Right now TypeScript does not know which of the three
  // potential types state could be.

  // Trying to access a property which isn't shared
  // across all types will raise an error
  state.code;

  // By switching on state, TypeScript can narrow the union
  // down in code flow analysis
  switch (state.state) {
    case "loading":
      return "Downloading...";
    case "failed":
      // The type must be NetworkFailedState here,
      // so accessing the `code` field is safe
      return `Error ${state.code} downloading`;
    case "success":
      return `Downloaded ${state.response.title} - ${state.response.summary}`;
  }
}
Property 'code' does not exist on type 'NetworkState'.
  Property 'code' does not exist on type 'NetworkLoadingState'.
```



#### 2. 交叉类型（Intersection Types）

*交叉类型*会将多种类型组合为一种。这使你可以将现有类型叠加在一起，以获得有所有所需功能的单个类型。例如，`Person & Serializable & Loggable`是一个`Person`、`Serializable`和`Loggable`。也就是说此类型的对象会有三种类型的所有成员。

例如，如果网络请求有一致的错误处理，则可以将错误处理分离为它自己的类型，并与相应的单个响应类型的类型合并。

```
interface ErrorHandling {
  success: boolean;
  error?: { message: string };
}

interface ArtworksData {
  artworks: { title: string }[];
}

interface ArtistsData {
  artists: { name: string }[];
}

// These interfaces are composed to have
// consistent error handling, and their own data.

type ArtworksResponse = ArtworksData & ErrorHandling;
type ArtistsResponse = ArtistsData & ErrorHandling;

const handleArtistsResponse = (response: ArtistsResponse) => {
  if (response.error) {
    console.error(response.error.message);
    return;
  }

  console.log(response.artists);
};
```



##### **通过交集混合**

通过交叉类型实现[mixin模式](#mixin模式)：

```
class Person {
  constructor(public name: string) {}
}

interface Loggable {
  log(name: string): void;
}

class ConsoleLogger implements Loggable {
  log(name: string) {
    console.log(`Hello, I'm ${name}.`);
  }
}

// Takes two objects and merges them together
function extend<First extends {}, Second extends {}>(
  first: First,
  second: Second
): First & Second {
  const result: Partial<First & Second> = {};
  for (const prop in first) {
    if (first.hasOwnProperty(prop)) {
      (result as First)[prop] = first[prop];
    }
  }
  for (const prop in second) {
    if (second.hasOwnProperty(prop)) {
      (result as Second)[prop] = second[prop];
    }
  }
  return result as First & Second;
}

const jim = extend(new Person("Jim"), ConsoleLogger.prototype);
jim.log(jim.name);
```



### 2.7 类（Classes）

- [1. 类](#1. 类)

- [2. 继承](#2. 继承)

- [3. 公有(public)、私有(private)及受保护的(protected)修饰符](#3. 公有(`public`)、私有(`private`)及受保护的(`protected`)修饰符)

- - [默认为public]
  - [ECMAScript私有字段]
  - [理解TypeScript的private]
  - [理解protected]

- [4. 只读(readonly)修饰符](4. 只读(readonly)修饰符)

- [5. 访问器](5. 访问器)

- [6. 静态属性](6. 静态属性)

- [7. 抽象类](7. 抽象类)

- [8. 高级技巧](8. 高级技巧)

- - [构造函数]
  - [将类做为接口使用]

传统的JavaScript使用函数和基于原型的继承来构建可重用的组件，但是对于程序员来说，不能使用类继承功能和从类中构建对象的面向对象的方法可能会有点不方便。从ECMAScript 2015（也称为ECMAScript 6）开始，JavaScript程序员已经能够使用基于类的面向对象的方法来构建应用。在TypeScript中，已经可以使用全部面向对象技术，并可以将其编译为可在所有主要浏览器和平台上使用的JavaScript，而不必等待新的JavaScript版本。

#### 1. 类

以下是一个简单的基于类的示例：

```
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello, " + this.greeting;
  }
}

let greeter = new Greeter("world");
```

如果你以前使用过C#或Java，那这种语法可能看起来很熟悉。我们定义了一个新的`Greeter`类，该类有三个成员：`greeting`属性、构造函数和`greet`方法。

你会注意到，在引用类成员时，我们会以`this.`开头。这表示是对其成员的访问。

在最后一行中，我们用`new`构造了`Greeter`类的实例。这会调用我们前面定义的构造函数，并创建一个有`Greeter`特征的新对象，然后运行该构造函数对其进行初始化。



#### 2. 继承

在TypeScript中，我们可以使用常见的面向对象模式。基于类的编程中，最基本的模式之一是通过继承创建新类以扩展现有的类。

我们来看一个示例：

```
class Animal {
  move(distanceInMeters: number = 0) {
    console.log(`Animal moved ${distanceInMeters}m.`);
  }
}

class Dog extends Animal {
  bark() {
    console.log("Woof! Woof!");
  }
}

const dog = new Dog();
dog.bark();
dog.move(10);
dog.bark();
```

以上示例展示了最基本的继承功能：类从基类中继承属性和方法。在这里，`Dog`是派生类，它是通过`extends`关键字从`Animal`基类派生的。派生类通常称为`子类`，而基类通常称为`超类`。

因为`Dog`扩展了`Animal`的功能，所以我们能够创建一个可以同时有`bark()`和`move()`方法的`Dog`实例。

接下来，看一个更复杂的实例：

```
class Animal {
  name: string;
  constructor(theName: string) {
    this.name = theName;
  }
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

class Snake extends Animal {
  constructor(name: string) {
    super(name);
  }
  move(distanceInMeters = 5) {
    console.log("Slithering...");
    super.move(distanceInMeters);
  }
}

class Horse extends Animal {
  constructor(name: string) {
    super(name);
  }
  move(distanceInMeters = 45) {
    console.log("Galloping...");
    super.move(distanceInMeters);
  }
}

let sam = new Snake("Sammy the Python");
let tom: Animal = new Horse("Tommy the Palomino");

sam.move();
tom.move(34);
```

此示例涵盖了我们之前未提到的一些其他功能。我们又看到了用`extends`关键字创建了`Animal`的两个新子类：`Horse`和`Snake`。

与前面的示例的不同之处在于，每个包含构造函数的派生类都必须调用`super()`，它会执行基类的构造函数。而且，在访问构造函数体中的属性之前，我们必须调用`super()`。这是TypeScript会强制执行的重要规则。

该示例还展示了如何用专用于子类的方法覆盖基类中的方法。在这里，`Snake`和`Horse`都创建了一个`move`方法，该方法将覆盖`Animal`的`move`，从而为每个类提供特定的功能。请注意，即使`tom`被声明为`Animal`，由于其值是`Horse`，所以调用`tom.move(34)`时会调用`Horse`中的重写方法：

```
Slithering...
Sammy the Python moved 5m.
Galloping...
Tommy the Palomino moved 34m.
```



#### 3. 公有(public)、私有(private)及受保护的(protected)修饰符

##### **默认为public**

在前面的示例中，我们可以自由访问在整个应用中声明的成员。如果你熟悉其他语言中的类，就可能已经注意到，我们不必用`public`关键字来完成此操作；例如，C#就要求每个成员都必须明确标记为`public`才能可见。而在TypeScript中，默认每个成员都是`public`的。

你仍可以明确地将成员标记为`public`。我们可以用以下方式编写上一节中的`Animal`类：

```
class Animal {
  public name: string;
  public constructor(theName: string) {
    this.name = theName;
  }
  public move(distanceInMeters: number) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}
```

##### **ECMAScript私有字段**

TypeScript 3.8中，TypeScript支持JavaScript新语法中的私有字段：

```
class Animal {
    #name: string;
    constructor(theName: string) { this.#name = theName; }
}

new Animal("Cat").#name; // Property '#name' is not accessible outside class 'Animal' because it has a private identifier.
```

该语法内置于JavaScript运行时中，可以更好地保证每个私有字段的隔离。关于这些私有字段相关介绍，请参考TypeScript 3.8的[release notes](https://devblogs.microsoft.com/typescript/announcing-typescript-3-8-beta/#ecmascript-private-fields)。

##### **理解TypeScript的private**

TypeScript还有一种将成员声明为标记为`private`的独特方法，标记后无法从其包含类的外部进行访问。例如：

```
class Animal {
  private name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}

new Animal("Cat").name; // Error: 'name' is private;
```

TypeScript是一种结构类型系统。当我们比较两种不同类型时，无论它们来自何处，如果所有成员的类型都是兼容的，那么我们就说这些类型本身是兼容的。

但是，在比较有`private`和`protected`成员的类型时，会以不同的方式对待这些类型。对于被认为是兼容的两种类型，如果其中一种具有`private`成员，则另一种必须有源自同一声明的`private`成员。`protected`成员也是如此。

让我们通过一个示例来了解它在实践中是如何发挥作用的：

```
class Animal {
  private name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}

class Rhino extends Animal {
  constructor() {
    super("Rhino");
  }
}

class Employee {
  private name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}

let animal = new Animal("Goat");
let rhino = new Rhino();
let employee = new Employee("Bob");

animal = rhino;
animal = employee; // Error: 'Animal' and 'Employee' are not compatible
```

在此示例中，我们有`Animal`和`Rhino`，其中`Rhino`是`Animal`的子类。我们还有一个新的`Employee`类，其结构在外观上与`Animal`相同。我们创建这些类的一些实例，然后尝试将它们彼此分配然后看会发生什么。因为`Animal`和`Rhino`从相同的私有名称声明（动物中的字符串）共享结构的私有端，所以它们是兼容的。但是，`Employee`则不同。当我们尝试从`Employee`分配给`Animal`时，会收到错误消息，指出这些类型不兼容。即使`Employee`也有一个名为`name`的私有成员，但其不是我们在`Animal`中声明的成员。

##### **理解protected**

`protected`修饰符的行为与`private`修饰符非常相似，只是声明为`protected`的成员也可以在派生类中访问。例如：

```
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

  public getElevatorPitch() {
    return `Hello, my name is ${this.name} and I work in ${this.department}.`;
  }
}

let howard = new Employee("Howard", "Sales");
console.log(howard.getElevatorPitch());
console.log(howard.name); // error
```

需要注意，虽然我们不能从`Person`外部使用`name`，但仍可以从`Employee`的实例方法中使用它，因为`Employee`继承自`Person`。

构造函数也被标记为`protected`。这意味着该类不能在其包含的类之外实例化，但是可以扩展。例如：

```
class Person {
  protected name: string;
  protected constructor(theName: string) {
    this.name = theName;
  }
}

// Employee can extend Person
class Employee extends Person {
  private department: string;

  constructor(name: string, department: string) {
    super(name);
    this.department = department;
  }

  public getElevatorPitch() {
    return `Hello, my name is ${this.name} and I work in ${this.department}.`;
  }
}

let howard = new Employee("Howard", "Sales");
let john = new Person("John"); // Error: The 'Person' constructor
```

#### 4. 只读(readonly)

可以用`readonly`关键字将属性设置为只读。只读属性必须在其声明或构造函数中进行初始化。

```
class Octopus {
  readonly name: string;
  readonly numberOfLegs: number = 8;
  constructor(theName: string) {
    this.name = theName;
  }
}
let dad = new Octopus("Man with the 8 strong legs");
dad.name = "Man with the 3-piece suit"; // error! name is readonly.
```

##### **参数属性**

在我们最后一个示例中，我们必须在`Octopus`类中声明一个只读成员`name`和一个构造函数参数`theName`。为了在执行`Octopus`构造函数之后有可访问`theName`的值，这是必需的。使用参数属性，你可以在同一个地方创建和初始化成员。这是使用参数属性对之前的`Octopus`类的进一步修改：

```
class Octopus {
  readonly numberOfLegs: number = 8;
  constructor(readonly name: string) {}
}
```

请注意，我们是如何完全删除`theName`的，只是在构造函数上使用缩短的`readonly name: string`参数来创建和初始化`name`成员。我们已将声明和赋值合并到了一个位置。

通过在构造函数参数前添加可访问性修饰符或只读、或二者兼有来声明参数属性。对参数属性可以使用`private`声明并初始化一个私有成员；同样，对于`public`、`protected`和`readonly`也是如此。



#### 5. 访问器

TypeScript支持 getters/setter 方法，以拦截对对象成员的访问。这样就可以更好地控制对象成员的访问。

让我们转换一个简单类，以使用`get`和`set`。首先，从一个没有getter和setter的示例开始：

```
class Employee {
  fullName: string;
}

let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
  console.log(employee.fullName);
}
```

虽然允许直接直接设置`fullName`非常方便，但我们还是希望在设置`fullName`时强制执行一些约束。

在接下来的版本中，我们添加一个setter以检查`newName`的长度，以确保它与我们的后端数据库字段的最大长度兼容。如果不兼容，则抛出错误，以通知用户代码出了问题。

为了保留现有功能，我们还添加了一个简单的getter以检索未修改的`fullName`：

```
const fullNameMaxLength = 10;

class Employee {
  private _fullName: string;

  get fullName(): string {
    return this._fullName;
  }

  set fullName(newName: string) {
    if (newName && newName.length > fullNameMaxLength) {
      throw new Error("fullName has a max length of " + fullNameMaxLength);
    }

    this._fullName = newName;
  }
}

let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
  console.log(employee.fullName);
}
```

为了证明访问器是有效的，可以尝试分配一个长度超过10个字符的名称，并验证是否收到错误。

有关访问器的几点注意事项：

首先，访问器要求你将编译器设置为输出ECMAScript 5或更高版本。不支持降级为ECMAScript 3。其次，带有`get`且没有`set`的访问器会自动推断为`readonly`。从代码生成`.d.ts`文件时，这会很有用，因为可以看到无法你的用户属性进行更改。



#### 6. 静态属性

目前为止，我们只讨论了类的实例成员，即实例化对象后显示在对象上的成员。我们还可以创建类的静态(`static`)成员，这些成员在类本身而不是实例上可见。在此示例中，我们将在*origin*上使用`static`，因为它是所有`static`的通用值。每个实例都可以通过在该属性前添加类名进行，类似于在前面加上了`this.`。在本以示例中，我们在实例访问前，可能以通过在静态属性前添加我们在此处添加`Grid.`访问。

```
class Grid {
  static origin = { x: 0, y: 0 };
  calculateDistanceFromOrigin(point: { x: number; y: number }) {
    let xDist = point.x - Grid.origin.x;
    let yDist = point.y - Grid.origin.y;
    return Math.sqrt(xDist * xDist + yDist * yDist) / this.scale;
  }
  constructor(public scale: number) {}
}

let grid1 = new Grid(1.0); // 1x scale
let grid2 = new Grid(5.0); // 5x scale

console.log(grid1.calculateDistanceFromOrigin({ x: 10, y: 10 }));
console.log(grid2.calculateDistanceFromOrigin({ x: 10, y: 10 }));
```



#### 7. 抽象类

抽象类是无法直接实例化，但可以从中派生其他类的基类。与接口不同，抽象类会包含其成员的详细实现。`abstract`关键字用于定义抽象类以及抽象类中的抽象方法。

```
abstract class Animal {
  abstract makeSound(): void;
  move(): void {
    console.log("roaming the earth...");
  }
}
```

抽象类中标记为抽象的方法不包含实现，必须在派生类中实现。抽象方法与接口方法的语法类似。两者都只定义了方法的签名，而没有馀具体的方法体。但是，抽象方法必须有`abstract`关键字，并且可以选择包括访问修饰符。

```
abstract class Department {
  constructor(public name: string) {}

  printName(): void {
    console.log("Department name: " + this.name);
  }

  abstract printMeeting(): void; // must be implemented in derived classes
}

class AccountingDepartment extends Department {
  constructor() {
    super("Accounting and Auditing"); // constructors in derived classes must call super()
  }

  printMeeting(): void {
    console.log("The Accounting Department meets each Monday at 10am.");
  }

  generateReports(): void {
    console.log("Generating accounting reports...");
  }
}

let department: Department; // ok to create a reference to an abstract type
department = new Department(); // error: cannot create an instance of an abstract class
department = new AccountingDepartment(); // ok to create and assign a non-abstract subclass
department.printName();
department.printMeeting();
department.generateReports(); // error: method doesn't exist on declared abstract type
```



#### 8. 高级技巧

##### **构造函数**

当在TypeScript中声明一个类时，实际上是在同时创建多个声明。首先，是*类实例*的类型：

```
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello, " + this.greeting;
  }
}

let greeter: Greeter;
greeter = new Greeter("world");
console.log(greeter.greet()); // "Hello, world"
```

如上所示，在`let greeter: Greeter`中，我们用`Greeter`作为`Greeter`类的实例类型。对于其他面向对象语言的程序员来说，这几乎是第二本质。

我们还将创建另一个称为*构造函数*的值。这是我们用`new`构建实例时要调用的函数。可以通过以上示例查看实际情况：

```
let Greeter = (function() {
  function Greeter(message) {
    this.greeting = message;
  }
  Greeter.prototype.greet = function() {
    return "Hello, " + this.greeting;
  };
  return Greeter;
})();

let greeter;
greeter = new Greeter("world");
console.log(greeter.greet()); // "Hello, world"
```

以上`let Greeter`将被分配构造函数。当我们调用`new`并运行此函数时，就可以获取到该类的实例。构造函数中还包含了该类的所有静态成员。也就是说，有一个*实例端*和一个*静态端*。

我们修改下示例以显示这些差异：

```
class Greeter {
  static standardGreeting = "Hello, there";
  greeting: string;
  greet() {
    if (this.greeting) {
      return "Hello, " + this.greeting;
    } else {
      return Greeter.standardGreeting;
    }
  }
}

let greeter1: Greeter;
greeter1 = new Greeter();
console.log(greeter1.greet()); // "Hello, there"

let greeterMaker: typeof Greeter = Greeter;
greeterMaker.standardGreeting = "Hey there!";

let greeter2: Greeter = new greeterMaker();
console.log(greeter2.greet()); // "Hey there!"
```

在本例中，`greeter1`的工作方式与之前类似。我们实例化`Greeter`类，并使用该对象。

接下来，我们直接使用该类。在这里，我们创建一个名为`greeterMaker`的新变量。这个变量将保存类本身，也就是其构造函数。在这里，我们使用了`typeof Greeter`，即：给我`Greeter`类本身的类型，而不是其实例。或者更确切地说：给我称为`Greeter`的符号的类型，也就是构造函数的类型。该类型将包含`Greeter`的所有静态成员，以及创建`Greeter`类实例的构造函数。然后，我们通过在`greeterMaker`上通过`new`创建了`Greeter`的新实例，并像以前一样调用它们。

##### **将类做为接口使用**

如我们上节所说，类声明做了两件事：表示类实例的类型和构造函数。因为类创建了类型，所以可以在可使用接口的位置使用它们。

```
class Point {
  x: number;
  y: number;
}

interface Point3d extends Point {
  z: number;
}

let point3d: Point3d = { x: 1, y: 2, z: 3 };
```



### 2.8 枚举（Enums）

- [1. 数字枚举](#1. 数字枚举)
- [2. 字符串枚举](#2. 字符串枚举)
- [3. 异构枚举](#3. 异构枚举)
- [4. 计算成员和常量成员](#4. 计算成员和常量成员)
- [5. 联合枚举和枚举成员类型](#5. 联合枚举和枚举成员类型)
- [6. 运行时枚举](#6. 运行时枚举)
- [7. 编译时枚举](#7. 编译时枚举)
- [8. 外部枚举](#8. 外部枚举)

枚举是TypeScript特有的少数功能之一，它不是JavaScript的类型级扩展。

枚举允许我们定义一组命名常量。使用枚举可以更轻松地记录意图或创建一组不同的案例。TypeScript提供数字和基于字符串的枚举。

#### 1. 数字枚举

首先从数字枚举开始，如果你使用过其他语言，可能会更熟悉。可以使用`enum`关键字定义一个枚举。

```
enum Direction {
  Up = 1,
  Down,
  Left,
  Right,
}
```

上面，我们定义了一个数字枚举，其中`Up`用`1`初始化。其下所有成员会从该点开始自动递增。也就是说，`Direction.Up`的值为`1`，`Down`的值为`2`，`Left`的值为`3`，`Right`的值为`4`。

如果需要，我们可以完全不使用初始化：

```
enum Direction {
  Up,
  Down,
  Left,
  Right
}
```

这样，`Up`的值为`0`，`Down`的值为`1`，依此类推。这种自动递增的行为在以下情况下很有用：我们并不在乎成员值本身，但在乎每个值都与同一个值不同枚举。

使用枚举很简单：只需从枚举本身访问任何成员作为属性，然后用枚举的名称声明类型：

```
enum Response {
  No = 0,
  Yes = 1
}

function respond(recipient: string, message: Response): void {
  // ...
}

respond("Princess Caroline", Response.Yes);
```

数值枚举可以混合在计算成员和常量成员中（参见下文）

。换而言之，没有初始化程序的枚举要么需要首先使用，要么必须在用数字常量或其他常量枚举成员初始化的数字枚举之后出现。也就是说，以下内容是不允许的：



```
enum E {
  A = getSomeValue(),
  B // Error! Enum member must have initializer.
}
```



#### 2. 字符串枚举

字符串枚举是一个类似的概念，但是在[运行时方面]有一些细微的差别，如下所述。在字符串枚举中，每个成员都必须使用字符串字面量或另一个字符串枚举成员进行常量初始化。

```
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT"
}
```

虽然字符串枚举没有自动递增的行为，但字符串枚举的好处是可以很好地“序列化”。换句话说，如果你正在调试并且必须读取数字枚举的运行时值，该值通常是不透明的-它本身无法传达任何有用的含义（尽管[反向映射]可以改善），字符串枚举允许你在代码运行时提供有意义且可读的值，但与枚举成员本身的名称无关。



#### 3. 异构枚举

从技术上讲，枚举可以与字符串和数字成员混合使用，但尚不清楚为什么要这样做：

```
enum BooleanLikeHeterogeneousEnum {
  No = 0,
  Yes = "YES"
}
```

除非你想巧妙地利用JavaScript的运行时行为，否则建议不要这样做。



#### 4. 计算成员和常量成员

每个枚举成员都有一个与之关联的值，该值可以是常量，也可以是计算值。枚举成员被视为常量，如果：

- 如果枚举中的第一个成员没有初始化，在这种情况下，其分配值为0：

```
 // E.X is constant:
  enum E {
    X
  }
```


- 没有初始化，并且前面的枚举成员是数字常量。在这种情况下，当前枚举成员的值将是前一个枚举成员的值加1：

```
// All enum members in 'E1' and 'E2' are constant.

  enum E1 {
    X,
    Y,
    Z
  }

  enum E2 {
    A = 1,
    B,
    C
  }
```

- 枚举成员使用常量枚举表达式初始化。常量枚举表达式是TypeScript表达式的子集，可以在编译时完全对其求值。表达式可以是以下常量枚举表达式：

  1. 字面量枚举表达式（基本就是字符串字面量或数字字面量）
  2. 对先前定义的常量枚举成员的引用（可以源自其他枚举）
  3. 带括号的常量枚举表达式
  4. 用于常量枚举表达式的`+`、`-`、`!`一元运算符之一
  5. `+`、`-`、`*`、`/`、`%`、`<<`、`>>`、`>>>`、`&`、`|`、`^`以常量枚举表达式作为操作数的二进制运算符

  将常量枚举表达式计算为`NaN`或`Infinity`会发现编译时错误。

在所有其他情况下，枚举成员被视为已计算：

```
enum FileAccess {
  // constant members
  None,
  Read = 1 << 1,
  Write = 1 << 2,
  ReadWrite = Read | Write,
  // computed member
  G = "123".length
}
```



#### 5. 联合枚举和枚举成员类型

有一个特殊的常量枚举成员的子集是未计算的：字面量枚举成员。字面量枚举成员是没有初始化值或有初始化值的常量枚举成员：

- 任何字符串字面量（如`"foo"`、`"bar"`、`"baz"`）
- 任何数字字面量（如`1`、`100`）
- 适用于任何数字字面量的一元减号（如`-1`，`-100`）
- 当枚举中的所有成员都有字面量枚举值时，就会使用一些特殊的语义。

首先枚举成员也会成为类型！例如，我们可以说某些成员只能有枚举成员的值：

```
enum ShapeKind {
  Circle,
  Square
}

interface Circle {
  kind: ShapeKind.Circle;
  radius: number;
}

interface Square {
  kind: ShapeKind.Square;
  sideLength: number;
}

let c: Circle = {
  kind: ShapeKind.Square, // Error! Type 'ShapeKind.Square' is not assignable to type 'ShapeKind.Circle'.
  radius: 100
};
```

另一个变化是枚举类型本身可以有效地成为每个枚举成员的并集。尽管我们还没有讨论[联合类型]，但是你只需要知道联合枚举，类型系统就可以利用这种情况，即：它知道枚举本身中存在的确切值集。因此，TypeScript可以捕获一些明显的错误，在这些错误中我们可能会错误地比较值。例如：

```
enum E {
  Foo,
  Bar
}

function f(x: E) {
  if (x !== E.Foo || x !== E.Bar) {
    //             ~~~~~~~~~~~
    // Error! This condition will always return 'true' since the types 'E.Foo' and 'E.Bar' have no overlap.
  }
}
```

在该示例中，我们首先检查`x`是不是`E.Foo`。如果该检查成功，则`||` 会短路，*if*体会运行。但是，如果检查不成功，则`x`只能是`E.Foo`，所以查看它是否等于`E.Ba`没有意义。



#### 6. 运行时枚举

枚举是在运行时存在的真实对象。例如下面的枚举：

```
enum E {
  X,
  Y,
  Z
}
```

可以传递给函数：

```
function f(obj: { X: number }) {
  return obj.X;
}

// Works, since 'E' has a property named 'X' which is a number.
f(E);
```



#### 7. 编译时枚举

虽然枚举是在运行时存在的真实对象，但`keyof`关键字的工作原理与你对典型对象的预期不同。相反，应使用`keyof typeof`获取一个类型，该类似将所有Enum键表示为字符串。

```
enum LogLevel {
  ERROR,
  WARN,
  INFO,
  DEBUG
}

/**
 * This is equivalent to:
 * type LogLevelStrings = 'ERROR' | 'WARN' | 'INFO' | 'DEBUG';
 */
type LogLevelStrings = keyof typeof LogLevel;

function printImportant(key: LogLevelStrings, message: string) {
  const num = LogLevel[key];
  if (num <= LogLevel.WARN) {
    console.log("Log level key is:", key);
    console.log("Log level value is:", num);
    console.log("Log level message is:", message);
  }
}
printImportant("ERROR", "This is a message");
```

##### **反向映射**

除了创建有成员属性名称的对象外，数字枚举成员还获得从枚举值到枚举名称的*反向映射*。例如，在此示例中：

```
enum Enum {
  A
}
let a = Enum.A;
let nameOfA = Enum[a]; // "A"
```

TypeScript可能会将其编译为以下JavaScript：

```
var Enum;
(function(Enum) {
  Enum[(Enum["A"] = 0)] = "A";
})(Enum || (Enum = {}));
var a = Enum.A;
var nameOfA = Enum[a]; // "A"
```

在此生成的代码中，一个枚举被编译到一个对象中，该对象同时存在正向（`name`->`value`）和反向（`value`->`name`）映射。其他枚举成员的引用始终作为属性访问发出，并且从不内联。

请记住，字符串枚举成员不会生成反向映射。

##### **const枚举**

在大多数情况下，枚举是一个完美有效的解决方案，但是有时要求会更严格。为了避免在访问枚举值时额外的生成代码和额外的间接调用的开销，可以使用常量枚举。常量枚举是在枚举上用`const`修饰符定义的：

```
const enum Enum {
  A = 1,
  B = A * 2
}
```

常量枚举只能用常量枚举表达式，并且与常规枚举不同，它们在编译期间会被完全删除。在使用站点内联了`const`枚举成员。这是可能的，因为`const`枚举不能有计算成员。

```
const enum Directions {
  Up,
  Down,
  Left,
  Right
}

let directions = [
  Directions.Up,
  Directions.Down,
  Directions.Left,
  Directions.Right
];
```

生成的代码将是：

```
var directions = [0 /* Up */, 1 /* Down */, 2 /* Left */, 3 /* Right */];
```



#### 8. 外部枚举

外部枚举用于描述已经存在的枚举类型的形状：

```
declare enum Enum {
  A = 1,
  B,
  C = 2
}
```

外部枚举和非外部枚举之间的一个重要区别是，在常规枚举中，如果没有其初始值设定项的成员被视为常量，则该成员将被视为常量。相反，始终将没有初始化的环境（和非*const*）枚举成员则视为已计算。



### 2.9 泛型（Generics）

- [1. 泛型Hello World](#1. 泛型Hello World)
- [2. 使用泛型类型变量](#2. 使用泛型类型变量)
- [3. 泛型类型](#3. 泛型类型)
- [4. 泛型类](#4. 泛型类)
- [5. 泛型约束](#5. 泛型约束)

软件工程的主要部分是构建不仅有良好定义和一致API，而且可以重用的组件。能够处理当前和未来数据的组件会为你提供构建大型软件系统的最灵活功能。

在C#和Java之类的语言中，用于创建可重用组件的工具箱中的主要工具之一是泛型，即：创建一种可以在多种类型而不是单个类型上工作的组件。这使用户可以使用这些组件并使用自己的类型。

#### 1. 泛型Hello World

首先，让我们做一个泛型的“hello world”：*identity*函数。该函数是一个将返回传入函数内容，类似于`echo`命令。

如果没有泛型，我们就要必须给函数指定一个特定的类型：

```
function identity(arg: number): number {
  return arg;
}
```

或者定义为`any`类型：

```
function identity(arg: any): any {
  return arg;
}
```

尽管使用`any`肯定是泛型的，但它会导致函数接受`arg`类型的所有类型，实际上我们正在丢失有关函数返回时该类型的信息。如果我们传入一个数字，则唯一的信息就是可以返回任何类型。

相反，我们需要一种捕获参数类型的方式，以便我们可以使用它来表示要返回的内容。在这里，我们将使用*类型变量*（*Type variable*），这是一种特殊的变量，适用于类型而不是值。

```
function identity<T>(arg: T): T {
  return arg;
}
```

现在，我们向*identity*函数添加了类型变量`T`。此`T`允许我们捕获用户提供的类型（例如：`number`），以便我们以后可以使用该信息。在这里，我们再次使用`T`作为返回类型。通过检查，现在可以看到参数和返回类型使用了相同的类型。这使我们能够将键入信息的信息投放到函数的一侧，而又从另一侧返回。

这个`identity`函数的泛型版本，因为它适用于多种类型。与使用`any`不同，它与第一个用`nubmer`作为参数和返回类型的`identity`函数一样精确（即，它不会丢失任何信息）。

编写完泛型*identity*函数后，我们可以采用以下两种方式之一进行调用。第一种方法是将所有参数（包括类型参数）传递给函数：

```
let output = identity("myString");  // type of output will be 'string'
```

在这里，我们将`T`的显式的设置为`string`，并做为函数参数之一。但并不是在`()`中表示，而是`<>`中。

第二种方法也更为常见，也就是使用类型参数推断。也就是说，我们希望编译器根据传入的参数类型为我们自动设置`T`的值：

```
let output = identity("myString");  // type of output will be 'string'
```

注意，我们不需要在尖括号（`<>`）中显式传递类型，编译器会通过`"myString"`来判断，并将`T`设置为其类型。虽然类型实参推断可以是使代码更短、更易读，但是当编译器无法推断类型时，你可能需要像上一示例中那样显式传递类型实参，这可能在更复杂情况下出现。



#### 2. 使用泛型类型变量

当你开始使用泛型时，你会注意到，当创建诸如`identity`之类的泛型函数时，编译器将强制你正确使用函数体中的任何泛型类型的参数。也就是说，实际上将这些参数会被视为可以是`any`和所有类型。

看下之前的`identity`函数：

```
function identity<T>(arg: T): T {
  return arg;
}
```

如果我们还希望在每次调用时，都将参数`arg`的长度打印到控制台，该怎么做呢？ 我们可能会这样写：

```
function loggingIdentity<T>(arg: T): T {
  console.log(arg.length);  // Error: T doesn't have .length
  return arg;
}
```

当我们这样做时，编译器会给我们一个错误，因为我们正在使用`arg`的`.length`成员，但是`arg`并不一定有该成员。正如前面说过，这些类型变量代表所有类型，所以使用此函数的人可能会传入一个`number`，而该数字没有`.length`成员。

假设我们实际上打算将此函数用于`T`数组，而不是直接用于`T`。如果我们正在处理数组，则`.length`成员是可用的。这时可以像创建其他类型的数组那样描述它：

```
function loggingIdentity<T>(arg: T[]): T[] {
  console.log(arg.length);  // Array has a .length, so no more error
  return arg;
}
```

可以将`loggingIdentity`的类型读取为：泛型函数`loggingIdentity`接受的类型参数`T`，并使用参数`arg`，它是`T`的数组，并返回`T`数组）。如果我们传入一个数字数组，就会得到一个数字数组，因为`T`会绑定到数字。这使我们可以将泛型类型变量`T`用作我们正在使用的类型的一部分，而不是整个类型，从而为我们提供了更大的灵活性。

我们可以用这种方式编写示例：

```
function loggingIdentity<T>(arg: Array<T>): Array<T> {
    console.log(arg.length);  // Array has a .length, so no more error
    return arg;
}
```

你可能已经从其他语言中熟悉了这种类型的类型。在下一节中，我们将介绍如何创建自己的泛型类型，如：`Array <T>`。



#### 3. 泛型类型

在前面的部分中，我们创建了可在多种类型上使用的泛型*identity*函数。在本节中，我们将探讨函数本身的类型以及如何创建泛型接口。

泛型函数的类型与非泛型函数的类型相似，首先列出类型参数，类似于函数声明：

```
function identity<T>(arg: T): T {
  return arg;
}

let myIdentity: <T>(arg: T) => T = identity;
```

也可以为类型中的泛型类型参数使用不同的名称，只要类型变量的数量以及类型变量的使用方式对应即可。

```
function identity<T>(arg: T): T {
  return arg;
}

let myIdentity: <T>(arg: U) => U = identity;
```

还可以将泛型类型写为对象字面量类型的调用签名：

```
function identity<T>(arg: T): T {
  return arg;
}

let myIdentity: {<T>(arg: T): T} = identity;
```

这样我们需要编写第一个泛型接口。让我们从上一个示例中的获取对象字面量，并将其移至接口：

```
interface GenericIdentityFn {
  <T>(arg: T): T;
}

function identity<T>(arg: T): T {
  return arg;
}

let myIdentity: GenericIdentityFn = identity;
```

在类似的示例中，我们可能希望将泛型参数移动为整个接口的参数。这样，我们就可以查看泛型类型（如：`Dictionary<string>`而不只是`Dictionary`）。这会使类型参数对接口的所有其他成员可见。

```
interface GenericIdentityFn<T> {
  (arg: T): T;
}

function identity<T>(arg: T): T {
  return arg;
}

let myIdentity: GenericIdentityFn<number> = identity;
```

在这里，我们的示例已经做了一些修改。现在，我们不再描述泛型函数，而是有一个非泛型函数签名，该签名是泛型类型的一部分。当我们用`GenericIdentityFn`时，还需要指定相应的类型参数（此处为`number`），以有效地锁定底层调用签名将使用的内容。

除了泛型接口，我们还可以创建泛型类。但请注意，无法创建泛型枚举和命名空间



#### 4. 泛型类

泛型类具有与泛型接口形状相似。泛型类在类名称后的尖括号（`<>`）中具有泛型类型参数列表。

```
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) {
  return x + y;
};
```

这实际上是`GenericNumber`类的字面量用法，你可能已经注意到，没有什么限制但只能使用`number`类型。我们本来可以使用`string`或更复杂的对象。

```
let stringNumeric = new GenericNumber<string>();
stringNumeric.zeroValue = "";
stringNumeric.add = function(x, y) {
  return x + y;
};

console.log(stringNumeric.add(stringNumeric.zeroValue, "test"));
```

与接口一样，将类型参数放在类本身也可以确保类的所有属性都使用相同的类型。

正如在[类一节](#类)中介绍的那样，类的类型有两个方面：静态端和实例端。泛型类仅在实例端是泛型，而静态端不是，所以在使用类时，静态成员不能使用类的类型参数。



#### 5. 泛型约束

在前面的示例中你可能记得，有时会想编写一个对一组类型起作用的泛型函数，在该类函数中应了解该类型集合将具有的功能。在我们的`loggingIdentity`示例中，我们希望能够访问`arg`的`.length`属性，但是编译器无法知道每种类型都具有`.length`属性，因此警告我们不能做此假设。

```
function loggingIdentity<T>(arg: T): T {
  console.log(arg.length);  // Error: T doesn't have .length
  return arg;
}
```

除了限制使用*any*类型和所有类型外，我们还希望限制此函数可以用于所有具有`.length`属性的类型。只要该类型具有此成员，我们就可以允许它，但是必须至少具有该成员。为此，我们必须列出我们要对`T`做的限制。

为此，我们将创建一个描述约束的接口。在这里，我们将创建一个具有单个`.length`属性的接口，然后用该接口和`extend`关键字来表示我们的约束：

```
interface Lengthwise {
  length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);  // Now we know it has a .length property, so no more error
  return arg;
}
```

由于泛型函数现在受到约束，因此它将不再适用于所有类型：

```
loggingIdentity(3);  // Error, number doesn't have a .length property
```

相反，我们需要传递其类型具有所有必需属性的值：

```
loggingIdentity({length: 10, value: 3});
```

##### **在泛型约束中使用类型参数**

可以声明受另一个类型参数约束的类型参数。例如，在这里我们想从一个指定名称的对象中获取属性，并希望确保不会意外地获取`obj`上不存在的属性，因此我们将在这两种类型之间设置约束：

```
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

let x = { a: 1, b: 2, c: 3, d: 4 };

getProperty(x, "a"); // okay
getProperty(x, "m"); // error: Argument of type 'm' isn't assignable to 'a' | 'b' | 'c' | 'd'.
```

##### **在泛型中使用类类型**

使用泛型在TypeScript中创建工厂时，有必要通过其构造函数来引用类类型。例如：

```
function create<T>(c: {new(): T; }): T {
    return new c();
}
```

一个更高级的示例是使用*prototype*属性来推断和约束构造函数和类类型的实例端之间的关系。

```
class BeeKeeper {
  hasMask: boolean;
}

class ZooKeeper {
  nametag: string;
}

class Animal {
  numLegs: number;
}

class Bee extends Animal {
  keeper: BeeKeeper;
}

class Lion extends Animal {
  keeper: ZooKeeper;
}

function createInstance<A extends Animal>(c: new () => A): A {
  return new c();
}

createInstance(Lion).keeper.nametag; // typechecks!
createInstance(Bee).keeper.hasMask; // typechecks!
```



## 3. 手册引用（Handbook Reference）

- [3.1 高级类型（Advanced Types）](#3.1 高级类型（Advanced Types）)
- [3.2 声明合并（Declaration Merging）](#3.2 声明合并（Declaration Merging）)
- [3.3 装饰器（Decorators）](#3.3 装饰器（Decorators）)
- [3.4 全局工具类型（Global Utility Types）](#3.4 全局工具类型（Global Utility Types）)
- [3.5 迭代器和生成器（Iterators and Generators）](#3.5 迭代器和生成器（Iterators and Generators）)
- [3.6 JSX](#3.6 JSX)
- [3.7 Mixins](#3.7 Mixins)
- [3.8 模块（Modules）](#3.8 模块（Modules）)
- [3.9 模块解析（Module Resolution）](#3.9 模块解析（Module Resolution）)
- [3.10 命名空间（Namespaces）](#3.10 命名空间（Namespaces）)
- [3.11 命名空间与模块（Namespaces and Modules）](#3.11 命名空间与模块（Namespaces and Modules）)
- [3.12 符号（Symbols）](#3.12 符号（Symbols）)
- [3.13 三斜线指令（`///`）](#3.13 三斜线指令（`///`）)
- [3.14 类型兼容性（Type Compatibility）](#3.14 类型兼容性（Type Compatibility）)
- [3.15 类型推断（Type Inference）](#3.15 类型推断（Type Inference）)
- [3.16 JavaScript文件类型检查](#3.16 JavaScript文件类型检查)
- [3.17 TypeScript 与DOM操作（TypeScript & the DOM）](#3.17 TypeScript 与DOM操作（TypeScript & the DOM）)
- [3.18 变量声明（Variable Declarations）](#3.18 变量声明（Variable Declarations）)



### 3.1 高级类型（Advanced Types）

- [1. 类型保护与区分类型（Type Guards and Differentiating Types）](#1. 类型保护与区分类型（Type Guards and Differentiating Types）)

- - 用户定义的类型防护
    - [使用类型断言]
    - [使用`in`操作符]
  - [`typeof`类型防护]
  - [`instanceof`类型防护]

- [2. 可空类型](#2. 可空类型)

- - [可选参数和属性]
  - [类型防护和类型断言]

- [3. 类型别名](#3. 类型别名)

- - [接口与类型别名]

- [4. 字符串字面量类型](#4. 字符串字面量类型)

- [5. 数字字面量类型](#5. 数字字面量类型)

- [6. 枚举成员类型](#6. 枚举成员类型)

- [7. 可辨识联合（Discriminated Unions）](#7. 可辨识联合（Discriminated Unions）)

- - [完整性检查]

- [8. 多态的`this`类型](#8. 多态的`this`类型)

- [9. 索引类型（Index types）](#9. 索引类型（Index types）)

- - [索引类型和索引签名]

- [10. 映射类型（Mapped types）](#10. 映射类型（Mapped types）)

- - [从映射类型推断]

- [11. 条件类型（Conditional Types）](#11. 条件类型（Conditional Types）)

- - [分布条件类型]
  - [条件类型中的类型推断]
  - [预定义的条件类型]



本部分列出了一些高级类型建模方法，它与[工具类型](#工具类型)文档协同使用，本部分包括TypeScript中的类型以及可在全局范围内可用的类型。

#### 1. 类型保护与区分类型（Type Guards and Differentiating Types）

联合类型对于当值可以重叠的形式进行建模时非常有用。当我们需要知道我们是否有一个`fly`的方法。 如果变量在运行时确实是`Fish`时会发生什么？JavaScript中用于区分两个可能值的常见方法是检查成员的存在。如前所述，只能访问保证属于联合类型的所有组成部分的成员。

```
let pet = getSmallPet();

// Each of these property accesses will cause an error
if (pet.swim) {
  pet.swim();
} else if (pet.fly) {
  pet.fly();
}
```

为了使相同的代码正常工作，我们需要使用类型断言：

```
let pet = getSmallPet();

if ((pet as Fish).swim) {
  (pet as Fish).swim();
} else if ((pet as Bird).fly) {
  (pet as Bird).fly();
}
```



##### **用户定义的类型防护**

注意，我们不得不多次使用类型断言。如果我们执行了检查，然后知道每个分支中`pet`的类型，那就更好了。

TypeScript有一个称为*类型防护*的东西。类型防护是一个表达式，它执行运行时检查以确保该类型在一定范围内。



###### 使用类型断言

要定义类型保护，我们只需要定义一个返回类型为类型断言的函数：

```
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
```

在本示例中，`pet is Fish`是类型断言。断言的形式为`parameterName is Type`，其中`parameterName`必须是当前函数签名中参数的名称。

当使用某些变量调用`isFish`时，如果原始类型兼容，TypeScript就会将该变量缩小为该特定类型。

```
// Both calls to 'swim' and 'fly' are now okay.

if (isFish(pet)) {
  pet.swim();
}
else {
  pet.fly();
}
```

请注意，TypeScript不仅在`if`分支中知道`pet`是`Fish`，而且， 它也知道在`else`分支中没有`Fish`，所以必须有`Bird`。



###### 使用`in`操作符

现在，`in`运算符现在做为类型的缩小表达式。

对于`n in x`表达式，其中`n`是字符串字面量或字符串字面量类型，`x`是联合类型，*"true"*分支缩小为具有可选或必需属性`in`的类型，而*"false"*分支缩小为有可选属性或缺少属性。

```
function move(pet: Fish | Bird) {
  if ("swim" in pet) {
    return pet.swim();
  }
  return pet.fly();
}
```



##### **typeof类型防护**

让我们回过头来编写使用联合类型的`padLeft`版本的代码。我们可以使用类型断言来编写它，如下所示：

```
function isNumber(x: any): x is number {
  return typeof x === "number";
}

function isString(x: any): x is string {
  return typeof x === "string";
}

function padLeft(value: string, padding: string | number) {
  if (isNumber(padding)) {
    return Array(padding + 1).join(" ") + value;
  }
  if (isString(padding)) {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${padding}'.`);
}
```

但是，必须定义一个函数来确定类型是否为原始类型，这很麻烦。幸运的是，不需要将`typeof x === "number"`抽象到其自己的函数中，因为TypeScript会自己将其识别为类型保护。这意味着我们可以内联编写这些检查。

```
function padLeft(value: string, padding: string | number) {
  if (typeof padding === "number") {
    return Array(padding + 1).join(" ") + value;
  }
  if (typeof padding === "string") {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${padding}'.`);
}
```

这些`typeof`类型防护有两种不同的形式：`typeof v === "typename"`和`typeof v !== "typename"`，其中`"typename"`必须是`"number"`、`"string"`、`"boolean"`或`"symbol"`。虽然TypeScript不会阻止你与其他字符串进行比较，但该语言不会将这些表达式识别为类型保护。



##### **instanceof类型防护**

如果你已经看了有关`typeof`类型防护的内容，并且熟悉JavaScript中的`instanceof`运算符，则可能对本节的内容有所了解。

`instanceof`类型防护是使用其构造函数缩小类型的一种方法。例如，让我们借用前面的字符串填充器示例：

```
interface Padder {
  getPaddingString(): string;
}

class SpaceRepeatingPadder implements Padder {
  constructor(private numSpaces: number) {}
  getPaddingString() {
    return Array(this.numSpaces + 1).join(" ");
  }
}

class StringPadder implements Padder {
  constructor(private value: string) {}
  getPaddingString() {
    return this.value;
  }
}

function getRandomPadder() {
  return Math.random() < 0.5
    ? new SpaceRepeatingPadder(4)
    : new StringPadder("  ");
}

// Type is 'SpaceRepeatingPadder | StringPadder'
let padder: Padder = getRandomPadder();

if (padder instanceof SpaceRepeatingPadder) {
  padder; // type narrowed to 'SpaceRepeatingPadder'
}
if (padder instanceof StringPadder) {
  padder; // type narrowed to 'StringPadder'
}
```

`instanceof`的右侧需要是一个构造函数，并且TypeScript将窄化为：

1. 函数原型属性的类型（如果其类型不是`any`）
2. 该类型的构造签名返回的类型的并集

以此顺序。



#### 2. 可空类型

TypeScript有两种特殊类型，即：`null`和`undefined`，它们分别有值*null*和*undefined*。我们在[基本类型部分](#基本类型部分)中简要提到了这些内容。默认情况下，类型检查器认为`null`和`undefined`可分配给任何东西。实际上，`null`和`undefined`是每种类型的有效值。也就是说即使你想阻止将它们分配给任何类型，也无法阻止它们。空值发明者Tony Hoare将此称为[“十亿美元的错误”](https://en.wikipedia.org/wiki/Null_pointer#History)。

通过`--strictNullChecks`标志可解决此问题：声明变量时，它不会自动包含`null`和`undefined`。你可以使用并集类型显式包括它们：

```
let s = "foo";
s = null; // error, 'null' is not assignable to 'string'
let sn: string | null = "bar";
sn = null; // ok

sn = undefined; // error, 'undefined' is not assignable to 'string | null'
```

请注意，TypeScript对待`null`和`undefined`的方式有所不同，以匹配JavaScript语义。`string | null`与`string | undefined`和`string | null`与`string | undefined | null`是不同的类型。

自TypeScript 3.7及其后，你可以使用[可选链](#可选链)来简化可空类型的使用。



##### **可选参数和属性**

通过`--strictNullChecks`，可选参数会自动添加`| undefined`：

```
function f(x: number, y?: number) {
  return x + (y || 0);
}
f(1, 2);
f(1);
f(1, undefined);
f(1, null); // error, 'null' is not assignable to 'number | undefined'
```

可选属性也是如此：

```
class C {
  a: number;
  b?: number;
}
let c = new C();
c.a = 12;
c.a = undefined; // error, 'undefined' is not assignable to 'number'
c.b = 13;
c.b = undefined; // ok
c.b = null; // error, 'null' is not assignable to 'number | undefined'
```



##### **类型防护和类型断言**

由于可为空的类型是通过联合实现的，所以需要使用类型保护来避免`null`。幸运的是，这与你使用JavaScript编写的代码相同：

```
function f(sn: string | null): string {
  if (sn == null) {
    return "default";
  } else {
    return sn;
  }
}
```

消除`null`在这里很明显，但是也可以使用terser运算符：

```
function f(sn: string | null): string {
  return sn || "default";
}
```

如果编译器无法消除`null`或`undefined`，则可以使用类型断言运算符手动删除它们。语法为后缀`!`，如：`identifier!`是从`identifier`类型中删除`null`和`undefined`：

```
function broken(name: string | null): string {
  function postfix(epithet: string) {
    return name.charAt(0) + ".  the " + epithet; // error, 'name' is possibly null
  }
  name = name || "Bob";
  return postfix("great");
}

function fixed(name: string | null): string {
  function postfix(epithet: string) {
    return name!.charAt(0) + ".  the " + epithet; // ok
  }
  name = name || "Bob";
  return postfix("great");
}
```

该示例在此处使用了嵌套函数，因为编译器无法消除嵌套函数内部的空值（立即调用的函数表达式除外）。 这是因为它无法跟踪对嵌套函数的所有调用，尤其是如果从外部函数返回它。不知道调用函数的位置，就无法知道主体执行时的`name`类型。



#### 3. 类型别名

类型别名是为类型创建新名称。类型别名有时与接口相似，但是可以命名基元、并集、元组和其他必须手工编写的其他类型。

```
type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
function getName(n: NameOrResolver): Name {
  if (typeof n === "string") {
    return n;
  } else {
    return n();
  }
}
```

别名实际并不会创建新类型，而是会创建一个新名称来引用该类型。虽然可以将原语用作文档的一种形式，但它并不是很有用。

就像接口一样，类型别名也可以是泛型的-我们可以添加类型参数并在别名声明的右侧使用它们：

```
type Container<T> = { value: T };
```

我们还可以在属性中使用类型别名来引用自身：

```
type Tree<T> = {
  value: T;
  left: Tree<T>;
  right: Tree<T>;
}
```

与交集类型一起使用，我们创造一些奇怪的类型：

```
type LinkedList<T> = T & { next: LinkedList<T> };

interface Person {
  name: string;
}

var people: LinkedList<Person>;
var s = people.name;
var s = people.next.name;
var s = people.next.next.name;
var s = people.next.next.next.name;
```

但是，类型别名不能出现在声明右侧的任何位置：

```
type Yikes = Array<Yikes>; // error
```



##### **接口与类型别名**

如前所述，类型别名可以起到类似接口的作用。 但是，有一些细微的差异。

不同之处在于，接口创建了一个新名称，该名称随处可见；而类型别名不会创建新名称，例如：错误消息不会使用别名。在下面的代码中，将鼠标悬停在编辑器中的`interfaced`上将显示其返回`Interface`，但将显示`aliased`将返回对象字面量类型。

```
type Alias = { num: number }
interface Interface {
  num: number;
}
declare function aliased(arg: Alias): Alias;
declare function interfaced(arg: Interface): Interface;
```

在较旧的TypeScript版本中，不能扩展或实现类型别名（也不能扩展/实现其他类型）。从2.7版开始，可以通过创建新的交集类型来扩展，如：`type Cat = Animal & { purrs: true }`。

由于[软件的理想状态是对扩展开放（对修改封闭）](https://en.wikipedia.org/wiki/Open/closed_principle)，因此，如果可能，应始终在类型别名上使用接口。

另一方面，如果无法使用接口表达某种状态，而需要使用并集或元组类型，则通常应使用类型别名。



#### 4. 字符串字面量类型

参考：[语言手册-字符串字面量类型](#语言手册-字符串字面量类型)



#### 5. 数字字面量类型

参考：[语言手册-数字字面量类型](#语言手册-数字字面量类型)



#### 6. 枚举成员类型

如前面[枚举章节](#枚举章节)所述，枚举成员具有类型，每个成员都进行字面量初始化时。

在很多时候，我们在谈论“单个类型”时，既指枚举成员类型，也指数字/字符串字面量类型，尽管许多用户会交替使用“单个类型”和“字面量类型”。



#### 7. 可辨识联合（Discriminated Unions）

可以组合单例类型、联合类型、类型保护和类型别名来构建称为*可辨识联合*的高级模式，也称为标记联合或代数数据类型。可辨识联合在函数式编程中很有用。某些语言会自动为区分可辨识联合，相反，TypeScript建立在现存的JavaScript模式上。它有3个要素：

1. 具有普通的单例类型属性-*可辨识*的特征
2. 一个类型别名包含了类型的联合-*联合*
3. 在公共属性上的类型保护

```
interface Square {
  kind: "square";
  size: number;
}
interface Rectangle {
  kind: "rectangle";
  width: number;
  height: number;
}
interface Circle {
    kind: "circle";
    radius: number;
}
```

首先，我们声明将要联合的接口。每个接口都有一个`kind`属性，该属性有不同的字符串字面量类型。`kind`属性称为*可辨识*特征或*标签*。其他属性特定于每个接口。请注意，当前接口不相关的。下面将它们联合到一起：

```
type Shape = Square | Rectangle | Circle;
```

现在使用可辨识联合：

```
function area(s: Shape) {
  switch (s.kind) {
    case "square":
      return s.size * s.size;
    case "rectangle":
      return s.height * s.width;
    case "circle":
      return Math.PI * s.radius ** 2;
  }
}
```



##### **完整性检查**

当没有涵盖所有可辨识联合变体时，我们希望编译器通知我们。例如，我们将`Triangle`添加到`Shape`，还需要更新`area`：

```
type Shape = Square | Rectangle | Circle | Triangle;
function area(s: Shape) {
  switch (s.kind) {
    case "square":
      return s.size * s.size;
    case "rectangle":
      return s.height * s.width;
    case "circle":
      return Math.PI * s.radius ** 2;
  }
  // should error here - we didn't handle case "triangle"
}
```

可以通过两种方式实现。首先传入`--strictNullChecks`并指定返回类型：

```
function area(s: Shape): number {
  // error: returns number | undefined
  switch (s.kind) {
    case "square":
      return s.size * s.size;
    case "rectangle":
      return s.height * s.width;
    case "circle":
      return Math.PI * s.radius ** 2;
  }
}
```

因为`switch`没有穷举所有类型，所以TypeScript知道该函数有时可能返回`undefined`。如果明确指定返回类型为`number`，则将收到错误消息，返回类型实际上是`number | undefined`。但是，此方法微妙之处于`--strictNullChecks`对旧代码支持不够友好。

第二种方法是使用`never`类型，用编译器用来检查完整性：

```
function assertNever(x: never): never {
  throw new Error("Unexpected object: " + x);
}
function area(s: Shape) {
  switch (s.kind) {
    case "square":
      return s.size * s.size;
    case "rectangle":
      return s.height * s.width;
    case "circle":
      return Math.PI * s.radius ** 2;
    default:
      return assertNever(s); // error here if there are missing cases
  }
}
```

在这里，`assertNever`会检查`s`的是否是`never`类型（即：删除所有其他情况后剩下的类型）。如果忘记某个*case*，`s`将会有真实的类型，并收到一个类型错误信息。这种方法需要你定义一个额外的函数，但在你忘记某个*case*时也会更加明显。



#### 8. 多态的this类型

多态的`this`类型表示包含类或接口的*子类型*，这被称为*F-bounded*多态性。这可以很容易的表现连贯的接口继承。例如，以下是一个简单的计算器，其在每次操作后都会返回`this`：

```
class BasicCalculator {
  public constructor(protected value: number = 0) {}
  public currentValue(): number {
    return this.value;
  }
  public add(operand: number): this {
    this.value += operand;
    return this;
  }
  public multiply(operand: number): this {
    this.value *= operand;
    return this;
  }
  // ... other operations go here ...
}

let v = new BasicCalculator(2).multiply(5).add(1).currentValue();
```

由于该类使用`this`类型，因此可以对其进行扩展，而新类可以使用旧方法而无需进行任何更改。

```
class ScientificCalculator extends BasicCalculator {
  public constructor(value = 0) {
    super(value);
  }
  public sin() {
    this.value = Math.sin(this.value);
    return this;
  }
  // ... other operations go here ...
}

let v = new ScientificCalculator(2)
        .multiply(5)
        .sin()
        .add(1)
        .currentValue();
```

如果没有`this`类型，`ScientificCalculator`将无法扩展`BasicCalculator`并保持接口的连贯性。`multiply`会返回没有`sin`方法的`BasicCalculator`。但是，对于`this`类型，`multiply`将返回`this`，此处为`ScientificCalculator`。



#### 9. 索引类型（Index types）

通过索引类型，可以使编译器检查使用动态属性名的代码。例如，一个常见的JavaScript模式是从对象中选择属性的子集：

```
function pluck(o, propertyNames) {
  return propertyNames.map(n => o[n]);
}
```

以下是如何在TypeScript中通过*索引类型查询*和*索引访问运算符*使用此函数：

```
function pluck<T, K extends keyof T>(o: T, propertyNames: K[]): T[K][] {
  return propertyNames.map(n => o[n]);
}

interface Car {
  manufacturer: string;
  model: string;
  year: number;
}
let taxi: Car = {
  manufacturer: 'Toyota',
  model: 'Camry',
  year: 2014
};

// Manufacturer and model are both of type string,
// so we can pluck them both into a typed string array
let makeAndModel: string[] = pluck(taxi, ['manufacturer', 'model']);

// If we try to pluck model and year, we get an
// array of a union type: (string | number)[]
let modelYear = pluck(taxi, ['model', 'year'])
```

编译器会检查`manufacturer`和`model`是否是`Car`的属性。本示例还引入了几个新运算符，首先是`keyof T`，*索引类型查询运算符*。对于任何类型`T`，`T`的键都是`T`已知的公共属性名称的并集。例如：

```
let carProps: keyof Car; // the union of ('manufacturer' | 'model' | 'year')
```

`keyof Car`可以与`'manufacturer' | 'model' | 'year'`互换。区别在于，如果你向`Car`添加另一个属性，例如：`ownersAddress: string`，那么`keyof Car`将自动更新为`'manufacturer' | 'model' | 'year' | 'ownersAddress'`。而且，你可以在像`pluck`这样的泛型上下文中使用`keyof`，这种情况下你可能无法提前知道属性名称。这样编译器将会检查你是否将正确的属性名称集传递给`pluck`：

```
// error, 'unknown' is not in 'manufacturer' | 'model' | 'year'
pluck(taxi, ['year', 'unknown']); /
```

第二个运算符是*索引访问运算符*`T[K]`。在这里，类型语法反映了表达式语法。这意味着`person['name']`的类型为`Person['name']`-在我们的示例中只是`string`。但是，就像索引类型查询一样，可以在泛型上下文中使用`T[K]`，这才是其强大之处。你只需要确保类型变量`K extends keyof T`即可。这是另一个名为`getProperty`的函数示例。

```
function getProperty<T, K extends keyof T>(o: T, propertyName: K): T[K] {
  return o[propertyName]; // o[propertyName] is of type T[K]
}
```

`getProperty`中的`o: T`和`propertyName: K`意味着`o[propertyName]: T[K]`。返回`T[K]`结果后，编译器将实例化键的实际类型，因此`getProperty`的返回类型会根据请求的属性而有所不同。

```
let name: string = getProperty(taxi, 'manufacturer');
let year: number = getProperty(taxi, 'year');

// error, 'unknown' is not in 'manufacturer' | 'model' | 'year'
let unknown = getProperty(taxi, 'unknown');
```



##### **索引类型和索引签名**

`keyof`和`T[K]`与索引签名交互。索引签名参数类型必须是“字符串”或“数字”。如果有一个字符串索引签名类型，那么`keyof T`将为`string | number`（而不仅仅是`string`，因为在JavaScript中，可以使用字符串（`object['42']`）或数字（`object[42]`）访问对象属性。`T[string]`只是索引签名的类型：

```
interface Dictionary<T> {
  [key: string]: T;
}
let keys: keyof Dictionary<number>; // string | number
let value: Dictionary<number>['foo']; // number
```

如果你的类型有数字索引签名，则`keyof T`仅是`number`。

```
interface Dictionary<T> {
  [key: number]: T;
}
let keys: keyof Dictionary<number>; // number
let value: Dictionary<number>['foo']; // Error, Property 'foo' does not exist on type 'Dictionary<number>'.
let value: Dictionary<number>[42]; // number
```



#### 10. 映射类型（Mapped types）

一个常见的任务是采用一个现有的类型并将其每个属性设为可选：

```
interface PersonPartial {
  name?: string;
  age?: number;
}
```

或者我们希望设置为只读：

```
interface PersonReadonly {
  readonly name: string;
  readonly age: number;
}
```

这在JavaScript中经常发生，TypeScript提供了一种基于旧类型创建新类型的方法-*映射类型*。在映射类型中，新类型以相同的方式转换旧类型中的每个属性。例如，可以将所有属性设置为`readonly`或可选类型。 以下是几个示例：

```
type Readonly<T> = {
  readonly [P in keyof T]: T[P];【
}
type Partial<T> = {
  [P in keyof T]?: T[P];
}
```

并像这样使用：

```
type PersonPartial = Partial<Person>;
type ReadonlyPerson = Readonly<Person>;
```

请注意，此语法描述的是类型而不是成员。如果要添加成员，则可以使用交集类型：

```
// Use this:
type PartialWithNewMember<T> = {
  [P in keyof T]?: T[P];
} & { newMember: boolean }

// **Do not** use the following!
// This is an error!
type PartialWithNewMember<T> = {
  [P in keyof T]?: T[P];
  newMember: boolean;
}
```

让我们看一下最简单的映射类型及其组成部分：

```
type Keys = 'option1' | 'option2';
type Flags = { [K in Keys]: boolean };
```

该语法与索引签名的语法类似，其内部使用`for .. in`。分为三个部分：

1. 类型变量`K`依次绑定到每个属性
2. 字符串字面量联合`Keys`，其中包含了要迭代的属性的名称
3. 属性的结果类型

在此示例中，`Keys`是属性名的硬编码列表，并且属性类型始终为`boolean`，因此此映射类型等同于编写：

```
type Flags = {
  option1: boolean;
  option2: boolean;
}
```

但在实际应用中，看起来像上面的`Readonly`或`Partial`。它们会基于某些现有类型，并且以某种方式转换属性。这就是`keyof`和索引访问类型的来源：

```
type NullablePerson = { [P in keyof Person]: Person[P] | null }
type PartialPerson = { [P in keyof Person]?: Person[P] }
```

但是有泛型版本会更加有用。

```
type Nullable<T> = { [P in keyof T]: T[P] | null }
type Partial<T>= { [P in keyof T]?: T[P] }
```

在这些示例中，属性列表是`keyof T`，而结果类型是`T[P]`的变体。对于映射类型的任何常规使用，这都是一个很好的模板。 这是因为这种转换是[同态的](#同态的)，也就是说映射仅适用于`T`的属性，而不适用于其他属性。编译器知道在添加任何新属性修饰符之前，它可以复制所有现有的属性修饰符。例如，如果`Person.name`为只读，则`Partial<Person>.name`将为只读且可选。

这是另一个示例，其中`T[P]`包装在`Proxy<T>`类中：

```
type Proxy<T> = {
  get(): T;
  set(value: T): void;
}
type Proxify<T> = {
  [P in keyof T]: Proxy<T[P]>;
}
function proxify<T>(o: T): Proxify<T> {
 // ... wrap proxies ...
}
let proxyProps = proxify(props);
```

请注意，`Readonly<T>`和`Partial<T>`如此有用，它们与`Pick`和`Record`一起包含在TypeScript的标准库中：

```
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
}
type Record<K extends keyof any, T> = {
  [P in K]: T;
}
```

`Readonly`、`Partial`和`Pick`是同态的，而`Record`不是同态的。提示`Record`不是同态的，是因为它不需要输入类型就可以从以下位置复制属性：

```
type ThreeStringProps = Record<'prop1' | 'prop2' | 'prop3', string>
```

非同态类型本质上是在创建新属性，因此它们无法从任何地方复制属性修改器。



##### **从映射类型推断**

已经知道了如何包装类型的属性，接下来要做的就是将它们拆包。幸运的是，这很简单：

```
function unproxify<T>(t: Proxify<T>): T {
  let result = {} as T;
  for (const k in t) {
    result[k] = t[k].get();
  }
  return result;
}

let originalProps = unproxify(proxyProps);
```

请注意，此展开推论仅适用于同态映射类型。如果映射的类型不是同态的，则必须为展开函数提供一个明确的类型参数。



#### 11. 条件类型（Conditional Types）

TypeScript 2.8引入了*条件类型*，这些条件类型增加了表达非均匀类型映射的能力。条件类型根据表示为类型关系测试的条件选择两种可能的类型之一：

```
T extends U ? X : Y
```

上面的类型表示当`T`可分配给`U`时，类型为`X`，否则为`Y`。

条件类型`T extends U ? X : Y`可*解析*为`X`或`Y`，也可以*延迟*，因为条件取决于一个或多个类型变量。当`T`或`U`包含类型变量时，是通过类型系统是否有足够的信息来推断`T`是否可分配给`U`来确定是解析为`X`还是`Y`还是延迟。

以下展示了可立即解析为某些类型的示例：

```
declare function f<T extends boolean>(x: T): T extends true ? string : number;

// Type is 'string | number'
let x = f(Math.random() < 0.5)
```

另一个示例是`TypeName`类型别名，该别名使用嵌套的条件类型：

```
type TypeName<T> = T extends string
  ? "string"
  : T extends number
  ? "number"
  : T extends boolean
  ? "boolean"
  : T extends undefined
  ? "undefined"
  : T extends Function
  ? "function"
  : "object";

type T0 = TypeName<string>;  // "string"
type T1 = TypeName<"a">;  // "string"
type T2 = TypeName<true>;  // "boolean"
type T3 = TypeName<() => void>;  // "function"
type T4 = TypeName<string[]>;  // "object"
```

但是，作为一个条件类型被延迟的示例-它们会保持而不是选择分支，将在以下示例中出现：

```
interface Foo {
  propA: boolean;
  propB: boolean;
}

declare function f<T>(x: T): T extends Foo ? string : number;

function foo<U>(x: U) {
  // Has type 'U extends Foo ? string : number'
  let a = f(x);

  // This assignment is allowed though!
  let b: string | number = a;
}
```

上面示例中，变量`a`的条件类型尚未选择分支。当另一段代码最终调用`foo`时，将用`U`替换为其他类型，并且TypeScript将重新评估条件类型，确定其是否可以实际选择分支。

同时，我们可以将条件类型分配给任何其他目标类型，只要条件的每个分支都可以分配给该目标即可。因此，在上面的示例中，我们可以将`U extends Foo ? string : number`分配给`string | number`，因为无论条件求值的结果是什么，它都是`string`或`number`。



##### **分布条件类型**

其中选中的类型为裸类型参数的条件类型称为*分布式条件类型*。实例化期间，分布条件类型自动分布在联合类型上。例如，将类型参数为`A | B | C`的`T`的实例化`T extends U ? X : Y`将被解析为`(A extends U ? X : Y) | (B extends U ? X : Y) | (C extends U ? X : Y)`。

示例：

```
type T10 = TypeName<string | (() => void)>;  // "string" | "function"
type T12 = TypeName<string | string[] | undefined>;  // "string" | "object" | "undefined"
type T11 = TypeName<string[] | number[]>;  // "object"
```

在分布条件类型`T extends U ? X : Y`的实例中，条件类型中对`T`的引用将解析为并集类型的各个组成部分，即：`T`是指条件类型分布在并集类型上的各个组成部分。此外，对`X`中的`T`的引用还有一个附加的类型参数约束`U`（即`T`被认为可分配给`X`中的`U`）。

示例：

```
type BoxedValue<T> = { value: T };
type BoxedArray<T> = { array: T[] };
type Boxed<T> = T extends any[] ? BoxedArray<T[number]> : BoxedValue<T>;

type T20 = Boxed<string>;  // BoxedValue<string>;
type T21 = Boxed<number[]>;  // BoxedArray<number>;
type T22 = Boxed<string | number[]>;  // BoxedValue<string> | BoxedArray<number>;
```

请注意，`T`在`Boxed<T>`的真实分支内有附加约束`any[]`，因此可以将数组的元素类型称为`T[number]`。另外，应注意在上一个示例中，条件类型是如何在联合类型上分布的。

条件类型的分布属性可以方便地用于*过滤联*合类型：

```
type Diff<T, U> = T extends U ? never : T;  // Remove types from T that are assignable to U
type Filter<T, U> = T extends U ? T : never;  // Remove types from T that are not assignable to U

type T30 = Diff<"a" | "b" | "c" | "d", "a" | "c" | "f">;  // "b" | "d"
type T31 = Filter<"a" | "b" | "c" | "d", "a" | "c" | "f">;  // "a" | "c"
type T32 = Diff<string | number | (() => void), Function>;  // string | number
type T33 = Filter<string | number | (() => void), Function>;  // () => void

type NonNullable<T> = Diff<T, null | undefined>;  // Remove null and undefined from T

type T34 = NonNullable<string | number | undefined>;  // string | number
type T35 = NonNullable<string | string[] | null | undefined>;  // string | string[]

function f1<T>(x: T, y: NonNullable<T>) {
  x = y;  // Ok
  y = x;  // Error
}

function f2<T extends string | undefined>(x: T, y: NonNullable<T>) {
  x = y;  // Ok
  y = x;  // Error
  let s1: string = x;  // Error
  let s2: string = y;  // Ok
}
```

与映射类型结合使用时，条件类型会特别有用：

```
type FunctionPropertyNames<T> = { [K in keyof T]: T[K] extends Function ? K : never }[keyof T];
type FunctionProperties<T> = Pick<T, FunctionPropertyNames<T>>;

type NonFunctionPropertyNames<T> = { [K in keyof T]: T[K] extends Function ? never : K }[keyof T];
type NonFunctionProperties<T> = Pick<T, NonFunctionPropertyNames<T>>;

interface Part {
  id: number;
  name: string;
  subparts: Part[];
  updatePart(newName: string): void;
}

type T40 = FunctionPropertyNames<Part>;  // "updatePart"
type T41 = NonFunctionPropertyNames<Part>;  // "id" | "name" | "subparts"
type T42 = FunctionProperties<Part>;  // { updatePart(newName: string): void }
type T43 = NonFunctionProperties<Part>;  // { id: number, name: string, subparts: Part[] }
```

与联合和交集类型类似，条件类型不允许递归引用自己。例如，以下会是一个错误：

```
type ElementType<T> = T extends any[] ? ElementType<T[number]> : T;  // Error
```



##### **条件类型中的类型推断**

在条件类型的`extends`子句中，可以有`infer`声明，该声明引入要推断的类型变量。可以在条件类型的真实分支中引用此类推断的类型变量。同一类型变量可能有多个`infer`位置。

例如，以下代码提取函数类型的返回类型：

```
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;
```

可以嵌套条件类型，以顺序评估的一系列模式匹配。

```
type Unpacked<T> =
  T extends (infer U)[] ? U :
  T extends (...args: any[]) => infer U ? U :
  T extends Promise<infer U> ? U :
  T;

type T0 = Unpacked<string>;  // string
type T1 = Unpacked<string[]>;  // string
type T2 = Unpacked<() => string>;  // string
type T3 = Unpacked<Promise<string>>;  // string
type T4 = Unpacked<Promise<string>[]>;  // Promise<string>
type T5 = Unpacked<Unpacked<Promise<string>[]>>;  // string
```

下面的示例演示了在协变量位置上，同一类型变量的多个候选时如何导致推断联合类型：

```
type Foo<T> = T extends { a: infer U, b: infer U } ? U : never;
type T10 = Foo<{ a: string, b: string }>;  // string
type T11 = Foo<{ a: string, b: number }>;  // string | number
```

同样，在变数位置中针对同一类型变量的多个候选项会导致得出交集类型：

```
type Bar<T> = T extends { a: (x: infer U) => void, b: (x: infer U) => void } ? U : never;
type T20 = Bar<{ a: (x: string) => void, b: (x: string) => void }>;  // string
type T21 = Bar<{ a: (x: string) => void, b: (x: number) => void }>;  // string & number
```

从有多个调用签名的类型（如，重载函数的类型）进行推断时，可能是最宽松的情况将根据最后一个签名进行推断。无法基于参数类型列表执行重载解析。

```
declare function foo(x: string): number;
declare function foo(x: number): string;
declare function foo(x: string | number): string | number;
type T30 = ReturnType<typeof foo>;  // string | number
```

对于常规类型参数，不能在约束子句中使用`infer`声明：

```
type ReturnType<T extends (...args: any[]) => infer R> = R;  // Error, not supported
```

但是，通过删除约束中的类型变量并指定条件类型，可以获得大致相同的效果：

```
type AnyFunction = (...args: any[]) => any;
type ReturnType<T extends AnyFunction> = T extends (...args: any[]) => infer R ? R : any;
```



##### **预定义的条件类型**

TypeScript 2.8中向`lib.d.ts`添加了几个预定义的条件类型：

- `Exclude<T, U>` – 从`T`中剔除可以赋值给`U`的类型
- `Extract<T, U>` – 从`T`中提取出可以赋值给`U`的类型
- `NonNullable<T>` – 从`T`中剔除`null`和`undefined`
- `ReturnType<T>` – 获取函数返回值类型
- `InstanceType<T>` – 获取构造函数类型的实例类型

示例：

```
type T00 = Exclude<"a" | "b" | "c" | "d", "a" | "c" | "f">;  // "b" | "d"
type T01 = Extract<"a" | "b" | "c" | "d", "a" | "c" | "f">;  // "a" | "c"

type T02 = Exclude<string | number | (() => void), Function>;  // string | number
type T03 = Extract<string | number | (() => void), Function>;  // () => void

type T04 = NonNullable<string | number | undefined>;  // string | number
type T05 = NonNullable<(() => string) | string[] | null | undefined>;  // (() => string) | string[]

function f1(s: string) {
  return { a: 1, b: s };
}

class C {
  x = 0;
  y = 0;
}

type T10 = ReturnType<() => string>;  // string
type T11 = ReturnType<(s: string) => void>;  // void
type T12 = ReturnType<(<T>() => T)>;  // {}
type T13 = ReturnType<(<T extends U, U extends number[]>() => T)>;  // number[]
type T14 = ReturnType<typeof f1>;  // { a: number, b: string }
type T15 = ReturnType<any>;  // any
type T16 = ReturnType<never>;  // never
type T17 = ReturnType<string>;  // Error
type T18 = ReturnType<Function>;  // Error

type T20 = InstanceType<typeof C>;  // C
type T21 = InstanceType<any>;  // any
type T22 = InstanceType<never>;  // never
type T23 = InstanceType<string>;  // Error
type T24 = InstanceType<Function>;  // Error
```

注意：`Exclude`类型是建议的`Diff`类型实现。使用`Exclude`这个名字是为了避免破坏已经定义了`Diff`的代码，并且TS官方感觉这个名字能更好地表达该类型的语义。



### 3.2 声明合并（Declaration Merging）

- [1. 介绍](#1. 介绍)

- [2. 基础概念](#2. 基础概念)

- [3. 合并接口](#3. 合并接口)

- [4. 合并命名空间](#4. 合并命名空间)

- [5. 命名空间与类、函数和枚举类型合并](#5. 命名空间与类、函数和枚举类型合并)

- - [合并命名空间和类]

- [6. 非法的合并](#6. 非法的合并)

- [7. 模块扩展](#7. 模块扩展)

- - [全局扩展]

#### 1. 介绍

TypeScript中的一些独特概念在类型层面上描述了JavaScript对象的模型。其中一个独特的例子是，TypeScript*“声明合并”*的概念。理解这一概念，也将帮助你更好的使用现有的JavaScript。同时，也有助于更多高级的抽象概念。

就本文而言，“声明合并”是指编译器将使用相同名称的两个独立声明合并为一个声明。合并后声明会有有原来两个原始声明的功能。可以合并任意数量的声明，而不仅限于两个声明。



#### 2. 基础概念

在TypeScript中，声明创建以下三种实体之一：命名空间、类型或值。创建*命名空间*的声明会创建一个命名空间，其中包含使用点（`.`）符号访问时使用的名称。创建*类型*的声明是：用声明的模型创建一个类型，并绑定到指定名称的类型。最后，创建*值*的声明创建会在JavaScript输出中可见。

| 声明类型 | 命名空间 | 类型 |  值  |
| :------- | :------: | :--: | :--: |
| 命名空间 |    X     |      |  X   |
| 类       |          |  X   |  X   |
| 枚举     |          |  X   |  X   |
| 接口     |          |  X   |      |
| 类型别名 |          |  X   |      |
| 函数     |          |      |  X   |
| 变量     |          |      |  X   |

了解每个声明创建的内容，有助于理解执行声明合并时有哪些东西被合并了。



#### 3. 合并接口

最简单也许最常见声明合并的类型是*接口合并*。在最基本的级别上，合并的机制是将两个声明的成员机械地放到有相同名称的单个接口中。

```
interface Box {
  height: number;
  width: number;
}

interface Box {
  scale: number;
}

let box: Box = {height: 5, width: 6, scale: 10};
```

接口的非函数成员应该是唯一的。如果它们唯一，那么它们必须是同一类型。如果两个接口声明了相同名称但类型不同的非函数成员，则编译器会报错。

对于函数成员，相同名称的函数成员会被视为描述了这一函数的重载。同时还要注意，在接口`A`与后面的接口`A`合并时，第二个接口的优先级将高于第一个接口。

如下所示：

```
interface Cloner {
  clone(animal: Animal): Animal;
}

interface Cloner {
  clone(animal: Sheep): Sheep;
}

interface Cloner {
  clone(animal: Dog): Dog;
  clone(animal: Cat): Cat;
}
```

以上三个接口合并为一个声明：

```
interface Cloner {
  clone(animal: Dog): Dog;
  clone(animal: Cat): Cat;
  clone(animal: Sheep): Sheep;
  clone(animal: Animal): Animal;
}
```

请注意，每组接口的元素顺序保持不变，但各组接口之间的顺序是排列在后面接口重载会出现在前面。

该规则有一个例外是有特殊函数签名时。如果签名的参数类型为*单一*字符串字面量类型（例如，不是字符串字面量的联合类型），那么它会被提升到其合并的重载列表的顶部。

例如，以下接口将合并在一起：

```
interface Document {
  createElement(tagName: any): Element;
}
interface Document {
  createElement(tagName: "div"): HTMLDivElement;
  createElement(tagName: "span"): HTMLSpanElement;
}
interface Document {
  createElement(tagName: string): HTMLElement;
  createElement(tagName: "canvas"): HTMLCanvasElement;
}
```

合并后的`Document`会像下面这样：

```
interface Document {
  createElement(tagName: "canvas"): HTMLCanvasElement;
  createElement(tagName: "div"): HTMLDivElement;
  createElement(tagName: "span"): HTMLSpanElement;
  createElement(tagName: string): HTMLElement;
  createElement(tagName: any): Element;
}
```



#### 4. 合并命名空间

与接口相似，有相同名称的*命名空间*也会合并其成员。由于命名空间同时创建了命名空间和值，因此我们需要了解两者是如何合并的。

对于合并命名空间，每个命名空间中声明的导出接口都将合并，从而形成单个合并了接口定义的命名空间。

要合并命名空间里的值，在每个声明点，如果已经存在有指定名称的命名空间，那么那么后来的命名空间的导出成员会被加到已经存在的那个模块里。

在此示例中，`Animals`的声明合并：

```
namespace Animals {
  export class Zebra { }
}

namespace Animals {
  export interface Legged { numberOfLegs: number; }
  export class Dog { }
}
```

等同于：

```
namespace Animals {
  export interface Legged { numberOfLegs: number; }

  export class Zebra { }
  export class Dog { }
}
```

除了这些合并外，我们还需要了解非导出成员是怎么处理的。非导出成员仅在原始（未合并）命名空间中可见。也就是说合并后，从其它声明中合并来的成员将无法访问其未导出成员。

在此示例中，我们可以更清楚地看到这一点：

```
namespace Animal {
  let haveMuscles = true;

  export function animalsHaveMuscles() {
      return haveMuscles;
  }
}

namespace Animal {
  export function doAnimalsHaveMuscles() {
    return haveMuscles;  // Error, because haveMuscles is not accessible here
  }
}
```

因为`haveMuscles`没有导出，只有`animalsHaveMuscles`函数共享了相同的未合并命名空间可以访问空上变量。`doAnimalsHaveMuscles`函数虽然是合并命名空间的一部分，但并不能访问未导出的成员。



#### 5. 命名空间与类、函数和枚举类型合并

命名空间很灵活，还可以与其它类型的声明合并。只要命名空间声明必须遵循将与之合并的声明。合并结果声明会有两种声明类型的属性。TypeScript使用这一功能来实现一些JavaScript中及其他编程语言中的某些设计模式。

##### **命名空间与类合并**

这让我们可以表示内部类：

```
class Album {
  label: Album.AlbumLabel;
}
namespace Album {
  export class AlbumLabel { }
}
```

合并成员的可见性规则与前面[ “合并命名空间”](#合并命名空间)部分中描述的规则相同，因此我们必须导出`AlbumLabel`类，以便合并类可访问。最终结果是在另一个类内部管理一个类。还可以使用命名空间将更多静态成员添加到现有类。

除了内部类的模式之外，你可能会熟悉JavaScript的做法，即创建一个函数，然后通过向该函数添加属性来扩展该函数。TypeScript使用声明合并达到这一目的，并保证类型安全。

```
function buildLabel(name: string): string {
  return buildLabel.prefix + name + buildLabel.suffix;
}

namespace buildLabel {
  export let suffix = "";
  export let prefix = "Hello, ";
}

console.log(buildLabel("Sam Smith"));
```

同样，命名空间可用于扩展有静态成员的枚举：

```
enum Color {
  red = 1,
  green = 2,
  blue = 4
}

namespace Color {
  export function mixColor(colorName: string) {
    if (colorName == "yellow") {
      return Color.red + Color.green;
    }
    else if (colorName == "white") {
      return Color.red + Color.green + Color.blue;
    }
    else if (colorName == "magenta") {
      return Color.red + Color.blue;
    }
    else if (colorName == "cyan") {
      return Color.green + Color.blue;
    }
  }
}
```



#### 6. 非法的合并

TypeScript并非允许所有合并。目前为目，类不能与其它类或变量合并。更多关于模仿类合并的内容，请参见[TypeScript中的Mixins](#TypeScript中的Mixins)部分。



#### 7. 模块扩展

虽然JavaScript模块不支持合并，但是可以通过导入然后打补丁的方式来更新现有对象。让我们看一个示例：

```
// observable.ts
export class Observable {
  // ... implementation left as an exercise for the reader ...
}

// map.ts
import { Observable } from "./observable";
Observable.prototype.map = function (f) {
  // ... another exercise for the reader
}
```

这在TypeScript中也可以正常工作，但是编译器不了解`Observable.prototype.map`。可以通过模块扩充来知诉编译器：

```
// observable.ts
export class Observable<T> {
  // ... implementation left as an exercise for the reader ...
}

// map.ts
import { Observable } from "./observable";
declare module "./observable" {
  interface Observable<T> {
    map<U>(f: (x: T) => U): Observable<U>;
  }
}
Observable.prototype.map = function (f) {
  // ... another exercise for the reader
}


// consumer.ts
import { Observable } from "./observable";
import "./map";
let o: Observable<number>;
o.map(x => x.toFixed());
```

模块名称的解析与`import`/`export`中的模块标识符相同。有关更多信息，请参见[模块](#模块)章节。当这些声明在扩展中合并时，就像它们在与原始文件中相同的位置声明了的一样。

但是，要记住两个限制：

1. 不能在扩充中声明新的顶级声明，而只能对现有声明进行扩展（补丁）。
2. 默认导出也不能被扩展，只能命名导出（因为需要通过导出名称来扩展导出，并且`default`是保留字-相关详细信息，请参见[#14080](https://github.com/Microsoft/TypeScript/issues/14080)）

##### **全局扩展**

还可以从模块内部将声明添加到全局作用域中：

```
// observable.ts
export class Observable<T> {
  // ... still no implementation ...
}

declare global {
  interface Array<T> {
    toObservable(): Observable<T>;
  }
}

Array.prototype.toObservable = function () {
  // ...
}
```

全局扩展与模块扩展的行为和限制是相同的。



### 3.3 装饰器（Decorators）

- [1. 介绍](#1. 介绍)

- [2. 装饰器](#2. 装饰器)

- - [装饰器工厂]
  - [装饰器组合]
  - [装饰器求值]
  - [类装饰器]
  - [方法装饰器]
  - [访问器装饰器]
  - [属性装饰器]
  - [参数装饰器]
  - [元数据]

#### 1. 介绍

随着TypeScript和ES6引入类，在某些情况，就需要额外的特性来支持注释或修改类及其成员。*装饰器*提供了一种类声明及成员添加注释和元编程语法的方法。装饰器是JavaScript语言标准流程[第2阶段](https://github.com/tc39/proposal-decorators)（参考：[JavaScript(ECMAScript) 语言标准历史及标准制定过程介绍](https://itbilu.com/javascript/js/V1APADgrG.html)）中的建议，可作为TypeScript的实验功能使用。

注意：装饰器是一项实验功能，在将来的版本中可能会更改。

要为装饰器启用实验性支持，必须在命令行或`tsconfig.json`中启用`experimentalDecorators`编译选项：

*命令行：*

```
tsc --target ES5 --experimentalDecorators
```

*tsconfig.json：*

```
{
  "compilerOptions": {
    "target": "ES5",
    "experimentalDecorators": true
  }
}
```



#### 2. 装饰器

*装饰器*是一种特殊类型的声明，它可以被附加到[类声明](#类声明)、[方法](#方法)、[访问符](#访问符)、[属性](#属性)或[参数](#参数)上。装饰器使用`@expression`的形式，`expression`求值后必须为是一个函数，它会在运行时被调用，被装饰的声明信息做为参数传入。

例如，有一个`@sealed`装饰器，我们可以这样定义`sealed`函数：

```
function sealed(target) {
  // do something with 'target' ...
}
```

*注意：后面的[类装饰器](#类装饰器)部分有一个更详细的示例。*



##### **装饰器工厂**

如果要将自定义装饰器应用于声明的方式，就需要写一个装饰器工厂含函数。*装饰器工厂*是一个返回表达式的函数，装饰器将在运行时调用该表达式。

我们可以像下面这样写一个装饰器工厂函数：

```
function color(value: string) { // this is the decorator factory
  return function (target) { // this is the decorator
    // do something with 'target' and 'value'...
  }
}
```

*更详细的示例请参考下方的[方法装饰器](#方法装饰器)内容。*



##### **装饰器组合**

多个装饰器可以应用到同一个声明中，就像以下示例：

- 写在同一行：
```
@f @g x
```

- 写在多行：
```
@f
@g
x
```

当多个装饰器应用于同一个声明时，其求值类似于[数学中的复合函数](http://en.wikipedia.org/wiki/Function_composition)。在这个模型中，当复合*f*和*g*时，复合的结果(*f* ∘ *g*)(*x*)等于*f*(*g*(*x*))。

同样，在TypeScript中当多个装饰器应用于同一个声明时，将执行以下步骤：

1. 由上至下依次对装饰器表达式求值。
2. 值的结果会被当作函数，由下至上依次调用。

如果要使用[装饰器工厂](#装饰器工厂)，则可以通过以下示例观察求值顺序：

```
function f() {
  console.log("f(): evaluated");
  return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
    console.log("f(): called");
  }
}

function g() {
  console.log("g(): evaluated");
  return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
    console.log("g(): called");
  }
}

class C {
  @f()
  @g()
  method() {}
}
```

控制台打印结果如下：

```
f(): evaluated
g(): evaluated
g(): called
f(): called
```

##### **装饰器求值**

关于如何将装饰器应用于类内部的各种声明，有一个明确定义的顺序：

1. *参数装饰器*，之后依次是*方法*、*访问器*或*属性装饰器*将应用于每个实例成员。
2. *参数装饰器*，之后依次是*方法*、*访问器*或*属性装饰器*将应用于每个静态成员。
3. *参数装饰器*应用于构造函数。
4. *类装饰器*应用于该类。



##### **类装饰器**

*类装饰器*在类声明之前声明。类装饰器应用于类的构造函数，可用于监视，修改或替换类定义。类装饰器不能在声明文件（`.d.ts`）或任何其它环境上下文（如，`declare`类）中使用。

类装饰器表达式将在运行时作为函数调用，类的构造函数为其唯一参数。

如果类装饰器返回一个值，它将用提供的构造函数替换类声明。

*注意如果要返回新的构造函数，则必须注意处理好原来的原型链。在运行时的装饰器调用逻辑不会为你做这些。*

以下是应用于`Greeter`类的类装饰器（`@sealed`）的示例：

```
@sealed
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello, " + this.greeting;
  }
}
```

可以这样定义`@sealed`装饰器：

```
function sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}
```

当前`@sealed`被执行的时候，其将会密封（[Object.seal()](#Object.seal())）构造函数和原型。

以下是一个重载构造函数的示例：

```
function classDecorator<T extends {new(...args:any[]):{}}>(constructor:T) {
  return class extends constructor {
    newProperty = "new property";
    hello = "override";
  }
}

@classDecorator
class Greeter {
  property = "property";
  hello: string;
  constructor(m: string) {
    this.hello = m;
  }
}

console.log(new Greeter("world"));
```



##### **方法装饰器**

*方法装饰器*在方法声明之前声明。它会被应用到方法的*属性描述符*，并可以用于监视、修改或替换方法定义。方法装饰器不能在声明文件（`.d.ts`）、重载或任何其他环境上下文（如，`declare`类）中使用。

方法装饰器表达式会在运行时被当作函数调用，并带有以下三个参数：

1. 静态成员的类的构造函数或实例成员的类的原型。
2. 成员的名称。
3. 成员的*属性描述符*。

*注意：如果你的代码生成目标小于ES5，则属性描述符会是`undefined`。*

如果方法装饰器返回一个值，其将用作方法的属性描述符。

*注意：如果你的代码生成目标小于ES5，会忽略返回值。*

以下是方法装饰器（`@enumerable`）的示例，其是应用于`Greeter`类的方法：

```
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }

  @enumerable(false)
  greet() {
    return "Hello, " + this.greeting;
  }
}
```

可以用下面的函数声明来定义`@enumerable`装饰器：

```
function enumerable(value: boolean) {
  return function(
    target: any,
    propertyKey: string,
    descriptor: PropertyDescriptor
  ) {
    descriptor.enumerable = value;
  };
}
```

这个`@enumerable(false)`是一个[装饰器工厂](#装饰器工厂)。当装饰器`@enumerable(false)`)被调用时，它会修改属性描述符的`enumerable`属性。



##### **访问器装饰器**

*访问器装饰器*在访问器声明之前被声明。其被应用于访问器的*属性描述符*，可用于监视、修改或替换访问器的定义。访问器装饰器不能在声明文件（`.d.ts`）或任何其它环境上下文（如，`declare`类）中使用。

*注意：TypeScript不允许同时装饰成员的`get`和`set`访问器。而是，成员的所有装饰器必须应用于按文档顺序指定的第一个访问器。这是因为装饰器应用于\*属性描述符\*时，其会将`get`和`set`访问器组合在一起，而不是分别声明。*

访问器装饰器表达式会在运行时作为函数调用，并带有以下三个参数：

1. 静态成员的类的构造函数或实例成员的类的原型。
2. 成员的名称。
3. 成员的*属性描述符*。

*注意：如果你的代码生成目标小于ES5，则属性描述符会是`undefined`。*

如果访问器装饰器返回一个值，其将用作该成员的属性描述符。

*注意：如果你的代码生成目标小于ES5，其将被忽略。*

以下是访问器装饰器（`@configurable`）的示例，其会应用于`Point`类成员：

```
class Point {
  private _x: number;
  private _y: number;
  constructor(x: number, y: number) {
    this._x = x;
    this._y = y;
  }

  @configurable(false)
  get x() {
    return this._x;
  }

  @configurable(false)
  get y() {
    return this._y;
  }
}
```

可以通过如下函数声明的方式来定义`@configurable`装饰器：

```
function configurable(value: boolean) {
  return function(
    target: any,
    propertyKey: string,
    descriptor: PropertyDescriptor
  ) {
    descriptor.configurable = value;
  };
}
```



##### **属性装饰器**

*属性装饰器*在属性声明之前被声明。不能在声明文件（`.d.ts`）或任何其它环境上下文（如，`declare`类）中使用属性装饰器。

属性装饰器表达式会在运行时作为函数调用，并带有以下两个参数：

1. 静态成员的类的构造函数或实例成员的类的原型。
2. 成员的名称。

*注意：属性描述符不会做为参数传入属性装饰器，这与TypeScript中初始化属性装饰器的方式有关。因为当前在定义原型成员时没有描述实例属性的机制，也没有监视或修改属性的初始化程序的方法。返回值也会被忽略。因此，属性装饰器只能用于观察已为类声明了指定名称的属性。*

我们可以用它来记录有关该属性的元数据，如以下所示：

```
class Greeter {
  @format("Hello, %s")
  greeting: string;

  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    let formatString = getFormat(this, "greeting");
    return formatString.replace("%s", this.greeting);
  }
}
```

然后定义`@format`装饰器和`getFormat`函数

```
import "reflect-metadata";

const formatMetadataKey = Symbol("format");

function format(formatString: string) {
  return Reflect.metadata(formatMetadataKey, formatString);
}

function getFormat(target: any, propertyKey: string) {
  return Reflect.getMetadata(formatMetadataKey, target, propertyKey);
}
```

以上`@format("Hello, %s")`是个[装饰器工厂](#装饰器工厂)。当`@format("Hello, %s")`被调用时，其将使用`reflect-metadata`库中的`Reflect.metadata`函数为该属性添加一条元数据。调用`getFormat`时，它将读取该格式的元数据值。

*注意，以上示例需要使用`reflect-metadata`库，查看[元数据](#元数据)以了解更多信息。*



##### **参数装饰器**

*参数装饰器*在参数声明之前声明。其应用于类构造函数或方法声明的函数。参数修饰符不能在声明文件（`.d.ts`）、重载或任何其它环境上下文（如，`declare`类）中使用。

参数装饰器表达式会在运行时作为函数调用，并带有以下三个参数：

1. 静态成员的类的构造函数或实例成员的类的原型。
2. 成员的名称。
3. 参数函数的参数列表中索引序号。

*注意：参数修饰符只能用于监视是否已在方法中声明了参数。*

参数装饰器的返回值会被忽略。

以下是示例中定义了参数修饰符（`@required`），其应用于`Greeter`类成员的参数：

```
class Greeter {
  greeting: string;

  constructor(message: string) {
    this.greeting = message;
  }

  @validate
  greet(@required name: string) {
    return "Hello " + name + ", " + this.greeting;
  }
}
```

然后我们使用以下的函数定义`@required`和`@validate`装饰器：

```
import "reflect-metadata";

const requiredMetadataKey = Symbol("required");

function required(
  target: Object,
  propertyKey: string | symbol,
  parameterIndex: number
) {
  let existingRequiredParameters: number[] =
    Reflect.getOwnMetadata(requiredMetadataKey, target, propertyKey) || [];
  existingRequiredParameters.push(parameterIndex);
  Reflect.defineMetadata(
    requiredMetadataKey,
    existingRequiredParameters,
    target,
    propertyKey
  );
}

function validate(
  target: any,
  propertyName: string,
  descriptor: TypedPropertyDescriptor<Function>
) {
  let method = descriptor.value;
  descriptor.value = function() {
    let requiredParameters: number[] = Reflect.getOwnMetadata(
      requiredMetadataKey,
      target,
      propertyName
    );
    if (requiredParameters) {
      for (let parameterIndex of requiredParameters) {
        if (
          parameterIndex >= arguments.length ||
          arguments[parameterIndex] === undefined
        ) {
          throw new Error("Missing required argument.");
        }
      }
    }

    return method.apply(this, arguments);
  };
}
```

`@required`装饰器添加了一个元数据实体，并将其标记为必需参数。然后`@validate`装饰器将现有的`greet`方法包装在一个函数中，该函数在调用原方法之前会先验证参数。

*注意，以上示例用到了`reflect-metadata`库，查看[元数据](#元数据)以了解更多信息。*



##### **元数据**

前面的一些示例中使用了`reflect-metadata`库，以支持[实验性的元数据API](https://github.com/rbuckton/ReflectDecorators)。该库尚未成为ECMAScript（JavaScript）标准的一部分。但是，一旦装饰器被正式采纳为ECMAScript标准的一部分，这些扩展将被提议采用。

可以通过*npm*安装这个库：

```
npm i reflect-metadata --save
```

TypeScript支持为带有装饰器的声明生成元数据。但需要在命令行或`tsconfig.json`里启用`emitDecoratorMetadata`编译选项。

命令行中：

```
tsc --target ES5 --experimentalDecorators --emitDecoratorMetadata
```

tsconfig.json：

```
{
  "compilerOptions": {
    "target": "ES5",
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

启用后，只要`reflect-metadata`库被引入了，设计阶段添加的类型信息就可以在运行时使用。

如下例所示：

```
import "reflect-metadata";

class Point {
  x: number;
  y: number;
}

class Line {
  private _p0: Point;
  private _p1: Point;

  @validate
  set p0(value: Point) {
    this._p0 = value;
  }
  get p0() {
    return this._p0;
  }

  @validate
  set p1(value: Point) {
    this._p1 = value;
  }
  get p1() {
    return this._p1;
  }
}

function validate<T>(
  target: any,
  propertyKey: string,
  descriptor: TypedPropertyDescriptor<T>
) {
  let set = descriptor.set;
  descriptor.set = function(value: T) {
    let type = Reflect.getMetadata("design:type", target, propertyKey);
    if (!(value instanceof type)) {
      throw new TypeError("Invalid type.");
    }
    set.call(target, value);
  };
}

import "reflect-metadata";

class Point {
    x: number;
    y: number;
}
```

TypeScript编译器可以通过`@Reflect.metadata`装饰器注入设计阶段的类型信息。可以认为其相当于下面的TypeScript：

```
class Line {
  private _p0: Point;
  private _p1: Point;

  @validate
  @Reflect.metadata("design:type", Point)
  set p0(value: Point) {
    this._p0 = value;
  }
  get p0() {
    return this._p0;
  }

  @validate
  @Reflect.metadata("design:type", Point)
  set p1(value: Point) {
    this._p1 = value;
  }
  get p1() {
    return this._p1;
  }
}
```

*注意：装饰器元数据是一项试验性功能，其可能会在将来的版本中发生重大更改。*



### 3.4 全局工具类型（Global Utility Types）

- [介绍](#介绍)
- [Partial](#Partial< T >)
- [Readonly](#Readonly< T >)
- [Record](#Record)
- [Pick](#Pick)
- [Omit](#Omit)
- [Exclude](#Exclude)
- [Extract](#Extract)
- [NonNullable](#NonNullable)
- [Parameters](#Parameters)
- [ConstructorParameters](#ConstructorParameters)
- [ReturnType](#ReturnType)
- [InstanceType](#InstanceType)
- [Required](#Required)
- [ThisParameterType](#ThisParameterType)
- [OmitThisParameter](#OmitThisParameter)
- [ThisType](#ThisType)



#### 介绍

TypeScript提供了一些工具类型，以方便进行常见的类型转换。这些工具类型在全局可用。



#### Partial< T >


构造一个类型，并将`T`的所有属性设置为可选。该工具会返回一个表示指定类型的所有子集的类型。


*示例*

```
interface Todo {
  title: string;
  description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
  return { ...todo, ...fieldsToUpdate };
}

const todo1 = {
  title: "organize desk",
  description: "clear clutter"
};

const todo2 = updateTodo(todo1, {
  description: "throw out trash"
});
```



#### Readonly< T >

构造类型`T`并设置其所有属性都为`readonly`，这意味着无法重新分配所构造类型的属性。

*示例*

```
interface Todo {
  title: string;
}

const todo: Readonly<Todo> = {
  title: "Delete inactive users"
};

todo.title = "Hello"; // Error: cannot reassign a readonly property
```

该工具对于表示在运行时会失败的赋值表达式很有用（即，当尝试[冻结对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)的属性重新赋值时）。

*Object.freeze*

```
function freeze<T>(obj: T): Readonly<T>;
```



#### Record<K,T>

构造具有类型`T`的属性`K`的类型。此工具可用于将类型的属性映射到另一个类型。

*示例*

```
interface PageInfo {
  title: string;
}

type Page = "home" | "about" | "contact";

const x: Record<Page, PageInfo> = {
  about: { title: "about" },
  contact: { title: "contact" },
  home: { title: "home" }
};
```



#### Pick<K,T>

通过从`T`中选取属性`K`来构造一个类型。

*示例*

```
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

const todo: TodoPreview = {
  title: "Clean room",
  completed: false
};
```



#### Omit<K,T>

通过从`T`中选取所有属性，然后删除`K`来构造一个类型。

*示例*

```
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type TodoPreview = Omit<Todo, "description">;

const todo: TodoPreview = {
  title: "Clean room",
  completed: false
};
```



#### Exclude<T,U>

通过从`T`中排除所有可分配给`U`的属性来构造类型。

*示例*

```
type T0 = Exclude<"a" | "b" | "c", "a">; // "b" | "c"
type T1 = Exclude<"a" | "b" | "c", "a" | "b">; // "c"
type T2 = Exclude<string | number | (() => void), Function>; // string | number
```



#### Extract<T,U>

通过从`T`中提取所有可分配给`U`的属性来构造类型。

*示例*

```
type T0 = Extract<"a" | "b" | "c", "a" | "f">; // "a"
type T1 = Extract<string | number | (() => void), Function>; // () => void
```



#### NonNullable< T >

通过从`T`中排除`null`和`undefined`来构造类型。

*示例*

```
type T0 = NonNullable<string | number | undefined>; // string | number
type T1 = NonNullable<string[] | null | undefined>; // string[]
```



#### Parameters< T >

构造函数类型`T`的参数类型的元组类型。

*示例*

```
declare function f1(arg: { a: number; b: string }): void;
type T0 = Parameters<() => string>; // []
type T1 = Parameters<(s: string) => void>; // [string]
type T2 = Parameters<<T>(arg: T) => T>; // [unknown]
type T4 = Parameters<typeof f1>; // [{ a: number, b: string }]
type T5 = Parameters<any>; // unknown[]
type T6 = Parameters<never>; // never
type T7 = Parameters<string>; // Error
type T8 = Parameters<Function>; // Error
```



#### ConstructorParameters< T >

通过`ConstructorParameters<T>`类型，我们可以提取构造函数类型的所有参数类型。它将生成具有所有参数类型的元组类型（如果`<T>`不是函数，则为`never`类型）。

*示例*

```
type T0 = ConstructorParameters<ErrorConstructor>; // [(string | undefined)?]
type T1 = ConstructorParameters<FunctionConstructor>; // string[]
type T2 = ConstructorParameters<RegExpConstructor>; // [string, (string | undefined)?]
```



#### ReturnType< T >

构造一个由函数`<T>`的返回类型组成的类型。

*示例*

```
declare function f1(): { a: number; b: string };
type T0 = ReturnType&glt;() => string>; // string
type T1 = ReturnType&glt;(s: string) => void>; // void
type T2 = ReturnType&glt;&glt;T>() => T>; // {}
type T3 = ReturnType&glt;&glt;T extends U, U extends number[]>() => T>; // number[]
type T4 = ReturnType&glt;typeof f1>; // { a: number, b: string }
type T5 = ReturnType&glt;any>; // any
type T6 = ReturnType&glt;never>; // any
type T7 = ReturnType&glt;string>; // Error
type T8 = ReturnType&glt;Function>; // Error
```



#### InstanceType< T >

构造一个由构造函数`<T>`的实例类型构成的类型。

*示例*

```
class C {
  x = 0;
  y = 0;
}

type T0 = InstanceType<typeof C>; // C
type T1 = InstanceType<any>; // any
type T2 = InstanceType<never>; // any
type T3 = InstanceType<string>; // Error
type T4 = InstanceType<Function>; // Error
```



#### Required< T >

构造一个由`<T>`的所有属性设置为`required`的类型。

*示例*

```
interface Props {
  a?: number;
  b?: string;
}

const obj: Props = { a: 5 }; // OK

const obj2: Required<Props> = { a: 5 }; // Error: property 'b' missing
```



#### ThisParameterType

提取函数类型的`this`参数的类型，如果函数类型没有`this`参数，则提取`unknown`。

注意：仅当启用`--strictFunctionTypes`时，此类型才能正常工作。参阅：[#32964](https://github.com/microsoft/TypeScript/issues/32964)。

*示例*

```
function toHex(this: Number) {
  return this.toString(16);
}

function numberToString(n: ThisParameterType<typeof toHex>) {
  return toHex.apply(n);
}
```



#### OmitThisParameter

从函数类型中删除`this`参数。

注意：仅当启用`--strictFunctionTypes`时，此类型才能正常工作。参阅：[#32964](https://github.com/microsoft/TypeScript/issues/32964)。

*示例*

```
function toHex(this: Number) {
  return this.toString(16);
}

// The return type of `bind` is already using `OmitThisParameter`, this is just for demonstration.
const fiveToHex: OmitThisParameter<typeof toHex> = toHex.bind(5);

console.log(fiveToHex());
```



#### ThisType< T >

该工具不返回转换后的类型。相反，它用作上下文`this`类型的标记。注意，必须启用`--noImplicitThis`标志才能使用此工具。

*示例*

```
// Compile with --noImplicitThis

type ObjectDescriptor<D, M> = {
  data?: D;
  methods?: M & ThisType<D & M>; // Type of 'this' in methods is D & M
};

function makeObject<D, M>(desc: ObjectDescriptor<D, M>): D & M {
  let data: object = desc.data || {};
  let methods: object = desc.methods || {};
  return { ...data, ...methods } as D & M;
}

let obj = makeObject({
  data: { x: 0, y: 0 },
  methods: {
    moveBy(dx: number, dy: number) {
      this.x += dx; // Strongly typed this
      this.y += dy; // Strongly typed this
    }
  }
});

obj.x = 10;
obj.y = 20;
obj.moveBy(5, 5);
```

在上面的示例中，`makeObject`的参数中的`methods`对象有上下文类型，其中包括`ThisType <D＆M>`，因此`methods`对象方法中的`this`类型为`{ x: number, y: number } & { moveBy(dx: number, dy: number): number }`。请注意，`methods`属性的类型如何同时成为推断目标和方法中`this`类型的来源。

`ThisType <T>`标记接口只是在`lib.d.ts`中声明的一个空接口。除了在对象字面量的上下文类型中识别外，该接口的作用类似于任何空接口。



### 3.5 迭代器和生成器（Iterators and Generators）

- [`for..of`语句](#`for..of`语句)
- [`for..of`与`for..in`语句](#`for..of`与`for..in`语句)
- [代码生成](#代码生成)

#### 可迭代性

当一个对象实现了[`Symbol.iterator`](#`Symbol.iterator`)属性时。一些内置类型，像：`Array`、`Map`、`Set`、`String`、`Int32Array`、`Uint32Array`等就都已实现了自己的`Symbol.iterator`属性。对象上的`Symbol.iterator`函数负责返回要迭代的值列表。



##### **for..of语句**

`for..of`循环访问可迭代对象，并在该对象上调用`Symbol.iterator`属性。以下是数组的一个简单的`for..of`循环：

```
let someArray = [1, "string", false];

for (let entry of someArray) {
  console.log(entry); // 1, "string", false
}
```



##### **for..of与for..in语句**

`for..of`与`for..in`均可返回一可迭代列表，但迭代的值确不同：`for..in`迭代对象的*键*列表，而`for..of`则会迭代键所对应的*值*列表。

以下示例展示了两者间的区别：

```
let list = [4, 5, 6];

for (let i in list) {
  console.log(i); // "0", "1", "2",
}

for (let i of list) {
  console.log(i); // "4", "5", "6"
}
```

另一个区别是`for..in`可以对任何对象操作，它做为检查对象属性的一种方法。而`for..of`主要关注可迭代对象的值。像`Map`和`Set`之类的内置对象实现了`Symbol.iterator`属性，允许所访问存储的值。

```
let pets = new Set(["Cat", "Dog", "Hamster"]);
pets["species"] = "mammals";

for (let pet in pets) {
  console.log(pet); // "species"
}

for (let pet of pets) {
  console.log(pet); // "Cat", "Dog", "Hamster"
}
```



##### **代码生成**

**ES5及ES3为生成目标**

为以ES5或ES3为兼容目标时，仅允许对`Array`类型的值使用迭代器。在非数组值上使用`for..of`循环是错误的，即使这些非数组值实现了`Symbol.iterator`属性。

编译器会将`for..of`循环生成一个简单的`for`循环，例如：

```
let numbers = [1, 2, 3];
for (let num of numbers) {
  console.log(num);
}
```

会生成：

```
var numbers = [1, 2, 3];
for (var _i = 0; _i < numbers.length; _i++) {
  var num = numbers[_i];
  console.log(num);
}
```

**以ECMAScript 2015及更高版本为生成目标**

以ECMAScipt 2015为兼容目标时，编译器会生成对应引擎中的内置`for..of`循环迭代器。



### 3.6 JSX

- [1. 介绍](#1. 介绍)

- [2. 基本用法](#2. 基本用法)

- [3. `as`操作符](#3. `as`操作符)

- [4. 类型检查](#4. 类型检查)

- - [固有元素]
  - [基于值的元素]
  - [函数组件]
  - [类组件]
  - [属性类型检查]
  - [子类型检查]
- [5. JSX结果类型](#5. JSX结果类型)

- [6. 嵌入表达式](#6. 嵌入表达式)

- [7. React集成](#7. React集成)

- [8. 工厂函数](#8. 工厂函数)

#### 1. 介绍

[JSX](https://facebook.github.io/jsx/)是一种可嵌入的类似XML的语法。其转换的语义跟据特定的实现而定，但应转换为有效的JavaScript。JSX因[React](https://reactjs.org/)框架而流行，但也有其他实现。TypeScript支持内嵌，类型检查以及将JSX直接编译为JavaScript。



#### 2. 基本用法

要使用JSX需要做两件事：

1. 对文件使用`.tsx`扩展名
2. 启用`jsx`选项

TypeScript有三种JSX模式：`preserve`、`react`、和`react-native`。这些模式仅在代码生成阶段起作用-类型检查不受影响。`preserve`模式下生成的代码会将JSX保留为输出的一部分，以供其它转换步骤（如：[Babel](https://babeljs.io/)）进一步使用。另外，输出文件会有`.jsx`扩展名。`react`模式会生成`React.createElement`，在使用之前不需要经过JSX转换，并且输出文件使用`.js`扩展名。`react-native`模式等效于`preserve`，因为它保留了所有JSX，但是输出文件扩展名是`.js`。

| 模式           | 输入      | 输出                         | 输出文件扩展名 |
| :------------- | :-------- | :--------------------------- | :------------- |
| `preserve`     | `<div />` | `<div />`                    | `.jsx`         |
| `react`        | `<div />` | `React.createElement("div")` | `.js`          |
| `react-native` | `<div />` | `<div />`                    | `.js`          |

可以在命令行中通过`--jsx`标志，或通过[tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)中的选项设置要使用的模式。

**注意：可以使用`--jsxFactory`选项指定在目标React JSX生成时要使用的JSX工厂函数（默认为：`React.createElement`）*



#### 3. `as`操作符

回顾一个怎么写类型断言：

```
var foo = <foo>bar;
```

这断言变量`bar`的类型为`foo`。由于TypeScript还使用尖括号来声明类型，因此将其与JSX的语法结合使用会带来一定的解析困难。因此，TypeScript不允许在`.tsx`文件中使用尖括号类型声明。

由于上述语法不能在`.tsx`文件中使用，因此应使用另一个类型断言运算符：`as`。该示例可以很容易地用`as`运算符重写。

```
var foo = bar as foo;
```

`as`操作符在`.ts`和`.tsx`文件中都可用，并且与尖括号类型断言方式是等价的。



#### 4. 类型检查

为了理解JSX的类型检查，必须首先了解*固有元素*和*基于值的元素*之间的区别。假设有一个JSX表达式`<expr />`，`expr`可以引用环境自带的内容（如，DOM环境中的`div`或`span`），也可以引用自定义组件。这很重要，原因有如下两点：

1. 对于React，固有元素会以字符串的形式生成（`React.createElement("div")`），而自定义组件却不是（`React.createElement(MyComponent)`）。
2. 在JSX元素中传入的属性类型应以不同的方式查找。固有元素属性本就是已知的，而自定义组件会自已指定其属性集。

TypeScript使用与[React相同的规范](http://facebook.github.io/react/docs/jsx-in-depth.html#html-tags-vs.-react-components)来区分这些。固有元素总是以小写字母开头，而基于值的元素总是以大写字母开头。



##### **固有元素**

固有元素使用特殊接口`JSX.IntrinsicElements`上查找。默认情况下，如果未指定此接口会全部通过，并且不会对内部元素进行类型检查。但是，如果存在此接口，则固有元素的名称要在`JSX.IntrinsicElements`接口的属性上来查找。例如：

```
declare namespace JSX {
  interface IntrinsicElements {
    foo: any
  }
}

<foo />; // ok
<bar />; // error
```

以上示例中，`<foo />`工作正常，而`<bar />`会报错。因为它没有在`JSX.IntrinsicElements`中指定。

*注意：也可以在`JSX.IntrinsicElements`上指定一个用于捕获所有字符串索引：*

```
declare namespace JSX {
  interface IntrinsicElements {
    [elemName: string]: any;
  }
}
```



##### **基于值的元素**

基于值的元素会简单的在它所在的作用域里按标识符查找。

```
import MyComponent from "./myComponent";

<MyComponent />; // ok
<SomeOtherComponent />; // error
```

可以通过两种方式定义基于值的元素：

1. 函数组件(FC)
2. 类组件

由于这两种类型的基于值的元素在JSX表达式中无法区分，因此TS会首先尝试使用重载解析将表达式解析为函数组件。如果解析成功，那么TS就完成了表达式到其声明的解析操作。如果该值无法解析为函数组件，那么TS将尝试将其解析为类组件。如果失败，TS会报告错误。



##### **函数组件**

顾名思义，该组件被定义为JavaScript函数，其第一个参数是`props`对象。TypeScript会强制要求其返回类型可赋值给`JSX.Element`。

```
interface FooProp {
  name: string;
  X: number;
  Y: number;
}

declare function AnotherComponent(prop: {name: string});
function ComponentFoo(prop: FooProp) {
  return <AnotherComponent name={prop.name} />;
}

const Button = (prop: {value: string}, context: { color: string }) => <button>
```

因为函数组件只是一个JavaScript函数，所以这里也可以使用函数重载：

```
interface ClickableProps {
  children: JSX.Element[] | JSX.Element
}

interface HomeProps extends ClickableProps {
  home: JSX.Element;
}

interface SideProps extends ClickableProps {
  side: JSX.Element | string;
}

function MainButton(prop: HomeProps): JSX.Element;
function MainButton(prop: SideProps): JSX.Element {
  ...
}
```

*注意：函数组件以前称为无状态功能组件（SFC）。由于在最新版本的React中不再将函数组件视为无状态，因此不建议使用SFC类型及其别名`StatelessComponent`*



##### **类组件**

可以定义类组件的类型。但是，需要首先理解两个新术语：*元素类类型*和*元素实例类型*。

现有`<Expr />`，*元素类类型*为`Expr`的类型。因此，在上面的示例中，如果`MyComponent`是ES6类，则类类型就是该类的构造函数和静态成员。如果`MyComponent`是工厂函数，则类类型将是该函数。

一旦建立类类型，实例类型由类类型的构造函数或调用签名（以存在者为准）的返回类型的并集来确定。同样，在ES6类的情况下，实例类型会是该类的实例的类型，如果是工厂函数，实例类型会是函数返回值的类型。

```
class MyComponent {
  render() {}
}

// use a construct signature
var myComponent = new MyComponent();

// element class type => MyComponent
// element instance type => { render: () => void }

function MyFactoryFunction() {
  return {
    render: () => {
    }
  }
}

// use a call signature
var myComponent = MyFactoryFunction();

// element class type => MyFactoryFunction
// element instance type => { render: () => void }
```

元素实例类型很有趣，因为它必须可赋值给`JSX.ElementClass`，否则会抛出错误。默认情况下，`JSX.ElementClass`是`{}`，但可以对其进行扩展以限制JSX使其符合正确的接口类型。

```
declare namespace JSX {
  interface ElementClass {
    render: any;
  }
}

class MyComponent {
  render() {}
}
function MyFactoryFunction() {
  return { render: () => {} }
}

<MyComponent />; // ok
<MyFactoryFunction />; // ok

class NotAValidComponent {}
function NotAValidFactoryFunction() {
  return {};
}

<NotAValidComponent />; // error
<NotAValidFactoryFunction />; // error
```



##### **属性类型检查**

属性类型检查的第一步是确定*元素属性的类型*，固有元素和基于值的元素之间略有不同。

对于固有元素，其是`JSX.IntrinsicElements`属性的类型。

```
declare namespace JSX {
  interface IntrinsicElements {
    foo: { bar?: boolean }
  }
}

// element attributes type for 'foo' is '{bar?: boolean}'
<foo bar />;
```

对于基于值的元素，要稍微复杂一些。它由先前确定的元素实例类型上的属性的类型确定。使用哪个属性由`JSX.ElementAttributesProperty`确定。应该用单一属性来声明，然后使用该属性的名称。从TypeScript 2.8开始，如果未提供`JSX.ElementAttributesProperty`，则将改用类元素的构造函数或函数调用的第一个参数的类型。

```
declare namespace JSX {
  interface ElementAttributesProperty {
    props; // specify the property name to use
  }
}

class MyComponent {
  // specify the property on the element instance type
  props: {
    foo?: string;
  }
}

// element attributes type for 'MyComponent' is '{foo?: string}'
<MyComponent foo="bar" />
```

元素属性类型用于对JSX中的属性进行类型检查。支持可选属性和必需属性。

```
declare namespace JSX {
  interface IntrinsicElements {
    foo: { requiredProp: string; optionalProp?: number }
  }
}

<foo requiredProp="bar" />; // ok
<foo requiredProp="bar" optionalProp={0} />; // ok
<foo />; // error, requiredProp is missing
<foo requiredProp={0} />; // error, requiredProp should be a string
<foo requiredProp="bar" unknownProp />; // error, unknownProp does not exist
<foo requiredProp="bar" some-unknown-prop />; // ok, because 'some-unknown-prop' is not a valid identifier
```

*注意：如果一个属性名不是合法的JS标识符（如：`data-\*`属性），并且它没出现在元素属性类型中时就不会当做一个错误。*

另外，`JSX.IntrinsicAttributes`接口可用于指定JSX框架使用的额外属性，这些属性通常不会被组件的*props*或*arguments*使用，如：React中的`key`。还有，`JSX.IntrinsicClassAttributes <T<`泛型类型也可用于类组件（而非函数组件）以指定相同类型的额外属性。在这种类型中，泛型参数表示类实例类型。在React中，这用于允许`Ref <T>`类型的`ref`属性。通常，这些接口上的所有属性都应该是可选的，除非你想让用户在JSX框架的每个标签上提供一些属性。

展开操作符也可以使用：

```
var props = { requiredProp: "bar" };
<foo {...props} />; // ok

var badProps = {};
<foo {...badProps} />; // error
```



##### **子类型检查**

在TypeScript 2.3中，TS引入了*children*类型检查。*children*是*元素属性(attribute)类型*中的特殊属性(property)，其中子`JSXExpressions`被视为插入到*attribute*中。与TS使用`JSX.ElementAttributesProperty`确定道具名称的方式类似，TS使用`JSX.ElementChildrenAttribute`确定这些*props*中*children*的名称。`JSX.ElementChildrenAttribute`应该使用单一属性声明。

```
declare namespace JSX {
  interface ElementChildrenAttribute {
    children: {};  // specify children name to use
  }
}
<div>
  <h1>Hello</h1>
</div>;

<div>
  <h1>Hello</h1>
  World
</div>;

const CustomComp = (props) => <div>{props.children}</div>
<CustomComp>
  <div>Hello World</div>
  {"This is just a JS expression..." + 1000}
</CustomComp>
```

可以像其它属性一样指定*children*的类型，这会覆盖默认类型，如：使用的[React类型](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/react)。

```
interface PropsType {
  children: JSX.Element
  name: string
}

class Component extends React.Component<PropsType, {}> {
  render() {
    return (
      <h2>
        {this.props.children}
      </h2>
    )
  }
}

// OK
<Component name="foo">
  <h1>Hello World</h1>
</Component>

// Error: children is of type JSX.Element not array of JSX.Element
<Component name="bar">
  <h1>Hello World</h1>
  <h2>Hello World</h2>
</Component>

// Error: children is of type JSX.Element not array of JSX.Element or string.
<Component name="baz">
  <h1>Hello</h1>
  World
</Component>
```



#### 5. JSX结果类型

默认情况下，JSX表达式的结果类型为`any`。可以通过指定`JSX.Element`接口来自定义类型。但是，无法从此接口检索关于JSX的元素、属性或子元素的类型信息。它是一个黑盒子。



#### 6. 嵌入表达式

JSX允许使用大括号（`{}`）将表达式内嵌在标签中。

```
var a = <div>
  {["foo", "bar"].map(i => <span>{i / 2}</span>)}
</div>
```

上面的代码会导致错误，因为无法用字符串来除以数字。使用`preserve`选项时，输出如下所示：

```
var a = <div>
    {['foo', 'bar'].map(function (i) { return <span>{i / 2}</span>; })}
</div>
```



#### 7. React集成

要将JSX与React一起使用，则应该使用[React类型](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/react)。这些类型定义了适用于React的`JSX`名称空间。

```
/// <reference path="react.d.ts" />

interface Props {
  foo: string;
}

class MyComponent extends React.Component<Props, {}> {
  render() {
    return <span>{this.props.foo}</span>
  }
}

<MyComponent foo="bar" />; // ok
<MyComponent foo={0} />; // error
```



#### 8. 工厂函数

`jsx: react`编译选项使用的工厂函数是可配置的。可以使用`jsxFactory`命令行选项或内联`@jsx`注释指令对每个文件进行设置。例如，如果将`jsxFactory`设置为`createElement`，则`<div />`使用`createElement("div")`createElement（“ div”）来生成，而不是`React.createElement("div")`。

注释编译指令可以像下面这样使用（在TypeScript 2.8中）：

```
import preact = require("preact");
/* @jsx preact.h */
const x = <div />;
```

生成为：

```
const preact = require("preact");
const x = preact.h("div", null);
```

工厂函数的选择也会影响到在返回全局`JSX`命名空间前，在其中查找`JSX`命名空间的位置（用于类型检查信息）。如果工厂函数定义为`React.createElement`（默认），则编译器将在检查全局`JSX`之前检查`React.JSX`。如果工厂函数定义为`h`，则会在全局`JSX`之前检查`h.JSX`。



### 3.7 Mixins

- [1. 介绍](#1. 介绍)
- [2. 混合示例](#2. 混合示例)
- [3. 理解示例](#3. 理解示例)

#### 1. 介绍

除传统的面向对象继承方式，还有流行一种从可重用组件构建类的方式，也就是是通过组合部分简单的类来构建。如果你了解Scala之类的语言的，那可能对*mixin*及其特性已经很熟悉，该模式在JavaScript中也很流行。



#### 2. 混合示例

下面的代码中演示了如何在TypeScript中使用混合。之后我们还会分析其工作方式。

```
// Disposable Mixin
class Disposable {
  isDisposed: boolean;
  dispose() {
    this.isDisposed = true;
  }
}

// Activatable Mixin
class Activatable {
  isActive: boolean;
  activate() {
    this.isActive = true;
  }
  deactivate() {
    this.isActive = false;
  }
}

class SmartObject {
  constructor() {
    setInterval(
      () => console.log(this.isActive + " : " + this.isDisposed),
      500
    );
  }

  interact() {
    this.activate();
  }
}

interface SmartObject extends Disposable, Activatable {}
applyMixins(SmartObject, [Disposable, Activatable]);

let smartObj = new SmartObject();
setTimeout(() => smartObj.interact(), 1000);

////////////////////////////////////////
// In your runtime library somewhere
////////////////////////////////////////

function applyMixins(derivedCtor: any, baseCtors: any[]) {
  baseCtors.forEach(baseCtor => {
    Object.getOwnPropertyNames(baseCtor.prototype).forEach(name => {
      Object.defineProperty(
        derivedCtor.prototype,
        name,
        Object.getOwnPropertyDescriptor(baseCtor.prototype, name)
      );
    });
  });
}
```



#### 3. 理解示例

上面的代码中代码中首先定义了两个，mixins将从这两个类开始。可以看到每个类都只定义了特定的行为或功能。稍后，我们会将它们混合在一起，以形成两种功能的新类。

```
// Disposable Mixin
class Disposable {
  isDisposed: boolean;
  dispose() {
    this.isDisposed = true;
  }
}

// Activatable Mixin
class Activatable {
  isActive: boolean;
  activate() {
    this.isActive = true;
  }
  deactivate() {
    this.isActive = false;
  }
}
```

接下来，我们将创建用于处理这两个mixin组合的类。我们来看一下它是如何做到的：

```
class SmartObject {
    ...
}

interface SmartObject extends Disposable, Activatable {}
```

以上你首先可能会注意到，我们没有在`SmartObject`类中扩展`Disposable`和`Activatable`，而是在`SmartObject`接口中对其进行了扩展。由于[声明合并](#声明合并)，`SmartObject`接口将混合到`SmartObject`类中。

这会将类视为接口，并且仅将`Disposable`和`Activatable`后面的类型混合到`SmartObject`类型，而不是实现中。这意味着我们必须在类上提供实现。除此之外，这正是我们使用mixins所要避免的。

最终，我们将mixins混合到类实现中。

```
applyMixins(SmartObject, [Disposable, Activatable]);
```

最后，我们创建一个辅助函数，它将帮我们进行混合操作。它遍历每个mixin的属性，并将它们复制到mixin的目标，并用其实现填充相应属性。

```
function applyMixins(derivedCtor: any, baseCtors: any[]) {
  baseCtors.forEach(baseCtor => {
    Object.getOwnPropertyNames(baseCtor.prototype).forEach(name => {
      Object.defineProperty(
        derivedCtor.prototype,
        name,
        Object.getOwnPropertyDescriptor(baseCtor.prototype, name)
      );
    });
  });
}
```



### 3.8 模块（Modules）

- [1. 介绍](#1. 介绍)

- [2. 导出](#2. 导出)

- - [导出声明]
  - [导出语句]
  - [重新导出]

- [3. 导入](#3. 导入)

- [4. 默认导出](#4. 默认导出)

- [5. `export =`和`export = require()`](#5. `export =`和`export = require()`)

- [6. 模块代码生成](#6. 模块代码生成)

- [7. 简单示例](#7. 简单示例)

- [8. 可选模块加载及其他高级加载方案](#8. 可选模块加载及其他高级加载方案)

- [9. 使用其他JavaScript库](#9. 使用其他JavaScript库)

- - [外部模块]
  - [外部模块简写]
  - [模块声明的通配符]
  - [UMD模块]

- [10. 结构化模块指南](#10. 结构化模块指南)

- - [尽可能在顶层导出]
  - [使用重导入来扩展]
  - [不要在模块中使用命名空间]
  - [危险信号]

#### 1. 介绍

自ECMAScript 2015开始，JavaScript有了模块的概念，TypeScript也延用这一概念。

模块在其自已的作用域内执行，而不是在全局作用域；这意味着在模块中声明的变量、函数、类等在模块外部不可见，除非使用[`export`形式](#`export`形式)之一将其显式导出。相反，要使用从不同模块导出的变量、函数、类、接口等，则必须使用[`import`形式](#`import`形式)之一将其导入。

模块是声明性的；模块之间的关系是根据文件级别的导入和导出指定的。

模块使用模块加载器导入其它模块。在运行时，模块加载器负责在执行模块之前查找并执行模块所有的依赖关系。在JavaScript中我们所熟知的模块加载器有，Node.js中使用的[CommonJS](https://en.wikipedia.org/wiki/CommonJS)模块加载器和用于Web应用的[RequireJS](http://requirejs.org/)中使用的[AMD](https://github.com/amdjs/amdjs-api/blob/master/AMD.md)模块加载器。

在TypeScript中与ECMAScript 2015中一样，任何包含顶级`import`或`export`的文件都被视为模块。相反，如果没有顶级`import`或`export`声明的文件将被视为脚本，其内容可以在全局范围内使用（因此也可用于模块）。



#### 2. 导出

##### **导出声明**

任何声明都可以通过添加`export`关键字来导出（如变量、函数、类、类型别名或接口）。

*StringValidator.ts*

```
export interface StringValidator {
  isAcceptable(s: string): boolean;
}
```

*ZipCodeValidator.ts*

```
import { StringValidator } from "./StringValidator";

export const numberRegexp = /^[0-9]+$/;

export class ZipCodeValidator implements StringValidator {
  isAcceptable(s: string) {
    return s.length === 5 && numberRegexp.test(s);
  }
}
```



##### **导出语句**

当需要为使用者重命名导出时，导出语句很方便，因此上面的示例可以写成：

```
class ZipCodeValidator implements StringValidator {
  isAcceptable(s: string) {
    return s.length === 5 && numberRegexp.test(s);
  }
}
export { ZipCodeValidator };
export { ZipCodeValidator as mainValidator };
```



##### **重新导出**

模块也会扩展其他模块，并导出该模块的部分功能。重新导出不会将其导入本地，也不会引入局部变量。

*ParseIntBasedZipCodeValidator.ts*

```
export class ParseIntBasedZipCodeValidator {
  isAcceptable(s: string) {
    return s.length === 5 && parseInt(s).toString() === s;
  }
}

// Export original validator but rename it
export {ZipCodeValidator as RegExpBasedZipCodeValidator} from "./ZipCodeValidator";
```

可选的，模块可以包装一个或多个模块，并使用`export * from "module"`组合所有导出。

*AllValidators.ts*

```
export * from "./StringValidator"; // exports 'StringValidator' interface
export * from "./ZipCodeValidator";  // exports 'ZipCodeValidator' and const 'numberRegexp' class
export * from "./ParseIntBasedZipCodeValidator"; //  exports the 'ParseIntBasedZipCodeValidator' class
                                                 // and re-exports 'RegExpBasedZipCodeValidator' as alias
                                                 // of the 'ZipCodeValidator' class from 'ZipCodeValidator.ts'
                                                 // module.
```



#### 3. 导入

从模块导入操作与导出一样简单。使用以下`import`方式之一，导入其它模块的导出内容：

**从模块导入某个导出内容：**

```
import { ZipCodeValidator } from "./ZipCodeValidator";

let myValidator = new ZipCodeValidator();
```

导入时还可以重命名：

```
import { ZipCodeValidator as ZCV } from "./ZipCodeValidator";
let myValidator = new ZCV();
```

**将整个模块导入单个变量，并使用它来访问模块导出：**

```
import * as validator from "./ZipCodeValidator";
let myValidator = new validator.ZipCodeValidator();
```

**有副作用的导入**

虽然不推荐这么做，但某些模块会设置一些可由其他模块使用的全局状态。这些模块可能没有任何导出，或者用户并不关注其导出。要导入这些模块，请使用：

```
import "./my-module.js";
```

**导入类型**

在TypeScript 3.8之前，可以用`import`导入类型。而TypeScript 3.8，可以用`import`语句或`import type`导入类型。

```
// Re-using the same import
import {APIResponseType} from "./api";

// Explicitly use import type
import type {APIResponseType} from "./api";
```



#### 4. 默认导出

每个模块都可以使用`default`导出。默认导出通过`default`关键字标记。每个模块只能有一个`default`导出。需要使用特殊的导入形式来导入`default`导出。

`default`导出很方便。例如，像jQuery之类的库就有`jQuery`或`$`形式的默认导出，并且我也可以用同样的`jQuery`或`$`名称来导入。

*JQuery.d.ts*

```
declare let $: JQuery;
export default $;
```

*App.ts*

```
import $ from "jquery";

$("button.continue").html( "Next Step..." );
```

类和函数声明可以直接被标记为默认导出。标记为默认导出的类和函数的可以省略名称。

*ZipCodeValidator.ts*

```
export default class ZipCodeValidator {
  static numberRegexp = /^[0-9]+$/;
  isAcceptable(s: string) {
    return s.length === 5 && ZipCodeValidator.numberRegexp.test(s);
  }
}
```

*Test.ts*

```
import validator from "./ZipCodeValidator";

let myValidator = new validator();
```

或

*StaticZipCodeValidator.ts*

```
const numberRegexp = /^[0-9]+$/;

export default function (s: string) {
  return s.length === 5 && numberRegexp.test(s);
}
```

*Test.ts*

```
import validate from "./StaticZipCodeValidator";

let strings = ["Hello", "98052", "101"];

// Use function validate
strings.forEach(s => {
  console.log(`"${s}" ${validate(s) ? "matches" : "does not match"}`);
});
```

`default`导出也可以只有值。

*OneTwoThree.ts*

```
export default "123";
```

*Log.ts*

```
import num from "./OneTwoThree";

console.log(num); // "123"
Export all as x #
```

**Export all as x**

有TypeScript 3.8中，可以使用`export * as ns`作为导出重命名的简写：

```
export * as utilities from "./utilities";
```

这将获取模块中所有的依赖项，并使其成为导出字段，然后可以像这样导入它：

```
import { utilities } from "./index";
```



#### 5. export =和export = require()

CommonJS和AMD通常都有一个`exports`对象，其中会包含模块的所有导出。

它们还支持使用一个*自定义对象*来替换`exports`。这类似于默认导出，但是，两者是不兼容的。TypeScript支持`export =`导出，以支持传统的CommonJS和AMD工作流程。

`export =`语法定义了一个模块导出对象。其可以是类、接口、命名空间、函数或枚举。

使用`export =`导出模块时，必须用TypeScript特定的`import module = require("module")`来导入模块。

*ZipCodeValidator.ts*

```
let numberRegexp = /^[0-9]+$/;
class ZipCodeValidator {
  isAcceptable(s: string) {
    return s.length === 5 && numberRegexp.test(s);
  }
}
export = ZipCodeValidator;
```

*Test.ts*

```
import zip = require("./ZipCodeValidator");

// Some samples to try
let strings = ["Hello", "98052", "101"];

// Validators to use
let validator = new zip();

// Show whether each string passed each validator
strings.forEach(s => {
  console.log(`"${ s }" - ${ validator.isAcceptable(s) ? "matches" : "does not match" }`);
});
```



#### 6. 模块代码生成

根据编译期间指定的模块目标，编译器会为Node.js（[CommonJS](http://wiki.commonjs.org/wiki/CommonJS)）、require.js（[AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)）、[UMD](https://github.com/umdjs/umd)、[SystemJS](https://github.com/systemjs/systemjs)或[ECMAScript 2015原生模块](http://www.ecma-international.org/ecma-262/6.0/#sec-modules)（ES6）的模块加载系统生成适合的代码。关于在生成的代码中执行`define`、`require`和`register`调用的详细信息，请查阅每个模块加载器的文档。

以下简单示例展示了导入和导出过程中使用的名称如何转换为模块加载代码。

*SimpleModule.ts*

```
import m = require("mod");
export let t = m.something + 1;
```

*AMD / RequireJS SimpleModule.js*

```
define(["require", "exports", "./mod"], function (require, exports, mod_1) {
  exports.t = mod_1.something + 1;
});
```

*CommonJS / Node SimpleModule.js*

```
var mod_1 = require("./mod");
exports.t = mod_1.something + 1;
```

*UMD SimpleModule.js*

```
(function(factory) {
  if (typeof module === "object" && typeof module.exports === "object") {
    var v = factory(require, exports);
    if (v !== undefined) module.exports = v;
  } else if (typeof define === "function" && define.amd) {
    define(["require", "exports", "./mod"], factory);
  }
})(function(require, exports) {
  var mod_1 = require("./mod");
  exports.t = mod_1.something + 1;
});
```

*System SimpleModule.js*

```
System.register(["./mod"], function(exports_1) {
  var mod_1;
  var t;
  return {
    setters: [
      function(mod_1_1) {
        mod_1 = mod_1_1;
      }
    ],
    execute: function() {
      exports_1("t", (t = mod_1.something + 1));
    }
  };
});
```

*原生 ECMAScript 2015 模块 SimpleModule.js*

```
import { something } from "./mod";
export var t = something + 1;
```



#### 7. 简单示例

下面我们整理前面示例中Validator的实现，每个模块中只有一个命名导出。

要进行编译，就必须在命令行上指定模块目标。对于Node.js，使用`--module commonjs`；对于require.js，应使用`--module amd`。例如：

```
tsc --module commonjs Test.ts
```

编译完成后，每个模块会生成一个单独的`.js`文件。就像用*reference*标签，编译器会根据`import`来编译相关文件。

*Validation.ts*

```
export interface StringValidator {
  isAcceptable(s: string): boolean;
}
```

*LettersOnlyValidator.ts*

```
import { StringValidator } from "./Validation";

const lettersRegexp = /^[A-Za-z]+$/;

export class LettersOnlyValidator implements StringValidator {
  isAcceptable(s: string) {
    return lettersRegexp.test(s);
  }
}
```

*ZipCodeValidator.ts*

```
import { StringValidator } from "./Validation";

const numberRegexp = /^[0-9]+$/;

export class ZipCodeValidator implements StringValidator {
  isAcceptable(s: string) {
    return s.length === 5 && numberRegexp.test(s);
  }
}
```

*Test.ts*

```
import { StringValidator } from "./Validation";
import { ZipCodeValidator } from "./ZipCodeValidator";
import { LettersOnlyValidator } from "./LettersOnlyValidator";

// Some samples to try
let strings = ["Hello", "98052", "101"];

// Validators to use
let validators: { [s: string]: StringValidator } = {};
validators["ZIP code"] = new ZipCodeValidator();
validators["Letters only"] = new LettersOnlyValidator();

// Show whether each string passed each validator
strings.forEach(s => {
  for (let name in validators) {
    console.log(
      `"${s}" - ${
        validators[name].isAcceptable(s) ? "matches" : "does not match"
      } ${name}`
    );
  }
});
```



#### 8. 可选模块加载及其他高级加载方案

有时，你可能只想在某些情况下加载模块。在TypeScript中，我们可以使用下面显示的模式来实现此加载方案和其他高级加载方案，以直接调用模块加载器并且可以保证类型安全。

编译器检测每个模块是否在所生成的JavaScript中引用了。如果模块标识符仅用作类型注释的一部分，而从未用作表达式，则不会生成该模块的`require`调用。省略未使用的引用是一个很好的性能优化，并且还允许可选地加载这些模块。

这种模式的核心思想是`import id = require("...")`可以让我们访问模块的导出类型。模块加载器会被动态调用（通过`require`），如下面的`if`块所示。这利用了省略引用优化，因此仅在需要时才加载模块。为使此模式正常工作，一定要注意通过`import`定义的标识符只能在表示类型位置使用（即，不能在会生成JavaScript的位置使用）。

为了保持类型安全，我们可以使用`typeof`关键字。当在表示类型的位置使用`typeof`关键字时，会得到一个类型的值，这种情况下表示模块的类型。

*示例：Node.js中的动态模块加载*

```
declare function require(moduleName: string): any;

import { ZipCodeValidator as Zip } from "./ZipCodeValidator";

if (needZipValidation) {
  let ZipCodeValidator: typeof Zip = require("./ZipCodeValidator");
  let validator = new ZipCodeValidator();
  if (validator.isAcceptable("...")) {
    /* ... */
  }
}
```

*示例：require.js中的动态模块加载*

```
declare function require(
  moduleNames: string[],
  onLoad: (...args: any[]) => void
): void;

import * as Zip from "./ZipCodeValidator";

if (needZipValidation) {
  require(["./ZipCodeValidator"], (ZipCodeValidator: typeof Zip) => {
    let validator = new ZipCodeValidator.ZipCodeValidator();
    if (validator.isAcceptable("...")) {
      /* ... */
    }
  });
}
```

*示例：System.js中的动态模块加载*

```
declare const System: any;

import { ZipCodeValidator as Zip } from "./ZipCodeValidator";

if (needZipValidation) {
  System.import("./ZipCodeValidator").then((ZipCodeValidator: typeof Zip) => {
    var x = new ZipCodeValidator();
    if (x.isAcceptable("...")) {
      /* ... */
    }
  });
}
```



#### 9. 使用其他JavaScript库

为了描述非TypeScript编写的库的特征，我们需要声明该库公开的API。

我们称它为声明是因为它不是“外部程序”的实现。通常，这些文件在`.d.ts`文件中定义。如果你熟悉C/C ++，就可以将它们视为`.h`文件。我们来看几个示例。

##### **外部模块**

在Node.js中，大多数任务是通过加载一个或多个模块来完成的。我们可以使用顶级`export`声明在自己的`.d.ts`文件中定义每个模块，但是将它们编写为一个更大的`.d.ts`文件会更加方便。为此，我们使用构造一个类似外部命名空间的方法，但是使用`module`关键字和将模块的名称进行引用，这些之后在`import`中使用。例如：

*node.d.ts(摘要)*

```
declare module "url" {
  export interface Url {
    protocol?: string;
    hostname?: string;
    pathname?: string;
  }

  export function parse(
    urlStr: string,
    parseQueryString?,
    slashesDenoteHost?
  ): Url;
}

declare module "path" {
  export function normalize(p: string): string;
  export function join(...paths: any[]): string;
  export var sep: string;
}
```

现在，我们可以`/// <reference> node.d.ts`，然后可以通过`import url = require("url");`或`import * as URL from "url"`来加载模块。

```
/// <eference path="node.d.ts"/>
import * as URL from "url";
let myUrl = URL.parse("http://www.itbilu.com");
```



##### **外部模块简写**

如果不想在使用模块前花时间编写模块声明，则可以简写声明以便快速使用。

*declarations.d.ts*

```
declare module "hot-new-module";
```

简写模块里的所有导出，将会是`any`类型。

```
import x, {y} from "hot-new-module";
x(y);
```

##### **模块声明的通配符**

有些模块加载器像[SystemJS](https://github.com/systemjs/systemjs/blob/master/docs/overview.md#plugin-syntax)和[AMD](https://github.com/amdjs/amdjs-api/blob/master/LoaderPlugins.md)允许导出非JavaScript内容。它们通常会使用一个前缀或后缀来表示特殊的加载语法。模块声明通配符可以用来表示这些情况。

```
declare module "*!text" {
  const content: string;
  export default content;
}
// Some do it the other way around.
declare module "json!*" {
  const value: any;
  export default value;
}
```

现在就可以导出`"*!text"`或`"json!*"`所匹配的内容了。

```
import fileContent from "./xyz.txt!text";
import data from "json!http://example.com/data.json";
console.log(data, fileContent);
```

##### **UMD模块**

一些库被设计用于兼容多个模块加载器，或者不用于模块加载（全局变量）。这些被称为[UMD](https://github.com/umdjs/umd)模块，可以通过导入或全局变量访问这些库。例如

*math-lib.d.ts*

```
export function isPrime(x: number): boolean;
export as namespace mathLib;
```

之前这个库可以在其它模块里导入使用：

```
import { isPrime } from "math-lib";
isPrime(2);
mathLib.isPrime(2); // ERROR: can't use the global definition from inside a module
```

它同样可以做为全局变量使用，但只能在某个脚本中（不带导出或导出的脚本）。

```
mathLib.isPrime(2);
```



#### 10. 结构化模块指南

##### **尽可能在顶层导出**

用户使用导出的内容时，应变尽可能易于使用。如果嵌套级别太多往往很麻烦，应仔细考虑如何构造模块。

当你从模块中导出一个命名空间，就是添加了一层嵌套层的示例。虽然命名空间有时也会有用，但在使用模块时它们会增加一个间接的级别。这可能很快成为用户的痛点，并且通常是不必要的。

导出类上的静态方法也有类似的问题-这个类本身就是一层嵌套。除非它能方便表述或易于使用，否则请考虑简单地导出一个辅助函数。

*如果仅导出单个`class`或`function`，使用`export default`*

就像“在顶层上导出”可减少模块使用复杂度一样，引入默认导出也是如此。如果模块的主要目的是导出一个特定的内容，则应考虑将其导出为默认导出。这使得导入和使用都更加容易。例如：

*MyClass.ts*

```
export default class SomeType {
  constructor() { ... }
}
```

*MyFunc.ts*

```
export default function getThing() {
  return "thing";
}
```

*Consumer.ts*

```
import t from "./MyClass";
import f from "./MyFunc";
let x = new t();
console.log(f());
```

这对消费者来说是最理想的。他们可以随心所欲的对类型命名（本例中为`t`），并且无需进行过多的*.*即可找到你的对象

*如果需要导出多个对象，则放到顶层导出中*

*MyThings.ts*

```
export class SomeType {
  /* ... */
}
export function someFunc() {
  /* ... */
}
```

相反的，当导入时：

*明确的列出导入名*

*Consumer.ts*

```
import { SomeType, someFunc } from "./MyThings";
let x = new SomeType();
let y = someFunc();
```

如果要导入大量内容，应使用命名空间导入模式

*MyLargeModule.ts*

```
export class Dog { ... }
export class Cat { ... }
export class Tree { ... }
export class Flower { ... }
```

*Consumer.ts*

```
import * as myLargeModule from "./MyLargeModule.ts";
let x = new myLargeModule.Dog();
```

##### **使用重导入来扩展**

通常，你可能需要扩展模块的功能。JS常见的模式是扩展原始对象，类似于JQuery扩展的工作方式。如前所述，模块不会像全局命名空间对象那样合并。推荐的解决方案是不要改变原始对象，而是导出一个新实体再扩展出新功能。

设想模块`Calculator.ts`中定义了的简单计算器实现。该模块还导出一个辅助函数，并通过传递输入字符串列表的方式，最后再写入结果来测试计算器功能。

*Calculator.ts*

```
export class Calculator {
  private current = 0;
  private memory = 0;
  private operator: string;

  protected processDigit(digit: string, currentValue: number) {
    if (digit >= "0" && digit <= "9") {
      return currentValue * 10 + (digit.charCodeAt(0) - "0".charCodeAt(0));
    }
  }

  protected processOperator(operator: string) {
    if (["+", "-", "*", "/"].indexOf(operator) >= 0) {
      return operator;
    }
  }

  protected evaluateOperator(
    operator: string,
    left: number,
    right: number
  ): number {
    switch (this.operator) {
      case "+":
        return left + right;
      case "-":
        return left - right;
      case "*":
        return left * right;
      case "/":
        return left / right;
    }
  }

  private evaluate() {
    if (this.operator) {
      this.memory = this.evaluateOperator(
        this.operator,
        this.memory,
        this.current
      );
    } else {
      this.memory = this.current;
    }
    this.current = 0;
  }

  public handleChar(char: string) {
    if (char === "=") {
      this.evaluate();
      return;
    } else {
      let value = this.processDigit(char, this.current);
      if (value !== undefined) {
        this.current = value;
        return;
      } else {
        let value = this.processOperator(char);
        if (value !== undefined) {
          this.evaluate();
          this.operator = value;
          return;
        }
      }
    }
    throw new Error(`Unsupported input: '${char}'`);
  }

  public getResult() {
    return this.memory;
  }
}

export function test(c: Calculator, input: string) {
  for (let i = 0; i < input.length; i++) {
    c.handleChar(input[i]);
  }

  console.log(`result of '${input}' is '${c.getResult()}'`);
}
```

下面使用导出的`test`函数来测试计算器。

*TestCalculator.ts*

```
import { Calculator, test } from "./Calculator";


let c = new Calculator();
test(c, "1+2*33/11="); // prints 9
```

现在对其进行扩展，使它支持10进制以外的进制输入。创建`ProgrammerCalculator.ts`。

*ProgrammerCalculator.ts*

```
import { Calculator } from "./Calculator";

class ProgrammerCalculator extends Calculator {
  static digits = [
    "0",
    "1",
    "2",
    "3",
    "4",
    "5",
    "6",
    "7",
    "8",
    "9",
    "A",
    "B",
    "C",
    "D",
    "E",
    "F"
  ];

  constructor(public base: number) {
    super();
    const maxBase = ProgrammerCalculator.digits.length;
    if (base <= 0 || base > maxBase) {
      throw new Error(`base has to be within 0 to ${maxBase} inclusive.`);
    }
  }

  protected processDigit(digit: string, currentValue: number) {
    if (ProgrammerCalculator.digits.indexOf(digit) >= 0) {
      return (
        currentValue * this.base + ProgrammerCalculator.digits.indexOf(digit)
      );
    }
  }
}

// Export the new extended calculator as Calculator
export { ProgrammerCalculator as Calculator };

// Also, export the helper function
export { test } from "./Calculator";
```

新模块`ProgrammerCalculator`导出的API与原来`Calculator`模块类似，但并没有修改原始模块中的任何对象。以下是`ProgrammerCalculator`的测试代码：

*TestProgrammerCalculator.ts*

```
import { Calculator, test } from "./ProgrammerCalculator";

let c = new Calculator(2);
test(c, "001+010="); // prints 3
```



##### **不要在模块中使用命名空间**

初次转为基于模块组织代码时，可能总是会想将导出包装在一层命名空间中。模块具有自己的作用域，并且仅导出的声明才会从模块外部可见。考虑到这一点，命名空间在使用模块时几乎没有价值。

在组织方面，命名空间很方便将全局范围内与逻辑相关的对象和类型组合在一起。例如，在C#中，可以在`System.Collections`中找到所有集合类型。通过将我们的类型组织到有层次的组织到命名空间中，我们为这些类型的使用者提供了用户体验。另一方面，模块必定已存在于文件系统中。我们必须通过路径和文件名来解析它们，因此有一种逻辑上的组织方案可供我们使用。我们可以创建一个`/collections/generic/`目录，并把相应的模块放在其中。

命名空间对于避免在全局范围内命名冲突很重要。例如，可能有`My.Application.Customer.AddForm`和`My.Application.Order.AddForm`–两种名称相同但命名空间不同的类型。但是，对于模块来说确不是问题。在同一个模块中，没有理由对两个对象使用相同的名称。从使用角度来讲，模块使用者可以定义其引用该模块的名称，因此也不可能发生意外的命名冲突。

更多关于模块和命名空间的讨论请参考：[命名空间和模块](#命名空间和模块)。



##### **危险信号**

以下情况可以视为模块结构的危险信号，应仔细检查是否要对外部模块使用命名空间：

- 文件的唯一顶级声明是`export namespace Foo { ... }`（删除`Foo`并将所有内容“上移”一个级别）
- 多个文件的顶层具有相同的`export namespace Foo {`（不要认为它们会合并为一个`Foo`！）



### 3.9 模块解析（Module Resolution）

- [1. 相对 vs. 非相对模块导入](#1. 相对 vs. 非相对模块导入)

- [2. 模块解析策略](#2. 模块解析策略)

- - [Classic]
  - [Node]

- [3. 附加模块解析标记](#3. 附加模块解析标记)

- - [Base URL]
  - [路径映射]
  - [通过rootDirs指定虚拟目录]

- [4. 跟踪模块解析](#4. 跟踪模块解析)

- [5. 使用`--noResolve`](#5. 使用`--noResolve`)

- [6. 常见问题](#6. 常见问题)

*本节假设你已经对模块知识有了一定的了解，请先阅读[模块](#模块)章节了解相关内容。*

*模块解析*是编译器确定导入内容时所执行的流程。考虑一个类似`import { a } from "moduleA"`的*import*语句；为了检查对`a`的任何使用，编译器需要确切知道其代表什么，并且需要检查它的定义`moduleA`。

这时，编译器会问：“`moduleA`的结构是怎样的？”，这听起来很简单，但`moduleA`可能在你写的`.ts`/`.tsx`文件中或在代码所依赖的`.d.ts`文件中定义。

首先，编译器会尝试查找表示导入模块的文件。编译器遵循两种不同策略之一：[Classic](#Classic)或[Node](#Node)。这些策略会告诉编译器*去哪里寻找`moduleA`*。

如果以上解析失败，并且模块模块名称不是相对名称（且是`moduleA`时），则编译器将尝试查找[外部模块声明](#外部模块声明)。接下来，会介绍到非相对导入。

最后，如果编译器无法解析模块，它将记录一个错误。在这种情况下，错误将类似于`error TS2307: Cannot find module 'moduleA'.`。



#### 1. 相对 vs. 非相对模块导入

根据模块引用是相对引用还是相对引用的不同，会以不同的方式解析模块导入。

**相对导入**是以`/`、`./`或`../`开头的。以下是一些示例：

- `import Entry from "./components/Entry";`
- `import { DefaultHeaders } from "../constants/http";`
- `import "/mod";`

所有其它形式的导入会被当作**非相对导入**。以下是一些示例：

- `import * as $ from "jquery";`
- `import { Component } from "@angular/core";`

*相对导入*是在解析时相对于导入它文件，并且无法解析为*外部模块声明*。对于自己的模块应该使用相对导入，以确保在运行时保持它们的相对位置。

*非相对导入*可以相对于`baseUrl`解析，也可以通过路径映射解决，将会在下面介绍。它们还可以解析为[外部模块声明](#外部模块声明)。导入任何外部依赖项时，请使用非相对路径。



#### 2. 模块解析策略

有两种模块解析策略：[Classic](#Classic)和[Node](#Node])。可以通过`--moduleResolution`标记来指定解析策略。如果未指定，那么在使用`--module AMD | System | ES2015`时默认为[Classic](#Classic)，其它情况为[Node](#Node)。



##### Classic
*Classic*以前是TypeScript的默认解析策略。现在，这一策略主要是为了向后兼容。

相对导入的模块相对于导入它的文件进行解析的。

所以，对于`/root/src/folder/A.ts`文件中的`import { b } from "./moduleB"`，其查找流程为：

`/root/src/folder/moduleB.ts`

``/root/src/folder/moduleB.d.ts`

``对于非相对导入的模块，编译器则会从包含导入文件的目录开始，依次向上级目录遍历，以尝试定位匹配的声明文件。示例：

``有一个对`moduleB`的非相对导入`import { b } from "moduleB"`，其位于``/root/src/folder/A.ts``文件中。编译器会以如下方式来定位它：  

``/root/src/folder/moduleB.ts``

``/root/src/folder/moduleB.d.ts``

``/root/src/moduleB.ts``

``/root/src/moduleB.d.ts``

``/root/moduleB.ts``

``/root/moduleB.d.ts``

``/moduleB.ts``

``/moduleB.d.ts`` 

##### **Node**

这一解析策略会尝试在运行时模仿[Node.js](https://nodejs.org/)模块的解析机制。[Node.js模块文档](https://nodejs.org/api/modules.html#modules_all_together)中概述了完整的Node.js模块解析算法。



##### **Node.js怎样解析模块**

为了理解TypeScript编译器遵循的解析步骤，弄清Node.js模块是非常重要的。通常，Node.js中的导入是通过名为`require`的函数来调来执行的。Node.js会根据`require`中指定的是相对路径还是非相对路径，采取不同的行为。

如果是相对路径非常简单。例如，假设文件路径为`/root/src/moduleA.js`，其中包含了一个`var x = require("./moduleB");`导入。Node.js会按以下顺序解析导入:

1.检查`/root/src/moduleA.js`文件是否存在

2.检查`/root/src/moduleA`目录中是否包含一个`package.json`，且`package.json`文件指定了一个`"main"`模块。

在我们的示例中，如果Node.js发现`/root/src/moduleA/package.json`文件包含了`{ "main": "lib/mainModule.js" }`，那么Node.js会引用`/root/src/moduleA/lib/mainModule.js`。

3.检查`/root/src/moduleA`目录中是否包含一个`index.js`，如果存在这个文件会被隐式的当做那个目录下的*"main"*模块。

可以通过Node.js文档了解更多详细信息：[文件模块(file modules)](https://nodejs.org/api/modules.html#modules_file_modules)和[文件夹模块(folder modules)](https://nodejs.org/api/modules.html#modules_folders_as_modules)。

但是，[非相对模块名](https://www.typescriptlang.org/docs/handbook/module-resolution.html#relative-vs-non-relative-module-imports)的解析完全不同。Node会在一个特殊的目录`node_modules`中查找你的模块。`node_modules`可能与当前文件在同级目录下，或者在上层目录中。Node会遍历上级目录，并在每个`node_modules`中查找，直到找到要加载的模块。

在上面的示例中，假设`/root/src/moduleA.js`中使用的是非相对路径导入的`var x = require("./moduleB");`。这样，Node会按以下顺序去解析模块`"moduleB"`，只到能匹配上：

1. `/root/src/node_modules/moduleB.js`

2. `/root/src/node_modules/moduleB/package.json` (如果指定了`"main"`属性)

3. `/root/src/node_modules/moduleB/index.js`

   

4. `/root/node_modules/moduleB.js`

5. `/root/node_modules/moduleB/package.json` (如果指定了`"main"`属性)

6. `/root/node_modules/moduleB/index.js`

   

7. `/node_modules/moduleB.js`

8. `/node_modules/moduleB/package.json` (如果指定了`"main"`属性)

9. `/node_modules/moduleB/index.js`

注意，在以上步骤中，*4*和*7*会跳到上一级目录。



##### **TypeScript解析模块**

TypeScript会模仿Node.js运行时解析策略，以便在编译时找到模块的定义文件。为此，TypeScript在Node解析的基础上添加了TypeScript源文件扩展名（`.ts`、`.tsx`和`.d.ts`）。TypeScript还会在`package.json`中使用一个名为`"types"`的字段来表示类似`"main"`的作用-编译器会通过它来查找要使用`"main"`定义文件。

例如，在`/root/src/moduleA.ts`中有一个导入语句`import { b } from "./moduleB"`，会按以下流程来查找 import {b}的导入语句将导致尝试以下位置来查找`"./moduleB"`：

1. `/root/src/moduleB.ts`
2. `/root/src/moduleB.tsx`
3. `/root/src/moduleB.d.ts`
4. `/root/src/moduleB/package.json` (如果指定了`"types"`属性)
5. `/root/src/moduleB/index.ts`
6. `/root/src/moduleB/index.tsx`
7. `/root/src/moduleB/index.d.ts`

前面所说，Node.js会首先查找`moduleB.js`文件，然后是合适的`package.josn`，再之后是`index.js`。

类似的，非相对导入也会遵循Node.js的解析逻辑，首先查找文件、再到合适的目录。所以，`/root/src/moduleA.ts`文件中的`import { b } from "moduleB"`会按以下顺序查找：

1. `/root/src/node_modules/moduleB.ts`

2. `/root/src/node_modules/moduleB.tsx`

3. `/root/src/node_modules/moduleB.d.ts`

4. `/root/src/node_modules/moduleB/package.json` (如果指定了`"types"`属性)

5. `/root/src/node_modules/@types/moduleB.d.ts`

6. `/root/src/node_modules/moduleB/index.ts`

7. `/root/src/node_modules/moduleB/index.tsx`

8. `/root/src/node_modules/moduleB/index.d.ts`

   

9. `/root/node_modules/moduleB.ts`

10. `/root/node_modules/moduleB.tsx`

11. `/root/node_modules/moduleB.d.ts`

12. `/root/node_modules/moduleB/package.json` (如果指定了`"types"`属性)

13. `/root/node_modules/@types/moduleB.d.ts`

14. `/root/node_modules/moduleB/index.ts`

15. `/root/node_modules/moduleB/index.tsx`

16. `/root/node_modules/moduleB/index.d.ts`

    

17. `/node_modules/moduleB.ts`

18. `/node_modules/moduleB.tsx`

19. `/node_modules/moduleB.d.ts`

20. `/node_modules/moduleB/package.json` (如果指定了`"types"`属性)

21. `/node_modules/@types/moduleB.d.ts`

22. `/node_modules/moduleB/index.ts`

23. `/node_modules/moduleB/index.tsx`

24. `/node_modules/moduleB/index.d.ts`

以上步骤比较多，但并不Node.js的查找流程复杂多少，其中*8*和*15*向上跳了两次目录。



#### 3. 附加模块解析标记

有时项目源码结构与输出结构不一致。通常，要经过一系列的构建步骤后最后生成输出。其中包括将`.ts`文件编译成`.js`，并将不同的依赖项目复制到同一输出位置。最终的结果就是，运行时的模块名称可能与包含其定义的源文件的名称并不相同。或者，最终输出的中的文件中的模块路径与编译时的源文件路径不同了。

TypeScript编译器有一些附加标志，用于通知编译器源码编译成最终输出时要发生的转换。

重要的一点要注意，编译器并不执行任何这些转换，而只是利用这些信息来指导模块导入解析。



##### **Base URL**

在使用AMD模块加载器的应用程序中，使用`baseUrl`是常见的做法，在这些应用中，模块在运行时被“部署”到单个文件夹中。这些模块的源代码可以位于不同的目录下，但是构建脚本会将它们放在一起。

设置`baseUrl`会告诉编译器可以在哪里找到模块。所有非相对名称的模块导入，都会被当做是相对于`baseUrl`。

`baseUrl`的值由以下两者之一决定：

- 命令行中*baseUrl*的值（如果指定的是相对路径，会相对于当前路径计算）
- `'tsconfig.json'`中的*baseUrl*属性（如果指定是相对路径，会相对于`'tsconfig.json'`中的路径计算）

注意，相对模块的导入不会被设置的*baseUrl*影响，它们总是相对于导入它们的文件。

更多关于*baseUrl*的介绍，请参考：[RequireJS](http://requirejs.org/docs/api.html#config-baseUrl)和[SystemJS](https://github.com/systemjs/systemjs/blob/master/docs/config-api.md#baseurl)相关文档。



##### **路径映射**

有时，模块不是直接放在*baseUrl*目录下。例如，导入模块`jquery`会在运行时转换为`"node_modules/jquery/dist/jquery.slim.min.js"`。加载器使用映射配置将模块名映射到运行时文件，参考[RequireJS](http://requirejs.org/docs/api.html#config-paths)及[SystemJS](https://github.com/systemjs/systemjs/blob/master/docs/config-api.md#paths)文档。

TypeScript编译器会通过`tsconfig.json`文件中的`"paths"`来支持这样的声明映射。下面是一个指定`jquery`的`"paths"`属性的示例：

```
{
  "compilerOptions": {
    "baseUrl": ".", // This must be specified if "paths" is.
    "paths": {
      "jquery": ["node_modules/jquery/dist/jquery"] // This mapping is relative to "baseUrl"
    }
  }
}
```

需要注意`"paths"`是相对于`"baseUrl"`来解析的。如果`"baseUrl"`被设置为除`"."`之外的其它的，比如`tsconfig.json`所在的目录，那么映射就必须做相应的修改。例如，上例中如果设置为`"baseUrl": "./src"`，那么*jquery*应该映射到`"../node_modules/jquery/dist/jquery"`。

还可以通过`"paths"`来指定复杂的映射，包括指定多个回退位置。假设项目中一些文件在一个位置，而其它的别的位置，构建过程需要将他们集中到一块。项目结构可能如下：

```
projectRoot
├── folder1
│   ├── file1.ts (imports 'folder1/file2' and 'folder2/file3')
│   └── file2.ts
├── generated
│   ├── folder1
│   └── folder2
│       └── file3.ts
└── tsconfig.json
```

相应的`tsconfig.json`文件如下：

```
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "*": ["*", "generated/*"]
    }
  }
}
```

这告诉编译器任何与模式`"*"`（即所有值）匹配的模块导入都在以下两个位置查找：

1. `"*"`：表示名称不会发生改变，所以映射为`<moduleName>` => `<baseUrl>/<moduleName>`
2. `"generated/*"`表示模块名添加了*“generated”*前缀，所以映射为`<moduleName>` => `<baseUrl>/generated/<moduleName>`

按照这一逻辑，编译器会尝试解析如下两个导入：

- 导入*‘folder1/file2’*

- 1. 匹配*'\*'*模式且通配符获取整个模块名
  2. 尝试列表中的第一个替换：*'\*'* -> `folder1/file2`
  3. 将结果替换为非相对名称 - 与*baseUrl* -> `projectRoot/folder1/file2.ts`合并
  4. 文件存在，完成

- 导入*‘folder2/file3’*

- 1. 匹配*'\*'*模式且通配符获取整个模块名
  2. 尝试列表中的第一个替换：*'\*'* -> `folder2/file3`
  3. 将结果替换为非相对名称 - 与*baseUrl* -> `projectRoot/folder2/file3.ts`合并
  4. 文件不存在，跳到第二个替换
  5. 第二个替换：*‘generated/\*’* -> `generated/folder2/file3`
  6. 将结果替换为非相对名称 - 与*baseUrl* -> `projectRoot/generated/folder2/file3.ts`合并
  7. 文件存在，完成



##### **通过`rootDirs`指定虚拟目录**

有时，编译来自多个目录的项目源文件会全部合并以生成单个输出目录。这可以看作是一组源目录创建了一个“虚拟”目录。

利用`rootDirs`，可以告诉编译器生成该“虚拟”目录的根目录（*roots*）；因此，编译器可以在“虚拟”目录中解析相对模块导入，就像合并到一个目录中一样。

例如，考虑以下项目结构：

```
 src
 └── views
     └── view1.ts (imports './template1')
     └── view2.ts

 generated
 └── templates
         └── views
             └── template1.ts (imports './view2')
```

其中，`src/views`目录中的文件是用于控制UI的用户代码。`generated/templates`目录中的文件是UI模板，在构建时通过模板生成器自动生成。构建中的一步会将`src/views`和`generated/templates`拷贝到同一目录下。在运行时，视图可以假设它的模板与它在同一目录下，因此可以使用相对导入`"./template"`。

可以通过`"rootDirs"`属性来告诉编译器。`"rootDirs"`指定了一个根目录列表，列表中的内容会在运行时被合并。所以，对于这个示例`tsconfig.json`配置如下：

```
{
  "compilerOptions": {
    "rootDirs": ["src/views", "generated/templates/views"]
  }
}
```

每次编译器在`rootDirs`之一的子文件夹中发现相对模块导入时，它会尝试在每个`rootDirs`中查找此导入。

`rootDirs`的灵活性不仅限于指定了要在逻辑上合并的物理源目录的列表。它提供的数组可以包括任意数量的临时目录名，无论它们是否存在。这允许编译器以类型安全的方式捕获复杂的绑定(*bundling*)和运行时功能，比如条件引入和项目特定的加载器插件。

假设一个国际化方案，在该方案中，构建工具通过插入特殊路径标记（如：`#{locale}`）作为相对模块路径（如：`./#{locale}/messages`）的一部分，自动生成特定于区域设置的包。在本示例设置中，该工具枚举了受支持的语言环境，将抽象的路径映射到`./zh/messages`、`./de/messages`等。

假设这些模块中的每个模块都导出一个字符串数组。 如，`./zh/messages`可能包含：

```
export default [
    "您好吗",
    "很高兴认识你"
];
```

利用`rootDirs`我们可以让编译器了解这个映射关系，进而也让编译器能够安全的解析`./#{locale}/messages`，就算这个目录永远不存在。例如，使用下面的`tsconfig.json`：

```
{
  "compilerOptions": {
    "rootDirs": [
      "src/zh",
      "src/de",
      "src/#{locale}"
    ]
  }
}
```

编译器现在可以将`import messages from './#{locale}/messages'`解析为`import messages from './zh/messages'`用于工具支持的目的，并且可以在开发时不必关心区域信息。



#### 4. 跟踪模块解析

如前所述，解析模块时，编译器可以访问当前文件夹之外的文件。这会导致很难确认模块为什么没有解析成功。使用`--traceResolution`标志，可以启用编译器模块解析跟踪，可以告诉我们模块解析过程中发生的情况。

假设我们有一个使用`typescript`模块的示例应用。`app.ts`有类似`import * as ts from "typescript"`的导入。

```
│   tsconfig.json
├───node_modules
│   └───typescript
│       └───lib
│               typescript.d.ts
└───src
        app.ts
```

通过`--traceResolution`来调用编译器：

```
tsc --traceResolution
```

结果输出类似如下：

```
======== Resolving module 'typescript' from 'src/app.ts'. ========
Module resolution kind is not specified, using 'NodeJs'.
Loading module 'typescript' from 'node_modules' folder.
File 'src/node_modules/typescript.ts' does not exist.
File 'src/node_modules/typescript.tsx' does not exist.
File 'src/node_modules/typescript.d.ts' does not exist.
File 'src/node_modules/typescript/package.json' does not exist.
File 'node_modules/typescript.ts' does not exist.
File 'node_modules/typescript.tsx' does not exist.
File 'node_modules/typescript.d.ts' does not exist.
Found 'package.json' at 'node_modules/typescript/package.json'.
'package.json' has 'types' field './lib/typescript.d.ts' that references 'node_modules/typescript/lib/typescript.d.ts'.
File 'node_modules/typescript/lib/typescript.d.ts' exist - use it as a module resolution result.
======== Module name 'typescript' was successfully resolved to 'node_modules/typescript/lib/typescript.d.ts'. ========
```

***需要注意的地方***

- 导入名称及位置

```
======== Resolving module ‘typescript’ from ‘src/app.ts’. ========
```

- 编译器使用的策略

```
Module resolution kind is not specified, using ‘NodeJs’.
```

- 从*npm*包中加载*types*

```
‘package.json’ has ‘types’ field ‘./lib/typescript.d.ts’ that references ‘node_modules/typescript/lib/typescript.d.ts’.
```

- 最终结果

```
======== Module name ‘typescript’ was successfully resolved to ‘node_modules/typescript/lib/typescript.d.ts’. ========
```



#### 5. 使用`--noResolve`

通常，编译器将在开始编译过程之前尝试解析所有模块导入。每次成功将`import`解析为文件时，该文件都会添加到一个文件列表中，以便编译器以后处理。

`--noResolve`编译选项会告诉编译器，不要将任何不是命令行传入的文件“添加”到编译列表中。但仍然会尝试将模块解析为文件，但是如果未指定文件，则不包含该文件。

示例：

*app.ts*

```
import * as A from "moduleA" // OK, 'moduleA' passed on the command-line
import * as B from "moduleB" // Error TS2307: Cannot find module 'moduleB'.
tsc app.ts moduleA.ts --noResolve
```

使用`--noResolve`选项来统计`app.ts`：

- 可能会正确找到`moduleA`，因为在命令行上指定了
- 查找`moduleB`会出错，因为没有命令行传入



#### 6. 常见问题

***为什么在`exclude`列表中的模块还会被编译？***

`tsconfig.json`会将文件夹转成一个“项目”。在不指定任何`“exclude”`或`“files”`的情况下，文件夹中的文件包含`tsconfig.json`及其所有子目录都包含在编译列表中。如果要排除某些文件，请使用`“exclude”`，如果希望指定所有要编译的文件而不是让编译器查找，请使用`“files”`。

有些是被`tsconfig.json`自动加入的。它们不会涉及到上面所说的模块解析。如果编译器标识出一个文件是模块的导入目标，则该文件将包括在编译中，无论先前步骤中是否将其排除。

因此，要从编译中排除文件，需要排除它的同时，还要排除所有对它使用了`import`或`/// <reference path =“ ...” />`指令的文件。



### 3.10 命名空间（Namespaces）

- [1. 介绍](#1. 介绍)

- [2. 第一步](#2. 第一步)

- - [验证器在一个文件中]

- [3. 命名空间](#3. 命名空间)

- - [命名空间的验证器]

- [4. 跨文件分割](#4. 跨文件分割)

- - [多文件命名空间]

- [5. 别名](#5. 别名)

- [6. 使用其它JavaScript库](#6. 使用其它JavaScript库)

- - [外部命名空间]

#### 1. 介绍

在本章节中，概述了用TypeScript中的命名空间来组织代码的相关方法。



#### 2. 第一步

首先我们从一段在本单中都可用的示例开始。以下我们编写了一些简单的字符串验证器，你可能会用它们来验证网页上的用户表单输入内容或检查外部数据。

##### **验证器在一个文件中**

```
interface StringValidator {
  isAcceptable(s: string): boolean;
}

let lettersRegexp = /^[A-Za-z]+$/;
let numberRegexp = /^[0-9]+$/;

class LettersOnlyValidator implements StringValidator {
  isAcceptable(s: string) {
    return lettersRegexp.test(s);
  }
}

class ZipCodeValidator implements StringValidator {
  isAcceptable(s: string) {
    return s.length === 5 && numberRegexp.test(s);
  }
}

// Some samples to try
let strings = ["Hello", "98052", "101"];

// Validators to use
let validators: { [s: string]: StringValidator } = {};
validators["ZIP code"] = new ZipCodeValidator();
validators["Letters only"] = new LettersOnlyValidator();

// Show whether each string passed each validator
for (let s of strings) {
  for (let name in validators) {
    let isMatch = validators[name].isAcceptable(s);
    console.log(`'${s}' ${isMatch ? "matches" : "does not match"} '${name}'.`);
  }
}
```



#### 3. 命名空间

随着我们添加更多验证器，我们会需要一种代码组织方案，以便我们在跟踪类型的同时而不必担心名称与其他对象命名冲突。因些，我们需要将对象包装到命名空间中，而不是将大量不同的名称放入全局命名空间。

在此示例中，我们将所有与验证器相关的实体都放到了名为`Validation`的命名空间中。因为我们希望这些接口和类在命名空间之外也可见，所以我们使用了`export`。相反，变量`letterRegexp`和`numberRegexp`是实现细节，因此它们不需要导出，并且对命名空间之外的代码不可见。在文件底部的测试代码中，我们现在需要限定在命名空间之外使用的类型的名称，如：`Validation.LettersOnlyValidator`。

##### **命名空间的验证器**

```
namespace Validation {
  export interface StringValidator {
    isAcceptable(s: string): boolean;
  }

  const lettersRegexp = /^[A-Za-z]+$/;
  const numberRegexp = /^[0-9]+$/;

  export class LettersOnlyValidator implements StringValidator {
    isAcceptable(s: string) {
      return lettersRegexp.test(s);
    }
  }

  export class ZipCodeValidator implements StringValidator {
    isAcceptable(s: string) {
      return s.length === 5 && numberRegexp.test(s);
    }
  }
}

// Some samples to try
let strings = ["Hello", "98052", "101"];

// Validators to use
let validators: { [s: string]: Validation.StringValidator } = {};
validators["ZIP code"] = new Validation.ZipCodeValidator();
validators["Letters only"] = new Validation.LettersOnlyValidator();

// Show whether each string passed each validator
for (let s of strings) {
  for (let name in validators) {
    console.log(
      `"${s}" - ${
        validators[name].isAcceptable(s) ? "matches" : "does not match"
      } ${name}`
    );
  }
}
```



#### 4. 跨文件分割

随着应用程序的增长，我们希望将代码拆分为多个文件，以使其易于维护。

##### **多文件命名空间**

在这里，我们将`Validation`命名空间拆分成多个文件。即使文件是分开的，它们仍可以使用相同的命名空间，并且在使用时可以像全部在一个位置一样。由于文件之间存在依赖性，因此我们将添加引用标签，以告知编译器文件之间的关系。我们的测试代码保持不变

*Validation.ts*

```
namespace Validation {
  export interface StringValidator {
    isAcceptable(s: string): boolean;
  }
}
```

*LettersOnlyValidator.ts*

```
/// <reference path="Validation.ts" />
namespace Validation {
  const lettersRegexp = /^[A-Za-z]+$/;
  export class LettersOnlyValidator implements StringValidator {
    isAcceptable(s: string) {
      return lettersRegexp.test(s);
    }
  }
}
```

*ZipCodeValidator.ts*

```
/// <reference path="Validation.ts" />
namespace Validation {
  const numberRegexp = /^[0-9]+$/;
  export class ZipCodeValidator implements StringValidator {
    isAcceptable(s: string) {
      return s.length === 5 && numberRegexp.test(s);
    }
  }
}
```

*Test.ts*

```
/// <reference path="Validation.ts" />
/// <reference path="LettersOnlyValidator.ts" />
/// <reference path="ZipCodeValidator.ts" />

// Some samples to try
let strings = ["Hello", "98052", "101"];

// Validators to use
let validators: { [s: string]: Validation.StringValidator } = {};
validators["ZIP code"] = new Validation.ZipCodeValidator();
validators["Letters only"] = new Validation.LettersOnlyValidator();

// Show whether each string passed each validator
for (let s of strings) {
  for (let name in validators) {
    console.log(
      `"${s}" - ${
        validators[name].isAcceptable(s) ? "matches" : "does not match"
      } ${name}`
    );
  }
}
```

一旦涉及多个文件，我们需要确保所有已编译的代码都已加载。有两种方法可以做到这一点。

首先，可以通过`--outFile`标志，将所有输入文件编译成一个JavaScript输出文件：

```
tsc --outFile sample.js Test.ts
```

编译器会根据文件中的引用标签自动排序输出文件。还可以分别指定每个文件：

```
tsc --outFile sample.js Validation.ts LettersOnlyValidator.ts ZipCodeValidator.ts Test.ts
```

此外，我们可以分别编译每个文件（默认），每个输入文件生成一个JavaScript文件。如果有多个JS文件，就需要在网页上通过`<script>`标签把所生成的文件按正确的顺序加载。例如：

*MyTestPage.html (excerpt)*

```
<script src="Validation.js" type="text/javascript" />
<script src="LettersOnlyValidator.js" type="text/javascript" />
<script src="ZipCodeValidator.js" type="text/javascript" />
<script src="Test.js" type="text/javascript" />
```



#### 5. 别名

简化命名空间的另一种方法是使用`import q = x.y.z`的方式为常用对象创建更短的名称。不要与用于加载模块的`import x = require("name")`方法混淆，该语法只是为指定符号创建别名。可以将这些类型的导入（通常称为别名）用于任何种类的标识符，包括从导入的模块创建对象。

```
namespace Shapes {
  export namespace Polygons {
    export class Triangle {}
    export class Square {}
  }
}

import polygons = Shapes.Polygons;
let sq = new polygons.Square(); // Same as 'new Shapes.Polygons.Square()'
```

注意，我们并没有使用`require`关键字，而是直接导入符号的限定名赋值。这与`var`类似，但其还可用于类型和导入的有命名空间含义的符号。重要的是，对于值来讲， `import`会生成与原始符号不同的引用，因此对别名`var`的修改并不会影响原始变量的值。



#### 6. 使用其它JavaScript库

为了描述非TypeScript编写的库的类型，我们需要声明该库导出的API。因为大多数JavaScript库仅公开一些顶级对象，所以命名空间是表示它们的一个好方法。

我们称其为声明，是因为它们不是外部程序的具体。通常，这些文件在`.d.ts`文件中定义。如果您熟悉C/C++，则可以将它们视为`.h`文件。让我们看几个示例。



##### **外部命名空间**

流行的库D3在名为`d3`的全局对象中定义其功能。由于此库是通过`<script>`标签（而非模块加载器）加载，因此其声明使用命名空间来定义其类型。为了让TypeScript编译器识别，我们使用外部命名空间声明。例如，我们可以开始编写如下代码：

*D3.d.ts (simplified excerpt)*

```
declare namespace D3 {
  export interface Selectors {
    select: {
      (selector: string): Selection;
      (element: EventTarget): Selection;
    };
  }

  export interface Event {
    x: number;
    y: number;
  }

  export interface Base extends Selectors {
    event: Event;
  }
}

declare var d3: D3.Base;
```



### 3.11 命名空间与模块（Namespaces and Modules）

- [1. 介绍](#1. 介绍)

- [2. 使用模块](#2. 使用模块)

- [3. 使用命名空间](#3. 使用命名空间)

- [4. 命名空间和模块的陷阱](#4. 命名空间和模块的陷阱)

- - [对模块使用`/// `]
  - [不必要的命名空间]
  - [模块的取舍]

#### 1. 介绍

本章节概述使用TypeScript中的模块和命名空间来组织代码的各种方法。还会介绍一些关于如何使用命名空间和模块的高级主题，及在TypeScript中使用它们时的一些常见陷阱。

关于ES模块的更多信息，请参见[模块](#模块)文档。有关TypeScript命名空间的更多信息，请参见[命名空间](#命名空间)文档。

注意：在较旧的TypeScript命名空间版本中，被称为“内部模块”（TypeScript 1.5之前）。“内部模块”现在称做“命名空间”， “外部模块”现在则简称为“模块”，这是为了与 [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/)里的术语保持一致



#### 2. 使用模块

模块可以包含代码和声明。

模块还依赖于模块加载器（如：CommonJs/Require.js）或支持ES模块的运行时。模块提供了更好的代码重用性，更强的隔离性以及更好的捆绑工具支持。

还值得注意的是，对于Node.js应用，模块是默认的及推荐的代码组织方式。

自ECMAScript 2015开始，模块成了语言的内置部分，并且可能会被所有兼容引擎所支持。因此，对于新项目，模块是推荐的代码组织机制。



#### 3. 使用命名空间

命名空间是TypeScript特定的代码组织方式。

命名空间在全局命名空间中只是普通的有名称JavaScript对象。这使得命名空间非常简单的构造和使用。与模块不同，它们可以跨多个文件，并且可以通过`--outFile`进行组合。命名空间是在Web应用中构建代码的一种好方法，可以将所有依赖项都通过`<script>`标签引用到HTML页面中。

就像所有全局命名空间污染一样，可能会很难识别组件间依赖关系，尤其是在大型应用中。



#### 4. 命名空间和模块的陷阱

在本节中，将介绍使用命名空间和模块时遇到的常见陷阱，以及如何避免这些情况。



##### **对模块使用/// < reference >**

一个常见的错误是使用`/// <reference>`引用模块文件，而非使用`import`。要理解之前的差异，首先需要要明白编译器是如何根据`import`路径（如，`import x from "...";`，`import x = require("...");`里面的`...`）来定位模块类型信息的。

编译器首会去查找相应路径下的`.ts`、`.tsx`或者`.d.ts`。如果这些文件都找不到，编译器会查找*外部模块声明*。回顾一下，它们是在`.d.ts`文件中声明的。

```
  myModules.d.ts
```

```
  // In a .d.ts file or .ts file that is not a module:
  declare module "SomeModule" {
    export function fn(): string;
  }
```

```
  myOtherModule.ts
```

```
  /// <reference path="myModules.d.ts" />
  import * as m from "SomeModule";
```

这里的引用标签指定了外部模块的位置。这就是一些TypeScript例子中引用`node.d.ts`的方式。



##### **不必要的命名空间**

如果想把命名空间转换为模块，则可能会像如下所示的文件一样：

```
  shapes.ts
```

```
  export namespace Shapes {
    export class Triangle { /* ... */ }
    export class Square { /* ... */ }
  }
```

顶层的模块`Shapes`包裹了`Triangle`和`Square`。对于使用它的人来说这是不友好和不易用的：
```
  shapeConsumer.ts
```

```
  import * as shapes from "./shapes";
  let t = new shapes.Shapes.Triangle(); // shapes.Shapes?
```

TypeScript中模块的主要特点是是两个不同的模块，永远不会在同一作用域中提供相同的名称。由于模块的使用者会为其命名，所以无需主动将导出的符号包装在命名空间中。

为什么不应该为模块内容命名空间，因为使用命名空间是为了提供逻辑分组和避免命名冲突。由于模块文件本身已经是一个逻辑分组，并且其顶级名称是由导入该文件的代码定义的，因此无需为导出的对象使用额外的模块层。

以下是改进的示例：
```
  shapes.ts
```

```
  export namespace Shapes {
    export class Triangle {
      /* ... */
    }
    export class Square {
      /* ... */
    }
  }
```
```
  shapeConsumer.ts
```

```
  import * as shapes from "./shapes";
  let t = new shapes.Triangle();
```



##### **模块的取舍**

就像JS文件和模块之间存在一一对应关系一样，TypeScript模块的源文件也与其生的JS文件一一对应。这样的产生影响是，无法根据目标模块系统来连接多个模块源文件。例如，目标模块系统为`commonjs`或`umd`时不能使用`outFile`选项，但是在TypeScript 1.8及更高版本中，目标模块系统为`commonjs`或`umd`时可以使用`outFile`选项。



### 3.12 符号（Symbols）

- [1. 介绍](#1. 介绍)

- [2. 众所周知的Symbols](#2. 众所周知的Symbols)

- - [Symbol.hasInstance]
  - [Symbol.isConcatSpreadable]
  - [Symbol.iterator]
  - [Symbol.match]
  - [Symbol.replace]
  - [Symbol.search]
  - [Symbol.species]
  - [Symbol.split]
  - [Symbol.toPrimitive]
  - [Symbol.toStringTag]
  - [Symbol.unscopables]

#### 1. 介绍

自ECMAScript 2015起，`symbol`（符号类型）已做为原生类型提供，就像`number`和`string`一样。

`symbol`值通过调用`Symbol`构造创建：

```
let sym1 = Symbol();

let sym2 = Symbol("key"); // optional string key
```

符号是不可变的，并且是唯一的。

```
let sym2 = Symbol("key");
let sym3 = Symbol("key");

sym2 === sym3; // false, symbols are unique
```

像字符串一样，符号可以用作对象属性的键。

```
const sym = Symbol();

let obj = {
  [sym]: "value"
};

console.log(obj[sym]); // "value"
```

符号也可以与计算属性声明结合使用，以声明对象属性和类成员。

```
const getClassNameSymbol = Symbol();

class C {
  [getClassNameSymbol]() {
    return "C";
  }
}

let c = new C();
let className = c[getClassNameSymbol](); // "C"
```



#### 2. 众所周知的Symbols

除了用户定义的符号外，还有众所周知的内置符号。内置符号用于表示内部语言行为。

以下是一些我们所知的符号列表：

##### **Symbol.hasInstance**

一个方法，会被`instanceof`运算符调用，用于识某个对象是否是构造函数的实例。

##### **Symbol.isConcatSpreadable**

一个布尔值，表示在对象上调用`Array.prototype.concat`时该对象是否可展开为其数组元素。

##### **Symbol.iterator**

方法，返回对象的默认迭代器。由`for-of`语句的语义调用。

##### **Symbol.match**

方法，用于正则表达式匹配字符串。由`String.prototype.match`方法调用

##### **Symbol.replace**

一个正则表达式方法，用于替换字符串的匹配子字符串。由`String.prototype.replace`方法调用。

##### **Symbol.search**

一个正则表达式方法，用于返回与正则表达式匹配的字符串中的索引位置。由`String.prototype.search`方法调用。

##### **Symbol.species**

函数值属性，构造函数，用于创建派生对象.

##### **Symbol.split**

正则表达式方法，用于在与正则表达式匹配的索引位置拆分字符串。由`String.prototype.split`方法调用。

##### **Symbol.toPrimitive**

方法，用于将对象转换为相应原始值。由`ToPrimitive`抽象操作调用。

##### **Symbol.toStringTag**

方法，返回创建对象的默认字符串描述。由内置方法`Object.prototype.toString`调用。

##### **Symbol.unscopables**

一个对象，其所拥有的属性名称是从关联对象的`with`作用域中排除的。



### 3.13 三斜线指令（///）

- [1. /// <reference path="..." />](# 1. /// <reference path="..." /> )
- [2. /// <reference types="..." />](# 2. /// <reference types="..." /> )
- [3. /// <reference lib="..." />](# 3. /// <reference lib="..." />)
- [4. /// <reference no-default-lib="true"/>](#4. /// <reference no-default-lib="true"/>)
- [5. /// <amd-module /> ](#5. /// <amd-module />)
- [6. /// <amd-dependency />](#6. /// <amd-dependency />)

三斜线指令是包含单个XML标签的单行注释。注释的内容会用作编译器指令。

三斜线指令*仅在*其包含文件的顶部有效。且三斜线指令只能在单行或多行注释之前，包括其他三斜线指令。如果它们出现在声明或声明之后，那么会被当做普通的单行注释，并且没有特殊含义。

#### 1. /// < reference path="..." />

`/// <reference path="..." />`指令是三斜线指令最常见的一种，它用于文件之间依赖关系的声明。

三斜线引用告诉编译器在编译过程中要引入的额外文件。



当使用`--out`或`--outFile`时，它们还以做为排序输出的方法。预处理通过后，文件会以与输入相同的顺序生成到输出文件位置。



***预处理输入文件***

编译器会对输入文件进行预处理，以解析所有三斜线引用指令。在此过程中，其它文件将添加到编译过程中。

该过程从一组*根文件*开始：它们是在命令行或`tsconfig.json`文件的`"files"`列表中指定的文件名。这些根文件按照指定的顺序进行预处理。当一个文件被添加到列表前，它所包含的所有三斜线引用及其目标都要被处理。按照在文件中出现的顺序，通过深度优先的方式解析三斜线引用。

如果不是根文件，三斜线文件的引用路径是相对于包含它的文件的。



***错误***

引用不存在的文件会报错。一个文件通过三斜线指令引用其自己也会报错。



***使用`--noResolve`***

如果指定`--noResolve`编译选项，三斜线引用会被忽略；它们不会增加新文件，也不会改完指定文件的顺序。



#### 2. /// < reference types="..." />

与`/// <reference path="..." />`指令类似，用于声明*依赖项*，`/// <reference types="..." />`指令声明对某个程序包的依赖性。

这些程序包名称的解析过程与import语句中的模块名称解析过程相似。考虑三重斜杠引用类型指令的一种简单方法是将其导入声明包。

例如，在声明文件中包含了`/// <reference types="node" />`，就表示声明的文件使用`@types/node/index.d.ts`中声明的名称；因此，这个包需要与声明文件一起包含在编译过程中。

仅当你手工创建`d.ts`文件时，才会使用这个指令。

对于在编译期间生成的声明文件，编译器将自动为添加`/// <reference types="..." />`；当且仅当生成的文件中使用了引用包中的声明时，才会在生成的声明文件中添加`/// <reference types="..." />`。

要声明`.ts`文件中`@types`包的依赖性，请在命令行或`tsconfig.json`中使用`--types`。有关更多详细信息，请参见[在`tsconfig.json`中使用`@types`，`typeRoots`和`types`](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html#types-typeroots-and-types)。



#### 3. /// < reference lib="..." />

此指令允许文件显式包括现有的内置*lib*文件。

内置*lib*文件的引用方式与*tsconfig.json*中的`"lib"`编译器选项相同（例如，使用`lib="es2015"`而不是`lib="lib.es2015.d.ts"`等）。

对于依赖内置类型声明文件作者，例如 建议使用DOM API或内置JS运行时构造函数（如，`Symbol`或`Iterable`），三斜线库引用指令。以前的版本中，这些`.d.ts`文件必须添加此类的forward/duplicate声明。

例如，在编译中的一个文件中添加`/// <reference lib="es2017.string" />`等效于使用`--lib es2017.string`进行编译。

```
/// <reference lib="es2017.string" />

"foo".padStart(4);
```



#### 4. /// < reference no-default-lib="true"/>

该指令会把文件标记成默认库。你会在`lib.d.ts`及其不同变体的顶部看到此注释。

这一指令指示编译器在编译中不包括默认库（即`lib.d.ts`）。这与在命令行上使用`--noLib`类似。

还要注意，在传入`--skipDefaultLibCheck`时，编译器将仅使用`/// <reference no-default-lib="true"/>`跳过文件检查。



#### 5. /// < amd-module />

默认情况下，AMD模块都是匿名生成的。当使用其它工具来处理生成的模块（如，`r.js`）时，可能会出现问题。

`amd-module`指令允许将可选模块名称传给编译器。

*amdModule.ts*

```
///<amd-module name="NamedModule"/>
export class C {
}
```

这会将`NamedModule`传入到AMD `define`函数中：

*amdModule.js*

```
define("NamedModule", ["require", "exports"], function(require, exports) {
  var C = (function() {
    function C() {}
    return C;
  })();
  exports.C = C;
});
```



#### 6. /// < amd-dependency />

*注意：此指令已被弃用。使用`import "moduleName";`语句代替。*

`/// `会告诉编译器有关非TS模块的依赖信息，需要将其注入结果模块的`require`调用中。

`amd-dependency`指令还可以有可选的`name`属性；这允许为amd依赖关系传入一个可选名称：

```
/// <amd-dependency path="legacy/moduleA" name="moduleA"/>
declare var moduleA:MyType
moduleA.callStuff()
```

生成的JS代码：

```
define(["require", "exports", "legacy/moduleA"], function(
  require,
  exports,
  moduleA
) {
  moduleA.callStuff();
});
```



### 3.14 类型兼容性（Type Compatibility）

- [1. 介绍](#1. 介)

- - [关于稳健性]

- [2. 开始](#2. 开始)

- [3. 比较两个函数](#3. 比较两个函数)

- - [函数参数的双方差]
  - [可选参数与剩余(`rest`)参数]
  - [函数重载]

- [4. 枚举](#4. 枚举)

- [5. 类](#5. 类)

- - [类中的私有及受保护成员]

- [6. 范型](#6. 范型)

- [7. 高级话题](#7. 高级话题)

- - [子类型与分配]

#### 1. 介绍

TypeScript中的类型兼容性基于结构子类型。结构化类型是一种仅基于其成员关联类型的方式，与标称类型相反。考虑以下代码：

```
interface Named {
  name: string;
}

class Person {
  name: string;
}

let p: Named;
// OK, because of structural typing
p = new Person();
```

在标称类型的语言（如C＃或Java）中，类似以上代码是错误的，因为`Person`类没有明确地将自己描述为`Named`接口的实现者。

TypeScript中的结构类型系统，是根据通常编写JavaScript代码的方式设计的。由于JavaScript广泛使用像函数表达式和对象字面量之类的匿名对象，因此使用结构类型系统而非名义上的类型，来表示JavaScript库中的各种关系会更加自然。

##### **关于稳健性**

TypeScript的类型系统允许某些在编译时不知道的操作是安全的。当类型系统有此属性时，据说它是不“稳健”的。我们仔细考虑了TypeScript允许不良行为发生的地方，在本文档中，将解释发生这些情况的原因以及其背后的动机。



#### 2. 开始

TypeScript的结构类型系统的基本规则是，如果`y`与`x`至少有相同的成员，则`x`与`y`兼容。例如：

```
interface Named {
  name: string;
}

let x: Named;
// y's inferred type is { name: string; location: string; }
let y = { name: "Alice", location: "Seattle" };
x = y;
```

为了检查是否可以将`y`分配给`x`，编译器会检查`x`中的每个属性都可以在`y`中找到对应的兼容属性。在这种情况下，`y`必须具有一个名为`name`的成员，它是一个字符串。如果有，则允许分配。

检查函数调用参数时，也使用相同的分配规则：

```
function greet(n: Named) {
  console.log("Hello, " + n.name);
}
greet(y); // OK
```

请注意，`y`有额外的`location`属性，但这不会产生错误。检查兼容性时，仅考虑目标类型的成员（在这种情况下为`Name`）。

此比较过程会以递归方式进行的，会检查每个成员和子成员的类型。



#### 3. 比较两个函数

虽然比较原始类型和对象类型相对简单，但是对于函数来说哪些应该被认为是兼容的。让我们从以下两个仅参数列表不同的函数的基本示例开始：

```
let x = (a: number) => 0;
let y = (b: number, s: string) => 0;

y = x; // OK
x = y; // Error
```

为了检查`x`是否可分配给`y`，首先会查看参数列表。`x`中的每个参数必须在`y`中有兼容类型的对应参数。请注意，不考虑参数名称，仅考虑其类型。在这种情况下，`x`的每个参数在`y`中都有一个对应的兼容参数，因此允许分配。

第二个赋值是一个错误，因为`y`具有`x`所没有的必需的第二个参数，因此不允许该赋值。

你可能想知道为什么允许像示例`y = x`那样“丢弃”参数。允许这种分配是因为，实际上在JavaScript中忽略额外的函数参数是很普遍的。例如，`Array#forEach`为回调函数提供了三个参数：数组元素、其索引和包含的数组。不过，提供仅使用第一个参数的回调很常用：

```
let items = [1, 2, 3];

// Don't force these extra parameters
items.forEach((item, index, array) => console.log(item));

// Should be OK!
items.forEach(item => console.log(item));
```

现在，使用两个仅返回值类型有所不同的函数，看看如何处理返回类型：

```
let x = () => ({name: "Alice"});
let y = () => ({name: "Alice", location: "Seattle"});

x = y; // OK
y = x; // Error, because x() lacks a location property
```

类型系统会强制源函数的返回类型是目标类型的返回类型的子类型。



##### **函数参数的双方差**

比较函数参数的类型时，如果源参数可分配给目标参数，则分配成功，反之亦然。这是不合理的，因为最终可能会给调用方一个采用更特殊类型的函数的功能，而调用一个较不特殊类型的函数。实际上，这种错误很少见，允许这种错误会可以使许多常见JavaScript模式可用。一个简单的例子：

```
enum EventType {
  Mouse,
  Keyboard
}

interface Event {
  timestamp: number;
}
interface MouseEvent extends Event {
  x: number;
  y: number;
}
interface KeyEvent extends Event {
  keyCode: number;
}

function listenEvent(eventType: EventType, handler: (n: Event) => void) {
  /* ... */
}

// Unsound, but useful and common
listenEvent(EventType.Mouse, (e: MouseEvent) => console.log(e.x + "," + e.y));

// Undesirable alternatives in presence of soundness
listenEvent(EventType.Mouse, (e: Event) =>
  console.log((e as MouseEvent).x + "," + (e as MouseEvent).y)
);
listenEvent(EventType.Mouse, ((e: MouseEvent) =>
  console.log(e.x + "," + e.y)) as (e: Event) => void);

// Still disallowed (clear error). Type safety enforced for wholly incompatible types
listenEvent(EventType.Mouse, (e: number) => console.log(e));
```

通过编译器标志`strictFunctionTypes`发生这种情况时，可以使TypeScript触发错误。



##### **可选参数与剩余(rest)参数**

比较函数兼容性时，可选参数和必需参数可以互换。源类型的额外可选参数不是错误，源类型中没有相应参数的目标类型的可选参数也不是错误。

当一个函数具有剩余参数时，其将视为不限数据的可选参数。

从类型系统的角度来看，这是不合理的，但是从运行时的角度来看，通常并不能很好地执行可选参数的想法，因为在大多数情况下，在该位置传递`undefined`是等效的。

以下示例是函数的常见模式，该函数采用回调并使用一些可预测（对于程序员）但未知的（对于类型系统）参数来调用它：

```
function invokeLater(args: any[], callback: (...args: any[]) => void) {
  /* ... Invoke callback with 'args' ... */
}

// Unsound - invokeLater "might" provide any number of arguments
invokeLater([1, 2], (x, y) => console.log(x + ", " + y));

// Confusing (x and y are actually required) and undiscoverable
invokeLater([1, 2], (x?, y?) => console.log(x + ", " + y));
```



##### **函数重载**

当函数具有重载时，源类型中的每个重载都必须与目标类型上的兼容签名匹配。这样可以确保在与源函数相同的所有情况下调用目标函数。



#### 4. 枚举

枚举与数字兼容，数字也与枚举兼容。来自不同枚举类型的枚举值被认为是不兼容的。例如：

```
enum Status {
  Ready,
  Waiting
}
enum Color {
  Red,
  Blue,
  Green
}

let status = Status.Ready;
status = Color.Green; // Error
```



#### 5. 类

类与对象字面量类型和接口的工作方式类似，但有一个例外：它们既有静态类型又有实例类型。比较一个类类型的两个对象时，仅比较实例的成员，静态成员和构造函数不影响兼容性：

```
class Animal {
  feet: number;
  constructor(name: string, numFeet: number) {}
}

class Size {
  feet: number;
  constructor(numFeet: number) {}
}

let a: Animal;
let s: Size;

a = s; // OK
s = a; // OK
```

##### **类中的私有及受保护成员**

类中的私有成员和受保护成员会影响其兼容性。在检查类实例的兼容性时，如果目标类型包含私有成员，那么源类型也必须包含源自同一类的私有成员。同样，对于具有受保护成员的实例也是如此。这样一来，一个类可以与其父类进行分配兼容，但不能与其他继承层次结构中有相同形状的类进行分配。



#### 6. 范型

因为TypeScript是结构类型系统，所以类型参数仅在作为成员类型的一部分使用时才影响结果类型。例如：

```
interface Empty<T> {}
let x: Empty<number>;
let y: Empty<string>;

x = y;  // OK, because y matches structure of x
```

在上面示例中，`x`和`y`是兼容的，因为它们的结构没有以区别的方式使用类型参数。通过将成员添加到`Empty<T>`来更改此示例，以下是其工作原理：

```
interface NotEmpty<T> {
  data: T;
}
let x: NotEmpty<number>;
let y: NotEmpty<string>;

x = y;  // Error, because x and y are not compatible
```

这样，指定了类型实参的泛型类型就可以像非泛型类型一样工作。

对于未指定类型实参的泛型类型，通过在所有未指定的类型实参的位置指定`any`来检查兼容性。然后，就像在非泛型情况下一样，检查结果类型的兼容性。

例如，

```
let identity = function<T>(x: T): T {
  // ...
}

let reverse = function<U>(y: U): U {
  // ...
}

identity = reverse;  // OK, because (x: any) => any matches (y: any) => any
```



#### 7. 高级话题

##### **子类型与分配**

到目前为止，我们使用了“兼容性”，这不是语言规范中定义的术语。在TypeScript中，有两种兼容性：子类型和赋值。这些区别在于，赋值扩展了子类型与规则的兼容性，以允许与`any`之间以及与`enum`之间的赋值以及相应的数值。

语言中的不同位置会根据情况使用两种兼容机制之一。出于实际目的，类型兼容性由分配兼容性决定，即使在`implements`和`extends`子句的情况下也是如此。

更多详细信息，请参考：[TypeScript spec](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md)。



### 3.15 类型推断（Type Inference）

- [1. 基础](#1. 基础)
- [2. 最佳通用类型](#2. 最佳通用类型)
- [3. 上下文类型](#3. 上下文类型)

在本节中，将介绍TypeScript中的类型推断，也就是将讨论在何处以及如何推断类型。

#### 1. 基础

在TypeScript中，在没有显式类型注释的情况下，有很多地方使用类型推断来提供类型信息。 例如，在此代码中：

```
let x = 3;
```

变量`x`的类型推断为`number`。在初始化变量和成员，设置参数默认值以及确定函数返回类型时会发生这种推断。

大多数情况下，类型推断很简单。接下来，我们将探讨类型推断中的一些细微差别。



#### 2. 最佳通用类型

从多个表达式进行类型推断时，这些表达式的类型将用于计算“最佳通用类型”。 例如：

```
let x = [0, 1, null];
```

上例中推断`x`的类型，我们需要考虑每个数组元素的类型。本例中有两种选择：`number`和`null`。最佳通用类型算法会考虑每个候选类型，并选择与所有其他候选类型兼容的类型。

由于必须从提供的候选类型中选择最合适通用类型，在某些情况下，类型有相同的结构，但是所有候选类型的上级类型都不是一种。例如：

```
let zoo = [new Rhino(), new Elephant(), new Snake()];
```

理想情况下，我们可能希望将`zoo`推断为`Animal[]`，但是由于数组中没有严格属于`Animal`类型的对象，因此我们无法推断数组元素的类型。要更正此问题，可以在没有一个类型是所有其他候选对象的超类型的情况下显式提供该类型：

```
let zoo: Animal[] = [new Rhino(), new Elephant(), new Snake()];
```

如果找不到最佳的通用类型，则会推断结果会是联合数组类型，`(Rhino | Elephant | Snake)[]`。



#### 3. 上下文类型

在TypeScript中，类型推断在某些情况下也可以在“另一个方向”上工作，这称为“上下文类型”。当表达式的类型由其所在位置隐含时，便会发生上下文类型化。例如：

```
window.onmousedown = function(mouseEvent) {
  console.log(mouseEvent.button);   //<- OK
  console.log(mouseEvent.kangaroo); //<- Error!
};
```

在这里，TypeScript类型检查器使用`Window.onmousedown`函数的类型来推断右侧赋值的函数表达式的类型。这样，就可以推断出`mouseEvent`参数的类型，该参数包含`button`属性，但不包含`kangaroo`属性。

TypeScript很智能，也可以推断其他上下文中的类型：

```
window.onscroll = function(uiEvent) {
  console.log(uiEvent.button); //<- Error!
}
```

基于将上述可将函数分配给`Window.onscroll`的事实，TypeScript会知道`uiEvent`是[UIEvent](https://developer.mozilla.org/en-US/docs/Web/API/UIEvent)，而不是上例所示的[MouseEvent](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent)。由于`UIEvent`对象不包含`button`属性，因此TypeScript将触发错误。

如果此函数不在上下文类型的位置，则该函数的参数将隐式地含有`any`类型，并且不会触发错误（除非使用`--noImplicitAny`选项）：

```
const handler = function(uiEvent) {
  console.log(uiEvent.button); //<- OK
}
```

我们还可以显式地将类型信息提供给函数的参数，以覆盖任何上下文类型：

```
window.onscroll = function(uiEvent: any) {
  console.log(uiEvent.button);  //<- Now, no error is given
};
```

但是，此代码将打印为`undefined`，因为`uiEvent`没有名为`button`的属性。

上下文类型在很多情况下都适用。常见的情况包括：函数调用的参数、赋值的右侧、类型断言、对象和数组字面量的成员以及*return*语句。上下文类型还是充当最佳通用类型的候选类型。例如：

```
function createZoo(): Animal[] {
  return [new Rhino(), new Elephant(), new Snake()];
}
```

在此示例中，最佳通用类型是一个有四个选项集合：`Animal`、`Rhino`、`Elephant`和`Snake`。其中，可以通过最佳通用类型算法选择`Animal`。



### 3.16 JavaScript文件类型检查

- [1. 用JSDoc类型表示类型信息](#1. 用JSDoc类型表示类型信息)

- [2. 属性通过类中的赋值语句推断](#2. 属性通过类中的赋值语句推断)

- [3. 构造函数等价于类](#3. 构造函数等价于类)

- [4. 支持*CommonJS*模块](#4. 支持*CommonJS*模块)

- [5. 类、函数、及对象字面量是命名空间](#5. 类、函数、及对象字面量是命名空间)

- [6. 对象字面量是开放式的](#6. 对象字面量是开放式的)

- [7. `null`、`undefined`、和空数组的类型是`any`或`any[\]`](#7. `null`、`undefined`、和空数组的类型是`any`或`any[\]`)

- [8. 函数参数是默认可选的](#8. 函数参数是默认可选的)

- [9. 通过`arguments`推断出的Var-args参数声明](#9. 通过`arguments`推断出的Var-args参数声明s)

- [10. 未指定类型的参数默认是`any`](#10. 未指定类型的参数默认是`any`)

- [11. 支持的JSDoc](#11. 支持的JSDoc)

- - [`@type`]
  - [`@param`和`@returns`]
  - [`@typedef`、`@callback`和`@param`]
  - [`@template`]
  - [`@constructor`]
  - [`@this`]
  - [`@extends`]
  - [`@enum`]

- [12. 更多示例](#12. 更多示例)

- [13. 已不支持的模式](#13. 已不支持的模式)

TypeScript 2.3及更高版本支持使用`--checkJs`对`.js`文件中进行类型检查和报告错误。

可以通过添加`// @ts-nocheck`注释来跳过对某些文件的检查；相反，可以去掉`--checkJs`并添加`// @ts-check`注释以选择仅检查某些`.js`文件。还可以通过在本行之前添加`// @ts-ignore`来忽略本行的错误。注意，如果使用了`tsconfig.json`，则JS检查将遵循一些严格的标志，如：`noImplicitAny`、`strictNullChecks`等。但由于JS检查相对宽松，因此同时使用严格的标记结果可能会令人意外。

以下是下几点对比`.js`文件与`.ts`文件两者在类型检查上的一些差异：

#### 1. 用JSDoc类型表示类型信息

在`.js`文件中，一般可以像在`.ts`文件中一样发进行推断类型。同样，当无法推断类型时，可以使用JSDoc来指定类型，就像`.ts`文件中使用类型注释。也像Typescript，`--noImplicitAny`会在编译器无法推断类型的位置报错。（对象字面量情况除外；有关详细信息，请参见下文。）

JSDoc注释装饰声明的将用于设置该声明的类型。例如：

```
/** @type {number} */
var x;

x = 0; // OK
x = false; // Error: boolean is not assignable to number
```

JSDoc所支持的模式列表，请参考：[JSDoc文档](#JSDoc文档)。



#### 2. 属性通过类中的赋值语句推断

ES2015没有提供类属性声明的规范。属性是动态分配的，就像对象字面量一样。

在`.js`文件中，编译器从类内部的属性分配推断属性类型。属性类型是在构造函数中指定的类型，除非未在其中定义，或者构造函数中指定的是`undefined`或`null`。在这种情况下，类型会是所有赋值类型的联合类型。在构造函数中定义的属性会认为是一直存在的，而仅在方法、*getter*或*setter*中定义的属性被认为是可选的。

```
class C {
  constructor() {
    this.constructorOnly = 0;
    this.constructorUnknown = undefined;
  }
  method() {
    this.constructorOnly = false; // error, constructorOnly is a number
    this.constructorUnknown = "plunkbat"; // ok, constructorUnknown is string | undefined
    this.methodOnly = "ok"; // ok, but methodOnly could also be undefined
  }
  method2() {
    this.methodOnly = true; // also, ok, methodOnly's type is string | boolean | undefined
  }
}
```

如果一个属性从没在类中设置过，其会被当做未知的。如果类有只读属性，应在构造函数中使用JSDoc添加声明，并通过注释指定类型。如果稍后会初始化，甚至不必提供值：

```
class C {
  constructor() {
    /** @type {number | undefined} */
    this.prop = undefined;
    /** @type {number | undefined} */
    this.count;
  }
}

let c = new C();
c.prop = 0; // OK
c.count = "string"; // Error: string is not assignable to number|undefined
```



#### 3. 构造函数等价于类

在ES2015之前，Javascript使用构造函数代替类。编译器支持此模式，并且将构造函数理解为与ES2015类等效。属性推断机制与上述中的规则完全相同。

```
function C() {
  this.constructorOnly = 0;
  this.constructorUnknown = undefined;
}
C.prototype.method = function () {
  this.constructorOnly = false; // error
  this.constructorUnknown = "plunkbat"; // OK, the type is string | undefined
};
```



#### 4. 支持*CommonJS*模块

在`.js`文件中，Typescript支持CommonJS模块。对`export`和`module.exports`的赋值会被认为是导出声明。同样的，会将`require`函数调用识别为模块导入。例如：

```
// same as `import module "fs"`
const fs = require("fs");

// same as `export function readFile`
module.exports.readFile = function (f) {
  return fs.readFileSync(f);
};
```

与Typescript模块相比，Javascript中的模块支持在语法上更宽容。大部分赋值和声明方式都是允许的。



#### 5. 类、函数、及对象字面量是命名空间

`.js`文件中的类是命名空间。这也可用于嵌套类。例如：

```
class C {}
C.D = class {};
```

在ES2015之前，可以用来模拟静态方法：

```
function Outer() {
  this.y = 2;
}
Outer.Inner = function () {
  this.yy = 2;
};
```

还可以用来创建简单的命名空间：

```
var ns = {};
ns.C = class {};
ns.func = function () {};
```

同时还支持其它变体：

```
// IIFE
var ns = (function (n) {
  return n || {};
})();
ns.CONST = 1;

// defaulting to global
var assign =
  assign ||
  function () {
    // code goes here
  };
assign.extra = 1;
```



#### 6. 对象字面量是开放式的

在`.ts`文件中，用于字面量初始化变量时也会声明其类型。不能添加未在原始字面量中指定的新成员。该规则在`.js`文件中放宽；对象字面量有有开放式类型（索引签名），该类型允许添加和访问最初未定义的属性。例如：

```
var obj = { a: 1 };
obj.b = 2; // Allowed
```

对象字面量的行为就像它们具有一个默认的索引签名`[x:string]: any`，可以将它们视为开放的映射，而不是封闭对象。

与其它特殊的JS检查行为一样，可以通过为变量指定JSDoc类型来修改此行为。例如：

```
/** @type {{a: number}} */
var obj = { a: 1 };
obj.b = 2; // Error, type {a: number} does not have property b
```



#### 7. null、undefined、和空数组的类型是any或any[]

任何初始化为`null`或`undefined`的变量、参数或属性，其属性都`any`，即使在严格模式下的`null`检查。任何用`[]`初始化的变量、参数或属性，其属性都`any[]`，即使在严格模式下的`null`检查。唯一例外的是上面有多次初始化的情况：

```
function Foo(i = null) {
  if (!i) i = 1;
  var j = undefined;
  j = 2;
  this.l = [];
}
var foo = new Foo();
foo.l.push(foo.i);
foo.l.push("end");
```



#### 8. 函数参数是默认可选的

由于在ES2015之前，无法在Javascript中为参数指定可选性，因此`.js`文件中的所有函数参数均被视为可选。允许调用时的参数少于声明参数数量。

重要的是要注意，调用使用过多的参数是错误的。

例如：

```
function bar(a, b) {
  console.log(a + " " + b);
}

bar(1); // OK, second argument considered optional
bar(1, 2);
bar(1, 2, 3); // Error, too many arguments
```

JSDoc注释的函数会从此规则中排除。可以通过JSDoc可选参数语法表示可选性。例如：

```
/**
 * @param {string} [somebody] - Somebody's name.
 */
function sayHello(somebody) {
  if (!somebody) {
    somebody = "John Doe";
  }
  console.log("Hello " + somebody);
}

sayHello();
```



#### 9. 通过arguments推断出的Var-args参数声明

如果函数体中有对`arguments`，那么这个函数会被隐式的认为有Var-args参数（如：`(...arg: any[]) => any`）。可以通过JSDoc的var-arg语法来指定`arguments`的类型。

```
/** @param {...number} args */
function sum(/* numbers */) {
  var total = 0;
  for (var i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}
```



#### 10. 未指定类型的参数默认是any

由于在Javascript中没有用于指定范型参数的语法，因此未指定的类型参数默认为`any`。

##### **在\*extends\*语句**

例如，`React.Component`定义为有两个参数，`Props`和`State`。在一个`.js`文件中，没有合法的*extends*语句指定方式。默认参数类型为`any`：

```
import { Component } from "react";

class MyComponent extends Component {
  render() {
    this.props.b; // Allowed, since this.props is of type any
  }
}
```

可以通过JSDoc的`@augments`参数来指定类型。例如：

```
import { Component } from "react";

/**
 * @augments {Component<{a: number}, State>}
 */
class MyComponent extends Component {
  render() {
    this.props.b; // Error: b does not exist on {a:number}
  }
}
```



##### **在JSDoc引用中**

JSDoc中未指定类型的参数默认为`any`：

```
/** @type{Array} */
var x = [];

x.push(1); // OK
x.push("string"); // OK, x is of type Array

/** @type{Array.} */
var y = [];

y.push(1); // OK
y.push("string"); // Error, string is not assignable to number
```



##### **在函数中调用**

对泛型函数的调用使用`arguments`来推断类型参数。有时，这一过程无法推断出类型，主要是因为缺少推断源；在这些情况下，类型参数将默认为`any`。例如：

```
var p = new Promise((resolve, reject) => {
  reject();
});

p; // Promise<any>;
```



#### 11. 支持的JSDoc

下面的列表列出了当前支持的JSDoc注释，你可以JavaScript文件中通过它们来提供类型。

请注意，列表中没列出的标签都还不支持（如：``@async）。

- `@type`
- `@param` (或 `@arg` 或 `@argument`)
- `@returns` (或 `@return`)
- `@typedef`
- `@callback`
- `@template`
- `@class` (或 `@constructor`)
- `@this`
- `@extends` (或 `@augments`)
- `@enum`

它们所表示的含义与*usejsdoc.org*中给出的标记的含义相同，或者是一个超集。下面的代码描述了它们的区别，并给出了每个标签的一些用法示例。



##### **@type**

可以使用`@type`标记并引用类型名称（在TypeScript声明或JSDoc`@typedef`标记中定义的原始类型）。可以使用任何Typescript类型以及大多数JSDoc类型。

```
/**
 * @type {string}
 */
var s;

/** @type {Window} */
var win;

/** @type {PromiseLike<string>} */
var promisedString;

// You can specify an HTML Element with DOM properties
/** @type {HTMLElement} */
var myElement = document.querySelector(selector);
element.dataset.myData = "";
```

`@type`可以指定联合类型，如：`string`和`boolean`类型的联合。

```
/**
 * @type {(string | boolean)}
 */
var sb;
```

注意，括号是可选的。

```
/**
 * @type {string | boolean}
 */
var sb;
```

有多种方式来指定数组类型：

```
/** @type {number[]} */
var ns;
/** @type {Array.<number>} */
var nds;
/** @type {Array<number>} */
var nas;
```

还可以指定对象字面量类型。如，一个有`a`(字符串)和`b`(数字)属性的对象，使用如下语法：

```
/** @type {{ a: string, b: number }} */
var var9;
```

可以使用标准的JSDoc语法或TypeScript语法，使用字符串和数字索引签名指定类似Map的对象和类似于数组的对象。

```
/**
 * A map-like object that maps arbitrary `string` properties to `number`s.
 *
 * @type {Object.<string, number>}
 */
var stringToNumber;

/** @type {Object.<number, object>} */
```

前面两种类型等同于TypeScript类型`{ [x: string]: number }`和`{ [x: number]: any }`。编译器识别出这两种语法。

可以使用TypeScript或Closure语法指定函数类型

```
/** @type {function(string, boolean): number} Closure syntax */
var sbn;
/** @type {(s: string, b: boolean) => number} Typescript syntax */
var sbn2;
```

或者可以直接使用`Function`类型。

```
/** @type {Function} */
var fn7;
/** @type {function} */
var fn6;
```

Closure中的其它类型也可以使用：

```
/**
 * @type {*} - can be 'any' type
 */
var star;
/**
 * @type {?} - unknown type (same as 'any')
 */
var question;
```

**转换**

TypeScript借签了Closure中的强制转换语法。可以通过在任何带括号的表达式之前添加`@type`标记，将类型转换为其他类型。

```
/**
 * @type {number | string}
 */
var numberOrString = Math.random() < 0.5 ? "hello" : 100;
var typeAssertedNumber = /** @type {number} */ (numberOrString);
```

**导入类型**

也可以使用导入类型从其它文件导入声明。此语法是TypesSript特有的，并且与JSDoc标准不同：

```
/**
 * @param p { import("./a").Pet }
 */
function walk(p) {
  console.log(`Walking ${p.name}...`);
}
```

导入类型也可以类型别名声明中使用：

```
/**
 * @typedef { import("./a").Pet } Pet
 */

/**
 * @type {Pet}
 */
var myPet;
myPet.name;
```

如果不知道导入类型，或者如果导入的类型不易识别，则可以使用导入类型从模块获取值的类型：

```
/**
 * @type {typeof import("./a").x }
 */
var x = require("./a").x;
```



##### **@param和@returns**

`@param`的语法与`@returns`相同，但增加了一参数名。使用`[]`可以把参数声名为可选的：

```
// Parameters may be declared in a variety of syntactic forms
/**
 * @param {string}  p1 - A string param.
 * @param {string=} p2 - An optional param (Closure syntax)
 * @param {string} [p3] - Another optional param (JSDoc syntax).
 * @param {string} [p4="test"] - An optional param with a default value
 * @return {string} This is the result
 */
function stringsStringStrings(p1, p2, p3, p4) {
  // TODO
}
```

函数的返回类型也类似：

```
/**
 * @return {PromiseLike<string>}
 */
function ps() {}

/**
 * @returns {{ a: string, b: number }} - May use '@returns' as well as '@return'
 */
function ab() {}
```



##### **@typedef、@callback和@param**

`@typedef`可以用来声明复杂类型，语法与`@param`类似。

```
/**
 * @typedef {Object} SpecialType - creates a new type named 'SpecialType'
 * @property {string} prop1 - a string property of SpecialType
 * @property {number} prop2 - a number property of SpecialType
 * @property {number=} prop3 - an optional number property of SpecialType
 * @prop {number} [prop4] - an optional number property of SpecialType
 * @prop {number} [prop5=42] - an optional number property of SpecialType with default
 */
/** @type {SpecialType} */
var specialTypeObject;
```

可以在第一行上使用`object`或`Object`。

```
/**
 * @typedef {object} SpecialType1 - creates a new type named 'SpecialType1'
 * @property {string} prop1 - a string property of SpecialType1
 * @property {number} prop2 - a number property of SpecialType1
 * @property {number=} prop3 - an optional number property of SpecialType1
 */
/** @type {SpecialType1} */
var specialTypeObject1;
```

`@param`允许使用类似的语法。注意，嵌套的属性名必须使用参数名做为前缀：

```
/**
 * @param {Object} options - The shape is the same as SpecialType above
 * @param {string} options.prop1
 * @param {number} options.prop2
 * @param {number=} options.prop3
 * @param {number} [options.prop4]
 * @param {number} [options.prop5=42]
 */
function special(options) {
  return (options.prop4 || 1001) + options.prop5;
}
```

`@callback`与`@typedef`相似，但它可以指定函数类型而不是对象类型：

```
/**
 * @callback Predicate
 * @param {string} data
 * @param {number} [index]
 * @returns {boolean}
 */
/** @type {Predicate} */
const ok = (s) => !(s.length % 2);
```

当然，所有这些类型都可以使用TypeScript的`@typedef`语法在同一行上声明：

```
/** @typedef {{ prop1: string, prop2: string, prop3?: number }} SpecialType */
/** @typedef {(data: string, index?: number) => boolean} Predicate */
```



##### **@template**

通过`@template`标签声明泛型类型：

```
/**
 * @template T
 * @param {T} x - A generic parameter that flows through to the return type
 * @return {T}
 */
function id(x) {
  return x;
}
```

使用逗号或多个标签来声明多个类型参数：

```
/**
 * @template T,U,V
 * @template W,X
 */
```

还可以在类型参数名称之前指定类型约束。仅列表中第一个类型参数受约束：

```
/**
 * @template {string} K - K must be a string or string literal
 * @template {{ serious(): string }} Seriousalizable - must have a serious method
 * @param {K} key
 * @param {Seriousalizable} object
 */
function seriousalize(key, object) {
  // ????
}
```



##### **@constructor**

编译器会根据`this`属性的赋值来推断构造函数，但可以添加`@constructor`标记以使检查更严格、提示更完善：

```
/**
 * @constructor
 * @param {number} data
 */
function C(data) {
  this.size = 0;
  this.initialize(data); // Should error, initializer expects a string
}
/**
 * @param {string} s
 */
C.prototype.initialize = function (s) {
  this.size = s.length;
};

var c = new C(0);
var result = C(1); // C should only be called with new
```

通过`@constructor`，会在构造函数`C`中检查`this`，因此你会在`initialize`方法中得到一个提示，如果传递给它一个数字，则会得到一个错误。如果直接调用`C`而不是构造它，也会收到错误。

不幸的是，这意味着那些即能构造也能直接调用的构造函数不能使用`@constructor`。



##### **@this**

通常编译器可以根据上下文来推断`this`的类型。但可以通过`@this`来指定其类型：

```
/**
 * @this {HTMLElement}
 * @param {*} e
 */
function callbackForLater(e) {
  this.clientHeight = parseInt(e); // should be fine!
}
```



##### **@extends**

当Javascript类扩展通用基类时，没有地方指定类型参数的类型。`@extends`标记为该类型参数提供了一个位置：

```
/**
 * @template T
 * @extends {Set<T>}
 */
class SortableSet extends Set {
  // ...
}
```

注意，`@extends`仅适用于类。当前，构造函数无法扩展类。



##### **@enum**

`@enum`使你可以创建对象字面量，其类型都是确定的类型。与JavaScript中的大多数对象字面量不同，它不允许添加额外成员。

```
/** @enum {number} */
const JSDocState = {
  BeginningOfLine: 0,
  SawAsterisk: 1,
  SavingComments: 2,
};
```

注意，`@enum`与TypeScript中的`enum`不同，它更加简单。但不同于TypeScript的枚举，`@enum`可以是任何类型：

```
/** @enum {function(number): number} */
const Math = {
  add1: (n) => n + 1,
  id: (n) => -n,
  sub1: (n) => n - 1,
};
```



#### 12. 更多示例

```
var someObj = {
  /**
   * @param {string} param1 - Docs on property assignments work
   */
  x: function (param1) {},
};

/**
 * As do docs on variable assignments
 * @return {Window}
 */
let someFunc = function () {};

/**
 * And class methods
 * @param {string} greeting The greeting to use
 */
Foo.prototype.sayHi = (greeting) => console.log("Hi!");

/**
 * And arrow functions expressions
 * @param {number} x - A multiplier
 */
let myArrow = (x) => x * x;

/**
 * Which means it works for stateless function components in JSX too
 * @param {{a: string, b: number}} test - Some param
 */
var fc = (test) => <div>{test.a.charAt(0)}</div>;

/**
 * A parameter can be a class constructor, using Closure syntax.
 *
 * @param {{new(...args: any[]): object}} C - The class to register
 */
function registerClass(C) {}

/**
 * @param {...string} p1 - A 'rest' arg (array) of strings. (treated as 'any')
 */
function fn10(p1) {}

/**
 * @param {...string} p1 - A 'rest' arg (array) of strings. (treated as 'any')
 */
function fn9(p1) {
  return p1.join();
}
```



#### 13. 已不支持的模式

除非对象也创建类型（如：构造函数），否则在值空间中将对象视为类型是不可以的。

```
function aNormalFunction() {}
/**
 * @type {aNormalFunction}
 */
var wrong;
/**
 * Use 'typeof' instead:
 * @type {typeof aNormalFunction}
 */
var right;
```

对象字面量上的属性类型上的`=`后缀不能指定这个属性是可选的：

```
/**
 * @type {{ a: string, b: number= }}
 */
var wrong;
/**
 * Use postfix question on the property name instead:
 * @type {{ a: string, b?: number }}
 */
var right;
```

可空类型（*Nullable*）仅在启用了`strictNullChecks`时才起作用：

```
/**
 * @type {?number}
 * With strictNullChecks: true -- number | null
 * With strictNullChecks: off  -- number
 */
var nullable;
```

非空类型没有意义，它们被当作原始类型对待：

```
/**
 * @type {!number}
 * Just has type number
 */
var normal;
```

与JSDoc的类型系统不同，TypeScript仅允许将类型标记为包含`null`或不包含`null`。没有显式的不可为空性—如果*strictNullChecks*启用，则`number`不可为空。如果关闭，则`number`可以为空。



### 3.17 TypeScript 与DOM操作（TypeScript & the DOM）

- [1. DOM操作](#1. DOM操作)
- [2. 基本示例](#2. 基本示例)
- [3. 文档接口](#3. 文档接口)
- [4. Node接口]#4. Node接口)
- [5. *child*和*childNodes*之间的区别](#5. *child*和*childNodes*之间的区别)
- [6. `querySelector`与`querySelectorAll`方法](#6. `querySelector`与`querySelectorAll`方法)
- [7. 了解更多](#7. 了解更多)

#### 1. DOM操作

*HTMLElement类型的探索：*

自标准化以来的20多年来，JavaScript已经走了很长一段路。尽管在2020年，JavaScript可以在服务器、数据科学甚至IoT设备上使用，但请记住其最流行的用例：Web浏览器。

网站由HTML和/或XML文档组成，这些文件是静态的，它们不会变动。*文档对象模型（DOM）*是由浏览器实现的编程接口，目的是使静态网站正常运行。DOM API可用于修改文档结构、样式和内容。该API非常强大，以至于围绕它开发了很多的前端框架（`jQuery`、`React`、`Angular`等），以使动态网站的开发更加容易。

TypeScript是JavaScript的类型化超集，它包含了DOM API的类型定义。这些定义可以在任何默认的TypeScript项目中轻松获得。在`lib.dom.d.ts`中的20,000+的定义行中，其中有一个：`HTMLElement`。此类型是使用TypeScript进行DOM操作的基础。

关于DOM类型定义的源码请参考：[lib.dom.d.ts](https://github.com/microsoft/TypeScript/blob/master/lib/lib.dom.d.ts)。



#### 2. 基本示例

以下是一个简单的`index.html`文件：

```
<!DOCTYPE html>
<html lang="en">
  <head><title>TypeScript Dom Manipulation</title></head>
  <body>
    <div id="app"></div>
        <!-- Assume index.js is the compiled output of index.ts -->
    <script src="index.js"></script>
  </body>
</html>
```

然后通过TypeScript添加`<p>Hello, World</p>`到`#app`元素中：

```
// 1. Select the div element using the id property
const app = document.getElementById("app");

// 2. Create a new <p></p> element programmatically
const p = document.createElement("p");

// 3. Add the text content
p.textContent = "Hello, World!";

// 4. Append the p element to the div element
app?.appendChild(p);
```

编译并运行`index.html`页面，结果为：

```
<div id="app">
  <p>Hello, World!</p>
</div>
```



#### 3. 文档接口

TypeScript代码中的第一行使用了全局变量`document`，检查该变量是否存在由`lib.dom.d.ts`文件中的`Document`接口定义。示例中包含了两个方法的调用：`getElementById`和`createElement`。

向其传递元素的ID，它会返回`HTMLElement`或`null`。此方法中引用了最重要的类型之一`HTMLElement`。它会充当所有其它元素接口的基础接口。例如，示例中的`p`变量的类型为`HTMLParagraphElement`。另外需要注意，此方法可以返回`null`。因为，如果该方法是否能够找到指定的元素，其无法在运行前确定。示例代码中的最后一行，使用了新的*可选链接运算符*来调用`appendChild`。

```
Document.getElementById
```

方法定义如下：

```
getElementById(elementId: string): HTMLElement | null;
Document.createElement
```

方法定义如下：

```
createElement<K extends keyof HTMLElementTagNameMap>(tagName: K, options?: ElementCreationOptions): HTMLElementTagNameMap[K];
createElement(tagName: string, options?: ElementCreationOptions): HTMLElement;
```

这是一个重载的函数定义。第二次重载非常最简单，并且类似于`getElementById`方法。向其传递任何`string`，其会返回标准的`HTMLElement`。此定义使开发人员能够创建唯一的HTML元素标签。

如`document.createElement('xyz')`会返回`<xyz></xyz>`元素，这显然不是HTML规范中的元素。

*如果需要使用该元素，就可以通过`document.getElementsByTagName`*获取元素。

对于`createElement`的第一个定义，它使用了一些高级通用模式。最好将其按块分解。从通用表达式开始：`<K extends keyof HTMLElementTagNameMap>`。该表达式定义了一个通用参数`K`，该参数被限制于`HTMLElementTagNameMap`接口的键中。映射接口包含每个指定的HTML标记名称及其对应的类型接口。例如，这是前5个映射值：

```
interface HTMLElementTagNameMap {
  "a": HTMLAnchorElement;
  "abbr": HTMLElement;
  "address": HTMLElement;
  "applet": HTMLAppletElement;
  "area": HTMLAreaElement;
    ...
}
```

有些元素没有唯一的属性，因此它们仅返回`HTMLElement`，而其他类型的确具有唯一的属性和方法，因此它们返回其特定的接口（会从`HTMLElement`扩展或实现）。

现在，对于其余的`createElement`定义：`(tagName: K, options?: ElementCreationOptions): HTMLElementTagNameMap[K]`。第一个参数`tagName`定义为通用参数`K`。TypeScript解释器足够聪明，可以从此参数推断出通用参数。这意味着开发人员在使用该方法时并不需要指定泛型参数。传递给`tagName`参数的任何值都将推断为`K`，所以可以在定义的其余部分中使用。那么，发生了什么；返回值`HTMLElementTagNameMap[K]`使用`tagName`参数，并使用它返回相应的类型。



#### 4. Node接口

`document.getElementById`函数会返回`HTMLElement`。`HTMLElement`接口扩展了`Element`接口，而`Element`接口扩展了`Node`接口。此原型扩展允许所有`HTMLElement`使用标准方法的子集。在示例代码中，我们使用在`Node`接口上定义的属性将新的`p`元素附加到网站。

```
Node.appendChild
```

代码中最后一行是`app?.appendChild(p)`。前面的`document.getElementById`部分详细介绍了此处使用的可选链接运算符，因为`app`在运行时可能为`null`。`appendChild`方法由以下方式定义：

```
appendChild<T extends Node>(newChild: T): T;
```

该方法与`createElement`方法的工作方式类似，因为从`newChild`参数推断出通用参数`T`。`T`被限制为另一个基本接口`Node`。



#### 5. *child*和*childNodes*之间的区别

以前，文档详细介绍了`HTMLElement`接口，该接口从`Element`扩展，而`Element`从`Node`扩展。在DOM API中，有子元素的概念。例如，在以下HTML中，`p`标签是`div`元素的子元素：

```
<div>
  <p>Hello, World</p>
  <p>TypeScript!</p>
</div>;

const div = document.getElementByTagName("div")[0];

div.children;
// HTMLCollection(2) [p, p]

div.childNodes;
// NodeList(2) [p, p]
```

获取`div`素后，子元素会返回包含`HTMLParagraphElements`的`HTMLCollection`列表。`childNodes`属性会返回类似`NodeList`的节点列表。每个`p`标签仍是`HTMLParagraphElements`类型，但是`NodeList`可以包含`HTMLCollection`列表中没有的其他HTML节点。

通过删除`p`标签之修改html，但保留文本。

```
<div>
  <p>Hello, World</p>
  TypeScript!
</div>;

const div = document.getElementByTagName("div")[0];

div.children;
// HTMLCOllection(1) [p]

div.childNodes;
// NodeList(2) [p, text]
```

我们看一下两个列表是是怎样更改的。`children`现在仅包含`<p>Hello, World</p>`元素，并且`childNodes`包含`text`节点，而不是两个`p`节点。`NodeList`的`text`部分是包含文本`TypeScript!`的节点。`children`列表不包含`Node`，因为它不被视为`HTMLElement`。



#### 6. querySelector与querySelectorAll方法

这两种方法都是获取适合dom元素列表的出色工具。它们在`lib.dom.d.ts`中定义为：

```
/**
 * Returns the first element that is a descendant of node that matches selectors.
 */
querySelector<K extends keyof HTMLElementTagNameMap>(selectors: K): HTMLElementTagNameMap[K] | null;
querySelector<K extends keyof SVGElementTagNameMap>(selectors: K): SVGElementTagNameMap[K] | null;
querySelector<E extends Element = Element>(selectors: string): E | null;

/**
 * Returns all element descendants of node that match selectors.
 */
querySelectorAll<K extends keyof HTMLElementTagNameMap>(selectors: K): NodeListOf<HTMLElementTagNameMap[K]>;
querySelectorAll<K extends keyof SVGElementTagNameMap>(selectors: K): NodeListOf<SVGElementTagNameMap[K]>;
querySelectorAll<E extends Element = Element>(selectors: string): NodeListOf<E>;
```

`querySelectorAll`的定义与`getElementByTagName`相似，不同点在于它会返回一个新类型：`NodeListOf`。这一返回类型本质上是标准JavaScript list元素的自定义实现。可以说，用`E[]`替换`NodeListOf<E&t;`会有类似的用户体验。`NodeListOf`仅的属性和方法有：`lengt`、`item(index)`、`forEach((value，key，parent) => void)`和数字索引。另外，方法会返回元素列表，而不是节点列表，这是`NodeList`从`.childNodes`方法返回的内容。虽然这看起来可能有所差异，但要注意接口`Element从Node`扩展。

查看这些方法的实际应用，请将代码修改为：

```
<ul>
  <li>First :)</li>
  <li>Second!</li>
  <li>Third times a charm.</li>
</ul>;

const first = document.querySelector("li"); // returns the first li element
const all = document.querySelectorAll("li"); // returns the list of all li elements
```



#### 7. 了解更多

`lib.dom.d.ts`类型定义的好处在于，它们反映了Mozilla（MDN）文档中注释的类型。例如，MDN[HTMLElement页面](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)`HTMLElement`页面关于HTMLElement接口的说明。这些页面列出了所有可用的属性、方法，甚至还列出了示例。 这些页面的另一个重要方面是它们提供了指向相应标准文档的链接。参考：[W3关于HTMLElement建议的链接](https://www.w3.org/TR/html52/dom.html#htmlelement)。

相关资源：

- ECMA-262标准：http://www.ecma-international.org/ecma-262/10.0/index.html#Title
- DOM介绍: [https://developer.mozilla.org/en-US/docs/Web/API/Document*Object*Model/Introduction](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)



### 3.18 变量声明（Variable Declarations）

- [1. var声明](#1. var声明)
  - [作用域规则]
  - [变量捕获怪癖]
- [2. let声明](#2. `let`声明)
  - [块级作用域]
  - [重新声明和阴影]
  - [块级变量捕获]
- [3. const声明](#3. 声明)
- [4. let与const](#4. let与const)
- [5. 解构](#5. 解构)
  - [数组解构]
  - [元组解构]
  - [对象解构]
- [6. 展开](#6. 展开)

`let`和`const`是JavaScript中两种相对较新的变量声明类型。正如我们前面提到的，`let`在某些方面类似于`var`，但是使用户可以避免在JavaScript中遇到的一些常见“陷阱”。

`const`是`let`的增强，因为它可以防止重新给变量赋值。

由于TypeScript是JavaScript的扩展，因此该语言自然支持`let`和`const`。在这里，我们将详细说明这些新声明及为什么它们比`var`更可取。

如果你直接使用过JavaScript，那么本节可能是刷新认知的好方法。如果你对JavaScript中的`var`声明的所有怪癖都非常熟悉，则可以跳过本节

#### 1. var声明

在传统的JavaScript中，声明变量始终使用`var`关键字：

```
var a = 10;
```

如上所示，我们刚刚声明了一个名为`a`的变量，其值为`10`。

我们还可以在函数内部声明变量：

```
function f() {
  var message = "Hello, world!";

  return message;
}
```

还可以在内部函数中访问相关的变量：

```
function f() {
  var a = 10;
  return function g() {
    var b = a + 1;
    return b;
  };
}

var g = f();
g(); // returns '11'
```

以上，我们在`f`函数中定义了一个变量`a`，该变量在函数`g`的任何位置都可以访问。即使在`f`完成运行后调用`g`，它也将能够访问和修改`a`。

```
function f() {
  var a = 1;

  a = 2;
  var b = g();
  a = 3;

  return b;

  function g() {
    return a;
  }
}

f(); // returns '2'
```

##### **作用域规则**

`var`声明相对于其他语言使用的规则有一些奇怪的作用域规则。请看以下示例：

```
function f(shouldInitialize: boolean) {
  if (shouldInitialize) {
    var x = 10;
  }

  return x;
}

f(true); // returns '10'
f(false); // returns 'undefined'
```

在这个示例中，变量`x`在`if`块内声明，但是我们仍然可以从该块外部访问它。这是因为`var`声明可在其包含函、模块、命名空间或全局范围内的任何位置访问。有人将其称为`var 作用域``函数作用域`。参数也在函数范围内。

这些范围规则可能会导致几类的错误。尤其是多次声明相同的变量不是错误，会导致问题加剧：

```
function sumMatrix(matrix: number[][]) {
  var sum = 0;
  for (var i = 0; i < matrix.length; i++) {
    var currentRow = matrix[i];
    for (var i = 0; i < currentRow.length; i++) {
      sum += currentRow[i];
    }
  }

  return sum;
}
```

以上示例中，内部的`for`循环会意外覆盖变量`i`，因为`i`引用是同一作用域变量。



##### **变量捕获怪癖**

快速猜测以下代码段的输出是什么：

```
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 100 * i);
}
```

不熟悉的人可能会认为，`setTimeout`会在指定时间后执行一个函数。

其实，其输出是这样的：

```
10
10
10
10
10
10
10
10
10
10
```

许多JavaScript开发人员都非常熟悉这种行为。但大多数人期望输出是：

```
0
1
2
3
4
5
6
7
8
9
```

正如前面提到的有关变量捕获的内容所说。我们传递给`setTimeout`的每个函数表达式实际上都来自同一作用域中的相同`i`。

也就是说，`setTimeout`将在几毫秒后运行一个函数，但是仅在`for`循环停止执行之后；到`for`循环停止执行时，`i`的值为`10`。因此，每次调用指定的函数时，其都会输出`10`！

常见的解决方法是使用IIFE（立即调用函数表达式，也就闭包）在每次迭代中捕获`i`：

```
for (var i = 0; i < 10; i++) {
  // capture the current state of 'i'
  // by invoking a function with its current value
  (function(i) {
    setTimeout(function() {
      console.log(i);
    }, 100 * i);
  })(i);
}
```

这种看起来很奇怪的模式实际上很常见。参数列表中的`i`实际上会覆盖在`for`循环中声明的`i`，但是由于我们将它们命名为相同的名称，从而不必对循环体进行太多修改。



#### 2. let声明

到此，你已经发现了`var`存在一些问题，这就是为什么引入`let`语句的原因。除了所使用关键字不同外，`let`语句的编写方式与`var`语句的编写方式相同。

```
let hello = "Hello!";
```

关键区别不在于语法，而在于语义，接下来我们将深入探讨语义。

##### **块级作用域**

当使用`let`声明一个变量时，它使用词法作用域或块级作用域。与用`var`声明的变量的范围泄漏到其包含函数不同，在其最近的包含块或`for`循环之外块作用域变量不可见。

```
function f(input: boolean) {
  let a = 100;

  if (input) {
    // Still okay to reference 'a'
    let b = a + 1;
    return b;
  }

  // Error: 'b' doesn't exist here
  return b;
}
```

在这里，我们定义了`a`和`b`两个局部变量。`a`的作用范围仅限于`f`的函数主体，而`b`的作用范围仅限于其被包含的`if`语句块。

在`catch`子句中声明的变量也有类似的作用域规则。

```
try {
  throw "oh no!";
} catch (e) {
  console.log("Oh well.");
}

// Error: 'e' doesn't exist here
console.log(e);
```

块范围变量的另一个特性是，在实际声明它们之前，不能对其进行读写。尽管这些变量在其整个范围内都“存在”，但直到声明它们之前的所有时间点都不可见。也就是说你不能在`let`语句之前访问它们。

```
a++; // illegal to use 'a' before it's declared;
let a;
```

需要注意的是，你仍然可以在声明之前捕获块范围的变量。唯一的问题是在声明之前调用该函数是非法的。如果是在ES2015中，则会引发运行时错误；但是，在TypeScript中是允许的，因此不会将其报告为错误。

```
function foo() {
  // okay to capture 'a'
  return a;
}

// illegal call 'foo' before 'a' is declared
// runtimes should throw an error here
foo();

let a;
```

更多相关信息，请参考：[Mozilla中对`let`的介绍](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let)。



##### **重新声明和阴影**

对于`var`声明，声明变量多少次无关紧要，你只会得到一个。

```
function f(x) {
  var x;
  var x;

  if (true) {
    var x;
  }
}
```

在上面的示例中，`x`的所有声明实际上都引用相同的`x`，这是完全有效的。这通常会成为错误的来源，而`x`声明并不会那么宽容。

```
let x = 10;
let x = 20; // error: can't re-declare 'x' in the same scope
```

并不需要TypeScript都对变量进行块作用域分析，以告诉我们存在问题。

```
function f(x) {
  let x = 100; // error: interferes with parameter declaration
}

function g() {
  let x = 100;
  var x = 100; // error: can't have both declarations of 'x'
}
```

这并不是说永远不能使用函数范围的变量来声明相同的块范围的变量，只需在明显不同的块中声明块范围的变量。

```
function f(condition, x) {
  if (condition) {
    let x = 100;
    return x;
  }

  return x;
}

f(false, 0); // returns '0'
f(true, 0); // returns '100'
```

在更嵌套的范围内引入新名称的行为称为*阴影*(*shadowing*)。它像一把双刃剑，因为它可能在意外阴影的情况下自行引入某些错误，同时还可以防止某些错误。例如，假设我们已经使用`let`变量定义了更早的`sumMatrix`函数。

```
function sumMatrix(matrix: number[][]) {
  let sum = 0;
  for (let i = 0; i < matrix.length; i++) {
    var currentRow = matrix[i];
    for (let i = 0; i < currentRow.length; i++) {
      sum += currentRow[i];
    }
  }

  return sum;
}
```

这一版本的循环实际上将正确执行求和，因为内部循环的`i`屏蔽了外部循环中的`i`。

为了使编写的代码更清晰，通常应避免阴影。虽然在某些情况下可以利用它，但是你应该有一个最佳的判断。



##### **块级变量捕获**

当我们第一次谈到使用`var`声明变量进行捕获时，我们简要地介绍了变量被捕获后的行为。为了更好地理解这一点，每次运行时，都会创建变量的“环境”。该环境及其捕获的变量，即使在其范围内的所有内容完成执行之后也可以存在。

```
function theCityThatAlwaysSleeps() {
  let getCity;

  if (true) {
    let city = "Seattle";
    getCity = function() {
      return city;
    };
  }

  return getCity();
}
```

由于我们是从运行环境中捕获`city`的，因此尽管`if`块已完成执行，我们仍然可以访问它。

回想一下，在我们前面的`setTimeout`示例中，最终需要使用IIFE来为`for`循环的每次迭代捕获变量的状态。实际上，我们是为所捕获的变量创建一个新的变量环境。这有点痛苦，但是幸运的是，在TypeScript中不必再这样做。

当声明为循环的一部分时，`let`声明的行为会大不相同。

这些声明不仅为循环本身引入了新的环境，还为每次迭代创建了新的作用域。由于无论如何我们都是通过IIFE进行此操作，因此我们可以将旧的`setTimeout`示例更改为仅使用`let`声明。

```
for (let i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 100 * i);
}
```

这将会符合预期的输出如下：

```
0
1
2
3
4
5
6
7
8
9
```



#### 3. const声明

`const`是另一种变量声明方法。

```
const numLivesForCat = 9;
```

它与`let`声明类似，但是，顾名思义，绑定后就无法更改其值。也就是说，它们具有与`let`相同的作用域规则，但是无法对其重新赋值。

但这并是说它们所引用的值是不可变的。

```
const numLivesForCat = 9;
const kitty = {
  name: "Aurora",
  numLives: numLivesForCat
};

// Error
kitty = {
  name: "Danielle",
  numLives: numLivesForCat
};

// all "okay"
kitty.name = "Rory";
kitty.name = "Kitty";
kitty.name = "Cat";
kitty.numLives--;
```

除非通过特定措施来避免，否则`const`变量的内部状态仍是可以修改的。而TypeScript允许你指定对象的成员为`readonly`。相关详细信息请参见[接口章节](#接口章节)。



#### 4. let与const

由于有两种类似范围语义的声明，很自然地你会问自己应使用哪一种，这时应该根据具体情况来判断。

根据[最小特权原则](#最小特权原则)，除计划修改的那些声明外，所有其他声明都应使用`const`。这样做的理由是，如果不需要写入变量，则在同一代码库上工作的其他人不应能够写入该对象，并且需要考虑是否确实需要将其重新分配给该变量。使用`const`还可以在推断数据流时使代码更可预测。



#### 5. 解构

TypeScript有另一个ECMAScript 2015的功能是“解构”，相关的完整参考，请参阅[Mozilla上的文章](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)。在本节中，我们会简要概述。

##### **数组解构**

解构的最简单形式是数组解构分配：

```
let input = [1, 2];
let [first, second] = input;
console.log(first); // outputs 1
console.log(second); // outputs 2
```

这将创建两个名为`first`和`second`的新变量。这与使用索引等效，但是更加方便：

```
first = input[0];
second = input[1];
```

解构也可以使用已经声明的变量：

```
// swap variables
[first, second] = [second, first];
```

也可以在函数参数中使用：

```
function f([first, second]: [number, number]) {
  console.log(first);
  console.log(second);
}
f([1, 2]);
```

还可以使用`...`（剩余操作符）语法为数组中的剩余项目创建变量：

```
let [first, ...rest] = [1, 2, 3, 4];
console.log(first); // outputs 1
console.log(rest); // outputs [ 2, 3, 4 ]
```

因为是JavaScript，因此可以忽略不需要的尾随元素：

```
let [first] = [1, 2, 3, 4];
console.log(first); // outputs 1
```

或其它元素：

```
let [, second, , fourth] = [1, 2, 3, 4];
console.log(second); // outputs 2
console.log(fourth); // outputs 4
```



##### **元组解构**

元组可以像数组一样被解构；解构变量会获取相应的元组元素的类型：

```
let tuple: [number, string, boolean] = [7, "hello", true];

let [a, b, c] = tuple; // a: number, b: string, c: boolean
```

解构超出元组元素范围会引发错误：

```
let [a, b, c, d] = tuple; // Error, no element at index 3
```

与数组一样，可以使用`...`来解构其余的元组，以获得较短的元组：

```
let [a, ...bc] = tuple; // bc: [string, boolean]
let [a, b, c, ...d] = tuple; // d: [], the empty tuple
```

或忽略尾随元素或其他元素：

```
let [a] = tuple; // a: number
let [, b] = tuple; // b: string
```



##### **对象解构**

也可对对象解构：

```
let o = {
  a: "foo",
  b: 12,
  c: "bar"
};
let { a, b } = o;
```

这会从`o.a`和`o.b`创建新的变量`a`和`b`。请注意，如果不需要，可以跳过`c`。

像数组解构一样，可以直接赋值而无需声明：

```
({ a, b } = { a: "baz", b: 101 });
```

注意，必须用括号将这个语句括起来。JavaScript通常会将`{`解析为块的开始。

你可以使用以下语法为对象中的其余项创建变量：

```
let { a, ...passthrough } = o;
let total = passthrough.b + passthrough.c.length;
```

*属性重命名*

可以为属性指定一个不同的名称：

```
let { a: newName1, b: newName2 } = o;
```

以上，我们可以将`a: newName1`理解为“`a`做为`newName1`”。就像：

```
let newName1 = o.a;
let newName2 = o.b;
```

令人困惑的是，这里的冒号并没有指定类型。如果指定了类型，则在整个解构之后仍需要编写类型：

```
let { a, b }: { a: string, b: number } = o;
```

*默认值*

默认值可以在属性未定义时指定一个默认值：

```
function keepWholeObject(wholeObject: { a: string, b?: number }) {
  let { a, b = 1001 } = wholeObject;
}
```

在这个示例中`b?`表示`b`是可选的，因此可能是不确定的。`keepWholeObject`现在有一个用于`wholeObject`的变量以及属性`a`和`b`，即使`b`未定义。



##### **函数声明**

解构同样可用于函数声明：

```
type C = { a: string, b?: number }
function f({ a, b }: C): void {
  // ...
}
```

但对于参数而言，指定默认值更为常见，并且通过解构正确获取默认值可能比较难处理。首先，需要记住将模式放在默认值之前：

```
function f({ a="", b=0 } = {}): void {
  // ...
}
f();
```

然后，你需要记住为非结构化属性（而不是主初始化程序）提供可选属性的默认值。请记住，`C`是使用可选的`b`定义的：

```
function f({ a, b = 0 } = { a: "" }): void {
  // ...
}
f({ a: "yes" }); // ok, default b = 0
f(); // ok, default to { a: "" }, which then defaults b = 0
f({}); // error, 'a' is required if you supply an argument
```

应小心使用解构。如前面的示例所示，除了最简单的解构表达式之外，其他任何东西都令人困惑。对于深度嵌套的解构尤其如此，即使不依赖重命名、默认值和类型注释，也很难理解。尝试使解构表达式小而简单。 您总是可以编写解构会产生自己的任务



#### 6. 展开

展开操作(`spread`)与解构相反。它允许你将一个数组散布到另一个数组中，或将一个对象散布到另一个对象中。例如：

```
let first = [1, 2];
let second = [3, 4];
let bothPlus = [0, ...first, ...second, 5];
```

这使`bothPlus`的值为`[0、1、2、3、4、5]`。展开会创建`first`和`second`的浅复制副本。其自身不会因展开而改变。

还可以展开对象：

```
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { ...defaults, food: "rich" };
```

现在`search`为`{ food: "rich", price: "$$", ambiance: "noisy" }`。对象展开比数组展开更复杂。 像数组展开一样，它是从左到右进行，但是结果仍然是一个对象。这意味着，在展开对象中位于后面的属性将覆盖之前的属性。因此，如果我们修改前面的示例以在最后展开：

```
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { food: "rich", ...defaults };
```

这时，`food`属性会被`defaults`中的值重写。在本例中，这并不是我们所期望的。

对象展开还有一些限制。首先，它仅包含对象自己的可枚举属性。这意味着你在展开对象实例时会丢失方法：

```
class C {
  p = 12;
  m() {}
}
let c = new C();
let clone = { ...c };
clone.p; // ok
clone.m(); // error!
```

其次，TypeScript编译器不允许泛型函数展开类型参数，该功能将在未来版本中提供。