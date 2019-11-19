# C# 指南

## C#教程

### C# 语言介绍

C#（读作“See Sharp”）是一种简单易用的新式编程语言，不仅面向对象，还类型安全。 C# 源于 C 语言系列，C、C++、Java 和 JavaScript 程序员很快就可以上手使用。 本教程概述了该语言的主要组件。 如果想要通过交互式示例探索语言，请尝试我们的 [C# 简介](https://docs.microsoft.com/zh-cn/dotnet/csharp/tutorials/intro-to-csharp/index)教程。

C# 是一种面向对象的语言。不仅如此，C# 还进一步支持***面向组件的***编程。 当代软件设计越来越依赖采用自描述的独立功能包形式的软件组件。 此类组件的关键特征包括：为编程模型提供属性、方法和事件；包含提供组件声明性信息的特性；包含自己的文档。 C# 提供了语言构造来直接支持这些概念，让 C# 成为一种非常自然的语言，可用于创建和使用软件组件。

多项 C# 功能有助于构造可靠耐用的应用程序：垃圾回收可自动回收无法访问的未使用对象占用的内存；异常处理提供了一种结构化的可扩展方法来执行错误检测和恢复；C# 语言的类型安全设计禁止读取未初始化的变量、为范围之外的数组编制索引或执行未检查的类型转换。

C# 采用***统一的类型系统***。 所有 C# 类型（包括 `int` 和 `double` 等基元类型）均继承自一个根 `object` 类型。 因此，所有类型共用一组通用运算，任何类型的值都可以一致地进行存储、传输和处理。 此外，C# 还支持用户定义的引用类型和值类型，从而支持对象动态分配以及轻量级结构的内嵌式存储。

为了确保 C# 程序和库能够持续兼容，C# 设计非常注重***版本控制***。 许多编程语言很少关注这个问题，因此，当引入新版依赖库时，用这些语言编写的程序会出现更多不必要的中断现象。 C# 设计中受版本控制加强直接影响的方面包括：单独的 `virtual` 和 `override` 修饰符，关于方法重载决策的规则，以及对显式接口成员声明的支持。

### Hello world

“Hello, World”程序历来都用于介绍编程语言。 下面展示了此程序的 C# 代码：

```csharp
using System;

class Hello
{
    static void Main()
    {
        Console.WriteLine("Hello, World");
    }
}
```

C# 源文件的文件扩展名通常为 `.cs`。 假设“Hello, World”程序存储在文件 hello.cs 中，则可以使用下列命令行编译此程序：

```console
csc hello.cs
```

这会生成名为 hello.exe 的可执行程序集。 运行此应用程序生成以下输出：

```console
Hello, World
```

 重要

编译 `csc` 命令实现的是完整框架，可能并不所有平台都适用。

“Hello, World”程序始于引用 `System` 命名空间的 `using` 指令。 命名空间提供了一种用于组织 C# 程序和库的分层方法。 命名空间包含类型和其他命名空间。例如，`System` 命名空间包含许多类型（如程序中引用的 `Console` 类）和其他许多命名空间（如 `IO` 和 `Collections`）。 借助引用给定命名空间的 `using` 指令，可以非限定的方式使用作为相应命名空间成员的类型。 由于使用 `using` 指令，因此程序可以使用 `Console.WriteLine` 作为 `System.Console.WriteLine` 的简写。

“Hello, World”程序声明的 `Hello` 类只有一个成员，即 `Main` 方法。 `Main` 方法是使用静态修饰符进行声明。 实例方法可以使用关键字 `this` 引用特定的封闭对象实例，而静态方法则可以在不引用特定对象的情况下运行。 按照约定，`Main` 静态方法是程序的入口点。

程序的输出是由 `System` 命名空间中 `Console` 类的 `WriteLine` 方法生成。 此类由标准类库提供。默认情况下，编译器会自动引用标准类库。

关于 C#，要介绍的内容还有很多。 下面各主题概述了 C# 语言元素。 通过这些概述，可以了解 C# 语言所有元素的基本信息，并获得深入了解 C# 语言元素所需的信息：

- 程序结构
  - 了解 C# 语言中的关键组织概念：***程序***、***命名空间***、***类型***、***成员***和***程序集***。
- 类型和变量
  - 了解 C# 语言中的***值类型***、***引用类型***和***变量***。
- 表达式
  - ***表达式***是在***操作数***和***运算符***的基础之上构造而成。 表达式生成的是值。
- 语句
  - ***语句***用于表示程序的操作。
- 类和对象
  - ***类***是最基本的 C# 类型。 ***对象***是类实例。 类是使用***成员***生成的，此主题也对此进行了介绍。
- 结构
  - 与类不同，***结构***是属于值类型的数据结构。
- 数组
  - ***数组***是一种数据结构，其中包含许多通过计算索引访问的变量。
- 接口
  - ***接口***定义了可由类和结构实现的协定。 接口可以包含方法、属性、事件和索引器。 接口不提供所定义的成员的实现代码，仅指定必须由实现接口的类或结构提供的成员。
- 枚举
  - ***枚举类型***是包含一组已命名常量的独特值类型。
- 委托
  - ***委托类型***表示对具有特定参数列表和返回类型的方法的引用。 通过委托，可以将方法视为可分配给变量并可作为参数传递的实体。 委托类似于其他一些语言中的函数指针概念，但与函数指针不同的是，委托不仅面向对象，还类型安全。
- 特性
  - 使用***特性***，程序可以指定关于类型、成员和其他实体的附加声明性信息。

### 程序结构

C# 中的关键组织结构概念包括***程序***、***命名空间***、***类型***、***成员***和***程序集***。 C# 程序由一个或多个源文件组成。 程序声明类型，而类型则包含成员，并被整理到命名空间中。 类型示例包括类和接口。 成员示例包括字段、方法、属性和事件。 编译完的 C# 程序实际上会打包到程序集中。 程序集的文件扩展名通常为 `.exe` 或 `.dll`，具体取决于实现的是***应用程序***还是***库***。

以下示例在 `Acme.Collections` 命名空间中声明 `Stack` 类：

```csharp
using System;
namespace Acme.Collections
{
    public class Stack
    {
        Entry top;
        public void Push(object data) 
        {
            top = new Entry(top, data);
        }

        public object Pop() 
        {
            if (top == null)
            {
                throw new InvalidOperationException();
            }
            object result = top.data;
            top = top.next;
            return result;
        }
        
        class Entry
        {
            public Entry next;
            public object data;
            public Entry(Entry next, object data)
            {
                this.next = next;
                this.data = data;
            }
        }
    }
}
```

此类的完全限定的名称为 `Acme.Collections.Stack`。 此类包含多个成员：一个 `top` 字段、两个方法（`Push` 和 `Pop`）和一个 `Entry` 嵌套类。 `Entry` 类还包含三个成员：一个 `next` 字段、一个 `data` 字段和一个构造函数。 假定示例的源代码存储在 `acme.cs` 文件中，以下命令行

console复制

```console
csc /t:library acme.cs
```

将示例编译成库（不含 `Main` 入口点的代码），并生成 `acme.dll` 程序集。

 重要

上述示例使用 `csc` 作为命令行 C# 编译器。 此编译器是 Windows 可执行文件。 若要在其他平台上使用 C#，应使用 .NET Core 工具。 .NET Core 生态系统使用 `dotnet` CLI 来管理命令行生成。 这包括管理依赖项和调用 C# 编译器。 有关在 .NET Core 支持的平台上使用这些工具的完整说明，请参阅[这篇教程](https://docs.microsoft.com/zh-cn/dotnet/core/tutorials/using-with-xplat-cli)。

程序集包含中间语言 (IL) 指令形式的可执行代码和元数据形式的符号信息。 执行前，程序集中的 IL 代码会被 .NET 公共语言运行时的实时 (JIT) 编译器自动转换成处理器专属代码。

由于程序集是包含代码和元数据的自描述功能单元，因此无需在 C# 中使用 `#include` 指令和头文件。 只需在编译程序时引用特定的程序集，即可在 C# 程序中使用此程序集中包含的公共类型和成员。 例如，此程序使用 `acme.dll` 程序集中的 `Acme.Collections.Stack` 类：



```csharp
using System;
using Acme.Collections;
class Example
{
    static void Main() 
    {
        Stack s = new Stack();
        s.Push(1);
        s.Push(10);
        s.Push(100);
        Console.WriteLine(s.Pop());
        Console.WriteLine(s.Pop());
        Console.WriteLine(s.Pop());
    }
}
```

如果程序存储在文件 `example.cs` 中，编译 `example.cs` 时，可以使用编译器的 /r 选项引用 acme.dll 程序集：

console复制

```console
csc /r:acme.dll example.cs
```

这会创建 `example.exe` 可执行程序集，它将在运行时输出以下内容：

console复制

```console
100
10
1
```

使用 C#，可以将程序的源文本存储在多个源文件中。 编译多文件 C# 程序时，可以将所有源文件一起处理，并且源文件可以随意相互引用。从概念上讲，就像是所有源文件在处理前被集中到一个大文件中一样。 在 C# 中，永远都不需要使用前向声明，因为声明顺序无关紧要（除了极少数的例外情况）。 C# 并不限制源文件只能声明一种公共类型，也不要求源文件的文件名必须与其中声明的类型相匹配。



### 类型和变量

C# 有两种类型：*值类型*和*引用类型*。 值类型的变量直接包含数据，而引用类型的变量则存储对数据（称为“对象”）的引用。 对于引用类型，两个变量可以引用同一对象；因此，对一个变量执行的运算可能会影响另一个变量引用的对象。 借助值类型，每个变量都有自己的数据副本；因此，对一个变量执行的运算不会影响另一个变量（`ref` 和 `out` 参数变量除外）。

C# 值类型又细分为*简单类型*、*枚举类型*、*结构类型*和*可以为 null 的值类型*。 C# 引用类型又细分为*类类型*、*接口类型*、*数组类型*和*委托类型*。

下面概述了 C# 的类型系统。

