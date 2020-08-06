## 概念

TypeScript 是 JavaScript 的一个超集，主要提供了可用于静态类型检查的类型系统和对 ES6 的支持，它由 Microsoft 开发，代码开源于 GitHub 上。

类：定义了一件事物的抽象特点，包含它的属性和方法。ts 中可以使用 `public` 、`private`、`protected`

接口：对象形状的描述，或对类一部分行为的描述（门、车、报警器的例子）[类与接口](https://ts.xcatliu.com/advanced/class-and-interfaces.html)

枚举：用于取值被限定在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等。

类型推论：如果没有明确的指定类型，那么 TypeScript 会依照类型推论（Type Inference）的规则推断出一个类型。

泛型：指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。

## 优缺点

优点

1. TypeScript 增加了代码的可读性和可维护性
    * 类型系统实际上是最好的文档，大部分的函数看看类型的定义就可以知道如何使用了
    * 可以在编译阶段就发现大部分错误，这总比在运行时候出错好
    * 增强了编辑器和 IDE 的功能，包括代码补全、接口提示、跳转到定义、重构等
2. TypeScript 非常包容
    * TypeScript 是 JavaScript 的超集，.js 文件可以直接重命名为 .ts 即可
    * 即使不显式的定义类型，也能够自动做出类型推论
    * 可以定义从简单到复杂的几乎一切类型
    * 即使 TypeScript 编译报错，也可以生成 JavaScript 文件
    * 兼容第三方库，即使第三方库不是用 TypeScript 写的，也可以编写单独的类型文件供 TypeScript 读取
3. TypeScript 拥有活跃的社区
    * 大部分第三方库都有提供给 TypeScript 的类型定义文件
    * Google 开发的 Angular2 就是使用 TypeScript 编写的
    * TypeScript 拥抱了 ES6 规范，也支持部分 ESNext 草案的规范

缺点

1. 有一定的学习成本，需要理解接口（Interfaces）、泛型（Generics）、类（Classes）、枚举类型（Enums）等前端工程师可能不是很熟悉的概念
2. 短期可能会增加一些开发成本，毕竟要多写一些类型的定义，不过对于一个需要长期维护的项目，TypeScript 能够减少其维护成本
3. 集成到构建流程需要一些工作量
4. 可能和一些库结合的不是很完美

## tsconfig

[理解 Typescript 配置文件](https://segmentfault.com/a/1190000013514680)

[完整配置](https://www.typescriptlang.org/docs/handbook/compiler-options.html)