- [值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/value-types-table)
  - [简单类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/value-types#simple-types)
    - 有符号的整型：`sbyte`、`short`、`int`、`long`
    - 无符号的整型：`byte`、`ushort`、`uint`、`ulong`
    - Unicode 字符：`char`
    - IEEE 二进制浮点：`float`、`double`
    - 高精度十进制浮点数：`decimal`
    - 布尔：`bool`
  - [枚举类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/enum)
    - 格式为 `enum E {...}` 的用户定义类型
  - [结构类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct)
    - 格式为 `struct S {...}` 的用户定义类型
  - [可以为 null 的值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/nullable-value-types)
    - 值为 `null` 的其他所有值类型的扩展
- [引用类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/reference-types)
  - [类类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class)
    - 其他所有类型的最终基类：`object`
    - Unicode 字符串：`string`
    - 格式为 `class C {...}` 的用户定义类型
  - [接口类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/interface)
    - 格式为 `interface I {...}` 的用户定义类型
  - [数组类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/arrays/index)
    - 一维和多维，例如 `int[]` 和 `int[,]`
  - [委托类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/delegate)
    - 格式为 `delegate int D(...)` 的用户定义类型

有关数值类型的详细信息，请参阅[整型类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)和[浮点类型表](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)。

C# 的 `bool` 类型用于表示布尔值（`true` 或 `false`）。

C# 使用 Unicode 编码处理字符和字符串。 `char` 类型表示 UTF-16 代码单元，`string` 类型表示一系列 UTF-16 代码单元。

C# 程序使用*类型声明*创建新类型。 类型声明指定新类型的名称和成员。 用户可定义以下五种 C# 类型：类类型、结构类型、接口类型、枚举类型和委托类型。

`class` 类型定义包含数据成员（字段）和函数成员（方法、属性及其他）的数据结构。 类类型支持单一继承和多形性，即派生类可以扩展和专门针对基类的机制。

`struct` 类型定义包含数据成员和函数成员的结构，这一点与类类型相似。 不过，与类不同的是，结构是值类型，通常不需要进行堆分配。 结构类型不支持用户指定的继承，并且所有结构类型均隐式继承自类型 `object`。

`interface` 类型将协定定义为一组已命名的公共函数成员。 实现 `interface` 的 `class` 或 `struct` 必须提供接口函数成员的实现代码。 `interface` 可以继承自多个基接口，`class` 和 `struct` 可以实现多个接口。

`delegate` 类型表示引用包含特定参数列表和返回类型的方法。 通过委托，可以将方法视为可分配给变量并可作为参数传递的实体。 委托类同于函数式语言提供的函数类型。 委托也类似于其他一些语言中的函数指针概念，但与函数指针不同的是，委托不仅面向对象，还类型安全。

`class`、`struct`、`interface` 和 `delegate` 类型全部都支持泛型，因此可以使用其他类型对它们进行参数化。

`enum` 类型是一种包含已命名常量的独特类型。 每个 `enum` 类型都有一个基础类型（必须是八种整型类型之一）。 `enum` 类型的值集与基础类型的值集相同。

C# 支持任意类型的一维和多维数组。 与上述类型不同，数组类型无需先声明即可使用。 相反，数组类型是通过在类型名称后面添加方括号构造而成。 例如，`int[]` 是 `int` 类型的一维数组，`int[,]` 是 `int` 类型的二维数组，`int[][]` 是由 `int` 类型的一维数组构成的一维数组。

可以为 null 的值类型也无需先声明即可使用。 对于所有不可以为 null 的值类型 `T`，都有对应的可以为 null 的值类型 `T?`，后者可以包含附加值 `null`。 例如，`int?` 是可以包含任何 32 位整数或值 `null` 的类型。

C# 采用统一的类型系统，因此任意类型的值都可视为 `object`。 每种 C# 类型都直接或间接地派生自 `object` 类类型，而 `object` 是所有类型的最终基类。 只需将值视为类型 `object`，即可将引用类型的值视为对象。 通过执行*装箱*和*取消装箱操作*，可以将值类型的值视为对象。 在以下示例中，`int` 值被转换成 `object`，然后又恢复成 `int`。



```csharp
using System;
class BoxingExample
{
    static void Main()
    {
        int i = 123;
        object o = i;    // Boxing
        int j = (int)o;  // Unboxing
    }
}
```

当值类型的值转换成 `object` 类型时，将分配 `object` 实例（亦称为“箱”）来包含值，然后该值会复制到相应的箱中。 相反，当 `object` 引用被显式转换成值类型时，将检查引用的 `object` 是否是具有正确值类型的箱；如果检查成功，则会将箱中的值复制出来。

C# 的统一类型系统实际上意味着可以“按需”将值类型转换成对象。 鉴于这种统一性，使用类型 `object` 的常规用途库可以与引用类型和值类型结合使用。

C# 有多种*变量*，其中包括字段、数组元素、局部变量和参数。 变量表示存储位置，每个变量都具有一种类型，用于确定可以在变量中存储哪些值，如下文所述。

- 不可以为 null 的值类型

  - 具有精确类型的值

- 可以为 null 的值类型

  - `null` 值或具有精确类型的值

- object

  - `null` 引用、对任意引用类型的对象的引用，或对任意值类型的装箱值的引用

- 类类型

  - `null` 引用、对类类型实例的引用，或对派生自类类型的类实例的引用

- 接口类型

  - `null` 引用、对实现接口类型的类类型实例的引用，或对实现接口类型的值类型的装箱值的引用

- 数组类型

  - `null` 引用、对数组类型实例的引用，或对兼容的数组类型实例的引用

- 委托类型

  - `null` 引用或对兼容的委托类型实例的引用

    

### 表达式

*表达式*是在*操作数*和*运算符*的基础之上构造而成。 表达式的运算符指明了向操作数应用的运算。 运算符的示例包括 `+`、`-`、`*`、`/` 和 `new`。 操作数的示例包括文本、字段、局部变量和表达式。

如果表达式包含多个运算符，那么运算符的*优先级*决定了各个运算符的计算顺序。 例如，表达式 `x + y * z` 相当于计算 `x + (y * z)`，因为 `*` 运算符的优先级高于 `+` 运算符。

如果操作数两边的两个运算符的优先级相同，那么运算符的*结合性*决定了运算的执行顺序：

- 除了赋值运算符和 null 合并运算符之外，所有二元运算符均为左结合 运算符，即从左向右执行运算。 例如，`x + y + z` 将计算为 `(x + y) + z`。
- 赋值运算符、null 合并 `??` 和 `??=` 运算符和条件运算符 `?:` 为右结合 运算符，即从右向左执行运算。 例如，`x = y = z` 将计算为 `x = (y = z)`。

可以使用括号控制优先级和结合性。 例如，`x + y * z` 先计算 `y` 乘 `z`，并将结果与 `x` 相加，而 `(x + y) * z` 则先计算 `x` 加 `y`，然后将结果与 `z` 相乘。

大部分运算符可[*重载*](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/operator-overloading)。 借助运算符重载，可以为一个或两个操作数为用户定义类或结构类型的运算指定用户定义运算符实现代码。

C# 提供多个运算符用于执行[算术](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/arithmetic-operators)、[逻辑](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/boolean-logical-operators)、[按位和移位](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators)运算以及[相等](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/equality-operators)和[排序](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/comparison-operators)比较。

要了解按优先级排序的完整 C# 运算符列表，请参阅 [C# 运算符](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/index)。

### 语句

程序操作使用*语句*进行表示。 C# 支持几种不同的语句，其中许多语句是从嵌入语句的角度来定义的。

使用*代码块*，可以在允许编写一个语句的上下文中编写多个语句。 代码块是由一系列在分隔符 `{` 和 `}` 内编写的语句组成。

*声明语句*用于声明局部变量和常量。

*表达式语句*用于计算表达式。 可用作语句的表达式包括方法调用、使用 `new` 运算符的对象分配、使用 `=` 和复合赋值运算符的赋值、使用 `++` 和 `--` 运算符和 `await` 表达式的递增和递减运算。

*选择语句*用于根据一些表达式的值从多个可能的语句中选择一个以供执行。 这一类语句包括 `if` 和 `switch` 语句。

*迭代语句*用于重复执行嵌入语句。 这一类语句包括 `while`、`do`、`for` 和 `foreach` 语句。

*跳转语句*用于转移控制权。 这一类语句包括 `break`、`continue`、`goto`、`throw`、`return` 和 `yield` 语句。

`try`...`catch` 语句用于捕获在代码块执行期间发生的异常，`try`...`finally` 语句用于指定始终执行的最终代码，无论异常发生与否。

`checked` 和 `unchecked` 语句用于控制整型类型算术运算和转换的溢出检查上下文。

`lock` 语句用于获取给定对象的相互排斥锁定，执行语句，然后解除锁定。

`using` 语句用于获取资源，执行语句，然后释放资源。

下面列出了可以使用的各种语句，以及每种语句的示例。

- 局部变量声明：

```csharp
static void Declarations(string[] args)
{
    int a;
    int b = 2, c = 3;
    a = 1;
    Console.WriteLine(a + b + c);
}
```

- 局部常量声明：

```csharp
static void ConstantDeclarations(string[] args)
{
    const float pi = 3.1415927f;
    const int r = 25;
    Console.WriteLine(pi * r * r);
}
```

- 表达式语句：



```csharp
static void Expressions(string[] args)
{
    int i;
    i = 123;                // Expression statement
    Console.WriteLine(i);   // Expression statement
    i++;                    // Expression statement
    Console.WriteLine(i);   // Expression statement
}
```

- `if` 语句：

```csharp
static void IfStatement(string[] args)
{
    if (args.Length == 0)
    {
        Console.WriteLine("No arguments");
    }
    else 
    {
        Console.WriteLine("One or more arguments");
    }
}
```

- `switch` 语句：

```csharp
static void SwitchStatement(string[] args)
{
    int n = args.Length;
    switch (n) 
    {
        case 0:
            Console.WriteLine("No arguments");
            break;
        case 1:
            Console.WriteLine("One argument");
            break;
        default:
            Console.WriteLine($"{n} arguments");
            break;
    }
}
```

- `while` 语句：

```csharp
static void WhileStatement(string[] args)
{
    int i = 0;
    while (i < args.Length) 
    {
        Console.WriteLine(args[i]);
        i++;
    }
}
```

- `do` 语句：

```csharp
static void DoStatement(string[] args)
{
    string s;
    do 
    {
        s = Console.ReadLine();
        Console.WriteLine(s);
    } while (!string.IsNullOrEmpty(s));
}
```

- `for` 语句：

```csharp
static void ForStatement(string[] args)
{
    for (int i = 0; i < args.Length; i++) 
    {
        Console.WriteLine(args[i]);
    }
}
```

- `foreach` 语句：

```csharp
static void ForEachStatement(string[] args)
{
    foreach (string s in args) 
    {
        Console.WriteLine(s);
    }
}
```

- `break` 语句：

```csharp
static void BreakStatement(string[] args)
{
    while (true) 
    {
        string s = Console.ReadLine();
        if (string.IsNullOrEmpty(s)) 
            break;
        Console.WriteLine(s);
    }
}
```

- `continue` 语句：

```csharp
static void ContinueStatement(string[] args)
{
    for (int i = 0; i < args.Length; i++) 
    {
        if (args[i].StartsWith("/")) 
            continue;
        Console.WriteLine(args[i]);
    }
}
```

- `goto` 语句：

```csharp
static void GoToStatement(string[] args)
{
    int i = 0;
    goto check;
    loop:
    Console.WriteLine(args[i++]);
    check:
    if (i < args.Length) 
        goto loop;
}
```

- `return` 语句：

```csharp
static int Add(int a, int b) 
{
    return a + b;
}
static void ReturnStatement(string[] args)
{
   Console.WriteLine(Add(1, 2));
   return;
}
```

- `yield` 语句：

```csharp
static System.Collections.Generic.IEnumerable<int> Range(int start, int end) 
{
    for (int i = start; i < end; i++) 
    {
        yield return i;
    }
    yield break;
}
static void YieldStatement(string[] args)
{
    foreach (int i in Range(-10,10)) 
    {
        Console.WriteLine(i);
    }
}
```

- `throw` 和 `try` 语句：

```csharp
static double Divide(double x, double y) 
{
    if (y == 0) 
        throw new DivideByZeroException();
    return x / y;
}
static void TryCatch(string[] args) 
{
    try 
    {
        if (args.Length != 2) 
        {
            throw new InvalidOperationException("Two numbers required");
        }
        double x = double.Parse(args[0]);
        double y = double.Parse(args[1]);
        Console.WriteLine(Divide(x, y));
    }
    catch (InvalidOperationException e) 
    {
        Console.WriteLine(e.Message);
    }
    finally 
    {
        Console.WriteLine("Good bye!");
    }
}
```

- `checked` 和 `unchecked` 语句：

```csharp
static void CheckedUnchecked(string[] args) 
{
    int x = int.MaxValue;
    unchecked 
    {
        Console.WriteLine(x + 1);  // Overflow
    }
    checked 
    {
        Console.WriteLine(x + 1);  // Exception
    }     
}
```

- `lock` 语句：

```csharp
class Account
{
    decimal balance;
    private readonly object sync = new object();
    public void Withdraw(decimal amount) 
    {
        lock (sync) 
        {
            if (amount > balance) 
            {
                throw new Exception(
                    "Insufficient funds");
            }
            balance -= amount;
        }
    }
}
```

- `using` 语句：

```csharp
static void UsingStatement(string[] args) 
{
    using (TextWriter w = File.CreateText("test.txt")) 
    {
        w.WriteLine("Line one");
        w.WriteLine("Line two");
        w.WriteLine("Line three");
    }
}
```

### 类和对象

*类*是最基本的 C# 类型。 类是一种数据结构，可在一个单元中就将状态（字段）和操作（方法和其他函数成员）结合起来。 类为动态创建的类*实例*（亦称为“*对象*”）提供了定义。 类支持*继承*和*多形性*，即*派生类*可以扩展和专门针对*基类*的机制。

新类使用类声明进行创建。 类声明的开头是标头，指定了类的特性和修饰符、类名、基类（若指定）以及类实现的接口。 标头后面是类主体，由在分隔符 `{` 和 `}` 内编写的成员声明列表组成。

以下是简单类 `Point` 的声明：

```csharp
public class Point
{
    public int x, y;
    public Point(int x, int y) 
    {
        this.x = x;
        this.y = y;
    }
}
```

类实例是使用 `new` 运算符进行创建，此运算符为新实例分配内存，调用构造函数来初始化实例，并返回对实例的引用。 以下语句创建两个 Point 对象，并将对这些对象的引用存储在两个变量中：

```csharp
Point p1 = new Point(0, 0);
Point p2 = new Point(10, 20);
```

当无法再访问对象时，对象占用的内存会被自动回收。 既没必要，也无法在 C# 中显式解除分配对象。

#### 成员

类成员要么是静态成员，要么是实例成员。 静态成员属于类，而实例成员则属于对象（类实例）。

下面概述了类可以包含的成员类型。

- 常量
  - 与类相关联的常量值
- 字段
  - 类的常量
- 方法
  - 类可以执行的计算和操作
- 属性
  - 与读取和写入类的已命名属性相关联的操作
- 索引器
  - 与将类实例编入索引（像处理数组一样）相关联的操作
- 事件
  - 类可以生成的通知
- 运算符
  - 类支持的转换和表达式运算符
- 构造函数
  - 初始化类实例或类本身所需的操作
- 终结器
  - 永久放弃类实例前要执行的操作
- 类型
  - 类声明的嵌套类型

#### 可访问性

每个类成员都有关联的可访问性，用于控制能够访问成员的程序文本区域。 可访问性有六种可能的形式。 总结如下。

- ```
  public
  ```

  - 访问不受限

- ```
  protected
  ```

  - 只能访问此类或派生自此类的类

- ```
  internal
  ```

  - 访问限于当前程序集（.exe、.dll 等）

- ```
  protected internal
  ```

  - 访问限于包含类、派生自包含类的类或同一程序集中的类

- ```
  private
  ```

  - 只能访问此类

- ```
  private protected
  ```

  - 访问限于同一程序集中的包含类或派生自包含类的类

#### 类型参数

类定义可能会按如下方式指定一组类型参数：在类名后面用尖括号括住类型参数名称列表。 然后，可以在类声明的主体中使用类型参数来定义类成员。 在以下示例中，`Pair` 的类型参数是 `TFirst` 和 `TSecond`：

```csharp
public class Pair<TFirst,TSecond>
{
    public TFirst First;
    public TSecond Second;
}
```

声明为需要使用类型参数的类类型被称为*泛型类类型*。 结构、接口和委托类型也可以是泛型。 使用泛型类时，必须为每个类型参数提供类型自变量：



```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First;     // TFirst is int
string s = pair.Second; // TSecond is string
```

包含类型自变量的泛型类型（如上面的 `Pair`）被称为*构造泛型类型*。

#### 基类

类声明可能会按如下方式指定基类：在类名和类型参数后面编写冒号和基类名。 省略基类规范与从 `object` 类型派生相同。 在以下示例中，`Point3D` 的基类是 `Point`，`Point` 的基类是 `object`：

```csharp
public class Point
{
    public int x, y;
    public Point(int x, int y) 
    {
        this.x = x;
        this.y = y;
    }
}
public class Point3D: Point
{
    public int z;
    public Point3D(int x, int y, int z) : 
        base(x, y) 
    {
        this.z = z;
    }
}
```

类继承其基类的成员。 继承是指隐式包含其基类的所有成员的类，实例和静态构造函数以及基类的终结器除外。 派生类可以其继承的类添加新成员，但无法删除继承成员的定义。 在上面的示例中，`Point3D` 从 `Point` 继承了 `x` 和 `y` 字段，每个 `Point3D` 实例均包含三个字段（`x`、`y` 和 `z`）。

可以将类类型隐式转换成其任意基类类型。 因此，类类型的变量可以引用相应类的实例或任意派生类的实例。 例如，类声明如上，`Point` 类型的变量可以引用 `Point` 或 `Point3D`：

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

#### 字段

*字段*是与类或类实例相关联的变量。

使用静态修饰符声明的字段定义的是静态字段。 静态字段只指明一个存储位置。 无论创建多少个类实例，永远只有一个静态字段副本。

不使用静态修饰符声明的字段定义的是实例字段。 每个类实例均包含相应类的所有实例字段的单独副本。

在以下示例中，每个 `Color` 类实例均包含 `r`、`g` 和 `b` 实例字段的单独副本，但分别只包含 `Black`、`White`、`Red`、`Green` 和 `Blue` 静态字段的一个副本：

```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);
    private byte r, g, b;
    public Color(byte r, byte g, byte b) 
    {
        this.r = r;
        this.g = g;
        this.b = b;
    }
}
```

如上面的示例所示，可以使用 `readonly` 修饰符声明*只读字段*。 只能在字段声明期间或在同一个类的构造函数中向 `readonly` 字段赋值。

#### 方法

*方法*是实现对象或类可执行的计算或操作的成员。 *静态方法*是通过类进行访问。 *实例方法*是通过类实例进行访问。

方法可能具有*参数*列表，用于表示传递给方法的值或变量引用；并具有*返回类型*，用于指定方法计算并返回的值的类型。 如果方法未返回值，则其返回类型为 `void`。

方法可能也包含一组类型参数，必须在调用方法时指定类型自变量，这一点与类型一样。 与类型不同的是，通常可以根据方法调用的自变量推断出类型自变量，无需显式指定。

在声明方法的类中，方法的*签名*必须是唯一的。 方法签名包含方法名称、类型参数数量及其参数的数量、修饰符和类型。 方法签名不包含返回类型。

#### 参数

参数用于将值或变量引用传递给方法。 方法参数从调用方法时指定的*自变量*中获取其实际值。 有四类参数：值参数、引用参数、输出参数和参数数组。

值参数 用于传递输入自变量。 值参数对应于局部变量，从为其传递的自变量中获取初始值。 修改值参数不会影响为其传递的自变量。

可以指定默认值，从而省略相应的自变量，这样值参数就是可选的。

引用参数 用于按引用传递自变量。 为引用参数传递的自变量必须是具有明确值的变量，并且在方法执行期间，引用参数指明的存储位置与自变量相同。 引用参数使用 `ref` 修饰符进行声明。 下面的示例展示了如何使用 `ref` 参数。

```csharp
using System;
class RefExample
{
    static void Swap(ref int x, ref int y) 
    {
        int temp = x;
        x = y;
        y = temp;
    }
    public static void SwapExample() 
    {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine($"{i} {j}");    // Outputs "2 1"
    }
}
```

输出参数 用于按引用传递自变量。 输出参数与引用参数类似，不同之处在于，不要求向调用方提供的自变量显式赋值。 输出参数使用 `out` 修饰符进行声明。 下面的示例演示如何通过 C# 7 中引入的语法使用 `out` 参数。

```csharp
    using System;
    class OutExample
    {
        static void Divide(int x, int y, out int result, out int remainder) 
        {
            result = x / y;
            remainder = x % y;
        }
        public static void OutUsage() 
        {
            Divide(10, 3, out int res, out int rem);
            Console.WriteLine("{0} {1}", res, rem);	// Outputs "3 1"
        }
    }
}
```

*参数数组*允许向方法传递数量不定的自变量。 参数数组使用 `params` 修饰符进行声明。 参数数组只能是方法的最后一个参数，且参数数组的类型必须是一维数组类型。 [System.Console](https://docs.microsoft.com/zh-cn/dotnet/api/system.console) 类的 Write 和 WriteLine 方法是参数数组用法的典型示例。 它们的声明方式如下。

```csharp
public class Console
{
    public static void Write(string fmt, params object[] args) { }
    public static void WriteLine(string fmt, params object[] args) { }
    // ...
}
```

在使用参数数组的方法中，参数数组的行为与数组类型的常规参数完全相同。 不过，在调用包含参数数组的方法时，要么可以传递参数数组类型的一个自变量，要么可以传递参数数组的元素类型的任意数量自变量。 在后一种情况中，数组实例会自动创建，并初始化为包含给定的自变量。 以下示例：

```csharp
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```

等同于编写以下代码：

```csharp
string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
```

#### 方法主体和局部变量

方法主体指定了在调用方法时执行的语句。

方法主体可以声明特定于方法调用的变量。 此类变量称为*局部变量*。 局部变量声明指定了类型名称、变量名称以及可能的初始值。 下面的示例声明了初始值为零的局部变量 `i` 和无初始值的局部变量 `j`。

```csharp
using System;
class Squares
{
    public static void WriteSquares() 
    {
        int i = 0;
        int j;
        while (i < 10) 
        {
            j = i * i;
            Console.WriteLine($"{i} x {i} = {j}");
            i = i + 1;
        }
    }
}
```

C# 要求必须先*明确赋值*局部变量，然后才能获取其值。 例如，如果上面的 `i` 声明未包含初始值，那么编译器会在后面使用 `i` 时报告错误，因为在后面使用时 `i` 不会在程序中进行明确赋值。

方法可以使用 `return` 语句将控制权返回给调用方。 在返回 `void` 的方法中，`return` 语句无法指定表达式。 在不返回 void 的方法中，`return` 语句必须包括用于计算返回值的表达式。

#### 静态和实例方法

使用静态修饰符声明的方法是*静态方法*。 静态方法不对特定的实例起作用，只能直接访问静态成员。

不使用静态修饰符声明的方法是*实例方法*。 实例方法对特定的实例起作用，并能够访问静态和实例成员。 其中调用实例方法的实例可以作为 `this` 显式访问。 在静态方法中引用 `this` 会生成错误。

以下 `Entity` 类包含静态和实例成员。

```csharp
class Entity
{
    static int nextSerialNo;
    int serialNo;
    public Entity() 
    {
        serialNo = nextSerialNo++;
    }
    public int GetSerialNo() 
    {
        return serialNo;
    }
    public static int GetNextSerialNo() 
    {
        return nextSerialNo;
    }
    public static void SetNextSerialNo(int value) 
    {
        nextSerialNo = value;
    }
}
```

每个 `Entity` 实例均有一个序列号（很可能包含此处未显示的其他一些信息）。 `Entity` 构造函数（类似于实例方法）将新实例初始化为包含下一个可用的序列号。 由于构造函数是实例成员，因此可以访问 `serialNo` 实例字段和 `nextSerialNo` 静态字段。

`GetNextSerialNo` 和 `SetNextSerialNo` 静态方法可以访问 `nextSerialNo` 静态字段，但如果直接访问 `serialNo` 实例字段，则会生成错误。

下面的示例展示了如何使用 Entity 类。

```csharp
using System;
class EntityExample
{
    public static void Usage() 
    {
        Entity.SetNextSerialNo(1000);
        Entity e1 = new Entity();
        Entity e2 = new Entity();
        Console.WriteLine(e1.GetSerialNo());            // Outputs "1000"
        Console.WriteLine(e2.GetSerialNo());            // Outputs "1001"
        Console.WriteLine(Entity.GetNextSerialNo());    // Outputs "1002"
    }
}
```

请注意，`SetNextSerialNo` 和 `GetNextSerialNo` 静态方法是在类中调用，而 `GetSerialNo` 实例方法则是在类实例中调用。

#### 虚方法、重写方法和抽象方法

如果实例方法声明中有 `virtual` 修饰符，可以将实例方法称为“*虚方法*”。 如果没有 virtual 修饰符，可以将实例方法称为“*非虚方法*”。

调用虚方法时，为其调用方法的实例的*运行时类型*决定了要调用的实际方法实现代码。 调用非虚方法时，实例的*编译时类型*是决定性因素。

可以在派生类中*重写*虚方法。 如果实例方法声明中有 override 修饰符，那么实例方法可以重写签名相同的继承虚方法。 但如果虚方法声明中引入新方法，重写方法声明通过提供相应方法的新实现代码，专门针对现有的继承虚方法。

*抽象方法*是没有实现代码的虚方法。 抽象方法使用 abstract 修饰符进行声明，只能在同样声明了 abstract 的类中使用。 必须在所有非抽象派生类中重写抽象方法。

下面的示例声明了一个抽象类 `Expression`，用于表示表达式树节点；还声明了三个派生类（`Constant`、`VariableReference` 和 `Operation`），用于实现常量、变量引用和算术运算的表达式树节点。 （这与表达式树类型相似，但不能与之混淆）。



```csharp
using System;
using System.Collections.Generic;
public abstract class Expression
{
    public abstract double Evaluate(Dictionary<string,object> vars);
}
public class Constant: Expression
{
    double value;
    public Constant(double value) 
    {
        this.value = value;
    }
    public override double Evaluate(Dictionary<string,object> vars) 
    {
        return value;
    }
}
public class VariableReference: Expression
{
    string name;
    public VariableReference(string name) 
    {
        this.name = name;
    }
    public override double Evaluate(Dictionary<string,object> vars) 
    {
        object value = vars[name];
        if (value == null) 
        {
            throw new Exception("Unknown variable: " + name);
        }
        return Convert.ToDouble(value);
    }
}
public class Operation: Expression
{
    Expression left;
    char op;
    Expression right;
    public Operation(Expression left, char op, Expression right) 
    {
        this.left = left;
        this.op = op;
        this.right = right;
    }
    public override double Evaluate(Dictionary<string,object> vars) 
    {
        double x = left.Evaluate(vars);
        double y = right.Evaluate(vars);
        switch (op) {
            case '+': return x + y;
            case '-': return x - y;
            case '*': return x * y;
            case '/': return x / y;
        }
        throw new Exception("Unknown operator");
    }
}
```

上面的四个类可用于进行算术表达式建模。 例如，使用这些类的实例，可以按如下方式表示表达式 `x + 3`。

```csharp
Expression e = new Operation(
    new VariableReference("x"),
    '+',
    new Constant(3));
```

调用 `Expression` 实例的 `Evaluate` 方法可以计算给定的表达式并生成 `double` 值。 此方法需要使用自变量 `Dictionary`，其中包含变量名称（作为项键）和值（作为项值）。 因为 `Evaluate` 是一个抽象方法，因此派生自 `Expression` 的非抽象类必须替代 `Evaluate`。

`Constant` 的 `Evaluate` 实现代码只返回存储的常量。 `VariableReference` 实现代码查找字典中的变量名称，并返回结果值。 `Operation` 实现代码先计算左右操作数（以递归方式调用其 `Evaluate` 方法），然后执行给定的算术运算。

以下程序使用 `Expression` 类根据不同的 `x` 和 `y` 值计算表达式 `x * (y + 2)`。

```csharp
using System;
using System.Collections.Generic;
class InheritanceExample
{
    public static void ExampleUsage() 
    {
        Expression e = new Operation(
            new VariableReference("x"),
            '*',
            new Operation(
                new VariableReference("y"),
                '+',
                new Constant(2)
            )
        );
        Dictionary<string,object> vars = new Dictionary<string, object>();
        vars["x"] = 3;
        vars["y"] = 5;
        Console.WriteLine(e.Evaluate(vars));		// Outputs "21"
        vars["x"] = 1.5;
        vars["y"] = 9;
        Console.WriteLine(e.Evaluate(vars));		// Outputs "16.5"
    }
}   
```

#### 方法重载

借助方法*重载*，同一类中可以有多个同名的方法，只要这些方法具有唯一签名即可。 编译如何调用重载的方法时，编译器使用*重载决策*来确定要调用的特定方法。 重载决策查找与自变量最匹配的方法；如果找不到最佳匹配项，则会报告错误。 下面的示例展示了重载决策的实际工作方式。 `UsageExample` 方法中每个调用的注释指明了实际调用的方法。

```csharp
using System;
class OverloadingExample
{
    static void F() 
    {
        Console.WriteLine("F()");
    }
    static void F(object x) 
    {
        Console.WriteLine("F(object)");
    }
    static void F(int x) 
    {
        Console.WriteLine("F(int)");
    }
    static void F(double x) 
    {
        Console.WriteLine("F(double)");
    }
    static void F<T>(T x) 
    {
        Console.WriteLine("F<T>(T)");
    }
    static void F(double x, double y) 
    {
        Console.WriteLine("F(double, double)");
    }
    public static void UsageExample()
    {
        F();            // Invokes F()
        F(1);           // Invokes F(int)
        F(1.0);         // Invokes F(double)
        F("abc");       // Invokes F<string>(string)
        F((double)1);   // Invokes F(double)
        F((object)1);   // Invokes F(object)
        F<int>(1);      // Invokes F<int>(int)
        F(1, 1);        // Invokes F(double, double)
    }
}
```

如示例所示，可以随时将自变量显式转换成确切的参数类型，并/或显式提供类型自变量，从而选择特定的方法。

#### 其他函数成员

包含可执行代码的成员统称为类的*函数成员*。 上一部分介绍了作为主要函数成员类型的方法。 此部分将介绍 C# 支持的其他类型函数成员：构造函数、属性、索引器、事件、运算符和终结器。

下面的示例展示了 `MyList` 泛型类，用于实现对象的可扩充列表。 此类包含最常见类型函数成员的多个示例。

 备注

此示例将创建 `MyList` 类，该类与 .NET 标准 [System.Collections.Generic.List](https://docs.microsoft.com/zh-cn/dotnet/api/system.collections.generic.list-1) 不同。 它说明了此教程中所需的概念，但不会替代该类。

```csharp
public class MyList<T>
{
    // Constant
    const int defaultCapacity = 4;

    // Fields
    T[] items;
    int count;

    // Constructor
    public MyList(int capacity = defaultCapacity) 
    {
        items = new T[capacity];
    }

    // Properties
    public int Count => count; 

    public int Capacity 
    {
        get { return items.Length; }
        set 
        {
            if (value < count) value = count;
            if (value != items.Length) 
            {
                T[] newItems = new T[value];
                Array.Copy(items, 0, newItems, 0, count);
                items = newItems;
            }
        }
    }

    // Indexer
    public T this[int index] 
    {
        get 
        {
            return items[index];
        }
        set 
        {
            items[index] = value;
            OnChanged();
        }
    }
    
    // Methods
    public void Add(T item) 
    {
        if (count == Capacity) Capacity = count * 2;
        items[count] = item;
        count++;
        OnChanged();
    }
    protected virtual void OnChanged() =>
        Changed?.Invoke(this, EventArgs.Empty);

    public override bool Equals(object other) =>
        Equals(this, other as MyList<T>);

    static bool Equals(MyList<T> a, MyList<T> b) 
    {
        if (Object.ReferenceEquals(a, null)) return Object.ReferenceEquals(b, null);
        if (Object.ReferenceEquals(b, null) || a.count != b.count)
            return false;
        for (int i = 0; i < a.count; i++) 
        {
            if (!object.Equals(a.items[i], b.items[i])) 
            {
                return false;
            }
        }
    return true;
    }

    // Event
    public event EventHandler Changed;

    // Operators
    public static bool operator ==(MyList<T> a, MyList<T> b) => 
        Equals(a, b);

    public static bool operator !=(MyList<T> a, MyList<T> b) => 
        !Equals(a, b);
}
```

#### 构造函数

C# 支持实例和静态构造函数。 *实例构造函数*是实现初始化类实例所需执行的操作的成员。 *静态构造函数*是实现在首次加载类时初始化类本身所需执行的操作的成员。

构造函数的声明方式与方法一样，都没有返回类型，且与所含类同名。 如果构造函数声明包含静态修饰符，则声明的是静态构造函数。 否则，声明的是实例构造函数。

实例构造函数可重载并且可具有可选参数。 例如，`MyList` 类声明一个具有单个可选 `int` 参数的实例构造函数。 实例构造函数使用 `new` 运算符进行调用。 下面的语句使用包含和不包含可选自变量的 `MyList` 类构造函数来分配两个 `MyList` 实例。

```csharp
MyList<string> list1 = new MyList<string>();
MyList<string> list2 = new MyList<string>(10);
```

与其他成员不同，实例构造函数不能被继承，且类中只能包含实际已声明的实例构造函数。 如果没有为类提供实例构造函数，则会自动提供不含参数的空实例构造函数。

#### 属性

*属性*是字段的自然扩展。 两者都是包含关联类型的已命名成员，用于访问字段和属性的语法也是一样的。 不过，与字段不同的是，属性不指明存储位置。 相反，属性包含*访问器*，用于指定在读取或写入属性值时要执行的语句。

属性的声明方式与字段类似，不同之处在于，属性声明以在分隔符 `{` 和 `}` 内写入的 get 访问器和/或 set 访问器结束，而不是以分号结束。 同时包含 get 访问器和 set 访问器的属性是*读写属性*，仅包含 get 访问器的属性是*只读属性*，仅包含 set 访问器的属性是*只写属性*。

get 访问器对应于包含属性类型的返回值的无参数方法。 如果在表达式中引用属性，除了作为赋值目标以外，调用的属性 get 访问器还可用于计算属性值。

set 访问器对应于包含一个名为 value 的参数但不含返回类型的方法。 如果将属性引用为赋值目标或 ++/-- 的操作数，将调用 set 访问器（由自变量提供新值）。

`MyList` 类声明以下两个属性：`Count` 和 `Capacity`（分别为只读和读写）。 下面的示例展示了如何使用这些属性：

```csharp
MyList<string> names = new MyList<string>();
names.Capacity = 100;   // Invokes set accessor
int i = names.Count;    // Invokes get accessor
int j = names.Capacity; // Invokes get accessor
```

类似于字段和方法，C# 支持实例属性和静态属性。 静态属性使用静态修饰符进行声明，而实例属性则不使用静态修饰符进行声明。

属性的访问器可以是虚的。 如果属性声明包含 `virtual`、`abstract` 或 `override` 修饰符，则适用于属性的访问器。

#### 索引器

借助*索引器*成员，可以将对象编入索引（像处理数组一样）。 索引器的声明方式与属性类似，不同之处在于，索引器成员名称格式为 `this` 后跟在分隔符 `[` 和 `]` 内写入的参数列表。 这些参数在索引器的访问器中可用。 类似于属性，索引器分为读写、只读和只写索引器，且索引器的访问器可以是虚的。

`MyList` 类声明一个需要使用 `int` 参数的读写索引器。 借助索引器，可以使用 `int` 值将 `MyList` 实例编入索引。 例如:

```csharp
MyList<string> names = new MyList<string>();
names.Add("Liz");
names.Add("Martha");
names.Add("Beth");
for (int i = 0; i < names.Count; i++) 
{
    string s = names[i];
    names[i] = s.ToUpper();
}
```

索引器可以进行重载。也就是说，类可以声明多个索引器，只要其参数的数量或类型不同即可。

#### 事件

借助*事件*成员，类或对象可以提供通知。 事件的声明方式与字段类似，不同之处在于，事件声明包括事件关键字，且类型必须是委托类型。

在声明事件成员的类中，事件的行为与委托类型的字段完全相同（前提是事件不是抽象的，且不声明访问器）。 字段存储对委托的引用，委托表示已添加到事件的事件处理程序。 如果没有任何事件处理程序，则字段为 `null`。

`MyList` 类声明一个 `Changed` 事件成员，指明已向列表添加了新项。 Changed 事件由 `OnChanged` 虚方法引发，此方法会先检查事件是否是 `null`（即不含任何处理程序）。 引发事件的概念恰恰等同于调用由事件表示的委托，因此，没有用于引发事件的特殊语言构造。

客户端通过*事件处理程序*响应事件。 使用 `+=` 和 `-=` 运算符分别可以附加和删除事件处理程序。 下面的示例展示了如何向 `MyList` 的 `Changed` 事件附加事件处理程序。

```csharp
class EventExample
{
    static int changeCount;
    static void ListChanged(object sender, EventArgs e) 
    {
        changeCount++;
    }
    public static void Usage() 
    {
        MyList<string> names = new MyList<string>();
        names.Changed += new EventHandler(ListChanged);
        names.Add("Liz");
        names.Add("Martha");
        names.Add("Beth");
        Console.WriteLine(changeCount);		// Outputs "3"
    }
}
```

对于需要控制事件的基础存储的高级方案，事件声明可以显式提供 `add` 和 `remove` 访问器，这在某种程度上与属性的 `set` 访问器类似。

#### 运算符

*运算符*是定义向类实例应用特定表达式运算符的含义的成员。 可以定义三种类型的运算符：一元运算符、二元运算符和转换运算符。 所有运算符都必须声明为 `public` 和 `static`。

`MyList` 类声明两个运算符（`operator ==` 和 `operator !=`），因此定义了向 `MyList` 实例应用这些运算符的表达式的新含义。 具体而言，这些运算符定义的是两个 `MyList` 实例的相等性（使用其 Equals 方法比较所包含的每个对象）。 下面的示例展示了如何使用 `==` 运算符比较两个 `MyList` 实例。

```csharp
MyList<int> a = new MyList<int>();
a.Add(1);
a.Add(2);
MyList<int> b = new MyList<int>();
b.Add(1);
b.Add(2);
Console.WriteLine(a == b);  // Outputs "True" 
b.Add(3);
Console.WriteLine(a == b);  // Outputs "False"
```

第一个 `Console.WriteLine` 输出 `True`，因为两个列表包含的对象不仅数量相同，而且值和顺序也相同。 如果 `MyList` 未定义 `operator ==`，那么第一个 `Console.WriteLine` 会输出 `False`，因为 `a` 和 `b` 引用不同的 `MyList` 实例。

#### 终结器

*终结器*是实现完成类实例所需的操作的成员。 终结器既不能包含参数和可访问性修饰符，也不能进行显式调用。 实例的终结器在垃圾回收期间自动调用。

垃圾回收器在决定何时收集对象和运行终结器时有很大自由度。 具体来说，终结器的调用时间具有不确定性，可以在任意线程上执行终结器。 因为这样或那样的原因，只有在没有其他可行的解决方案时，类才能实现终结器。

处理对象析构的更好方法是使用 `using` 语句。

### 结构

***结构***是可以包含数据成员和函数成员的数据结构，这一点与类一样；与类不同的是，结构是值类型，无需进行堆分配。 结构类型的变量直接存储结构数据，而类类型的变量存储对动态分配的对象的引用。 结构类型不支持用户指定的继承，并且所有结构类型均隐式继承自类型 [ValueType](https://docs.microsoft.com/zh-cn/dotnet/api/system.valuetype)，后者又隐式继承自 `object`。

结构对包含值语义的小型数据结构特别有用。 复数、坐标系中的点或字典中的键值对都是结构的典型示例。 对小型数据结构使用结构（而不是类）在应用程序执行的内存分配次数上存在巨大差异。 例如，以下程序创建并初始化包含 100 个点的数组。 通过将 `Point` 实现为类，可单独实例化 101 个对象，一个对象用于数组，其他所有对象分别用于 100 个元素。

```csharp
public class PointExample
{
    public static void Main() 
    {
        Point[] points = new Point[100];
        for (int i = 0; i < 100; i++)
            points[i] = new Point(i, i);
    }
}
```

也可以选择将 Point 实现为结构。

```csharp
struct Point
{
    public int x, y;
    public Point(int x, int y) 
    {
        this.x = x;
        this.y = y;
    }
}
```

现在，仅实例化一个对象（即用于数组的对象），`Point` 实例存储内嵌在数组中。

使用 `new` 运算符调用结构构造函数，类似于类构造函数。 然而，结构构造函数只返回结构值本身（通常在堆栈的临时位置中），并在必要时复制此值，而非在托管堆上动态分配对象并返回对此对象的引用。

借助类，两个变量可以引用同一对象；因此，对一个变量执行的运算可能会影响另一个变量引用的对象。 借助结构，每个变量都有自己的数据副本；因此，对一个变量执行的运算不会影响另一个变量。 例如，以下代码片段生成的输出取决于 Point 是类还是结构。

```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 20;
Console.WriteLine(b.x);
```

如果 `Point` 是类，则输出 20，因为 `a` 和 `b` 引用同一对象。 如果 `Point` 是结构，则输出 10，因为将 `a` 赋值给 `b` 创建了值副本，而此副本不受后面对 `a.x` 的赋值的影响。

以上示例突出显示了结构的两个限制。 首先，复制整个结构通常比复制对象引用效率更低，因此通过结构进行的赋值和值参数传递可能比通过引用类型成本更高。 其次，除 `in`、`ref` 和 `out` 参数以外，无法创建对结构的引用，这就表示在很多应用场景中都不能使用结构。

### 数组

***数组***是一种数据结构，其中包含许多通过计算索引访问的变量。 数组中的变量（亦称为数组的***元素***）均为同一种类型，我们将这种类型称为数组的***元素类型***。

数组类型是引用类型，声明数组变量只是为引用数组实例预留空间。 实际的数组实例是在运行时使用 new 运算符动态创建而成。 new 运算指定了新数组实例的***长度***，然后在此实例的生存期内固定使用这个长度。 数组元素的索引介于 `0` 到 `Length - 1` 之间。 `new` 运算符自动将数组元素初始化为其默认值（例如，所有数值类型的默认值为 0，所有引用类型的默认值为 `null`）。

以下示例创建 `int` 元素数组，初始化此数组，然后打印输出此数组的内容。

```csharp
using System;
class ArrayExample
{
    static void Main() 
    {
        int[] a = new int[10];
        for (int i = 0; i < a.Length; i++) 
        {
            a[i] = i * i;
        }
        for (int i = 0; i < a.Length; i++) 
        {
            Console.WriteLine($"a[{i}] = {a[i]}");
        }
    }
}
```

上面的示例创建***一维数组***，并对其执行运算。 C# 还支持***多维数组***。 数组类型的维数（亦称为数组类型的***秩***）是 1 与数组类型方括号内的逗号数量相加的结果。 以下示例分别分配一维、二维、三维数组。

```csharp
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
```

`a1` 数组包含 10 个元素，`a2` 数组包含 50 个元素 (10 × 5)，`a3` 数组包含 100 个元素 (10 × 5 × 2)。 数组的元素类型可以是任意类型（包括数组类型）。 包含数组类型元素的数组有时称为***交错数组***，因为元素数组的长度不必全都一样。 以下示例分配由 `int` 数组构成的数组：

```csharp
int[][] a = new int[3][];
a[0] = new int[10];
a[1] = new int[5];
a[2] = new int[20];
```

第一行创建包含三个元素的数组，每个元素都是 `int[]` 类型，并且初始值均为 `null`。 后面的代码行将这三个元素初始化为引用长度不同的各个数组实例。

通过 new 运算符，可以使用***数组初始值设定项***（在分隔符 `{` 和 `}` 内编写的表达式列表）指定数组元素的初始值。 以下示例分配 `int[]`，并将其初始化为包含三个元素。

```csharp
int[] a = new int[] {1, 2, 3};
```

请注意，可从 { 和 } 内的表达式数量推断出数组的长度。 局部变量和字段声明可以进一步缩短，这样就不用重新声明数组类型了。

```csharp
int[] a = {1, 2, 3};
```

以上两个示例等同于以下示例：

```csharp
int[] t = new int[3];
t[0] = 1;
t[1] = 2;
t[2] = 3;
int[] a = t;
```

### 接口

***接口***定义了可由类和结构实现的协定。 接口可以包含方法、属性、事件和索引器。 接口不提供所定义的成员的实现代码，仅指定必须由实现接口的类或结构提供的成员。

接口可以采用***多重继承***。 在以下示例中，接口 `IComboBox` 同时继承自 `ITextBox` 和 `IListBox`。

```csharp
interface IControl
{
    void Paint();
}
interface ITextBox: IControl
{
    void SetText(string text);
}
interface IListBox: IControl
{
    void SetItems(string[] items);
}
interface IComboBox: ITextBox, IListBox {}
```

类和结构可以实现多个接口。 在以下示例中，类 `EditBox` 同时实现 `IControl` 和 `IDataBound`。

```csharp
interface IDataBound
{
    void Bind(Binder b);
}
public class EditBox: IControl, IDataBound
{
    public void Paint() { }
    public void Bind(Binder b) { }
} 
```

当类或结构实现特定接口时，此类或结构的实例可以隐式转换成相应的接口类型。 例如

```csharp
EditBox editBox = new EditBox();
IControl control = editBox;
IDataBound dataBound = editBox;
```

如果已知实例不是静态地实现特定接口，可以使用动态类型显式转换功能。 例如，以下语句使用动态类型显式转换功能来获取对象的 `IControl` 和 `IDataBound` 接口实现代码。 因为对象的运行时实际类型是 `EditBox`，所以显式转换会成功。

```csharp
object obj = new EditBox();
IControl control = (IControl)obj;
IDataBound dataBound = (IDataBound)obj;
```

在前面的 `EditBox` 类中，`IControl` 接口中的 `Paint` 方法和 `IDataBound` 接口中的 `Bind` 方法均使用公共成员进行实现。 C# 还支持显式***接口成员实现代码***，这样类或结构就不会将成员设为公共成员。 显式接口成员实现代码是使用完全限定的接口成员名称进行编写。 例如，`EditBox` 类可以使用显式接口成员实现代码来实现 `IControl.Paint` 和 `IDataBound.Bind` 方法，如下所示。

```csharp
public class EditBox: IControl, IDataBound
{
    void IControl.Paint() { }
    void IDataBound.Bind(Binder b) { }
}
```

显式接口成员只能通过接口类型进行访问。 例如，只有先将 `EditBox` 引用转换成 `IControl` 接口类型，才能调用上面 EditBox 类提供的 `IControl.Paint` 实现代码。

```csharp
EditBox editBox = new EditBox();
editBox.Paint();            // Error, no such method
IControl control = editBox;
control.Paint();            // Ok
```

### 枚举

***枚举类型***是包含一组已命名常量的独特值类型。 需要定义包含一组离散值的类型时，可以定义枚举。 枚举使用一种整型值类型作为其基础存储， 并提供离散值的语义含义。

以下示例声明并使用名为“`Color`”的 `enum` 类型，其中包含三个常量值（`Red`、`Green` 和 `Blue`）。

```csharp
using System;
enum Color
{
    Red,
    Green,
    Blue
}
class EnumExample
{
    static void PrintColor(Color color) 
    {
        switch (color) 
        {
            case Color.Red:
                Console.WriteLine("Red");
                break;
            case Color.Green:
                Console.WriteLine("Green");
                break;
            case Color.Blue:
                Console.WriteLine("Blue");
                break;
            default:
                Console.WriteLine("Unknown color");
                break;
        }
    }
    static void Main() 
    {
        Color c = Color.Red;
        PrintColor(c);
        PrintColor(Color.Blue);
    }
}
```

每个 `enum` 类型都有对应的整型类型（称为 `enum` 类型的***基础类型***）。 如果 `enum` 类型未显式声明基础类型，则基础类型为 `int`。 `enum` 类型的存储格式和可取值范围由基础类型决定。 `enum` 类型需要使用的一组值不受其 `enum` 成员限制。 尤其是，基础类型的 `enum` 的任何值都可以显式转换成 `enum` 类型，并作为 `enum` 类型的不同有效值。

以下示例声明基础类型为 `sbyte` 且名为“`Alignment`”的 `enum` 类型。

```csharp
enum Alignment: sbyte
{
    Left = -1,
    Center = 0,
    Right = 1
}
```

如上面的示例所示，`enum` 成员声明可以包含用于指定成员值的常数表达式。 每个 `enum` 成员的常量值都必须介于 `enum` 的基础类型范围内。 如果 `enum` 成员声明未显式指定值，那么会为成员指定值 0（如果是 `enum` 类型中的首个成员）或原文前一个 `enum` 成员的值加 1。

可使用类型显式转换功能将 `Enum` 值转换成整型值，反之亦然。 例如:

```csharp
int i = (int)Color.Blue;    // int i = 2;
Color c = (Color)2;         // Color c = Color.Blue;  
```

任何 `enum` 类型的默认值都是已转换成 `enum` 类型的整型值 0。 如果变量被自动初始化为默认值，这就是为 `enum` 类型的变量指定的值。 为了让 `enum` 类型的默认值可供方便使用，文本类型 `0` 隐式转换成任意 `enum` 类型。 因此，可以运行以下命令。

```csharp
Color c = 0;
```

### 委托

***委托类型***表示对具有特定参数列表和返回类型的方法的引用。 通过委托，可以将方法视为可分配给变量并可作为参数传递的实体。 委托类似于其他一些语言中的函数指针概念，但与函数指针不同的是，委托不仅面向对象，还类型安全。

下面的示例声明并使用 `Function` 委托类型。

```csharp
using System;
delegate double Function(double x);
class Multiplier
{
    double factor;
    public Multiplier(double factor) 
    {
        this.factor = factor;
    }
    public double Multiply(double x) 
    {
        return x * factor;
    }
}
class DelegateExample
{
    static double Square(double x) 
    {
        return x * x;
    }
    static double[] Apply(double[] a, Function f) 
    {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }
    static void Main() 
    {
        double[] a = {0.0, 0.5, 1.0};
        double[] squares = Apply(a, Square);
        double[] sines = Apply(a, Math.Sin);
        Multiplier m = new Multiplier(2.0);
        double[] doubles =  Apply(a, m.Multiply);
    }
}
```

`Function` 委托类型实例可以引用需要使用 `double` 自变量并返回 `double` 值的方法。 `Apply` 方法将给定的函数应用于 `double[]` 的元素，从而返回包含结果的 `double[]`。 在 `Main` 方法中，`Apply` 用于向 `double[]` 应用三个不同的函数。

委托可以引用静态方法（如上面示例中的 `Square` 或 `Math.Sin`）或实例方法（如上面示例中的 `m.Multiply`）。 引用实例方法的委托还会引用特定对象，通过委托调用实例方法时，该对象会变成调用中的 `this`。

还可以使用匿名函数创建委托，这些函数是便捷创建的“内联方法”。 匿名函数可以查看周围方法的局部变量。 因此，可以更轻松地编写上面的乘数示例，而无需使用 Multiplier 类：



```csharp
double[] doubles =  Apply(a, (double x) => x * 2.0);
```

委托的一个有趣且有用的属性是，它不知道也不关心所引用的方法的类；只关心引用的方法是否具有与委托相同的参数和返回类型。

### 特性

C# 程序中的类型、成员和其他实体支持使用修饰符来控制其行为的某些方面。 例如，方法的可访问性是由 `public`、`protected`、`internal` 和 `private` 修饰符控制。 C# 整合了这种能力，以便可以将用户定义类型的声明性信息附加到程序实体，并在运行时检索此类信息。 程序通过定义和使用***特性***来指定此类额外的声明性信息。

以下示例声明了 `HelpAttribute` 特性，可将其附加到程序实体，以提供指向关联文档的链接。

```csharp
using System;

public class HelpAttribute: Attribute
{
    string url;
    string topic;
    public HelpAttribute(string url) 
    {
        this.url = url;
    }

    public string Url => url;

    public string Topic {
        get { return topic; }
        set { topic = value; }
    }
}
```

所有特性类都派生自标准库提供的 [Attribute](https://docs.microsoft.com/zh-cn/dotnet/api/system.attribute) 基类。 特性的应用方式为，在相关声明前的方括号内指定特性的名称以及任意自变量。 如果特性的名称以 `Attribute` 结尾，那么可以在引用特性时省略这部分名称。 例如，可按如下方法使用 `HelpAttribute`。

```csharp
[Help("https://docs.microsoft.com/dotnet/csharp/tour-of-csharp/attributes")]
public class Widget
{
    [Help("https://docs.microsoft.com/dotnet/csharp/tour-of-csharp/attributes", 
    Topic = "Display")]
    public void Display(string text) {}
}
```

此示例将 `HelpAttribute` 附加到 `Widget` 类。 还向此类中的 `Display` 方法附加了另一个 `HelpAttribute`。 特性类的公共构造函数控制了将特性附加到程序实体时必须提供的信息。 可以通过引用特性类的公共读写属性（如上面示例对 `Topic` 属性的引用），提供其他信息。

可以在运行时使用反射来读取和操纵特性定义的元数据。 如果使用这种方法请求获取特定特性，便会调用特性类的构造函数（在程序源中提供信息），并返回生成的特性实例。 如果是通过属性提供其他信息，那么在特性实例返回前，这些属性会设置为给定值。

下面的代码示例展示了如何获取与 `Widget` 类及其 `Display` 方法相关联的 `HelpAttribute` 实例。

```csharp
Type widgetType = typeof(Widget);

//Gets every HelpAttribute defined for the Widget type
object[] widgetClassAttributes = widgetType.GetCustomAttributes(typeof(HelpAttribute), false);

if (widgetClassAttributes.Length > 0)
{
    HelpAttribute attr = (HelpAttribute)widgetClassAttributes[0];
    Console.WriteLine($"Widget class help URL : {attr.Url} - Related topic : {attr.Topic}");
}

System.Reflection.MethodInfo displayMethod = widgetType.GetMethod(nameof(Widget.Display));

//Gets every HelpAttribute defined for the Widget.Display method
object[] displayMethodAttributes = displayMethod.GetCustomAttributes(typeof(HelpAttribute), false);

if (displayMethodAttributes.Length > 0)
{
    HelpAttribute attr = (HelpAttribute)displayMethodAttributes[0];
    Console.WriteLine($"Display method help URL : {attr.Url} - Related topic : {attr.Topic}");
}

Console.ReadLine();
```



## C# 概念

### C#类型系统

#### 类型、变量和值

C# 是一种强类型语言。 每个变量和常量都有一个类型，每个求值的表达式也是如此。 每个方法签名指定了每个输入参数和返回值的类型。 .NET 类库定义了一组内置数值类型以及表示各种逻辑构造的更复杂类型（如文件系统、网络连接、对象的集合和数组以及日期）。 典型的 C# 程序使用类库中的类型，以及对程序问题域的专属概念进行建模的用户定义类型。

类型中可存储以下信息：

- 类型变量所需的存储空间。
- 可以表示的最大值和最小值。
- 包含的成员（方法、字段、事件等）。
- 继承自的基类型。
- 在运行时分配变量内存的位置。
- 允许执行的运算种类。

编译器使用类型信息来确保在代码中执行的所有操作都是*类型安全*。 例如，如果声明 [int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) 类型的变量，那么编译器允许在加法和减法运算中使用此变量。 如果尝试对 [bool](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/bool) 类型的变量执行这些相同操作，则编译器将生成错误，如以下示例所示：

```csharp
int a = 5;             
int b = a + 2; //OK

bool test = true;
  
// Error. Operator '+' cannot be applied to operands of type 'int' and 'bool'.
int c = a + test;
```

 备注

C 和 C++ 开发人员请注意，在 C# 中，[bool](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/bool) 不能转换为 [int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)。

编译器将类型信息作为元数据嵌入可执行文件中。 公共语言运行时 (CLR) 在运行时使用元数据，以在分配和回收内存时进一步保证类型安全性。

#### 在变量声明中指定类型

当在程序中声明变量或常量时，必须指定其类型或使用 [var](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/var) 关键字让编译器推断类型。 以下示例显示了一些使用内置数值类型和复杂用户定义类型的变量声明：

```csharp
// Declaration only:
float temperature;
string name;
MyClass myClass;

// Declaration with initializers (four examples):
char firstLetter = 'C';
var limit = 3;
int[] source = { 0, 1, 2, 3, 4, 5 };
var query = from item in source
            where item <= limit
            select item;
```

方法签名指定方法参数的类型和返回值。 以下签名显示了需要 [int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) 作为输入参数并返回字符串的方法：

```csharp
public string GetName(int ID)
{
    if (ID < names.Length)
        return names[ID];
    else
        return String.Empty;
}
private string[] names = { "Spencer", "Sally", "Doug" };
```

在声明变量后，不能使用新类型重新声明该变量，并且不能为其分配与其声明的类型不兼容的值。 例如，不能在声明 [int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) 后向其赋值 [true](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/true-literal) 布尔值。 不过，可以将值转换成其他类型。例如，在将值赋给新变量或作为方法自变量传递时。 编译器会自动执行不会导致数据丢失的*类型转换*。 如果类型转换可能会导致数据丢失，必须在源代码中进行*显式转换*。

有关详细信息，请参阅[显式转换和类型转换](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/types/casting-and-type-conversions)。

#### 内置类型

C# 提供了一组标准的内置数值类型来表示整数、浮点值、布尔表达式、文本字符、十进制值和其他数据类型。 还有内置的 `string` 和 `object` 类型。 这些类型可供在任何 C# 程序中使用。 有关内置类型的详细信息，请参阅[内置类型参考表](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/built-in-types-table)。

#### 自定义类型

可以使用[结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct)、[类](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class)、[接口](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/interface)，和[枚举](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/enum)构造创建你自己的自定义类型。 .NET 类库本身就是 Microsoft 提供的一组自定义类型，以供你在自己的应用程序中使用。 默认情况下，类库中最常用的类型在任何 C# 程序中均可用。 对于其他类型，只有在显式添加对定义这些类型的程序集的项目引用时才可用。 编译器引用程序集之后，你可以声明在源代码的此程序集中声明的类型的变量（和常量）。 有关详细信息，请参阅 [.NET 类库](https://docs.microsoft.com/zh-cn/dotnet/standard/class-library-overview)。

#### 通用类型系统

对于 .NET 中的类型系统，请务必了解以下两个基本要点：

- 它支持继承原则。 类型可以派生自其他类型（称为*基类型*）。 派生类型继承（有一些限制）基类型的方法、属性和其他成员。 基类型可以继而从某种其他类型派生，在这种情况下，派生类型继承其继承层次结构中的两种基类型的成员。 所有类型（包括 [System.Int32](https://docs.microsoft.com/zh-cn/dotnet/api/system.int32)C# 关键字：[int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)等内置数值类型）最终都派生自单个基类型，即 [System.Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object)（C# 关键字：[object](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/reference-types)。 这样的统一类型层次结构称为[通用类型系统](https://docs.microsoft.com/zh-cn/dotnet/standard/base-types/common-type-system) (CTS)。 若要详细了解 C# 中的继承，请参阅[继承](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/inheritance)。
- CTS 中的每种类型被定义为值类型或引用类型。 这包括 .NET 类库中的所有自定义类型以及你自己的用户定义类型。 使用 [struct](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct) 关键字定义的类型是值类型；所有内置数值类型都是 `structs`。 使用 [class](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class) 关键字定义的类型是引用类型。 引用类型和值类型遵循不同的编译时规则和运行时行为。

下图展示了 CTS 中值类型和引用类型之间的关系。

下图显示 CTS 中的值类型和引用类型：

![屏幕截图显示了 CTS 值类型和引用类型。](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/types/media/index/value-reference-types-common-type-system.png)

 备注

你可能会发现，最常用的类型全都被整理到了 [System](https://docs.microsoft.com/zh-cn/dotnet/api/system) 命名空间中。 不过，包含类型的命名空间与类型是值类型还是引用类型没有关系。

#### 值类型

值类型派生自[System.ValueType](https://docs.microsoft.com/zh-cn/dotnet/api/system.valuetype)（派生自 [System.Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object)）。 派生自 [System.ValueType](https://docs.microsoft.com/zh-cn/dotnet/api/system.valuetype) 的类型在 CLR 中具有特殊行为。 值类型变量直接包含它们的值，这意味着在声明变量的任何上下文中内联分配内存。 对于值类型变量，没有单独的堆分配或垃圾回收开销。

值类型分为两类：[结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct)和[枚举](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/enum)。

内置数值类型是结构，包含可以访问的属性和方法：

```csharp
// Static method on type byte.
byte b = byte.MaxValue;
```

不过，可以声明数值类型并向其赋值，就像它们是简单的非聚合类型一样：

```csharp
byte num = 0xA;
int i = 5;
char c = 'Z';
```

例如，值类型为“密封” ，这意味着不能从 [System.Int32](https://docs.microsoft.com/zh-cn/dotnet/api/system.int32) 派生类型，并且不能将结构定义为从任何用户定义的类或结构继承，因为结构只能从 [System.ValueType](https://docs.microsoft.com/zh-cn/dotnet/api/system.valuetype) 继承。 但是，一个结构可以实现一个或多个接口。 可将结构类型强制转换为它实现的任何接口类型；这会导致装箱 操作发生，以将结构包装在托管堆上的引用类型对象内。 当你将值类型传递给使用 [System.Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object) 或任何接口类型作为输入参数的方法时，就会发生装箱操作。 有关详细信息，请参阅[装箱和取消装箱](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/types/boxing-and-unboxing)。

使用 [struct](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct) 关键字可以创建你自己的自定义值类型。 结构通常用作一小组相关变量的容器，如以下示例所示：

```csharp
public struct Coords
{
    public int x, y;

    public Coords(int p1, int p2)
    {
        x = p1;
        y = p2;
    }
}
```

有关结构的详细信息，请参阅[结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/structs)。 有关 .NET 中的值类型的详细信息，请参阅[值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/value-types)。

另一种值类型是[枚举](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/enum)。 枚举定义的是一组已命名的整型常量。 例如，.NET 类库中的 [System.IO.FileMode](https://docs.microsoft.com/zh-cn/dotnet/api/system.io.filemode) 枚举包含一组已命名的常量整数，用于指定打开文件应采用的方式。 下面的示例展示了具体定义：

```csharp
public enum FileMode
{
    CreateNew = 1,
    Create = 2,
    Open = 3,
    OpenOrCreate = 4,
    Truncate = 5,
    Append = 6,
}
```

`System.IO.FileMode.Create` 常量的值为 2。 不过，名称对于阅读源代码的人来说更有意义，因此，最好使用枚举，而不是常量数字文本。 有关详细信息，请参阅 [System.IO.FileMode](https://docs.microsoft.com/zh-cn/dotnet/api/system.io.filemode)。

所有枚举从 [System.Enum](https://docs.microsoft.com/zh-cn/dotnet/api/system.enum)（继承自 [System.ValueType](https://docs.microsoft.com/zh-cn/dotnet/api/system.valuetype)）继承。 适用于结构的所有规则也适用于枚举。 有关枚举的详细信息，请参阅[枚举类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/enumeration-types)。

#### 引用类型

定义为[类](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class)、[委托](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/reference-types)、数组或[接口](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/interface)的类型是*引用类型*。 在运行时，当声明引用类型的变量时，该变量会一直包含值 [null](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/null)，直至使用 [new](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/new-operator) 运算符显式创建对象，或者为该变量分配已经在其他位置使用 `new` 创建的对象，如下所示：

```csharp
MyClass mc = new MyClass();
MyClass mc2 = mc;
```

接口必须与实现它的类对象一起初始化。 如果 `MyClass` 实现 `IMyInterface`，则按以下示例所示创建 `IMyInterface` 的实例：

```csharp
IMyInterface iface = new MyClass();
```

创建对象后，内存会在托管堆上进行分配，并且变量只保留对对象位置的引用。 对于托管堆上的类型，在分配内存和 CLR 自动内存管理功能（称为“*垃圾回收*”）回收内存时都会产生开销。 不过，垃圾回收功能也已经过高度优化，大多数情况下，都不会导致性能问题出现。 有关垃圾回收的详细信息，请参阅[自动内存管理](https://docs.microsoft.com/zh-cn/dotnet/standard/automatic-memory-management)。

所有数组都是引用类型，即使元素是值类型，也不例外。 虽然数组隐式派生自 [System.Array](https://docs.microsoft.com/zh-cn/dotnet/api/system.array) 类，但可以使用 C# 提供的简化语法声明和使用数组，如以下示例所示：

```csharp
// Declare and initialize an array of integers.
int[] nums = { 1, 2, 3, 4, 5 };

// Access an instance property of System.Array.
int len = nums.Length;
```

引用类型完全支持继承。 创建类时，可以继承自其他任何未定义为[密封](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/sealed)的接口或类，而其他类也可以继承自你的类并重写你的虚方法。 若要详细了解如何创建你自己的类，请参阅[类和结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/index)。 有关继承和虚方法的详细信息，请参阅[继承](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/inheritance)。

#### 文本值的类型

在 C# 中，文本值从编译器接收类型。 可以通过在数字末尾追加一个字母来指定数字文本应采用的类型。 例如，若要将值 4.56 指定为应按浮点值处理，请在数字后面追加“f”或“F”：`4.56f`。 如果没有追加字母，那么编译器就会推断文本值的类型。 若要详细了解可以使用字母后缀指定哪些类型，请参阅[值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/value-types)中的各个类型参考页。

由于文本已类型化，且所有类型最终都是从 [System.Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object) 派生，因此可以编写和编译如下所示的代码：

```csharp
string s = "The answer is " + 5.ToString();
// Outputs: "The answer is 5"
Console.WriteLine(s);

Type type = 12345.GetType();
// Outputs: "System.Int32"
Console.WriteLine(type);
```

#### 泛型类型

可使用一个或多个类型参数声明、作为客户端代码在创建类型实例时将提供的实际类型（具体类型）的占位符的类型。 这种类型称为泛型类型。 例如，.NET 类型 [System.Collections.Generic.List](https://docs.microsoft.com/zh-cn/dotnet/api/system.collections.generic.list-1) 具有一个类型参数，它按照惯例被命名为 *T*。当创建类型的实例时，指定列表将包含的对象的类型，例如字符串：

```csharp
List<string> stringList = new List<string>();
stringList.Add("String example");
// compile time error adding a type other than a string:
stringList.Add(4);
```

使用类型参数，可以重用同一个类来保留任何类型的元素，而无需将每个元素转换成[对象](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/reference-types)。 泛型集合类称为*强类型集合*，因为编译器知道集合元素的具体类型，并能在编译时抛出错误，例如当尝试向上面示例中的 `stringList` 对象添加整数时。 有关详细信息，请参阅[泛型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/generics/index)。

#### 隐式类型、匿名类型和可以为 null 的值类型

如前所述，你可以使用 [var](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/var) 关键字隐式键入一个局部变量（但不是类成员）。 变量仍可在编译时获取类型，但类型是由编译器提供。 有关详细信息，请参阅[隐式类型局部变量](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables)。

在某些情况下，为不打算在方法边界外存储或传递的各组简单的相关值创建已命名的类型并不方便。 因此，可以创建*匿名类型*。 有关详细信息，请参阅[匿名类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/anonymous-types)。

普通值类型不能包含值 [null](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/null)。 不过，可以在类型后面附加 `?`，创建可以为 null 的值类型。 例如，`int?` 是还可以包含值 [null](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/null) 的 `int` 类型。 可以为 null 的值类型是泛型结构类型 [System.Nullable](https://docs.microsoft.com/zh-cn/dotnet/api/system.nullable-1) 的实例。 在将数据传入和传出数据库（数值可能为 null）时，可以为 null 的值类型特别有用。 有关详细信息，请参阅[可以为 null 的值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/nullable-value-types)。

#### 相关章节

有关详细信息，请参阅下列主题：

- [强制转换和类型转换](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [装箱和取消装箱](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/types/boxing-and-unboxing)
- [使用类型 dynamic](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/types/using-type-dynamic)
- [值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/value-types)
- [引用类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/reference-types)
- [类和结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/index)
- [匿名类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/anonymous-types)
- [泛型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/generics/index)





### 可为空引用类型

C#8.0 引入了“可为空引用类型”和“不可为空引用类型”，使你能够对引用类型变量的属性作出重要声明 ：

- 引用不应为 null 。

   

  当变量不应为 null 时，编译器会强制执行规则，以确保在不首先检查它们是否为 null 的情况下取消引用这些变量是安全的：

  - 必须将变量初始化为非 null 值。
  - 变量永远不能赋值为 `null`。

- 引用可为 null 。

   

  当变量可以为 null 时，编译器会强制执行不同的规则以确保你已正确检查空引用：

  - 只有当编译器可以保证该值不为 null 时，才可以取消引用该变量。
  - 这些变量可以使用默认的 `null` 值进行初始化，也可以在其他代码中赋值为 `null`。

在 C# 的早期版本中，无法从变量声明中确定设计意图，与处理引用变量相比，这个新功能提供了显著的好处。 编译器不提供针对引用类型的空引用异常的安全性：

- 引用可为 null 。 将引用类型初始化为 null 或稍后将其指定为 null 时，编译器不会发出警告。
- 假定引用不为 null 。 当引用类型被取消引用时，编译器不会发出任何警告。 （使用可为空引用，只要取消引用可能为 null 的变量，编译器就会发出警告）。

通过添加可为空引用类型，你可以更清楚地声明你的意图。 `null` 值是表示变量不引用值的正确方法。 请勿使用此功能从代码中删除所有 `null` 值。 相反，应该向编译器和其他读取代码的开发人员声明你的意图。 通过声明意图，编译器会在你编写与该意图不一致的代码时通知你。

使用与[可为空值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/nullable-value-types)相同的语法记录**可为空引用类型**：将 `?` 附加到变量的类型。 例如，以下变量声明表示可为空的字符串变量 `name`：

```csharp
string? name;
```

未将 `?` 附加到类型名称的任何变量都是“不可为空引用类型” 。 这包括启用此功能时现有代码中的所有引用类型变量。

编译器使用静态分析来确定可为空引用是否为非 null。 如果你在一个可为空引用可能是 null 时对其取消引用，编译器将向你发出警告。 可以通过使用 [NULL 包容运算符](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/null-forgiving) `!` 后跟变量名称来替代此行为。 例如，若知道 `name` 变量不为 null 但编译器仍发出警告，则可以编写以下代码来覆盖编译器的分析：

```csharp
name!.Length;
```

#### 类型为 Null 性

任何引用类型都可以具有四个“为 Null 性”中的一个，它描述了何时生成警告 ：

- *不可为空*：无法将 null 分配给此类型的变量。 在取消引用之前，无需对此类型的变量进行 null 检查。
- *可为空*：可将 null 分配给此类型的变量。 在不首先检查 `null` 的情况下取消引用此类型的变量时发出警告。
- *无视*：这是 C# 8.0 之前版本的状态。 可以取消引用或分配此类型的变量而不发出警告。
- *未知*：这通常针对类型参数，约束不告知编译器类型是否必须是“可为空”或“不可为空” 。

变量声明中类型的为 Null 性由声明变量的“可为空上下文”控制 。

#### 可为空上下文

可为空上下文可以对编译器如何解释引用类型变量进行精细控制。 可以启用或禁用任何给定源代码行的“可为空注释上下文” 。 可以将 C# 8.0 之前的编译器视为在禁用的可为空上下文中编译所有代码：任何引用类型都可以为空。 还可以启用或禁用可为空警告上下文 。 可为空警告上下文指定编译器使用其流分析生成的警告。

可以使用 .csproj 文件中的 `Nullable` 元素为项目设置可为空注释上下文和可为空警告上下文。 此元素配置编译器如何解释类型的为 Null 性以及生成哪些警告。 有效设置如下：

- `enable`：“启用”可为空注释上下文 。

   

  “启用”可为空警告上下文 。

  - 引用类型的变量，例如 `string` 是“不可为空”。 启用所有为 Null 性警告。

- `warnings`：“禁用”可为空注释上下文 。

   

  “启用”可为空警告上下文 。

  - 引用类型的变量是“无视”。 启用所有为 Null 性警告。

- `annotations`：“启用”可为空注释上下文 。

   

  “禁用”可为空警告上下文 。

  - 引用类型的变量（例如字符串）不可为 null。 禁用所有为 Null 性警告。

- `disable`：“禁用”可为空注释上下文 。

   

  “禁用”可为空警告上下文 。

  - 引用类型的变量是“无视”，就像早期版本的 C# 一样。 禁用所有为 Null 性警告。

**示例**：

```xml
<Nullable>enable</Nullable>
```

你还可以使用指令在项目的任何位置设置这些相同的上下文：

- `#nullable enable`：将可为空注释上下文和可为空警告上下文设置为“已启用” 。
- `#nullable disable`：将可为空注释上下文和可为空警告上下文设置为“已禁用” 。
- `#nullable restore`：将可为空注释上下文和可为空警告上下文还原到项目设置。
- `#nullable disable warnings`：将可为空警告上下文设置为“已禁用” 。
- `#nullable enable warnings`：将可为空警告上下文设置为“已启用” 。
- `#nullable restore warnings`：将可为空警告上下文还原到项目设置。
- `#nullable disable annotations`：将可为空注释上下文设置为“禁用” 。
- `#nullable enable annotations`：将可为空注释上下文设置为“启用” 。
- `#nullable restore annotations`：将注释警告上下文还原到项目设置。

默认情况下，可为空注释和警告上下文处于禁用状态 。 这意味着无需更改现有代码即可进行编译，并且不会生成任何新警告。

##### 可为空注释上下文

编译器在已禁用的可为空注释上下文中使用以下规则：

- 不能在已禁用的上下文中声明可为空引用。
- 可以将所有引用变量分配为 null。
- 取消引用引用类型的变量时不会生成警告。
- 可能不会在禁用的上下文中使用 null 包容运算符。

该行为与以前版本的 C# 相同。

编译器在已启用的可为空注释上下文中使用以下规则：

- 引用类型的任何变量都是“不可为空引用” 。
- 任何不可为空引用都可以安全地取消引用。
- 任何可为空引用类型（在变量声明中的类型之后由 `?` 标记）可为 null。 静态分析确定在取消引用该值时是否已知该值不为 null。 否则，编译器会发出警告。
- 你可以使用 null 包容运算符声明可为空引用不为 null。

在已启用的可为空注释上下文中，附加到引用类型的 `?` 字符声明“可为空引用类型” 。 可将 NULL 包容运算符 `!` 附加到表达式以声明表达式不为 NULL 。

##### 可为空警告上下文

可为空警告上下文与可为空注释上下文不同。 即使禁用新注释，也可以启用警告。 编译器使用静态流分析来确定任何引用的“null 状态” 。 当“可为空警告上下文”未被“禁用”时，null 状态为“非 null”或“可能为 null” 。 如果在编译器确定引用“可能为 null”时取消引用该引用，编译器会向你发出警告 。 除非编译器可以确定以下两个条件之一，否则引用的状态为“可能为 null” ：

1. 该变量已明确分配给非 null 值。
2. 在取消引用之前，已检查变量或表达式是否为 null。

当可为空警告上下文处于启用状态时，只要取消引用“可能为 null”状态的变量或表达式，编译器就会生成警告 。 此外，在将“可能为 null”变量或表达式分配给已启用的可为空注释上下文中的不可为空引用类型时，将生成警告 





### 使用特性和约束描述可为null的API

#### 更新库以使用可为空的引用类型，并将可为空的规则传达给调用方

加入的[可空引用类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/nullable-references)意味着你可以声明与否`null`的值允许或期望为每个变量。此外，你可以申请一些属性：`AllowNull`，`DisallowNull`，`MaybeNull`，`NotNull`，`NotNullWhen`，`MaybeNullWhen`，并`NotNullWhenNotNull`完整地描述参数和返回值的空状态。这在您编写代码时提供了很棒的经验。如果将不可为空的变量设置为，则会收到警告`null`。如果在取消引用可空变量之前未对其进行空检查，则会收到警告。更新您的图书馆可能要花费一些时间，但是值得付出。您向编译器提供的有关*何时执行*以下操作的更多信息`null`值是允许还是禁止，API用户会得到更好的警告。让我们从一个熟悉的例子开始。假设您的库具有以下API来检索资源字符串：

```csharp
bool TryGetMessage(string key, out string message)
```

前面的示例遵循`Try*`.NET中熟悉的模式。此API有两个参考参数：`key`和`message`参数。该API具有以下与这些参数的无效性有关的规则：

- `null`调用者不应将用作参数`key`。
- `null`调用者可以传递一个变量，该变量的值作为的参数`message`。
- 如果该`TryGetMessage`方法返回`true`，则的值`message`不为null。如果返回值是`false,`的值`message`（且它的null状态）为null。

规则`key`可以完全由变量类型表示：`key`应为不可为空的引用类型。该`message`参数是比较复杂的。它允许`null`作为参数，但保证成功后该`out`参数不为null。对于这些情况，您需要更丰富的词汇表来描述期望。

更新您的库以获取可为空的引用所需要的不仅仅是花`?`一些变量和类型名称。前面的示例表明，您需要检查API并考虑对每个输入参数的期望。考虑对返回值的保证，以及方法返回时的任何`out`或`ref`参数。然后将这些规则传达给编译器，当调用者不遵守这些规则时，编译器将提供警告。

这项工作需要时间。让我们从使您的库或应用程序可为空的策略开始，同时平衡其他要求和可交付成果。您将看到如何平衡正在进行的开发以启用可空引用类型。您将学习通用类型定义的挑战。您将学习如何应用属性来描述各个API的前提条件和条件前提。

#### 选择可为空的策略

首选是默认情况下是否应该将可空引用类型打开或关闭。您有两种策略：

- 为整个项目启用可为空的引用类型，并在尚未准备就绪的代码中将其禁用。
- 仅对已为可空引用类型注释的代码启用可空引用类型。

在为可空引用类型更新库时向库中添加其他功能时，第一种策略最有效。所有新开发都是可为空的。更新现有代码时，将在这些类中启用可为空的引用类型。

按照第一个策略，您可以执行以下操作：

1. 通过将`enable`元素添加到*csproj*文件中，为整个项目启用可为空的类型。
2. 将`#nullable disable`杂项添加到项目中的每个源文件中。
3. 在处理每个文件时，请删除编译指示并解决所有警告。

第一个策略有更多的前期工作来将杂注添加到每个文件中。这样做的好处是，添加到项目中的每个新代码文件都可以为空。任何新作品都将为可空值；仅现有代码必须更新。

如果库通常是稳定的，则第二种策略效果更好，并且开发的主要重点是采用可为空的引用类型。注释API时，您可以打开可为空的引用类型。完成后，为整个项目启用可为空的引用类型。

按照第二种策略，您可以执行以下操作：

1. 将`#nullable enable`杂项添加到要使可为空的文件中。
2. 解决任何警告。
3. 继续前两个步骤，直到使整个库可为空为止。
4. 通过将`enable`元素添加到*csproj*文件中，为整个项目启用可为空的类型。
5. 删除`#nullable enable`杂物，因为它们不再需要。

第二种策略的前期工作较少。权衡是，创建新文件时的首要任务是添加编译指示并使它可以为空。如果您的团队中的任何开发人员忘记了，新的代码现在都在工作中，以使所有代码都可以为空。

您选择哪种策略取决于项目中正在进行多少积极的开发。您的项目越成熟和稳定，第二个策略就越好。开发的功能越多，第一个策略就越好。

#### 可为空的警告是否应该引入重大更改？

在启用可为空的引用类型之前，变量被视为*可为可空的oblivious*。启用可为空的引用类型后，所有这些变量都是*不可为空的*。如果这些变量未初始化为非空值，则编译器将发出警告。

另一个可能的警告源是尚未初始化的返回值。

解决编译器警告的第一步是`?`在参数和返回类型上使用注释，以指示参数或返回值何时为空。如果引用变量不能为null，则原始声明正确。这样做时，您的目标不仅仅是修复警告。更为重要的目标是使编译器了解您潜在的空值的意图。在检查警告时，您将为图书馆做出下一个重大决定。您是否要考虑修改API签名以更清楚地传达您的设计意图？对于`TryGetMessage`前面检查的方法，更好的API签名可能是：

```csharp
string? TryGetMessage(string key);
```

返回值指示成功或失败，如果找到该值，则返回该值。在许多情况下，更改API签名可以改善它们传递空值的方式。

但是，对于公共图书馆或具有庞大用户群的图书馆，您可能希望不引入任何API签名更改。对于这些情况和其他常见模式，您可以应用属性来更清楚地定义参数或返回值何时为`null`。无论您是否考虑更改API的表面，您都可能会发现仅类型注释不足以描述`null`参数值或返回值。在这些情况下，您可以应用属性来更清楚地描述API。

#### 属性扩展类型注释

添加了几个属性来表示有关变量的空状态的其他信息。您在C＃8引入可为空的引用类型之前编写的所有代码都是*null忽略的*。这意味着任何引用类型变量都可以为null，但不需要进行null检查。一旦您的代码可以为*空*，这些规则就会更改。引用类型永远不能是`null`值，并且`null`在取消引用之前，必须先检查可空引用类型。

正如您在`TryGetValue`API场景中所看到的，API 的规则可能更复杂。您的许多API对于何时可以或不可以使用变量都有更复杂的规则`null`。在这些情况下，您将使用以下属性之一来表达这些规则：

- [AllowNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.allownullattribute)：不可为空的输入参数可以为null。
- [DisallowNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.disallownullattribute)：可为空的输入参数绝不能为null。
- [MaybeNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.maybenullattribute)：不可为null的返回值可以为null。
- [NotNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullattribute)：可为空的返回值永远不会为null。
- [MaybeNullWhen](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.maybenullwhenattribute)：当方法返回指定`bool`值时，不可为空的输入参数可能为null 。
- [NotNullWhen](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullwhenattribute)：当方法返回指定`bool`值时，可为空的输入参数将不为null 。
- [NotNullIfNotNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullifnotnullattribute)：如果指定参数的参数不为null，则返回值不为null。

前面的描述是对每个属性的快速参考。以下各节将更详尽地描述其行为和含义。

添加这些属性可为编译器提供有关API规则的更多信息。在启用了可为空的上下文中编译调用代码时，当调用者违反这些规则时，编译器将对其进行警告。这些属性不会对您的实现启用其他检查。

#### 指定前提条件：`AllowNull`和`DisallowNull`

考虑一个读/写属性，该属性永远不会返回，`null`因为它具有合理的默认值。`null`将访问者设置为默认值时，呼叫者会传递给它。例如，考虑一个在聊天室中要求输入屏幕名称的消息传递系统。如果未提供，则系统生成一个随机名称：

```csharp
public string ScreenName
{
   get => screenName;
   set => screenName = value ?? GenerateRandomScreenName();
}
private string screenName;
```

当您在可为空的遗忘上下文中编译前面的代码时，一切都很好。启用可为空的引用类型后，该`ScreenName`属性将成为不可为空的引用。这对于`get`访问器是正确的：它永远不会返回`null`。呼叫者无需检查返回属性是否为`null`。但是现在将属性设置为`null`生成警告。为了继续支持这种类型的代码，请将[System.Diagnostics.CodeAnalysis.AllowNullAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.allownullattribute)属性添加到该属性，如以下代码所示：

```csharp
[AllowNull]
public string ScreenName
{
   get => screenName;
   set => screenName = value ?? GenerateRandomScreenName();
}
private string screenName = GenerateRandomScreenName();
```

您可能需要`using`为[System.Diagnostics.CodeAnalysis](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis)添加指令以使用此属性以及本文中讨论的其他属性。该属性应用于属性，而不应用于`set`访问器。该`AllowNull`属性指定*前提条件*，并且仅适用于输入。该`get`访问有返回值，但没有输入参数。因此，该`AllowNull`属性仅适用于`set`访问器。

前面的示例演示了`AllowNull`在参数上添加属性时要查找的内容：

1. 该变量的一般约定是不应将其设为`null`，因此您需要一个不可为null的引用类型。
2. 在某些情况下，输入变量为`null`，尽管它们不是最常见的用法。

大多数情况下你所需要的属性，或该属性`in`，`out`和`ref`论据。该`AllowNull`属性是最好的选择，当一个变量是典型的非空，但你需要允许`null`为前提。

将其与使用方案进行对比`DisallowNull`：您可以使用此属性来指定不应为可空类型的输入变量`null`。考虑`null`默认值为的属性，但客户端只能将其设置为非空值。考虑以下代码：

```csharp
public string ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new ArgumentNullException(nameof(value), "Cannot set to null");
}
string _comment;
```

前面的代码是表达设计的最佳方式，它`ReviewComment`可以是`null`但不能设置为`null`。一旦此代码可以为空，您就可以使用[System.Diagnostics.CodeAnalysis.DisallowNullAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.disallownullattribute)向调用者更清楚地表达此概念：

```csharp
[DisallowNull] 
public string? ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new ArgumentNullException(nameof(value), "Cannot set to null");
}
string? _comment;
```

在可为空的上下文中，`ReviewComment` `get`访问器可以返回的默认值`null`。编译器警告在访问之前必须对其进行检查。此外，它警告调用者，即使可能`null`，调用者也不应将其显式设置为`null`。该`DisallowNull`属性还指定一个*前提条件*，它不影响`get`访问器。`DisallowNull`当您观察以下方面的特征时，应该选择使用该属性：

1. 该变量可能`null`在核心场景中，通常是在首次实例化时。
2. 该变量不应显式设置为`null`。

这些情况在本来可以*忽略的*代码中很常见。可能是在两个不同的初始化操作中设置了对象属性。可能只有在完成一些异步工作之后才设置某些属性。

使用`AllowNull`和`DisallowNull`属性，您可以指定变量的前提条件可能与这些变量的可空注释不匹配。这些提供有关API特征的更多详细信息。此附加信息可帮助调用者正确使用您的API。请记住，您使用以下属性指定了前提条件：

- [AllowNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.allownullattribute)：不可为空的输入参数可以为null。
- [DisallowNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.disallownullattribute)：可为空的输入参数绝不能为null。

#### 指定后置条件：`MaybeNull`和`NotNull`

假设您有一个具有以下签名的方法：

```csharp
public Customer FindCustomer(string lastName, string firstName)
```

您可能已经编写了这样的方法，以`null`在找不到所需名称时返回。该`null`清楚地表明该记录没有被发现。在此示例中，您可能会将返回类型从更改`Customer`为`Customer?`。将返回值声明为可为空的引用类型可以明确指定此API的意图。

由于[通用定义和可空性](https://docs.microsoft.com/zh-cn/dotnet/csharp/nullable-attributes#generic-definitions-and-nullability)所涵盖的原因[，](https://docs.microsoft.com/zh-cn/dotnet/csharp/nullable-attributes#generic-definitions-and-nullability)该技术不适用于通用方法。您可能具有遵循类似模式的通用方法：

```csharp
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> match)
```

您不能指定返回值为`T?`。`null`当找不到所需的项目时，该方法返回。由于无法声明`T?`返回类型，因此可以将`MaybeNull`注释添加到return方法中：

```csharp
[return: MaybeNull]
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> match)
```

前面的代码通知调用者该合同隐含一个不可为空的类型，但返回值实际上*可能*为null。`MaybeNull`当您的API应该是不可为null的类型（通常是通用类型参数）时，请使用属性，但是在某些情况下`null`会返回该实例。

您也可以指定返回值或`out`or `ref`参数不为null，即使该类型是可为null的类型也是如此。考虑一种确保数组足够容纳多个元素的方法。如果输入参数不具有容量，则例程将分配一个新数组并将所有现有元素复制到该数组中。如果输入参数为`null`，则例程将分配新的存储。如果有足够的容量，则例程将不执行任何操作：

```csharp
public void EnsureCapacity<T>(ref T[] storage, int size)
```

您可以按以下方式调用此例程：

```csharp
// messages has the default value (null) when EnsureCapacity is called:
EnsureCapacity<string>(ref messages, 10);
// messages is not null.
EnsureCapacity<string>(messages, 50);
```

启用空引用类型后，您要确保前面的代码在编译时没有警告。当方法返回时，`storage`保证参数不为null。但是，可以`EnsureCapacity`使用空引用进行调用。您可以创建`storage`可为空的引用类型，并将`NotNull`后置条件添加到参数声明中：

```csharp
public void EnsureCapacity<T>([NotNull]ref T[]? storage, int size)
```

前面的代码非常清楚地表达了现有合同：调用者可以传递带有`null`值的变量，但是保证返回值永远不会为null。该`NotNull`属性对于可以作为参数传递的`ref`和`out`参数最有用`null`，但是保证方法返回时该参数不为null。

您可以使用以下属性指定无条件后置条件：

- [MaybeNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.maybenullattribute)：不可为null的返回值可以为null。
- [NotNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullattribute)：可为空的返回值永远不会为null。

#### 指定条件后置条件：`NotNullWhen`，`MaybeNullWhen`，和`NotNullIfNotNull`

您可能熟悉[String.IsNullOrEmpty（String）](https://docs.microsoft.com/en-us/dotnet/api/system.string.isnullorempty#System_String_IsNullOrEmpty_System_String_)`string`方法。当参数为null或空字符串时，此方法返回。这是null检查的一种形式：如果方法返回，则调用者无需对参数进行null检查。为了使这种方法可以感知可空值，您可以将参数设置为可空值类型，然后添加属性：`true``false``NotNullWhen`

```csharp
bool IsNullOrEmpty([NotNullWhen(false)]string? value);
```

通知编译器`false`不需要对返回值进行任何检查的任何代码。该属性的添加通知编译器`IsNullOrEmpty`进行必要的空检查的静态分析：返回时`false`，输入参数不是`null`。

```csharp
string? userInput = GetUserInput();
if (!(string.IsNullOrEmpty(userInput))
{
   int messageLength = userInput.Length; // no null check needed.
}
// null check needed on userInput here.
```

所述[String.IsNullOrEmpty（字符串）](https://docs.microsoft.com/en-us/dotnet/api/system.string.isnullorempty#System_String_IsNullOrEmpty_System_String_)所示上述用于.NET核心3.0方法将进行注释。您的代码库中可能有类似的方法，用于检查对象的状态是否为空值。编译器无法识别自定义的null检查方法，因此您需要自己添加注释。添加属性时，编译器的静态分析会知道何时对测试的变量进行空检查。

这些属性的另一个用途是`Try*`模式。对于后置条件`ref`和`out`变量是通过返回值传递。考虑前面显示的这种方法：

```csharp
bool TryGetMessage(string key, out string message)
```

前面的方法遵循典型的.NET习惯用法：返回值指示是否将`message`其设置为找到的值，或者，如果没有找到消息，则返回默认值。如果该方法返回`true`，则的值`message`不为null；否则，该方法设置`message`为null。

您可以使用`NotNullWhen`属性传达该成语。当您更新为空的引用类型的签名，让`message`一个`string?`并添加属性：

```csharp
bool TryGetMessage(string key, [NotNullWhen(true)] out string? message)
```

在前面的例子中，的值`message`已知是当不为空`TryGetMessage`的回报`true`。您应该以相同的方式在代码库中注释类似的方法：参数可以是`null`，并且当方法返回时，已知参数不为null `true`。

您可能还需要一个最终属性。有时，返回值的空状态取决于一个或多个输入参数的空状态。每当某些输入参数不是时，这些方法将返回非null值`null`。要正确注释这些方法，请使用`NotNullIfNotNull`属性。请考虑以下方法：

```csharp
string GetTopLevelDomainFromFullUrl(string url);
```

如果`url`参数不为null，则输出为not `null`。启用可空引用后，只要您的API绝不接受空输入，该签名就可以正常工作。但是，如果输入可以为空，则返回值也可以为空。因此，您可以将签名更改为以下代码：

```csharp
string? GetTopLevelDomainFromFullUrl(string? url);
```

这也可以，但是通常会迫使调用者执行额外的`null`检查。合同规定，`null`仅当输入参数为时，返回值`url`才是`null`。要表达该合同，您需要对此方法进行注释，如以下代码所示：

```csharp
[return: NotNullIfNotNull("url")]
string? GetTopLevelDomainFromFullUrl(string? url);
```

返回值和参数均已注有注释，`?`指出两者中的任何一个都可以为`null`。该属性进一步阐明，当`url`参数为not 时，返回值将不为null `null`。

您可以使用以下属性指定条件后置条件：

- [MaybeNullWhen](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.maybenullwhenattribute)：当方法返回指定`bool`值时，不可为空的输入参数可能为null 。
- [NotNullWhen](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullwhenattribute)：当方法返回指定`bool`值时，可为空的输入参数将不为null 。
- [NotNullIfNotNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullifnotnullattribute)：如果指定参数的输入参数不为null，则返回值不为null。

#### 泛型定义和可空性

正确传达通用类型和通用方法的空状态需要特别注意。这源于以下事实：可为空的值类型和可为空的引用类型根本不同。一个`int?`为同义词`Nullable`，而`string?`是`string`由编译器添加的属性。结果是编译器在`T?`不知道`T`a `class`或a的情况下无法为其生成正确的代码`struct`。

这并不意味着您不能将可为空的类型（值类型或引用类型）用作封闭的泛型类型的类型参数。这两个`List`和`List`是有效的实例`List`。

它的意思是您不能`T?`在没有约束的情况下在泛型类或方法声明中使用。例如，[Enumerable.FirstOrDefault （IEnumerable ）](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.firstordefault#System_Linq_Enumerable_FirstOrDefault__1_System_Collections_Generic_IEnumerable___0__)不会更改为return `T?`。您可以通过添加`struct`或`class`约束来克服此限制。无论使用哪种这些约束，编译器知道如何为这两种生成代码`T`和`T?`。

您可能希望将用于通用类型参数的类型限制为不可为空的类型。您可以通过`notnull`在该类型参数上添加约束来实现。应用该约束时，type参数不能为可为空的类型。

#### 结论

添加可为空的引用类型可提供初始词汇表，以描述您的API对可能为的变量的期望`null`。附加属性提供了更丰富的词汇表，用于将变量的空状态描述为前提条件和后置条件。这些属性可以更清楚地描述您的期望，并为使用您的API的开发人员提供更好的体验。

在为可为空的上下文更新库时，添加这些属性以指导API用户正确使用。这些属性可帮助您完全描述输入参数和返回值的空状态：

- [AllowNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.allownullattribute)：不可为空的输入参数可以为null。
- [DisallowNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.disallownullattribute)：可为空的输入参数绝不能为null。
- [MaybeNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.maybenullattribute)：不可为null的返回值可以为null。
- [NotNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullattribute)：可为空的返回值永远不会为null。
- [MaybeNullWhen](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.maybenullwhenattribute)：当方法返回指定`bool`值时，不可为空的输入参数可能为null 。
- [NotNullWhen](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullwhenattribute)：当方法返回指定`bool`值时，可为空的输入参数将不为null 。
- [NotNullIfNotNull](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.codeanalysis.notnullifnotnullattribute)：如果指定参数的输入参数不为null，则返回值不为null。

### 命名空间

在 C# 编程中，命名空间在两个方面被大量使用。 首先，.NET Framework 使用命名空间来组织许多类，如下所示：

```csharp
System.Console.WriteLine("Hello World!");
```

`System` 是一个命名空间，`Console` 是该命名空间中的一个类。 可以使用 `using` 关键字，如此则不必使用完整的名称，如下例所示：

```csharp
using System;
```

```csharp
Console.WriteLine("Hello");
Console.WriteLine("World!");
```

有关详细信息，请参阅 [using 指令](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/using-directive)。

其次，在较大的编程项目中，声明自己的命名空间可以帮助控制类和方法名称的范围。 使用 [namespace](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/namespace) 关键字可声明命名空间，如下例所示：

```csharp
namespace SampleNamespace
{
    class SampleClass
    {
        public void SampleMethod()
        {
            System.Console.WriteLine(
              "SampleMethod inside SampleNamespace");
        }
    }
}
```

命名空间的名称必须是有效的 C# [标识符名称](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/inside-a-program/identifier-names)。

#### 命名空间概述

命名空间具有以下属性：

- 它们组织大型代码项目。
- 通过使用 `.` 运算符分隔它们。
- `using` 指令可免去为每个类指定命名空间的名称。
- `global` 命名空间是“根”命名空间：`global::System` 始终引用 .NET [System](https://docs.microsoft.com/zh-cn/dotnet/api/system) 命名空间。

#### C# 语言规范

有关详细信息，请参阅 [C# 语言规范](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/language-specification/introduction)中的[命名空间](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/language-specification/namespaces)部分。





### 基本类型

#### 类型、变量和值

C# 是一种强类型语言。 每个变量和常量都有一个类型，每个求值的表达式也是如此。 每个方法签名指定了每个输入参数和返回值的类型。 .NET Framework 类库定义了一组内置数值类型以及表示各种逻辑构造的更复杂类型（如文件系统、网络连接、对象的集合和数组以及日期）。 典型的 C# 程序使用类库中的类型，以及对程序问题域的专属概念进行建模的用户定义类型。

类型中可存储以下信息：

- 类型变量所需的存储空间。
- 可以表示的最大值和最小值。
- 包含的成员（方法、字段、事件等）。
- 继承自的基类型。
- 在运行时分配变量内存的位置。
- 允许执行的运算种类。

编译器使用类型信息来确保在代码中执行的所有操作都是*类型安全*。 例如，如果声明 [int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) 类型的变量，那么编译器允许在加法和减法运算中使用此变量。 如果尝试对 [bool](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/bool) 类型的变量执行这些相同操作，则编译器将生成错误，如以下示例所示：

```csharp
int a = 5;             
int b = a + 2; //OK

bool test = true;

// Error. Operator '+' cannot be applied to operands of type 'int' and 'bool'.
int c = a + test;
```

 备注

C 和 C++ 开发人员请注意，在 C# 中，[bool](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/bool) 不能转换为 [int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)。

编译器将类型信息作为元数据嵌入可执行文件中。 公共语言运行时 (CLR) 在运行时使用元数据，以在分配和回收内存时进一步保证类型安全性。

#### 在变量声明中指定类型

当在程序中声明变量或常量时，必须指定其类型或使用 [var](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/var) 关键字让编译器推断类型。 以下示例显示了一些使用内置数值类型和复杂用户定义类型的变量声明：

C#复制

```csharp
// Declaration only:
float temperature;
string name;
MyClass myClass;

// Declaration with initializers (four examples):
char firstLetter = 'C';
var limit = 3;
int[] source = { 0, 1, 2, 3, 4, 5 };
var query = from item in source
            where item <= limit
            select item;
```

方法签名指定方法参数的类型和返回值。 以下签名显示了需要 [int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) 作为输入参数并返回字符串的方法：

C#复制

```csharp
public string GetName(int ID)
{
    if (ID < names.Length)
        return names[ID];
    else
        return String.Empty;
}
private string[] names = { "Spencer", "Sally", "Doug" };
```

在声明变量后，不能使用新类型重新声明该变量，并且不能为其分配与其声明的类型不兼容的值。 例如，不能在声明 [int](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) 后向其赋值 [true](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/true-literal) 布尔值。 不过，可以将值转换成其他类型。例如，在将值赋给新变量或作为方法自变量传递时。 编译器会自动执行不会导致数据丢失的*类型转换*。 可能导致数据丢失的转换需要在源代码进行强制转换。

有关详细信息，请参阅[强制转换和类型转换](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/types/casting-and-type-conversions)。

#### 内置类型

C# 提供了一组标准的内置数值类型来表示整数、浮点值、布尔表达式、文本字符、十进制值和其他数据类型。 另外，还有内置**字符串**和**对象**类型。 这些类型可供在任何 C# 程序中使用。 有关内置类型的详细信息，请参阅[内置类型参考表](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/built-in-types-table)。

#### 自定义类型

可以使用[结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class)、[类](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class)、[接口](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/interface)，和[枚举](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/enum)构造创建你自己的自定义类型。 .NET Framework 类库本身就是 Microsoft 提供的一组自定义类型，以供你在自己的应用程序中使用。 默认情况下，类库中最常用的类型在任何 C# 程序中均可用。 对于其他类型，只有在显式添加对定义这些类型的程序集的项目引用时才可用。 编译器引用程序集之后，你可以声明在源代码的此程序集中声明的类型的变量（和常量）。

#### 泛型类型

可使用一个或多个类型参数声明、作为客户端代码在创建类型实例时将提供的实际类型（具体类型）的占位符的类型。 这种类型称为泛型类型。 例如，.NET Framework 类型 [List](https://docs.microsoft.com/zh-cn/dotnet/api/system.collections.generic.list-1) 具有一个类型参数，它按照惯例被命名为 *T*。创建类型实例时，指定列表将包含的对象类型，例如字符串：

C#复制

```csharp
List<string> strings = new List<string>();
```

使用类型参数，可以重用同一个类来保留任何类型的元素，而无需将每个元素转换成[对象](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/reference-types#the-object-type)。 泛型集合类称为*强类型集合*，因为编译器知道集合元素的具体类型，并能在编译时抛出错误，例如当尝试向上面示例中的 `strings` 对象添加整数时。 有关详细信息，请参阅[泛型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/generics/index)。

#### 隐式类型、匿名类型和元组类型

如前所述，你可以使用 [var](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/var) 关键字隐式键入一个局部变量（但不是类成员）。 变量在编译时仍可接收类型，但类型由编译器提供。 有关详细信息，请参阅[隐式类型本地变量](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables)。

在某些情况下，为不打算存储或传递外部方法边界的简单相关值集合创建命名类型是不方便的。 为此，你可以创建匿名类型。 有关详细信息，请参阅[匿名类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/anonymous-types)。

经常需要从方法返回多个值。 可以创建在单个方法调用中返回多个值的元组类型。 有关详细信息，请参阅[元组](https://docs.microsoft.com/zh-cn/dotnet/csharp/tuples)。

#### 通用类型系统

了解 .NET Framework 中的类型系统的两个基本点非常重要：

- 它支持继承原则。 类型可以派生自其他类型（称为*基类型*）。 派生类型继承（有一些限制）基类型的方法、属性和其他成员。 基类型可以继而从某种其他类型派生，在这种情况下，派生类型继承其继承层次结构中的两种基类型的成员。 所有类型（包括 [Int32](https://docs.microsoft.com/zh-cn/dotnet/api/system.int32) (C# keyword: `int`) 等内置数值类型）最终都派生自单个基类型，即 [Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object) (C# keyword: `object`)。 此统一类型层次结构称为[通用类型系统](https://docs.microsoft.com/zh-cn/dotnet/standard/common-type-system) (CTS)。 有关 C# 中的继承的详细信息，请参阅[继承](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/inheritance)。
- CTS 中的每种类型被定义为值类型或引用类型。 这包括 .NET Framework 类库中的所有自定义类型以及你自己的用户定义类型。 使用 [struct](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct) 关键字定义的类型是值类型；所有内置数值类型都是 **structs**。 有关值类型的详细信息，请参阅[结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/structs)。 使用 [class](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class) 关键字定义的类型是引用类型。 有关引用类型的详细信息，请参阅[类](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/classes)。 引用类型和值类型具有不同的编译时规则和不同的运行时行为。

### 类

#### 引用类型

定义为[类](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class)的一个类型是*引用类型*。 在运行时，如果声明引用类型的变量，此变量就会一直包含值 [null](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/null)，直到使用 [new](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/new-operator) 运算符显式创建类实例，或直到为此变量分配可能已在其他位置创建的兼容类型的对象，如下面的示例所示：

```csharp
//Declaring an object of type MyClass.
MyClass mc = new MyClass();

//Declaring another object of the same type, assigning it the value of the first object.
MyClass mc2 = mc;
```

创建对象时，在该托管堆上为该特定对象分足够的内存，并且该变量仅保存对所述对象位置的引用。 当分配托管堆上的类型和由 CLR 的自动内存管理功能对其进行回收（称为*垃圾回收*）时，需要开销。 但是，垃圾回收已是高度优化，并且在大多数情况下，不会产生性能问题。 有关垃圾回收的详细信息，请参阅[自动内存管理和垃圾回收](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/gc)。

#### 声明类

使用后跟唯一标识符的 [class](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class) 关键字可以声明类，如下例所示：

```csharp
//[access modifier] - [class] - [identifier]
public class Customer
{
   // Fields, properties, methods and events go here...
}
```

`class` 关键字前面是访问级别。 因为此例中使用的是 [public](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/public)，所以任何人都可以创建此类的实例。 类的名称遵循 `class` 关键字。 类名称必须是有效的 C# [标识符名称](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/inside-a-program/identifier-names)。 定义的其余部分是类的主体，其中定义了行为和数据。 类上的字段、属性、方法和事件统称为*类成员*。

#### 创建对象

虽然它们有时可以互换使用，但类和对象是不同的概念。 类定义对象类型，但不是对象本身。 对象是基于类的具体实体，有时称为类的实例。

可通过使用 [new](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/new-operator) 关键字，后跟对象要基于的类的名称，来创建对象，如：

C#复制

```csharp
Customer object1 = new Customer();
```

创建类的实例后，会将一个该对象的引用传递回程序员。 在上一示例中，`object1` 是对基于 `Customer` 的对象的引用。 该引用指向新对象，但不包含对象数据本身。 事实上，可以创建对象引用，而完全无需创建对象本身：

```csharp
 Customer object2;
```

不建议创建这样一个不引用对象的对象引用，因为尝试通过这类引用访问对象会在运行时失败。 但实际上可以使用这类引用来引用某个对象，方法是创建新对象，或者将其分配给现有对象，例如：

```csharp
Customer object3 = new Customer();
Customer object4 = object3;
```

此代码创建指向同一对象的两个对象引用。 因此，通过 `object3` 对对象做出的任何更改都会在后续使用 `object4` 时反映出来。 由于基于类的对象是通过引用来实现其引用的，因此类被称为引用类型。

#### 类继承

类完全支持继承 ，这是面向对象的编程的基本特点。 创建类时，可以继承自其他任何未定义为 [sealed](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/sealed) 的接口或类，而且其他类也可以继承自你的类并重写类虚方法。

继承是通过使用*派生*来完成的，这意味着类是通过使用其数据和行为所派生自的*基类*来声明的。 基类通过在派生的类名称后面追加冒号和基类名称来指定，如：

```csharp
public class Manager : Employee
{
    // Employee fields, properties, methods and events are inherited
    // New Manager fields, properties, methods and events go here...
}
```

类声明基类时，会继承基类除构造函数外的所有成员。 有关详细信息，请参阅[继承](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/inheritance)。

与 C++ 不同，C# 中的类只能直接从基类继承。 但是，因为基类本身可能继承自其他类，因此类可能间接继承多个基类。 此外，类还可以直接实现多个接口。 有关详细信息，请参阅[接口](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/interfaces/index)。

类可以声明为 [abstract](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/abstract)（抽象）。 抽象类包含抽象方法，抽象方法包含签名定义但不包含实现。 抽象类不能实例化。 只能通过可实现抽象方法的派生类来使用该类。 与此相反，[sealed](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/sealed)（密封）类不允许其他类继承。 有关详细信息，请参阅[抽象类、密封类和类成员](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members)。

类定义可以在不同的源文件之间分割。 有关详细信息，请参阅[分部类和方法](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)。

#### 示例

以下示例定义了一个公共类，该类包含一个[自动实现的属性](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)、一个方法和一个名为构造函数的特殊方法。 有关详细信息，请参阅[属性](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/properties)、[方法](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/methods)和[构造函数](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/constructors)主题。 然后使用 `new` 关键字实例化类的实例。

```csharp
using System;

public class Person
{
    // Constructor that takes no arguments:
    public Person()
    {
        Name = "unknown";
    }

    // Constructor that takes one argument:
    public Person(string name)
    {
        Name = name;
    }

    // Auto-implemented readonly property:
    public string Name { get; }

    // Method that overrides the base class (System.Object) implementation.
    public override string ToString()
    {
        return Name;
    }
}
class TestPerson
{
    static void Main()
    {
        // Call the constructor that has no parameters.
        var person1 = new Person();
        Console.WriteLine(person1.Name);

        // Call the constructor that has one parameter.
        var person2 = new Person("Sarah Jones");
        Console.WriteLine(person2.Name);
        // Get the string representation of the person2 instance.
        Console.WriteLine(person2);

        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}
// Output:
// unknown
// Sarah Jones
// Sarah Jones
```

#### C# 语言规范

有关详细信息，请参阅 [C# 语言规范](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/language-specification/index)。 该语言规范是 C# 语法和用法的权威资料。

### 结构

结构 是一个值类型。 创建结构时，分配给结构的变量保留结构的实际数据。 将结构分配给新变量时，会复制结构。 因此，新变量和原始变量包含相同数据的副本（共两个）。 对一个副本所做的更改不会影响另一个副本。

值类型变量直接包含它们的值，这意味着在声明变量的任何上下文中内联分配内存。 对于值类型变量，没有单独的堆分配或垃圾回收开销。

值类型分为两类：[结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct)和[枚举](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/enum)。

内置数值类型是结构，包含可以访问的属性和方法：

```csharp
// Static method on type Byte.  
byte b = Byte.MaxValue;
```

不过，可以声明数值类型并向其赋值，就像它们是简单的非聚合类型一样：

```csharp
byte num = 0xA;  
int i = 5;  
char c = 'Z';
```

例如，值类型为“密封” ，这意味着不能从 [Int32](https://docs.microsoft.com/zh-cn/dotnet/api/system.int32) 派生类型，并且不能将结构定义为从任何用户定义的类或结构继承，因为结构只能从 [ValueType](https://docs.microsoft.com/zh-cn/dotnet/api/system.valuetype) 继承。 但是，一个结构可以实现一个或多个接口。 可将结构类型强制转换为接口类型；这将导致“装箱” 操作，以将结构包装在托管堆上的引用类型对象内。 当将值类型传递到接受 [Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object) 作为输入参数的方法时，将发生装箱操作。 有关详细信息，请参阅[装箱和取消装箱](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/types/boxing-and-unboxing)。

使用 [struct](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct) 关键字可以创建你自己的自定义值类型。 结构通常用作一小组相关变量的容器，如以下示例所示：

```csharp
public struct Coords
{
    public int x, y;

    public Coords(int p1, int p2)
    {
        x = p1;
        y = p2;
    }
}
```

有关 .NET Framework 中的值类型的详细信息，请参阅[通用类型系统](https://docs.microsoft.com/zh-cn/dotnet/standard/common-type-system)。

结构与类具有许多相同的语法，但结构比类受到的限制更多：

- 在结构声明中，除非将字段声明为 `const` 或 `static`，否则无法初始化。
- 结构不能声明无参数构造函数（没有参数的构造函数）或终结器。
- 结构在分配时进行复制。 将结构分配给新变量时，将复制所有数据，并且对新副本所做的任何修改不会更改原始副本的数据。 使用值类型的集合（如 Dictionary<string, myStruct>）时，请务必记住这一点。
- 结构是值类型，而类是引用类型。
- 与类不同，无需使用 `new` 运算符即可对结构进行实例化。
- 结构可以声明具有参数的构造函数。
- 一个结构无法继承自另一个结构或类，并且它不能为类的基类。 所有结构都直接继承自 [ValueType](https://docs.microsoft.com/zh-cn/dotnet/api/system.valuetype)，后者继承自 [Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object)。
- 结构可以实现接口。

#### 可以为 null 的值类型

普通值类型不能具有 [null](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/null) 值。 不过，可以在类型后面附加 `?`，创建可以为 null 的值类型。 例如，`int?` 是还可以包含值 [null](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/null) 的 `int` 类型。 可以为 null 的值类型是泛型结构类型 [Nullable](https://docs.microsoft.com/zh-cn/dotnet/api/system.nullable-1) 的实例。 在将数据传入和传出数据库（数值可能为 NULL 或未定义）时，可为空的值类型特别有用。 有关详细信息，请参阅[可以为 null 的值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/nullable-value-types)。



### 元组

#### C# 元组类型

C# 元组是使用轻量语法定义的类型。 其优点包括：更简单的语法，基于元素数量（称为“基数”）和元素类型的转换规则，以及一致的副本、相等测试和赋值规则。 但另一方面，元组不支持一些与继承相关的面向对象的语法。 [C# 7.0 中的新增功能](https://docs.microsoft.com/zh-cn/dotnet/csharp/whats-new/csharp-7#tuples)文章中的“元组”一节对其进行了概述。

在本文中，你将了解用于控制 C# 7.0 及更高版本中的元组的语言规则、这些规则的各种用法，以及有关如何使用元组的初步指导。

 备注

新的元组功能需要 [ValueTuple](https://docs.microsoft.com/zh-cn/dotnet/api/system.valuetuple) 类型。 为在不包括该类型的平台上使用它，必须添加 NuGet 包 [`System.ValueTuple`](https://www.nuget.org/packages/System.ValueTuple/)。

这类似于依赖框架提供的类型的其他语言功能。 例如，依赖 `INotifyCompletion` 接口的 `async` 和 `await`，依赖 `IEnumerable` 的 LINQ。 但是，随着 .NET 越来越不依赖平台，交付机制也在发生改变。 .NET Framework 交付频率可能不会与语言编译器的始终相同。 新语言功能依赖于新类型时，这些类型将在交付语言功能时以 NuGet 包的形式提供。 这些新类型添加到 .NET 标准 API 并作为框架的一部分交付后，将删除 NuGet 包要求。

我们先解释一下为什么要添加新的元组支持。 方法返回单个对象。 借助元组，可以更轻松地对该单个对象中的多个值打包。

.NET Framework 已具有泛型 `Tuple` 类。 但这些类有两个主要限制。 其一，`Tuple` 类将其属性命名为 `Item1`、`Item2` 等。 这些名称未承载任何语义信息。 使用这些 `Tuple` 类型无法表达各属性的含义。 通过新的语言功能，可对元组中的各元素进行声明并为其赋予有意义的语义名称。

`Tuple` 类因其引用类型会导致更多性能问题。 使用任一 `Tuple` 类型即意味着分配对象。 在热路径中，分配许多小型对象可能会对应用程序性能产生明显的影响。 因此，元组的语言支持使用新的 `ValueTuple` 结构。

为避免这些缺陷，可创建 `class` 或 `struct` 来承载多个元素。 但这样做不仅加大了工作量，还掩盖了你的设计意图。 创建 `struct` 或 `class` 意味着定义一个具有数据和行为的类型。 很多时候，你其实只是想存储单个对象中的多个值而已。

这些语言功能和 `ValueTuple` 泛型结构共同实施以下规则：不能向这些元组类型添加任何行为（方法）。 所有 `ValueTuple` 类型都是*可变结构*。 每个成员字段都是公共字段。 这使它们变得非常轻量。 但是，这意味着在要求永久性的场合无法使用元组。

元组是比 `class` 和 `struct` 类型更为简单灵活的数据容器。 我们来探讨一下它们之间的差异。

#### 命名元组和未命名元组

`ValueTuple` 结构具有名为 `Item1`、`Item2`、`Item3` 等的字段，与现有 `Tuple` 类型中定义的属性类似。 这些名称是可用于*未命名元组*的唯一名称。 如果不为元组提供任何备用字段名称，即表示创建了一个未命名元组：

```csharp
var unnamed = ("one", "two");
```

上例中的元组已使用文本常量进行初始化，并且不会有 C# 7.1 中使用“元组字段名称投影” 创建的元素名称。

但是，在初始化元组时，可以使用新语言功能为每个字段提供更好的名称。 如此便创建了*命名元组*。 命名元组仍将元素命名为 `Item1`、`Item2`、`Item3` 等。 不过，它们还会为这些已命名的元素提供同义词。 通过为每个元素指定名称即可创建命名元组。 其中一种方式是在元组初始化过程中指定名称：

```csharp
var named = (first: "one", second: "two");
```

这些同义词由编译器和语言处理，因此，你可以高效地使用命名元组。 IDE 和编辑器可以使用 Roslyn API 读取这些语义名称。 可以在同一程序集中的任何位置通过这些语义名称引用命名元组的元素。 编译器在生成已编译的输出时，会将已定义的名称替换为 `Item*` 等效项。 已编译的 Microsoft 中间语言 (MSIL) 不包括为这些元素赋予的名称。

从 C# 7.1 开始，元组的字段名称可能会通过用于初始化此元组的变量提供。 这称为[元组投影初始值设定项](https://docs.microsoft.com/zh-cn/dotnet/csharp/tuples#tuple-projection-initializers) 。 以下代码用于创建名为 `accumulation` 的元组，包含元素 `count`（整数）和 `sum`（双精度）。

```csharp
var sum = 12.5;
var count = 5;
var accumulation = (count, sum);
```

编译器必须传达为从公共方法或属性返回的元组创建的这些名称。 在这种情况下，编译器会在方法上添加 [TupleElementNamesAttribute](https://docs.microsoft.com/zh-cn/dotnet/api/system.runtime.compilerservices.tupleelementnamesattribute) 特性。 此特性包含一个 [TransformNames](https://docs.microsoft.com/zh-cn/dotnet/api/system.runtime.compilerservices.tupleelementnamesattribute.transformnames#System_Runtime_CompilerServices_TupleElementNamesAttribute_TransformNames) 列表属性，该属性包含为元组中的每个元素赋予的名称。

 备注

Visual Studio 等开发工具还读取其元数据，并提供 IntelliSense 和其他使用元数据字段名称的功能。

请务必理解新元组和 `ValueTuple` 类型的这些基础知识，这样才能理解将命名元组赋给彼此的规则。

#### 元组投影初始值设定项

一般情况下，元组投影初始值设定项使用元组初始化语句右侧的变量或字段名称。 如果未提供显式名称，上述名称将优先于任何投影的名称。 例如，在以下初始值设定项中，元素为 `explicitFieldOne` 和 `explicitFieldTwo`，而非 `localVariableOne` 和 `localVariableTwo`：

```csharp
var localVariableOne = 5;
var localVariableTwo = "some text";

var tuple = (explicitFieldOne: localVariableOne, explicitFieldTwo: localVariableTwo);
```

对于任何未提供显式名称的字段，将投影适用的隐式名称。 不要求提供显式或隐式语义名称。 以下初始化表达式具有字段名称 `Item1`其值为 `42`和 `stringContent`（其值为“The answer to everything”）：

```csharp
var stringContent = "The answer to everything";
var mixedTuple = (42, stringContent);
```

在以下两种情况下，不会将候选字段名称投影到元组字段：

1. 候选名称是保留元组名称时。 示例包括 `Item3`、`ToString` 或 `Rest`。
2. 候选名称重复了另一元组的显式或隐式字段名称时。

这两个条件可避免多义性。 如果这些名称已用作元组中某字段的字段名称，它们将导致多义。 这两个条件都不会导致编译时错误。 但不会向没有投影名称的元素投影语义名称。 以下示例说明了这两个条件：

```csharp
var ToString = "This is some text";
var one = 1;
var Item1 = 5;
var projections = (ToString, one, Item1);
// Accessing the first field:
Console.WriteLine(projections.Item1);
// There is no semantic name 'ToString'
// Accessing the second field:
Console.WriteLine(projections.one);
Console.WriteLine(projections.Item2);
// Accessing the third field:
Console.WriteLine(projections.Item3);
// There is no semantic name 'Item1`.

var pt1 = (X: 3, Y: 0);
var pt2 = (X: 3, Y: 4);

var xCoords = (pt1.X, pt2.X);
// There are no semantic names for the fields
// of xCoords. 

// Accessing the first field:
Console.WriteLine(xCoords.Item1);
// Accessing the second field:
Console.WriteLine(xCoords.Item2);
```

这些情况不会导致编译器错误，因为当元组字段名称投影不可用时，它将成为使用 C# 7.0 编写的代码的一项重大改变。

#### 相等和元组

从 C# 7.3 开始，元组类型支持 `==` 和 `!=` 运算符。 这些运算符按顺序将左边参数的每个成员与右边参数的每个成员进行比较。 这些比较将发生短路。 只要有一对不相等，它们即会停止计算成员。 以下代码示例使用 `==`，但比较规则均适用于 `!=`。 以下代码示例演示两对整数的相等比较：

```csharp
var left = (a: 5, b: 10);
var right = (a: 5, b: 10);
Console.WriteLine(left == right); // displays 'true'
```

有几条规则，可使元组相等测试更方便。 如果其中一个元组是可以为空值的元组，则元组相等将执行[提升转换](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/language-specification/conversions#lifted-conversion-operators)，如以下代码中所示：

```csharp
var left = (a: 5, b: 10);
var right = (a: 5, b: 10);
(int a, int b)? nullableTuple = right;
Console.WriteLine(left == nullableTuple); // Also true
```

元组相等还将对这两个元组的每个成员执行隐式转换。 这些转换包括提升转换、扩大转换或其他隐式转换。 以下示例演示整数 2 元组可以与较长的 2 元组进行比较，因为进行了从整数元组到较长元组的隐式转换：

```csharp
// lifted conversions
var left = (a: 5, b: 10);
(int? a, int? b) nullableMembers = (5, 10);
Console.WriteLine(left == nullableMembers); // Also true

// converted type of left is (long, long)
(long a, long b) longTuple = (5, 10);
Console.WriteLine(left == longTuple); // Also true

// comparisons performed on (long, long) tuples
(long a, int b) longFirst = (5, 10);
(int a, long b) longSecond = (5, 10);
Console.WriteLine(longFirst == longSecond); // Also true
```

元组成员名称不参与相等测试。 但是，如果其中一个操作数是含有显式名称的元组文本，则当这些名称与其他操作数的名称不匹配时，编译器将生成警告 CS8383。 在两个操作数都为元组文本的情况下，警告位于右侧操作数，如以下示例中所述：

```csharp
(int a, string b) pair = (1, "Hello");
(int z, string y) another = (1, "Hello");
Console.WriteLine(pair == another); // true. Member names don't participate.
Console.WriteLine(pair == (z: 1, y: "Hello")); // warning: literal contains different member names
```

最后，元组可能包含嵌套元组。 元组相等通过嵌套元组比较每个操作数的“形状”，如以下示例中所示：

```csharp
(int, (int, int)) nestedTuple = (1, (2, 3));
Console.WriteLine(nestedTuple == (1, (2, 3)) );
```

当两个元组具有不同形状时，比较它们是否相等（或不相等）将出现编译时错误。 编译器不会尝试对嵌套元组进行任何析构来比较它们。

#### 赋值和元组

语言支持在具有相同元素数量的元组类型之间赋值，其中每个右侧元素都可被隐式转换为相应的左侧元素。 对于其他转换，不考虑进行赋值。 当两个元组具有不同形状时，将一个元祖分配给另一个元祖将出现编译时错误。 编译器不会尝试对嵌套元组进行任何析构来分配它们。 让我们看一下元组类型之间允许的赋值类型。

注意以下示例中使用的这些变量：

```csharp
// The 'arity' and 'shape' of all these tuples are compatible. 
// The only difference is the field names being used.
var unnamed = (42, "The meaning of life");
var anonymous = (16, "a perfect square");
var named = (Answer: 42, Message: "The meaning of life");
var differentNamed = (SecretConstant: 42, Label: "The meaning of life");
```

前两个变量（`unnamed` 和 `anonymous`）没有为元素提供语义名称。 字段名称为 `Item1` 和 `Item2`。 后两个变量（`named` 和 `differentName`）为元素提供了语义名称。 这两个元组具有不同的元素名称。

这四个元组具有相同数量的元素（称为“基数”），这些元素的类型也完全一样。 因此可进行以下赋值：

```csharp
unnamed = named;

named = unnamed;
// 'named' still has fields that can be referred to
// as 'answer', and 'message':
Console.WriteLine($"{named.Answer}, {named.Message}");

// unnamed to unnamed:
anonymous = unnamed;

// named tuples.
named = differentNamed;
// The field names are not assigned. 'named' still has 
// fields that can be referred to as 'answer' and 'message':
Console.WriteLine($"{named.Answer}, {named.Message}");

// With implicit conversions:
// int can be implicitly converted to long
(long, string) conversion = named;
```

请注意，元组的名称未赋值。 元素的赋值顺序遵循元素在元组中的顺序。

元素类型或数量不同的元组不可赋值：

```csharp
// Does not compile.
// CS0029: Cannot assign Tuple(int,int,int) to Tuple(int, string)
var differentShape = (1, 2, 3);
named = differentShape;
```

#### 作为方法返回值的元组

元组最常见的用途之一是作为方法返回值。 我们来看一个示例。 以下面的方法为例，该方法计算一个数列的标准差：

```csharp
public static double StandardDeviation(IEnumerable<double> sequence)
{
    // Step 1: Compute the Mean:
    var mean = sequence.Average();

    // Step 2: Compute the square of the differences between each number 
    // and the mean:
    var squaredMeanDifferences = from n in sequence
                                 select (n - mean) * (n - mean);
    // Step 3: Find the mean of those squared differences:
    var meanOfSquaredDifferences = squaredMeanDifferences.Average();

    // Step 4: Standard Deviation is the square root of that mean:
    var standardDeviation = Math.Sqrt(meanOfSquaredDifferences);
    return standardDeviation;
}
```

 备注

这些示例计算得出未修正的样本标准差。 与 `Average` 扩展方法一样，修正后的样本标准差公式将与平均数之差的平方的总和除以 (N-1)，而不是 N。 有关这些标准差公式之间的区别的更多详细信息，请查看统计信息文本。

前面的代码采用教科书上的标准差公式。 它会生成正确的答案，但实施起来非常低效。 此方法对数列进行两次计算：一次生成平均数，一次生成与平均数之差的平方的平均数。 （请记住，LINQ 查询进行迟缓计算，因此，在计算与平均数的差以及这些差的平均数时只需计算一次。）

有一个计算标准差的备用公式，它只对数列计算一次。 此计算公式在计算数列时生成两个值：数列中所有项的总和，以及每个平方值的总和：

```csharp
public static double StandardDeviation(IEnumerable<double> sequence)
{
    double sum = 0;
    double sumOfSquares = 0;
    double count = 0;

    foreach (var item in sequence)
    {
        count++;
        sum += item;
        sumOfSquares += item * item;
    }

    var variance = sumOfSquares - sum * sum / count;
    return Math.Sqrt(variance / count);
}
```

此版本虽然只对序列进行一次枚举。 但其代码不可重复使用。 到后面，你会发现许多不同的统计计算会用到数列项数、数列总和以及数列平方和。 让我们重构此方法，编写一个可生成这三个值的实用方法。 所有这三个值都可以作为一个元组返回。

让我们更新此方法，以便将在计算过程中得出的三个值存储在一个元组中。 以下是更新后的版本：

```csharp
public static double StandardDeviation(IEnumerable<double> sequence)
{
    var computation = (Count: 0, Sum: 0.0, SumOfSquares: 0.0);

    foreach (var item in sequence)
    {
        computation.Count++;
        computation.Sum += item;
        computation.SumOfSquares += item * item;
    }

    var variance = computation.SumOfSquares - computation.Sum * computation.Sum / computation.Count;
    return Math.Sqrt(variance / computation.Count);
}
```

在 Visual Studio 的重构支持下，可以轻松地将核心统计信息的功能提取到私有方法中。 从而得到一个 `private static` 方法，该方法返回具有 `Sum`、`SumOfSquares` 和 `Count` 这三个值的元组类型：

```csharp
public static double StandardDeviation(IEnumerable<double> sequence)
{
    (int Count, double Sum, double SumOfSquares) computation = ComputeSumAndSumOfSquares(sequence);

    var variance = computation.SumOfSquares - computation.Sum * computation.Sum / computation.Count;
    return Math.Sqrt(variance / computation.Count);
}

private static (int Count, double Sum, double SumOfSquares) ComputeSumAndSumOfSquares(IEnumerable<double> sequence)
{
    var computation = (count: 0, sum: 0.0, sumOfSquares: 0.0);

    foreach (var item in sequence)
    {
        computation.count++;
        computation.sum += item;
        computation.sumOfSquares += item * item;
    }

    return computation;
}
```

如果你想手动进行一些快速编辑，该语言可提供更多选项供你使用。 首先，可以使用 `var` 声明来初始化 `ComputeSumAndSumOfSquares` 方法调用的元组结果。 此外，还可以在 `ComputeSumAndSumOfSquares` 方法内创建三个离散变量。 下面的代码演示了最终版本：

```csharp
public static double StandardDeviation(IEnumerable<double> sequence)
{
    var computation = ComputeSumAndSumOfSquares(sequence);

    var variance = computation.SumOfSquares - computation.Sum * computation.Sum / computation.Count;
    return Math.Sqrt(variance / computation.Count);
}

private static (int Count, double Sum, double SumOfSquares) ComputeSumAndSumOfSquares(IEnumerable<double> sequence)
{
    double sum = 0;
    double sumOfSquares = 0;
    int count = 0;

    foreach (var item in sequence)
    {
        count++;
        sum += item;
        sumOfSquares += item * item;
    }

    return (count, sum, sumOfSquares);
}
```

这个最终版本可用于任何需要这三个值或其任意子集的方法。

该语言支持其他用于管理这些元组返回方法中的元素名称的选项。

可以删除返回值声明中的字段名称，返回一个未命名元组：

```csharp
private static (double, double, int) ComputeSumAndSumOfSquares(IEnumerable<double> sequence)
{
    double sum = 0;
    double sumOfSquares = 0;
    int count = 0;

    foreach (var item in sequence)
    {
        count++;
        sum += item;
        sumOfSquares += item * item;
    }

    return (sum, sumOfSquares, count);
}
```

此元组的字段被命名为 `Item1`、`Item2` 和 `Item3`。 建议为从方法返回的元组的元素提供语义名称。

元组另一个常见的用途是在你创作 LINQ 查询时。 最终投影的结果通常包含被选中的对象的某些（而不是全部）属性。

传统做法是将查询结果投影成一个匿名类型的对象序列。 这种做法存在很多限制，主要是因为匿名类型无法在方法的返回类型中方便地命名。 也可以将 `object` 或 `dynamic` 用作结果类型，但这种备用方法会产生高昂的性能成本。

返回一个元组类型序列非常简单，并且不管是在编译时还是通过 IDE 工具，都可以获取其元素的名称和类型。 以 ToDo 应用程序为例。 可以定义一个与下面类似的类，以表示待办事项列表中的某一项：

```csharp
public class ToDoItem
{
    public int ID { get; set; }
    public bool IsDone { get; set; }
    public DateTime DueDate { get; set; }
    public string Title { get; set; }
    public string Notes { get; set; }    
}
```

移动应用程序可能支持当前待办事项的简洁版，即仅显示标题。 该 LINQ 查询生成一个仅包含 ID 和标题的投影。 返回一个元组序列的方法很好地表达了该设计：

```csharp
internal IEnumerable<(int ID, string Title)> GetCurrentItemsMobileList()
{
    return from item in AllItems
           where !item.IsDone
           orderby item.DueDate
           select (item.ID, item.Title);
}
```

 备注

在 C# 7.1 中，通过元组投影可使用元素，以类似于在匿名类型中命名属性的方式创建命名元组。 在以上代码中，查询投影中的 `select` 语句将创建具有元素 `ID` 和 `Title` 的元组。

命名元组可以是签名的一部分。 它让编译器和 IDE 工具提供静态检查，看结果的用法是否正确。 命名元组还承载了静态类型信息，因此无需使用高成本的运行时功能（如反射或动态绑定）来处理结果。

#### 析构

通过对方法返回的元组进行析构，可以解封元组中的所有项 。 有三种元组析构方法。 首先，可在括号内显式声明每个字段的类型，为元组中的每个元素创建离散变量：

```csharp
public static double StandardDeviation(IEnumerable<double> sequence)
{
    (int count, double sum, double sumOfSquares) = ComputeSumAndSumOfSquares(sequence);

    var variance = sumOfSquares - sum * sum / count;
    return Math.Sqrt(variance / count);
}
```

也可以通过在括号外使用 `var` 关键字，隐式声明元组中每个字段的类型化变量：

```csharp
public static double StandardDeviation(IEnumerable<double> sequence)
{
    var (sum, sumOfSquares, count) = ComputeSumAndSumOfSquares(sequence);

    var variance = sumOfSquares - sum * sum / count;
    return Math.Sqrt(variance / count);
}
```

还可以在括号内将 `var` 关键字与任意或全部变量声明结合使用。

```csharp
(double sum, var sumOfSquares, var count) = ComputeSumAndSumOfSquares(sequence);
```

即使元组中的每个字段都具有相同的类型，也不能在括号外使用特定类型。

也可以使用现有声明析构元组：

```csharp
public class Point
{
    public int X { get; set; }
    public int Y { get; set; }

    public Point(int x, int y) => (X, Y) = (x, y);
}
```

 警告

不能混合现有声明和括号内的声明。 例如，不允许以下内容：`(var x, y) = MyMethod();`。 这将产生错误 CS8184，因为 x 在括号内声明，且 y 以前在其他位置声明。

##### 析构用户定义类型

如上所示，可以析构任何元组类型。 也可以对任何用户定义的类型（类、结构甚至接口）轻松启用析构。

类型作者可定义一个或多个赋值给任意数量的 `out` 变量的 `Deconstruct` 方法，这类变量表示构成该类型的数据元素。 例如，以下 `Person` 类型定义 `Deconstruct` 方法，该方法将 person 对象析构成表示名字和姓氏的元素：

```csharp
public class Person
{
    public string FirstName { get; }
    public string LastName { get; }

    public Person(string first, string last)
    {
        FirstName = first;
        LastName = last;
    }

    public void Deconstruct(out string firstName, out string lastName)
    {
        firstName = FirstName;
        lastName = LastName;
    }
}
```

该析构方法支持从 `Person` 赋值给两个表示 `FirstName` 和 `LastName` 属性的字符串：

```csharp
var p = new Person("Althea", "Goodwin");
var (first, last) = p;
```

即使对未创作的类型，也可以启用析构。 `Deconstruct` 方法可以是一种扩展方法，用于解封对象的可访问数据成员。 以下示例显示从 `Person` 类型派生的 `Student` 类型，以及将 `Student` 析构成三个变量（表示 `FirstName`、`LastName` 和 `GPA`）的扩展方法：

```csharp
public class Student : Person
{
    public double GPA { get; }
    public Student(string first, string last, double gpa) :
        base(first, last)
    {
        GPA = gpa;
    }
}

public static class Extensions
{
    public static void Deconstruct(this Student s, out string first, out string last, out double gpa)
    {
        first = s.FirstName;
        last = s.LastName;
        gpa = s.GPA;
    }
}
```

`Student` 对象现在有两个可访问的 `Deconstruct` 方法：为 `Student` 类型声明的扩展方法，以及 `Person` 类型的成员。 两者都可用，可将 `Student` 析构为两个或三个变量。 如果为 student 分配三个变量，则返回名字、姓氏和 GPA。 如果为 student 分配两个变量，则仅返回名字和姓氏。

```csharp
var s1 = new Student("Cary", "Totten", 4.5);
var (fName, lName, gpa) = s1;
```

在某个类或类层次结构中定义多个 `Deconstruct` 方法时应非常小心。 具有相同数量的 `out` 参数的多个 `Deconstruct` 方法很快就会产生歧义。 调用方可能无法轻松调用所需的 `Deconstruct` 方法。

在此示例中，发生有歧义的调用的几率很小，因为用于 `Person` 的 `Deconstruct` 方法有两个输出参数，而用于 `Student` 的 `Deconstruct` 方法有三个输出参数。

析构运算符不参与测试相等。 下面的示例生成编译器错误 CS0019：

```csharp
Person p = new Person("Althea", "Goodwin");
if (("Althea", "Goodwin") == p)
    Console.WriteLine(p);
```

`Deconstruct` 方法无法将 `Person` 对象 `p` 转换为包含两个字符串的元组，但它在相等测试上下文中不适用。

#### 元组作为 out 参数

元组自身可用作 out 参数 。 不要与前面提到的[析构函数](https://docs.microsoft.com/zh-cn/dotnet/csharp/tuples#deconstruction)部分中的任何多义性混淆。 在方法调用中，只需描述元组的形状：

```csharp
Dictionary<int, (int, string)> dict = new Dictionary<int, (int, string)>();
dict.Add(1, (234, "First!"));
dict.Add(2, (345, "Second"));
dict.Add(3, (456, "Last"));

// TryGetValue already demonstrates using out parameters
dict.TryGetValue(2, out (int num, string place) pair);

Console.WriteLine($"{pair.num}: {pair.place}");

/*
 * Output:
 * 345: Second
 */
```

另外，还可以使用 [unnamed ](https://docs.microsoft.com/zh-cn/dotnet/csharp/tuples#named-and-unnamed-tuples)元组，并将其字段作为 `Item1` 和 `Item2` 引用：

```csharp
dict.TryGetValue(2, out (int, string) pair);
// ...
Console.WriteLine($"{pair.Item1}: {pair.Item2}");
```

#### 结束语

命名元组的新语言和库支持简化了设计工作：与类和结构一样，使用数据结构存储多个元素，但不定义行为。 对这些类型使用元组非常简单明了。 既可以获得静态类型检查的所有好处，又不需要使用更复杂的 `class` 或 `struct` 语法来创作类型。 即便如此，元组还是对 `private` 或 `internal` 这样的实用方法最有用。 当公共方法返回具有多个元素的值时，请创建用户定义的类型（`class` 或 `struct` 类型）。

### 析构元组和其他类型

元组提供一种从方法调用中检索多个值的轻量级方法。 但是，一旦检索到元组，就必须处理它的各个元素。 按元素逐个执行此操作会比较麻烦，如下例所示。 `QueryCityData` 方法返回一个 3 元组，并通过单独的操作将其每个元素分配给一个变量。

```csharp
using System;

public class Example
{
    public static void Main()
    {
        var result = QueryCityData("New York City");

        var city = result.Item1;
        var pop = result.Item2;
        var size = result.Item3;

         // Do something with the data.
    }

    private static (string, int, double) QueryCityData(string name)
    {
        if (name == "New York City")
            return (name, 8175133, 468.48);

        return ("", 0, 0);
    }
}
```

从对象检索多个字段值和属性值可能同样麻烦：必须按成员逐个将字段值或属性值赋给一个变量。

从 C# 7.0 开始，用户可从元组中检索多个元素，或在单个析构操作中从对象检索多个字段值、属性值和计算值 。 析构元组时，将其元素分配给各个变量。 析构对象时，将选定值分配给各个变量。

#### 析构元组

C# 提供内置的元组析构支持，可在单个操作中解包一个元组中的所有项。 用于析构元组的常规语法与用于定义元组的语法相似：将要向其分配元素的变量放在赋值语句左侧的括号中。 例如，以下语句将 4 元组的元素分配给 4 个单独的变量：

```csharp
var (name, address, city, zip) = contact.GetAddressInfo();
```

有三种方法可用于析构元组：

- 可以在括号内显式声明每个字段的类型。 以下示例使用此方法来析构由 `QueryCityData` 方法返回的 3 元组。

  C#复制

  ```csharp
  public static void Main()
  {
      (string city, int population, double area) = QueryCityData("New York City");
  
      // Do something with the data.
  }
  ```

- 可使用 `var` 关键字，以便 C# 推断每个变量的类型。 将 `var` 关键字放在括号外。 以下示例在析构由 `QueryCityData` 方法返回的 3 元组时使用类型推理。

  C#复制

  ```csharp
  public static void Main()
  {
      var (city, population, area) = QueryCityData("New York City");
  
      // Do something with the data.
  }
  ```

  还可在括号内将 `var` 关键字单独与任一或全部变量声明结合使用。

  C#复制

  ```csharp
  public static void Main()
  {
      (string city, var population, var area) = QueryCityData("New York City");
  
      // Do something with the data.
  }
  ```

  这很麻烦，不建议这样做。

- 最后，可将元组析构到已声明的变量中。

  C#复制

  ```csharp
  public static void Main()
  {
      string city = "Raleigh";
      int population = 458880;
      double area = 144.8;
  
      (city, population, area) = QueryCityData("New York City");
  
      // Do something with the data.
  }
  ```

请注意，即使元组中的每个字段都具有相同的类型，也不能在括号外指定特定类型。 这会生成编译器错误 CS8136：“析构 var (...) 形式不允许对 var 使用特定类型。”

请注意，还必须将元组的每个元素分配给一个变量。 如果省略任何元素，编译器将生成错误 CS8132，“无法将 ‘x’ 元素的元组析构为 ‘y’ 变量”。

请注意，不能混合析构左侧上现有变量的声明和赋值。 编译器生成错误 CS8184“析构不能混合左侧的声明和表达式”。 当成员包括新声明的和现有的变量。

#### 使用弃元析构元组元素

析构元组时，通常只需要关注某些元素的值。 从 C# 7.0 开始，便可利用 C# 对弃元的支持，弃元是一种仅能写入的变量，且其值将被忽略 。 在赋值中，通过下划线字符 (_) 指定弃元。 可弃元任意数量的值，且均由单个弃元 `_` 表示。

以下示例演示了对元组使用弃元时的用法。 `QueryCityDataForYears` 方法返回一个 6 元组，包含城市名称、城市面积、一个年份、该年份的城市人口、另一个年份及该年份的城市人口。 该示例显示了两个年份之间人口的变化。 对于元组提供的数据，我们不关注城市面积，并在一开始就知道城市名称和两个日期。 因此，我们只关注存储在元组中的两个人口数量值，可将其余值作为占位符处理。

```csharp
using System;
using System.Collections.Generic;

public class Example
{
    public static void Main()
    {
        var (_, _, _, pop1, _, pop2) = QueryCityDataForYears("New York City", 1960, 2010);

        Console.WriteLine($"Population change, 1960 to 2010: {pop2 - pop1:N0}");
    }
   
    private static (string, double, int, int, int, int) QueryCityDataForYears(string name, int year1, int year2)
    {
        int population1 = 0, population2 = 0;
        double area = 0;
      
        if (name == "New York City")
        {
            area = 468.48; 
            if (year1 == 1960)
            {
                population1 = 7781984;
            }
            if (year2 == 2010)
            {
                population2 = 8175133;
            }
            return (name, area, year1, population1, year2, population2);
        }

        return ("", 0, 0, 0, 0, 0);
    }
}
// The example displays the following output:
//      Population change, 1960 to 2010: 393,149
```

#### 析构用户定义类型

对于非元组类型的解构，C# 不提供内置支持。 但是，用户作为类、结构或接口的创建者，可通过实现一个或多个 `Deconstruct`方法来析构该类型的实例。 该方法返回 void，且要析构的每个值由方法签名中的 [out](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/out-parameter-modifier) 参数指示。 例如，下面的 `Person` 类的 `Deconstruct` 方法返回名字、中间名和姓氏：

```csharp
public void Deconstruct(out string fname, out string mname, out string lname)
```

然后，可使用类似于以下的分配来析构名为 `p` 的 `Person` 类的实例：

```csharp
var (fName, mName, lName) = p;
```

以下示例重载 `Deconstruct` 方法以返回 `Person` 对象的各种属性组合。 单个重载返回：

- 名字和姓氏。
- 名字、姓氏和中间名。
- 名字、姓氏、城市名和省/市/自治区名。

```csharp
using System;

public class Person
{
    public string FirstName { get; set; }
    public string MiddleName { get; set; }
    public string LastName { get; set; }
    public string City { get; set; }
    public string State { get; set; }

    public Person(string fname, string mname, string lname, 
                  string cityName, string stateName)
    {
        FirstName = fname;
        MiddleName = mname;
        LastName = lname;
        City = cityName;
        State = stateName;
    }

    // Return the first and last name.
    public void Deconstruct(out string fname, out string lname)
    {
        fname = FirstName;
        lname = LastName;
    }

    public void Deconstruct(out string fname, out string mname, out string lname)
    {
        fname = FirstName;
        mname = MiddleName;
        lname = LastName;
    }

    public void Deconstruct(out string fname, out string lname, 
                            out string city, out string state)
    {
        fname = FirstName;
        lname = LastName;
        city = City;
        state = State;
    }
}

public class Example
{
    public static void Main()
    {
        var p = new Person("John", "Quincy", "Adams", "Boston", "MA");

        // Deconstruct the person object.
        var (fName, lName, city, state) = p;
        Console.WriteLine($"Hello {fName} {lName} of {city}, {state}!");
    }
}
// The example displays the following output:
//    Hello John Adams of Boston, MA!
```

因为可重载 `Deconstruct` 方法来反映通常从对象中提取的数据组，所以应使用独特明确的签名来定义 `Deconstruct` 方法。 如果有多个 `Deconstruct` 方法具有相同数量的 `out` 参数，或具有相同数量和类型的 `out` 参数且顺序不同，则可能会造成混淆。

以下示例中的重载 `Deconstruct` 方法演示一种混淆的可能性。 第一个重载按该顺序返回 `Person` 对象的名字、中间名、姓氏和年龄。 第二个重载仅将姓名信息与年收入一起返回，但名字、中间名和姓氏的顺序不同。 这使得在析构 `Person` 实例时容易混淆参数的顺序。

```csharp
using System;

public class Person
{
    public string FirstName { get; set; }
    public string MiddleName { get; set; }
    public string LastName { get; set; }
    public string City { get; set; }
    public string State { get; set; }
    public DateTime DateOfBirth { get; set; }
    public Decimal AnnualIncome { get; set; }

    public void Deconstruct(out string fname, out string mname, out string lname, out int age)
    {
        fname = FirstName;
        mname = MiddleName;
        lname = LastName;
        age = DateTime.Now.Year - DateOfBirth.Year;

        if (DateTime.Now.DayOfYear - (new DateTime(DateTime.Now.Year, DateOfBirth.Month, DateOfBirth.Day)).DayOfYear < 0)
            age--;
    }

    public void Deconstruct(out string lname, out string fname, out string mname, out decimal income)
    {
        fname = FirstName;
        mname = MiddleName;
        lname = LastName;
        income = AnnualIncome;
    }
}
```

#### 使用弃元析构用户定义类型

就像使用[元组](https://docs.microsoft.com/zh-cn/dotnet/csharp/deconstruct#deconstructing-tuple-elements-with-discards)一样，可使用弃元来忽略 `Deconstruct` 方法返回的选定项。 每个弃元均由名为“_”的变量定义，一个析构操作可包含多个弃元。

以下示例将 `Person` 对象析构为四个字符串（名字、姓氏、城市和省/市/自治区），但舍弃姓氏和省/市/自治区。

```csharp
// Deconstruct the person object.
var (fName, _, city, _) = p;
Console.WriteLine($"Hello {fName} of {city}!");
// The example displays the following output:
//      Hello John of Boston!
```

#### 使用扩展方法析构用户定义的类型

如果没有创建类、结构或接口，仍可通过实现一个或多个 `Deconstruct` [扩展方法](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/extension-methods)来析构该类型的对象，以返回所需值。

以下示例为 [System.Reflection.PropertyInfo](https://docs.microsoft.com/zh-cn/dotnet/api/system.reflection.propertyinfo) 类定义了两个 `Deconstruct` 扩展方法。 第一个方法返回一组值，指示属性的特征，包括其类型、是静态还是实例、是否为只读，以及是否已编制索引。 第二个方法指示属性的可访问性。 因为 get 和 set 访问器的可访问性可能不同，所以布尔值指示属性是否具有单独的 get 和 set 访问器，如果是，则指示它们是否具有相同的可访问性。 如果只有一个访问器，或者 get 和 set 访问器具有相同的可访问性，则 `access` 变量指示整个属性的可访问性。 否则，get 和 set 访问器的可访问性由 `getAccess` 和 `setAccess` 变量指示。

```csharp
using System;
using System.Collections.Generic;
using System.Reflection;

public static class ReflectionExtensions
{
    public static void Deconstruct(this PropertyInfo p, out bool isStatic,
                                   out bool isReadOnly, out bool isIndexed,
                                   out Type propertyType)
    {
        var getter = p.GetMethod;

        // Is the property read-only?
        isReadOnly = ! p.CanWrite;

        // Is the property instance or static?
        isStatic = getter.IsStatic;

        // Is the property indexed?
        isIndexed = p.GetIndexParameters().Length > 0;

        // Get the property type.
        propertyType = p.PropertyType;
    }

    public static void Deconstruct(this PropertyInfo p, out bool hasGetAndSet,
                                   out bool sameAccess, out string access,
                                   out string getAccess, out string setAccess)
    {
        hasGetAndSet = sameAccess = false;
        string getAccessTemp = null;
        string setAccessTemp = null;

        MethodInfo getter = null;
        if (p.CanRead) 
            getter = p.GetMethod;

        MethodInfo setter = null;
        if (p.CanWrite) 
            setter = p.SetMethod;

        if (setter != null && getter != null)
            hasGetAndSet = true;

        if (getter != null)
        {
            if (getter.IsPublic)
                getAccessTemp = "public";
            else if (getter.IsPrivate)
                getAccessTemp = "private";
            else if (getter.IsAssembly)
                getAccessTemp = "internal";
            else if (getter.IsFamily)
                getAccessTemp = "protected";
            else if (getter.IsFamilyOrAssembly) 
                getAccessTemp = "protected internal";
        }

        if (setter != null)
        {
            if (setter.IsPublic)
                setAccessTemp = "public";
            else if (setter.IsPrivate)
                setAccessTemp = "private";
            else if (setter.IsAssembly)
                setAccessTemp = "internal";
            else if (setter.IsFamily)
                setAccessTemp = "protected";
            else if (setter.IsFamilyOrAssembly)
                setAccessTemp = "protected internal";
        }

        // Are the accessibility of the getter and setter the same?
        if (setAccessTemp == getAccessTemp)
        {
            sameAccess = true;
            access = getAccessTemp;
            getAccess = setAccess = String.Empty;
        }
        else
        {
            access = null;
            getAccess = getAccessTemp;
            setAccess = setAccessTemp;
        }
    }
}

public class Example
{
    public static void Main()
    {
        Type dateType = typeof(DateTime);
        PropertyInfo prop = dateType.GetProperty("Now");
        var (isStatic, isRO, isIndexed, propType) = prop;
        Console.WriteLine($"\nThe {dateType.FullName}.{prop.Name} property:");
        Console.WriteLine($"   PropertyType: {propType.Name}");
        Console.WriteLine($"   Static:       {isStatic}");
        Console.WriteLine($"   Read-only:    {isRO}");
        Console.WriteLine($"   Indexed:      {isIndexed}");

        Type listType = typeof(List<>);
        prop = listType.GetProperty("Item", 
                                    BindingFlags.Public | BindingFlags.NonPublic | BindingFlags.Instance | BindingFlags.Static);
        var (hasGetAndSet, sameAccess, accessibility, getAccessibility, setAccessibility) = prop;
        Console.Write($"\nAccessibility of the {listType.FullName}.{prop.Name} property: ");

        if (!hasGetAndSet | sameAccess)
        {
            Console.WriteLine(accessibility);
        }
        else
        {
            Console.WriteLine($"\n   The get accessor: {getAccessibility}");
            Console.WriteLine($"   The set accessor: {setAccessibility}");
        }
    }
}
// The example displays the following output:
//       The System.DateTime.Now property:
//          PropertyType: DateTime
//          Static:       True
//          Read-only:    True
//          Indexed:      False
//       
//       Accessibility of the System.Collections.Generic.List`1.Item property: public
```

### 接口

接口包含非抽象[类](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class)或[结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/struct)必须实现的一组相关功能的定义。

例如，使用接口可以在类中包括来自多个源的行为。 该功能在 C# 中十分重要，因为该语言不支持类的多重继承。 此外，如果要模拟结构的继承，也必须使用接口，因为它们无法实际从另一个结构或类继承。

可使用 [interface](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/interface) 关键字定义接口。 如以下示例所示。

```csharp
interface IEquatable<T>
{
    bool Equals(T obj);
}
```

结构名称必须是有效的 C# [标识符名称](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/inside-a-program/identifier-names)。 按照约定，接口名称以大写字母 `I` 开头。

实现 [IEquatable](https://docs.microsoft.com/zh-cn/dotnet/api/system.iequatable-1) 接口的任何类或结构都必须包含与该接口指定的签名匹配的 [Equals](https://docs.microsoft.com/zh-cn/dotnet/api/system.iequatable-1.equals) 方法的定义。 因此，可以依靠实现 `IEquatable` 的类来包含 `Equals` 方法，类的实例可以通过该方法确定它是否等于相同类的另一个实例。

`IEquatable` 的定义不为 `Equals` 提供实现。 类或结构可以实现多个接口，但是类只能从单个类继承。

有关抽象类的详细信息，请参阅[抽象类、密封类及类成员](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members)。

接口可以包含方法、属性、事件、索引器或这四种成员类型的任意组合。 有关示例的链接，请参阅[相关部分](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/interfaces/index#BKMK_RelatedSections)。 接口不能包含常量、字段、运算符、实例构造函数、终结器或类型。 接口成员会自动成为公共成员，不能包含任何访问修饰符。 成员也不能是[静态](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/static)成员。

若要实现接口成员，实现类的对应成员必须是公共、非静态，并且具有与接口成员相同的名称和签名。

当类或结构实现接口时，类或结构必须为该接口定义的所有成员提供实现。 接口本身不提供类或结构可以通过继承基类功能的方式来继承的任何功能。 但是，如果基类实现接口，则从基类派生的任何类都会继承该实现。

下面的示例演示 [IEquatable](https://docs.microsoft.com/zh-cn/dotnet/api/system.iequatable-1) 接口的实现。 实现类 `Car` 必须提供 [Equals](https://docs.microsoft.com/zh-cn/dotnet/api/system.iequatable-1.equals) 方法的实现。

```csharp
public class Car : IEquatable<Car>
{
    public string Make {get; set;}
    public string Model { get; set; }
    public string Year { get; set; }

    // Implementation of IEquatable<T> interface
    public bool Equals(Car car)
    {
        return this.Make == car.Make &&
               this.Model == car.Model &&
               this.Year == car.Year;
    }
}
```

类的属性和索引器可以为接口中定义的属性或索引器定义额外的访问器。 例如，接口可能会声明包含 [get](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/get) 取值函数的属性。 实现此接口的类可以声明包含 `get` 和 [set](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/set) 取值函数的同一属性。 但是，如果属性或索引器使用显式实现，则访问器必须匹配。 有关显式实现的详细信息，请参阅[显式接口实现](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation)和[接口属性](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/interface-properties)。

接口可以从其他接口继承。 类可能通过它继承的基类或通过其他接口继承的接口来多次包含某个接口。 但是，类只能提供接口的实现一次，并且仅当类将接口作为类定义的一部分 (`class ClassName : InterfaceName`) 进行声明时才能提供。 如果由于继承实现接口的基类而继承了接口，则基类会提供接口的成员的实现。 但是，派生类可以重新实现任何虚拟接口成员，而不是使用继承的实现。

基类还可以使用虚拟成员实现接口成员。 在这种情况下，派生类可以通过重写虚拟成员来更改接口行为。 有关虚拟成员的详细信息，请参阅[多态性](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/polymorphism)。

#### 接口摘要

接口具有以下属性：

- 接口类似于只有抽象成员的抽象基类。 实现接口的任何类或结构都必须实现其所有成员。
- 接口无法直接进行实例化。 其成员由实现接口的任何类或结构来实现。
- 接口可以包含事件、索引器、方法和属性。
- 接口不包含方法的实现。
- 一个类或结构可以实现多个接口。 一个类可以继承一个基类，还可实现一个或多个接口。

#### 本节内容

[显式接口实现](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation)
说明如何创建特定于接口的类成员。

[如何：显式实现接口成员](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/interfaces/how-to-explicitly-implement-interface-members)
提供有关如何显式实现接口的成员的示例。

[如何：显式实现两个接口的成员](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces)
提供有关如何使用继承显式实现接口的成员的示例。

#### 相关部分

- [接口属性](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/interface-properties)
- [接口中的索引器](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/indexers/indexers-in-interfaces)
- [如何：实现接口事件](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/events/how-to-implement-interface-events)
- [类和结构](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/index)
- [继承](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
- [方法](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/methods)
- [多态性](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/polymorphism)
- [抽象类、密封类及类成员](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members)
- [属性](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/properties)
- [事件](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/events/index)
- [索引器](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/indexers/index)

### 方法

方法是包含一系列语句的代码块。 程序通过调用该方法并指定任何所需的方法参数使语句得以执行。 在 C# 中，每个执行的指令均在方法的上下文中执行。 `Main` 方法是每个 C# 应用程序的入口点，并在启动程序时由公共语言运行时 (CLR) 调用。

 备注

本主题讨论命名的方法。 有关匿名函数的信息，请参阅[匿名函数](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-functions)。



#### 方法签名

通过指定在 `class` 或 `struct` 中声明方法：

- 可选的访问级别，如 `public` 或 `private`。 默认值为 `private`。
- 可选的修饰符，如 `abstract` 或 `sealed`。
- 返回值，或 `void`（如果该方法不具有）。
- 方法名。
- 任何方法参数。 方法参数在括号内，并且用逗号分隔。 空括号指示方法不需要任何参数。

这些部分一同构成方法签名。

 备注

出于方法重载的目的，方法的返回类型不是方法签名的一部分。 但是在确定委托和它所指向的方法之间的兼容性时，它是方法签名的一部分。

以下实例定义了一个包含五种方法的名为 `Motorcycle` 的类：

```csharp
using System;

abstract class Motorcycle
{
   // Anyone can call this.
   public void StartEngine() {/* Method statements here */ }

   // Only derived classes can call this.
   protected void AddGas(int gallons) { /* Method statements here */ }

   // Derived classes can override the base class implementation.
   public virtual int Drive(int miles, int speed) { /* Method statements here */ return 1; }

   // Derived classes can override the base class implementation.
   public virtual int Drive(TimeSpan time, int speed) { /* Method statements here */ return 0; }

   // Derived classes must implement this.
   public abstract double GetTopSpeed(); 
}
```

请注意，`Motorcycle` 类包括一个重载的方法 `Drive`。 两个方法具有相同的名称，但必须根据其参数类型来区分。



#### 方法调用

方法可以是实例 的或静态的 。 调用实例方法需要将对象实例化，并对该对象调用方法；实例方法可对该实例及其数据进行操作。 通过引用该方法所属类型的名称来调用静态方法；静态方法不对实例数据进行操作。 尝试通过对象实例调用静态方法会引发编译器错误。

调用方法就像访问字段。 在对象名称（如果调用实例方法）或类型名称（如果调用 `static` 方法）后添加一个句点、方法名称和括号。 自变量列在括号里，并且用逗号分隔。

该方法定义指定任何所需参数的名称和类型。 调用方调用该方法时，它为每个参数提供了称为自变量的具体值。 自变量必须与参数类型兼容，但调用代码中使用的自变量名（如果有）不需要与方法中定义的自变量名相同。 在下面示例中，`Square` 方法包含名为 i 的类型为 `int` 的单个参数。 第一种方法调用将向 `Square` 方法传递名为 num 的 `int` 类型的变量；第二个方法调用将传递数值常量；第三个方法调用将传递表达式。

```csharp
public class Example
{
   public static void Main()
   {
      // Call with an int variable.
      int num = 4;
      int productA = Square(num);

      // Call with an integer literal.
      int productB = Square(12);

      // Call with an expression that evaluates to int.
      int productC = Square(productA * 3);
   }
   
   static int Square(int i)
   {
      // Store input argument in a local variable.
      int input = i;
      return input * input;
   }
}
```

方法调用最常见的形式是使用位置自变量；它会以与方法参数相同的顺序提供自变量。 因此，可在以下示例中调用 `Motorcycle` 类的方法。 例如，`Drive` 方法的调用包含两个与方法语法中的两个参数对应的自变量。 第一个成为 `miles` 参数的值，第二个成为 `speed` 参数的值。

```csharp
class TestMotorcycle : Motorcycle
{
   public override double GetTopSpeed()
   {
      return 108.4;
   }

   static void Main()
   {
      
      TestMotorcycle moto = new TestMotorcycle();

      moto.StartEngine();
      moto.AddGas(15);
      moto.Drive(5, 20);
      double speed = moto.GetTopSpeed();
      Console.WriteLine("My top speed is {0}", speed);            
   }
}
```

调用方法时，也可以使用命名的自变量 ，而不是位置自变量。 使用命名的自变量时，指定参数名，然后后跟冒号（":"）和自变量。 只要包含了所有必需的自变量，方法的自变量可以任何顺序出现。 下面的示例使用命名的自变量来调用 `TestMotorcycle.Drive` 方法。 在此示例中，命名的自变量以相反于方法参数列表中的顺序进行传递。

```csharp
using System;

class TestMotorcycle : Motorcycle
{
   public override int Drive(int miles, int speed)
   {
      return (int) Math.Round( ((double)miles) / speed, 0);
   }

   public override double GetTopSpeed()
   {
      return 108.4;
   }

   static void Main()
   {
      
      TestMotorcycle moto = new TestMotorcycle();
      moto.StartEngine();
      moto.AddGas(15);
      var travelTime = moto.Drive(speed: 60, miles: 170);
      Console.WriteLine("Travel time: approx. {0} hours", travelTime);            
   }
}
// The example displays the following output:
//      Travel time: approx. 3 hours
```

可以同时使用位置自变量和命名的自变量调用方法。 但是，位置自变量不能位于命名的自变量之后。 下面的示例使用一个位置自变量和一个命名的自变量从上一个示例中调用 `TestMotorcycle.Drive` 方法。

```csharp
var travelTime = moto.Drive(170, speed: 55);
```



#### 继承和重写方法

除了类型中显式定义的成员，类型还继承在其基类中定义的成员。 由于托管类型系统中的所有类型都直接或间接继承自 [Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object) 类，因此所有类型都继承其成员，如 [Equals(Object)](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.equals#System_Object_Equals_System_Object_)、[GetType()](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.gettype#System_Object_GetType) 和 [ToString()](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.tostring#System_Object_ToString)。 下面的示例定义 `Person` 类，实例化两个 `Person` 对象，并调用 `Person.Equals` 方法来确定两个对象是否相等。 但是，`Equals` 方法不是在 `Person` 类中定义；而是继承自 [Object](https://docs.microsoft.com/zh-cn/dotnet/api/system.object)。

```csharp
using System;

public class Person
{
   public String FirstName;
}

public class Example
{
   public static void Main()
   {
      var p1 = new Person();
      p1.FirstName = "John";
      var p2 = new Person();
      p2.FirstName = "John";
      Console.WriteLine("p1 = p2: {0}", p1.Equals(p2));
   }
}
// The example displays the following output:
//      p1 = p2: False
```

类型可以使用 `override` 关键字并提供重写方法的实现来重写继承的成员。 方法签名必须与重写的方法的签名一样。 下面的示例类似于上一个示例，只不过它重写 [Equals(Object)](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.equals#System_Object_Equals_System_Object_) 方法。 （它还重写 [GetHashCode()](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.gethashcode#System_Object_GetHashCode) 方法，因为这两种方法用于提供一致的结果。）

```csharp
using System;

public class Person
{
   public String FirstName;

   public override bool Equals(object obj)
   {
      var p2 = obj as Person; 
      if (p2 == null)
         return false;
      else
         return FirstName.Equals(p2.FirstName);
   }

   public override int GetHashCode()
   {
      return FirstName.GetHashCode();
   } 
}

public class Example
{
   public static void Main()
   {
      var p1 = new Person();
      p1.FirstName = "John";
      var p2 = new Person();
      p2.FirstName = "John";
      Console.WriteLine("p1 = p2: {0}", p1.Equals(p2));
   }
}
// The example displays the following output:
//      p1 = p2: True
```



#### 传递参数

C# 中的所有类型不是值类型 就是引用类型 。 有关内置值类型的列表，请参阅[类型和变量](https://docs.microsoft.com/zh-cn/dotnet/csharp/tour-of-csharp/types-and-variables)。 默认情况下，值类型和引用类型均按值传递给方法。



#### 按值传递参数

值类型按值传递给方法时，传递的是对象的副本而不是对象本身。 因此，当控件返回调用方时，对已调用方法中的对象的更改对原始对象无影响。

下面的示例按值向方法传递值类型，且调用的方法尝试更改值类型的值。 它定义属于值类型的 `int` 类型的变量，将其值初始化为 20，并将该类型传递给将变量值改为 30 的名为 `ModifyValue` 的方法。 但是，返回方法时，变量的值保持不变。

```csharp
using System;

public class Example
{
   public static void Main()
   {
      int value = 20;
      Console.WriteLine("In Main, value = {0}", value);
      ModifyValue(value);
      Console.WriteLine("Back in Main, value = {0}", value);
   }

   static void ModifyValue(int i)
   {
      i = 30;
      Console.WriteLine("In ModifyValue, parameter value = {0}", i);
      return;
   }
}
// The example displays the following output:
//      In Main, value = 20
//      In ModifyValue, parameter value = 30
//      Back in Main, value = 20
```

引用类型的对象按值传递到方法中时，将按值传递对对象的引用。 也就是说，该方法接收的不是对象本身，而是指示该对象位置的自变量。 控件返回到调用方法时，如果通过使用此引用更改对象的成员，此更改将反映在对象中。 但是，当控件返回到调用方时，替换传递到方法的对象对原始对象无影响。

下面的示例定义名为 `SampleRefType` 的类（属于引用类型）。 它实例化 `SampleRefType` 对象，将 44 赋予其 `value` 字段，并将该对象传递给 `ModifyObject` 方法。 该示例执行的内容实质上与先前示例相同，均按值将自变量传递到方法。 但因为使用了引用类型，结果会有所不同。 `ModifyObject` 中所做的对 `obj.value` 字段的修改，也会将 `Main` 方法中的自变量 `rt` 的 `value` 字段更改为 33，如示例中的输出值所示。

```csharp
using System;

public class SampleRefType
{
    public int value;
}

public class Example
{
    public static void Main()
    {
        var rt = new SampleRefType();
        rt.value = 44;
        ModifyObject(rt);
        Console.WriteLine(rt.value);
    }
        
    static void ModifyObject(SampleRefType obj)
    {
        obj.value = 33;
    }
}
```



#### 按引用传递参数

如果想要更改方法中的自变量值并想要在控件返回到调用方法时反映出这一更改，请按引用传递参数。 要按引用传递参数，请使用 [`ref`](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/ref) 或 [`out`](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/out-parameter-modifier) 关键字。 还可以使用 [`in`](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/in-parameter-modifier) 关键字，按引用传递值以避免复制，但仍防止修改。

下面的示例与上一个示例完全一样，只是换成按引用将值传递给 `ModifyValue` 方法。 参数值在 `ModifyValue` 方法中修改时，值中的更改将在控件返回调用方时反映出来。

```csharp
using System;

public class Example
{
   public static void Main()
   {
      int value = 20;
      Console.WriteLine("In Main, value = {0}", value);
      ModifyValue(ref value);
      Console.WriteLine("Back in Main, value = {0}", value);
   }

   static void ModifyValue(ref int i)
   {
      i = 30;
      Console.WriteLine("In ModifyValue, parameter value = {0}", i);
      return;
   }
}
// The example displays the following output:
//      In Main, value = 20
//      In ModifyValue, parameter value = 30
//      Back in Main, value = 30
```

引用参数所使用的常见模式涉及交换变量值。 将两个变量按引用传递给一个方法，然后该方法将二者内容进行交换。 下面的示例交换整数值。

```csharp
using System;

public class Example
{
   static void Main()
   {
      int i = 2, j = 3;
      System.Console.WriteLine("i = {0}  j = {1}" , i, j);

      Swap(ref i, ref j);

      System.Console.WriteLine("i = {0}  j = {1}" , i, j);
   }

   static void Swap(ref int x, ref int y)
   {
      int temp = x;
      x = y;
      y = temp;
   }   
}
// The example displays the following output:
//      i = 2  j = 3
//      i = 3  j = 2
```

通过传递引用类型的参数，可以更改引用本身的值，而不是其单个元素或字段的值。



#### 参数数组

有时，向方法指定精确数量的自变量这一要求是受限的。 通过使用 `params` 关键字来指示一个参数是一个参数数组，可通过可变数量的自变量来调用方法。 使用 `params` 关键字标记的参数必须为数组类型，并且必须是该方法的参数列表中的最后一个参数。

然后，调用方可通过以下三种方式中的任一个来调用方法：

- 传递相应类型的数组，该类型包含所需数量的元素。
- 向该方法传递相应类型的单独自变量的逗号分隔列表。
- 不向参数数组提供参数。

以下示例定义了一个名为 `GetVowels` 的方法，该方法返回参数数组中的所有元音。 `Main` 方法演示了调用方法的全部三种方式。 调用方不需要为包含 `params` 修饰符的形参提供任何实参。 在这种情况下，参数为 `null`。

```csharp
using System;
using System.Linq;

class Example
{
    static void Main()
    {
        string fromArray = GetVowels(new[] { "apple", "banana", "pear" });
        Console.WriteLine($"Vowels from array: '{fromArray}'");

        string fromMultipleArguments = GetVowels("apple", "banana", "pear");
        Console.WriteLine($"Vowels from multiple arguments: '{fromMultipleArguments}'");

        string fromNoValue = GetVowels();
        Console.WriteLine($"Vowels from no value: '{fromNoValue}'");
    }

    static string GetVowels(params string[] input)
    {
        if (input == null || input.Length == 0)
        {
            return string.Empty;
        }

        var vowels = new char[] { 'A', 'E', 'I', 'O', 'U' };
        return string.Concat(
            input.SelectMany(
                word => word.Where(letter => vowels.Contains(char.ToUpper(letter)))));
    }
}

// The example displays the following output:
//     Vowels from array: 'aeaaaea'
//     Vowels from multiple arguments: 'aeaaaea'
//     Vowels from no value: ''
```



#### 可选参数和自变量

方法定义可指定其参数是必需的还是可选的。 默认情况下，参数是必需的。 通过在方法定义中包含参数的默认值来指定可选参数。 调用该方法时，如果未向可选参数提供自变量，则改为使用默认值。

参数的默认值必须由以下几种表达式中的一种来赋予：

- 常量，例如文本字符串或数字。
- `new ValType()` 形式的表达式，其中 `ValType` 是值类型。 请注意，这会调用该值类型的隐式无参数构造函数，该函数不是类型的实际成员。
- `default(ValType)` 形式的表达式，其中 `ValType` 是值类型。

如果某个方法同时包含必需的和可选的参数，则在参数列表末尾定义可选参数，即在定义完所有必需参数之后定义。

下面的示例定义方法 `ExampleMethod`，它具有一个必需参数和两个可选参数。

```csharp
using System;

public class Options
{
   public void ExampleMethod(int required, int optionalInt = default(int),
                             string description = "Optional Description")
   {
      Console.WriteLine("{0}: {1} + {2} = {3}", description, required, 
                        optionalInt, required + optionalInt);
   }
}
```

如果使用位置自变量调用包含多个可选自变量的方法，调用方必须逐一向所有需要自变量的可选参数提供自变量。 例如，在使用 `ExampleMethod` 方法的情况下，如果调用方向 `description` 参数提供自变量，还必须向 `optionalInt` 参数提供一个自变量。 `opt.ExampleMethod(2, 2, "Addition of 2 and 2");` 是一个有效的方法调用；`opt.ExampleMethod(2, , "Addition of 2 and 0");` 生成编译器错误“缺少自变量”。

如果使用命名的自变量或位置自变量和命名的自变量的组合来调用某个方法，调用方可以省略方法调用中的最后一个位置自变量后的任何自变量。

下面的示例三次调用了 `ExampleMethod` 方法。 前两个方法调用使用位置自变量。 第一个方法同时省略了两个可选自变量，而第二个省略了最后一个自变量。 第三个方法调用向必需的参数提供位置自变量，但使用命名的自变量向 `description` 参数提供值，同时省略 `optionalInt` 自变量。

```csharp
public class Example
{
   public static void Main()
   {
      var opt = new Options();
      opt.ExampleMethod(10);
      opt.ExampleMethod(10, 2);
      opt.ExampleMethod(12, description: "Addition with zero:");
   }
} 
// The example displays the following output:
//      Optional Description: 10 + 0 = 10
//      Optional Description: 10 + 2 = 12
//      Addition with zero:: 12 + 0 = 12
```

使用可选参数会影响重载决策 ，或影响 C# 编译器决定方法应调用哪个特定重载时所使用的方式，如下所示：

- 如果方法、索引器或构造函数的每个参数是可选的，或按名称或位置对应于调用语句中的单个自变量，且该自变量可转换为参数的类型，则方法、索引器或构造函数为执行的候选项。
- 如果找到多个候选项，则会将用于首选转换的重载决策规则应用于显式指定的自变量。 将忽略可选形参已省略的实参。
- 如果两个候选项不相上下，则会将没有可选形参的候选项作为首选项，对于这些可选形参，已在调用中为其省略了实参。 这是重载决策中的常规引用的结果，该引用用于参数较少的候选项。



#### 返回值

方法可以将值返回到调用方。 如果列在方法名之前的返回类型不是 `void`，则该方法可通过使用 `return` 关键字返回值。 带 `return` 关键字且后跟与返回类型匹配的变量、常数或表达式的语句将向方法调用方返回该值。 具有非空的返回类型的方法都需要使用 `return` 关键字来返回值。 `return` 关键字还会停止执行该方法。

如果返回类型为 `void`，没有值的 `return` 语句仍可用于停止执行该方法。 没有 `return` 关键字，当方法到达代码块结尾时，将停止执行。

例如，这两种方法都使用 `return` 关键字来返回整数：

```csharp
class SimpleMath
{
    public int AddTwoNumbers(int number1, int number2)
    {
        return number1 + number2;
    }

    public int SquareANumber(int number)
    {
        return number * number;
    }
}
```

若要使用从方法返回的值，调用方法可以在相同类型的值足够的地方使用该方法调用本身。 也可以将返回值分配给变量。 例如，以下两个代码示例实现了相同的目标：

```csharp
int result = obj.AddTwoNumbers(1, 2);
result = obj.SquareANumber(result);
// The result is 9.
Console.WriteLine(result);
```

```csharp
result = obj.SquareANumber(obj.AddTwoNumbers(1, 2));
// The result is 9.
Console.WriteLine(result);
```

在这种情况下，使用本地变量 `result`存储值是可选的。 此步骤可以帮助提高代码的可读性，或者如果需要存储该方法整个范围内自变量的原始值，则此步骤可能很有必要。

有时，需要方法返回多个值。 从 C# 7.0 开始，可以使用元组类型 和元组文本 轻松实现此目的。 元组类型定义元组元素的数据类型。 元组文本提供返回的元组的实际值。 在下面的示例中，`(string, string, string, int)` 定义 `GetPersonalInfo` 方法返回的元组类型。 表达式 `(per.FirstName, per.MiddleName, per.LastName, per.Age)` 是元组文本；方法返回 `PersonInfo` 对象的第一个、中间和最后一个名称及其使用期限。

```csharp
public (string, string, string, int) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

然后调用方可通过类似以下的代码使用返回的元组：

```csharp
var person = GetPersonalInfo("111111111")
Console.WriteLine("{person.Item1} {person.Item3}: age = {person.Item4}");
```

还可向元组类型定义中的元组元素分配名称。 下面的示例展示 `GetPersonalInfo` 方法的替代版本，该方法使用命名的元素：

```csharp
public (string FName, string MName, string LName, int Age) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

然后可修改上一次对 `GetPersonInfo` 方法的调用，如下所示：

```csharp
var person = GetPersonalInfo("111111111");
Console.WriteLine("{person.FName} {person.LName}: age = {person.Age}");
```

如果将数组作为自变量传递给一个方法，并修改各个元素的值，则该方法不一定会返回该数组，尽管选择这么操作的原因是为了实现更好的样式或功能性的值流。 这是因为 C# 会按值传递所有引用类型，而数组引用的值是指向该数组的指针。 在下面的示例中，引用该数组的任何代码都能观察到在 `DoubleValues` 方法中对 `values` 数组内容的更改。

```csharp
using System;

public class Example
{
   static void Main(string[] args)  
   {  
      int[] values = { 2, 4, 6, 8 };
      DoubleValues(values);
      foreach (var value in values)
         Console.Write("{0}  ", value);
   }  
  
   public static void DoubleValues(int[] arr)
   {
      for (int ctr = 0; ctr <= arr.GetUpperBound(0); ctr++)
         arr[ctr] = arr[ctr] * 2;
   }
}
// The example displays the following output:
//       4  8  12  16
```



#### 扩展方法

通常，可以通过两种方式向现有类型添加方法：

- 修改该类型的源代码。 当然，如果并不拥有该类型的源代码，则无法执行该操作。 并且，如果还添加任何专用数据字段来支持该方法，这会成为一项重大更改。
- 在派生类中定义新方法。 无法使用其他类型（如结构和枚举）的继承来通过此方式添加方法。 也不能使用此方式向封闭类“添加”方法。

使用扩展方法，可向现有类型“添加”方法，而无需修改类型本身或在继承的类型中实现新方法。 扩展方法也无需驻留在与其扩展的类型相同的程序集中。 要把扩展方法当作是定义的类型成员一样调用。

有关详细信息，请参阅[扩展方法](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/extension-methods)。



#### 异步方法

通过使用异步功能，你可以调用异步方法而无需使用显式回调，也不需要跨多个方法或 lambda 表达式来手动拆分代码。

如果用 [async](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/async) 修饰符标记方法，则可以在该方法中使用 [await](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/await) 运算符。 当控件到达异步方法中的 `await` 表达式时，如果等待的任务未完成，控件将返回到调用方，并在等待任务完成前，包含 `await` 关键字的方法中的进度将一直处于挂起状态。 任务完成后，可以在方法中恢复执行。

 备注

异步方法在遇到第一个尚未完成的 awaited 对象或到达异步方法的末尾时（以先发生者为准），将返回到调用方。

异步方法可以具有 [Task](https://docs.microsoft.com/zh-cn/dotnet/api/system.threading.tasks.task-1)、[Task](https://docs.microsoft.com/zh-cn/dotnet/api/system.threading.tasks.task)、 或 `void` 返回类型。 `void` 返回类型主要用于定义需要 `void` 返回类型的事件处理程序。 无法等待返回 `void` 的异步方法，并且返回 void 方法的调用方无法捕获该方法引发的异常。 从 C# 7.0 开始，异步方法可以有[任何类似任务的返回类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/whats-new/csharp-7#generalized-async-return-types)。

在下面的示例中，`DelayAsync` 是一个异步方法，包含返回整数的 return 语句。 由于它是异步方法，其方法声明必须具有返回类型 `Task`。 因为返回类型是 `Task`，`DoSomethingAsync` 中 `await` 表达式的计算将如以下 `int result = await delayTask` 语句所示得出整数。

```csharp
using System;
using System.Diagnostics;
using System.Threading.Tasks;

public class Example
{
    // This Click event is marked with the async modifier.
    public static void Main()
    {
       DoSomethingAsync().Wait();
    }

    private static async Task DoSomethingAsync()
    {
        int result = await DelayAsync();
        Console.WriteLine("Result: " + result);
    }

    private static async Task<int> DelayAsync()
    {
        await Task.Delay(100);
        return 5;
    }

    // Output:
    //  Result: 5
}
// The example displays the following output:
//        Result: 5
```

异步方法不能声明任何 [in](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/in-parameter-modifier)、[ref](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/ref) 或 [out](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/out-parameter-modifier) 参数，但是可以调用具有这类参数的方法。

有关异步方法的详细信息，请参阅[使用 Async 和 Await 的异步编程](https://docs.microsoft.com/zh-cn/dotnet/csharp/async)、[异步程序中的控制流](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/async/control-flow-in-async-programs)和[异步返回类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/async/async-return-types)。



#### Expression-Bodied 成员

具有立即仅返回表达式结果，或单个语句作为方法主题的方法定义很常见。 以下是使用 `=>` 定义此类方法的语法快捷方式：

C#复制

```csharp
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);
```

如果该方法返回 `void` 或是异步方法，则该方法的主体必须是语句表达式（与 lambda 相同）。 对于属性和索引器，两者必须是只读，并且不使用 `get` 访问器关键字。



#### Iterators

迭代器对集合执行自定义迭代，如列表或数组。 迭代器使用 [yield return](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/yield) 语句返回元素，每次返回一个。 到达 `yield return` 语句后，会记住当前位置，以便调用方可以请求序列中的下一个元素。

迭代器的返回类型可以是 [IEnumerable](https://docs.microsoft.com/zh-cn/dotnet/api/system.collections.ienumerable)、 [IEnumerable](https://docs.microsoft.com/zh-cn/dotnet/api/system.collections.generic.ienumerable-1)、 [IEnumerator](https://docs.microsoft.com/zh-cn/dotnet/api/system.collections.ienumerator)或 [IEnumerator](https://docs.microsoft.com/zh-cn/dotnet/api/system.collections.generic.ienumerator-1)。

有关更多信息，请参见 [迭代器](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/iterators)。

#### 请参阅

- [访问修饰符](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/access-modifiers)
- [静态类和静态类成员](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)
- [继承](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
- [抽象类、密封类及类成员](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members)
- [params](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/params)
- [out](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/out-parameter-modifier)
- [ref](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/ref)
- [in](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/in-parameter-modifier)
- [传递参数](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters)