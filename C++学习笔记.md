# C++学习笔记（上）

## 基本概念

### 程序语言是什么

1. **定义**
   程序语言是**人与计算机沟通的工具**，通过编写代码来指示计算机执行任务。

2. **组成**

   - **语法**：代码的结构规则。
   - **语义**：代码的含义和行为。
   - **标准库**：提供常用功能的预定义代码集合。

3. 历史：计算机语言的发展了从低级到高级的演变，有**机器语言**、**汇编语言**、**高级语言**三个阶段。

   | 阶段     | 时期           | 特点                                         | 优点                         | 缺点                 |
   | :------- | :------------- | :------------------------------------------- | :--------------------------- | :------------------- |
   | 机器语言 | 1940年代       | 二进制代码，直接由硬件执行                   | 执行效率高                   | 难以编写、阅读和维护 |
   | 汇编语言 | 1950年代       | 使用**助记符**，需**汇编器**转换为机器语言   | 比机器语言易读写，效率高     | 依赖硬件，移植性差   |
   | 高级语言 | 1950年代末至今 | 接近人类语言，需**编译器**转换成机器语言执行 | 易读、易写、易维护，移植性强 | 执行效率通常较低     |

### 开发环境搭建

**集成开发环境（Integrated Development Environment，IDE）**：一种软件应用程序，为开发者提供全面的编程工具和环境。它通常包括以下核心组件：

- **代码编辑器**：用于编写和编辑源代码，支持语法高亮、自动补全等功能。
- **编译器**：将源代码转换为机器代码或直接执行。
- **调试器**：帮助开发者查找和修复代码中的错误。
- **构建自动化工具**：用于编译、链接和打包代码。
- **图形用户界面（GUI）**：提供直观的操作界面，方便开发者管理项目和文件。

**头文件：**一种包含**函数、变量、宏等的声明**的文件，通常以.h 扩展名结尾。

- 头文件可以被多个源文件共享，通过预处理指令 **#include** 来引用。

  - **`#include <filename>`**：包含**标准库头文件**或**系统提供**的头文件，编译器会在标准库路径和系统指定的路径中查找该文件。

  - **`#include "filename"`**：包含**用户自定义**的头文件，编译器首先在当前文件所在目录查找（如果头文件位于子目录中，使用相对路径或绝对路径），如果未找到，则继续在标准库路径中查找。

**主函数（`main` 函数）：**C/C++程序的**入口点**（程序执行的起点）。

- 程序运行时，操作系统会首先调用 `main` 函数，然后从 `main` 函数开始执行程序逻辑。

- 在C/C++中，`main` 函数的定义通常有以下两种形式：带参数和不带参数。

  - 带参数的形式：

    ```C++
    int main(int argc, char* argv[]) {
        // 程序逻辑
        return 0;
    }
    ```

    - `argc`（argument count）：
      - 表示命令行参数的数量。
      - 至少为 1，第一个参数是**程序本身的名称**。
    - `argv`（argument vector）：
      - 是一个字符串数组，存储命令行参数。
      - `argv[0]` 是程序名称，`argv[1]` 到 `argv[argc-1]` 是**用户输入的参数**。

  - 不带参数的形式：

    ```C++
    int main() {
        // 程序逻辑
        return 0;
    }
    ```

**折叠代码：**在C++中，`#pragma region` 是一个**非标准**的预处理指令，主要用于在支持它的IDE（如Visual Studio）中折叠代码块。

```C++
#pragma region MyRegion
void foo() {
    // 代码
}

void bar() {
    // 代码
}
#pragma endregion
```

### 变量

**作用**：给一段指定的内存空间起名，方便操作这段内存

**语法**：`数据类型 变量名 = 初始值;`

C++在创建变量时，必须给变量一个**初始值**，否则会报错。

```c++
#include<iostream>
using namespace std;

int main() {
	int a = 10;
	cout << "a = " << a << endl;
	system("pause");
	return 0;
}
```

### 常量

**作用**：用于记录程序中不可更改的数据

C++定义常量两种方式：

1. **\#define** 宏常量： `#define 常量名 常量值`
   * 通常在文件上方定义，表示一个常量


2. **const**修饰的变量 `const 数据类型 常量名 = 常量值`
   * 通常在变量定义前加关键字`const`，修饰该变量为常量，不可修改

```c++
// 1、宏常量
#define day 7

int main() {
	cout << "一周里总共有 " << day << " 天" << endl;

	// 2、const修饰变量
	const int month = 12;
	cout << "一年里总共有 " << month << " 个月份" << endl;
	
	system("pause");

	return 0;
}
```

### 关键字

**作用：**关键字是C++中预先保留的单词（标识符）

* 在定义变量或者常量时候，不要用关键字

C++关键字如下：

| 关键字       | 含义         | 关键字    | 含义           | 关键字           | 含义           |
| :----------- | :----------- | :-------- | :------------- | :--------------- | :------------- |
| asm          | 汇编指令     | auto      | 自动类型推断   | bool             | 布尔类型       |
| break        | 跳出循环     | case      | 条件分支       | catch            | 异常捕获       |
| char         | 字符类型     | class     | 类定义         | const            | 常量修饰       |
| const_cast   | 常量转换     | continue  | 继续循环       | default          | 默认分支       |
| delete       | 释放内存     | do        | 循环语句       | double           | 双精度浮点类型 |
| dynamic_cast | 动态类型转换 | else      | 条件分支       | enum             | 枚举类型       |
| explicit     | 显式构造函数 | export    | 导出模板       | extern           | 外部声明       |
| false        | 布尔假值     | float     | 单精度浮点类型 | for              | 循环语句       |
| friend       | 友元声明     | goto      | 跳转语句       | if               | 条件语句       |
| inline       | 内联函数     | int       | 整型           | long             | 长整型         |
| mutable      | 可变成员     | namespace | 命名空间       | new              | 动态内存分配   |
| operator     | 运算符重载   | private   | 私有成员       | protected        | 受保护成员     |
| public       | 公有成员     | register  | 寄存器变量     | reinterpret_cast | 强制类型转换   |
| return       | 返回值       | short     | 短整型         | signed           | 有符号类型     |
| sizeof       | 类型大小     | static    | 静态成员       | static_cast      | 静态类型转换   |
| struct       | 结构体定义   | switch    | 多分支语句     | template         | 模板定义       |
| this         | 当前对象指针 | throw     | 抛出异常       | true             | 布尔真值       |
| try          | 异常捕获     | typedef   | 类型别名       | typeid           | 类型信息       |
| typename     | 类型名       | union     | 联合体         | unsigned         | 无符号类型     |
| using        | 命名空间使用 | virtual   | 虚函数         | void             | 无类型         |
| volatile     | 易变变量     | wchar_t   | 宽字符类型     | while            | 循环语句       |

### 标识符命名规则

**作用**：C++规定给标识符（变量、常量）命名时，有一套自己的规则

* 标识符不能是关键字
* 标识符只能由**字母、数字、下划线**组成
* 第一个字符必须为字母或下划线
* 标识符中字母区分大小写

## 数据类型

C++规定在创建一个变量或者常量时，必须要指定出相应的数据类型，否则无法给变量分配内存。

### 整型

**作用**：整型变量表示的是整数类型的数据

C++中能够表示整型的类型有以下几种方式，区别在于**所占内存空间不同**：

| **数据类型**        | **占用空间**                                    | 取值范围         |
| ------------------- | ----------------------------------------------- | ---------------- |
| short(短整型)       | 2字节                                           | [-2^15 ~ 2^15-1] |
| int(整型)           | 4字节                                           | [-2^31 ~ 2^31-1] |
| long(长整形)        | Windows为4字节，Linux为4字节(32位)，8字节(64位) | [-2^31 ~ 2^31-1] |
| long long(长长整形) | 8字节                                           | [-2^63 ~ 2^63-1] |

### sizeof关键字

**作用：**利用`sizeof`关键字可以统计数据类型所占内存大小

**语法：** `sizeof( 数据类型/变量)`

```C++
int main() {

	cout << "short 类型所占内存空间为： " << sizeof(short) << endl;
	cout << "int 类型所占内存空间为： " << sizeof(int) << endl;
	cout << "long 类型所占内存空间为： " << sizeof(long) << endl;
	cout << "long long 类型所占内存空间为： " << sizeof(long long) << endl;
	system("pause");

	return 0;
}
```

### 浮点型

**作用**：用于表示**小数**

浮点型变量分为两种：

1. 单精度浮点型`float`
2. 双精度浮点型`double`

两者的**区别**在于表示的有效数字范围不同。

| **数据类型** | **占用空间** | **有效数字范围** |
| ------------ | ------------ | ---------------- |
| float        | 4字节        | 7位有效数字      |
| double       | 8字节        | 15～16位有效数字 |

```C++
int main() {

	float f1 = 3.14f;
	double d1 = 3.14;

	cout << f1 << endl;
	cout << d1<< endl;

	cout << "float  sizeof = " << sizeof(f1) << endl;
	cout << "double sizeof = " << sizeof(d1) << endl;

	//科学计数法
	float f2 = 3e2; // 3 * 10 ^ 2 
	cout << "f2 = " << f2 << endl;

	float f3 = 3e-2;  // 3 * 0.1 ^ 2
	cout << "f3 = " << f3 << endl;

	system("pause");

	return 0;
}
```

### 字符型

**作用：**字符型变量用于显示单个字符

**语法：**`char ch = 'a';`

- C和C++中字符型变量占用1个字节。
- 字符型变量并不是把字符本身放到内存中存储，而是将对应的ASCII编码放入到存储单元

```cpp
int main() {
	
	char ch = 'a';
	cout << ch << endl;
	cout << sizeof(char) << endl;

	cout << (int)ch << endl;  //查看字符a对应的ASCII码
	ch = 97;
	cout << ch << endl;

	system("pause");

	return 0;
}
```

ASCII码表格：

| **ASCII**值 | **控制字符** | **ASCII**值 | **字符** | **ASCII**值 | **字符** | **ASCII**值 | **字符** |
| ----------- | ------------ | ----------- | -------- | ----------- | -------- | ----------- | -------- |
| 0           | NUT          | 32          | (space)  | 64          | @        | 96          | 、       |
| 1           | SOH          | 33          | !        | 65          | A        | 97          | a        |
| 2           | STX          | 34          | "        | 66          | B        | 98          | b        |
| 3           | ETX          | 35          | #        | 67          | C        | 99          | c        |
| 4           | EOT          | 36          | $        | 68          | D        | 100         | d        |
| 5           | ENQ          | 37          | %        | 69          | E        | 101         | e        |
| 6           | ACK          | 38          | &        | 70          | F        | 102         | f        |
| 7           | BEL          | 39          | ,        | 71          | G        | 103         | g        |
| 8           | BS           | 40          | (        | 72          | H        | 104         | h        |
| 9           | HT           | 41          | )        | 73          | I        | 105         | i        |
| 10          | LF           | 42          | *        | 74          | J        | 106         | j        |
| 11          | VT           | 43          | +        | 75          | K        | 107         | k        |
| 12          | FF           | 44          | ,        | 76          | L        | 108         | l        |
| 13          | CR           | 45          | -        | 77          | M        | 109         | m        |
| 14          | SO           | 46          | .        | 78          | N        | 110         | n        |
| 15          | SI           | 47          | /        | 79          | O        | 111         | o        |
| 16          | DLE          | 48          | 0        | 80          | P        | 112         | p        |
| 17          | DCI          | 49          | 1        | 81          | Q        | 113         | q        |
| 18          | DC2          | 50          | 2        | 82          | R        | 114         | r        |
| 19          | DC3          | 51          | 3        | 83          | S        | 115         | s        |
| 20          | DC4          | 52          | 4        | 84          | T        | 116         | t        |
| 21          | NAK          | 53          | 5        | 85          | U        | 117         | u        |
| 22          | SYN          | 54          | 6        | 86          | V        | 118         | v        |
| 23          | TB           | 55          | 7        | 87          | W        | 119         | w        |
| 24          | CAN          | 56          | 8        | 88          | X        | 120         | x        |
| 25          | EM           | 57          | 9        | 89          | Y        | 121         | y        |
| 26          | SUB          | 58          | :        | 90          | Z        | 122         | z        |
| 27          | ESC          | 59          | ;        | 91          | [        | 123         | {        |
| 28          | FS           | 60          | <        | 92          | /        | 124         | \|       |
| 29          | GS           | 61          | =        | 93          | ]        | 125         | }        |
| 30          | RS           | 62          | >        | 94          | ^        | 126         | `        |
| 31          | US           | 63          | ?        | 95          | _        | 127         | DEL      |

ASCII 码大致由以下两部分组成：

* ASCII 非打印控制字符： ASCII 表上的数字 **0-31** 分配给了控制字符，用于控制像打印机等一些外围设备。
* ASCII 打印字符：数字 **32-126** 分配给了能在键盘上找到的字符，当查看或打印文档时就会出现。

### 转义字符

**作用：**用于表示一些**不能显示出来**的ASCII字符。

转义字符表格：

| **转义字符** | **含义**                                | **ASCII**码值（十进制） |
| ------------ | --------------------------------------- | ----------------------- |
| \a           | 警报                                    | 007                     |
| \b           | 退格(BS) ，将当前位置移到前一列         | 008                     |
| \f           | 换页(FF)，将当前位置移到下页开头        | 012                     |
| **\n**       | **换行(LF) ，将当前位置移到下一行开头** | **010**                 |
| \r           | 回车(CR) ，将当前位置移到本行开头       | 013                     |
| **\t**       | **水平制表(HT)  （跳到下一个TAB位置）** | **009**                 |
| \v           | 垂直制表(VT)                            | 011                     |
| **\\\\**     | **代表一个反斜线字符"\"**               | **092**                 |
| \'           | 代表一个单引号（撇号）字符              | 039                     |
| \"           | 代表一个双引号字符                      | 034                     |
| \?           | 代表一个问号                            | 063                     |
| \0           | 数字0                                   | 000                     |
| \ddd         | 8进制转义字符，d范围0~7                 | 3位8进制                |
| \xhh         | 16进制转义字符，h范围0~9，a~f，A~F      | 3位16进制               |

### 字符串型

**作用**：用于表示一串字符。

**C风格字符串**： `char 变量名[] = "字符串值"`

```C++
int main() {

	char str1[] = "hello world";
	cout << str1 << endl;
    
	system("pause");

	return 0;
}
```

> 注意：C风格的字符串要用双引号括起来

**C++风格字符串**：  `string  变量名 = "字符串值"`

```C++
int main() {

	string str = "hello world";
	cout << str << endl;
	
	system("pause");

	return 0;
}
```

注意：C++风格字符串，需要加入头文件`#include\<string>`

### 布尔类型

**作用：**布尔数据类型代表真或假的值。

- bool类型占1个字节大小

```C++
int main() {

	bool flag = true;
	cout << flag << endl; // 1

	flag = false;
	cout << flag << endl; // 0

	cout << "size of bool = " << sizeof(bool) << endl; //1
	
	system("pause");
	return 0;
}
```

### 数据的输入

`cin` 是 C++ 标准输入流对象（`istream` 类的实例），用于从标准输入（通常是键盘）读取数据。

- 输入缓冲区

  - 当用户输入数据时，数据不会直接赋给变量，而是先存入**输入缓冲区**。

  - `cin` 从缓冲区提取数据，按照变量类型进行解析。

  - 如果成功，数据被提取，缓冲区中的该数据被消耗。

  - 如果失败（类型不匹配或遇到非法字符），`cin` 会进入错误状态。

`cin` 维护以下状态标志（通过 `ios_base` 继承）：

| 状态标志  | 含义                        |
| :-------- | :-------------------------- |
| `goodbit` | 一切正常（值为 `0`）        |
| `eofbit`  | 到达文件末尾（End-Of-File） |
| `failbit` | 提取失败（如类型不匹配）    |
| `badbit`  | 严重错误（如流被破坏）      |

- 语法：`cin >> 变量`

```cpp
int main(){

	//整型输入
	int a = 0;
	cout << "请输入整型变量：" << endl;
	cin >> a;
	cout << a << endl;

	//浮点型输入
	double d = 0;
	cout << "请输入浮点型变量：" << endl;
	cin >> d;
	cout << d << endl;

	//字符型输入
	char ch = 0;
	cout << "请输入字符型变量：" << endl;
	cin >> ch;
	cout << ch << endl;

	//字符串型输入
	string str;
	cout << "请输入字符串型变量：" << endl;
	cin >> str;
	cout << str << endl;

	//布尔类型输入
	bool flag = true;
	cout << "请输入布尔型变量：" << endl;
	cin >> flag;
	cout << flag << endl;
    
	system("pause");
	return EXIT_SUCCESS;
}
```

- `cin` 的常用方法

  -  `cin.clear()`，重置错误状态标志，当 `cin.fail()` 为 `true` 时，必须先调用 `clear()` 才能继续使用 `cin`。

    ```cpp
    int num;
    cin >> num;  // 如果用户输入"abc"，会触发 failbit
    if (cin.fail()) {
        cin.clear();  // 必须清除错误状态！
    }
    ```

  -  `cin.ignore()`，丢弃缓冲区中的字符。

    ```cpp
    cin.ignore(n, delim);  // 丢弃 n 个字符，或直到遇到分隔符 delim
    ```

  - `cin.get()`，读取单个字符（包括空格和换行符）。

    ```
    char ch;
    ch = cin.get();  // 读取一个字符
    ```

  - `cin.getline()`，读取一行字符串（可包含空格）。

    ```cpp
    cin.getline(char_array, size, delim);  // 读取到 delim（默认 '\n'）
    ```

  - `cin.peek()`，查看下一个字符，但不从缓冲区提取。

    ```cpp
    char next = cin.peek();  // 查看下一个字符
    if (next == '\n') {
        cout << "即将遇到换行符！";
    }
    ```

## 运算符

**作用：**用于执行代码的运算。

| **运算符类型** | **作用**                               |
| -------------- | -------------------------------------- |
| 算术运算符     | 用于处理四则运算                       |
| 赋值运算符     | 用于将表达式的值赋给变量               |
| 比较运算符     | 用于表达式的比较，并返回一个真值或假值 |
| 逻辑运算符     | 用于根据表达式的值返回真值或假值       |

### 算数运算符

**作用**：用于处理四则运算。

| **运算符** | **术语**   | **示例**    | **结果**  |
| ---------- | ---------- | ----------- | --------- |
| +          | 正号       | +3          | 3         |
| -          | 负号       | -3          | -3        |
| +          | 加         | 10 + 5      | 15        |
| -          | 减         | 10 - 5      | 5         |
| *          | 乘         | 10 * 5      | 50        |
| /          | 除         | 10 / 5      | 2         |
| %          | 取模(取余) | 10 % 3      | 1         |
| ++         | 前置递增   | a=2; b=++a; | a=3; b=3; |
| ++         | 后置递增   | a=2; b=a++; | a=3; b=2; |
| --         | 前置递减   | a=2; b=--a; | a=1; b=1; |
| --         | 后置递减   | a=2; b=a--; | a=1; b=2; |

### 赋值运算符

**作用：**用于将表达式的值赋给变量。

| **运算符** | **术语** | **示例**   | **结果**  |
| ---------- | -------- | ---------- | --------- |
| =          | 赋值     | a=2; b=3;  | a=2; b=3; |
| +=         | 加等于   | a=0; a+=2; | a=2;      |
| -=         | 减等于   | a=5; a-=3; | a=2;      |
| *=         | 乘等于   | a=2; a*=2; | a=4;      |
| /=         | 除等于   | a=4; a/=2; | a=2;      |
| %=         | 模等于   | a=3; a%2;  | a=1;      |

### 比较运算符

**作用：**用于表达式的比较，并返回一个真值或假值。

| **运算符** | **术语** | **示例** | **结果** |
| ---------- | -------- | -------- | -------- |
| ==         | 相等于   | 4 == 3   | 0        |
| !=         | 不等于   | 4 != 3   | 1        |
| <          | 小于     | 4 < 3    | 0        |
| \>         | 大于     | 4 > 3    | 1        |
| <=         | 小于等于 | 4 <= 3   | 0        |
| \>=        | 大于等于 | 4 >= 1   | 1        |

### 逻辑运算符

**作用：**用于根据表达式的值返回真值或假值。

| **运算符** | **术语** | **示例** | **结果**                                                 |
| ---------- | -------- | -------- | -------------------------------------------------------- |
| !          | 非       | !a       | 如果a为假，则!a为真；  如果a为真，则!a为假。             |
| &&         | 与       | a && b   | 如果a和b都为真，则结果为真，否则为假。                   |
| \|\|       | 或       | a \|\| b | 如果a和b有一个为真，则结果为真，二者都为假时，结果为假。 |

## 程序流程结构

C/C++支持最基本的三种程序运行结构：**顺序**结构、**选择**结构、**循环**结构。

* 顺序结构：程序按顺序执行，不发生跳转
* 选择结构：依据条件是否满足，有选择的执行相应功能
* 循环结构：依据条件是否满足，循环多次执行某段代码

### 选择结构

#### if语句

**作用：**执行满足条件的语句。

单行if语句：

```cpp
int main() {
	int score = 0;
	cout << "请输入一个分数：" << endl;
	cin >> score;
	cout << "您输入的分数为： " << score << endl;

	//if语句
	//注意事项，在if判断语句后面，不要加分号
	if (score > 600)
	{
		cout << "我考上了一本大学！！！" << endl;
	}

	system("pause");
	return 0;
}
```

多行if语句：

```cpp
int main() {
	int score = 0;
	cout << "请输入考试分数：" << endl;
	cin >> score;

	if (score > 600)
	{
		cout << "我考上了一本大学" << endl;
	}
	else
	{
		cout << "我未考上一本大学" << endl;
	}

	system("pause");
	return 0;
}
```

多条件if语句：

```cpp
int main() {

	int score = 0;

	cout << "请输入考试分数：" << endl;

	cin >> score;

	if (score > 600)
	{
		cout << "我考上了一本大学" << endl;
	}
	else if (score > 500)
	{
		cout << "我考上了二本大学" << endl;
	}
	else if (score > 400)
	{
		cout << "我考上了三本大学" << endl;
	}
	else
	{
		cout << "我未考上本科" << endl;
	}

	system("pause");

	return 0;
}
```

嵌套if语句：

```cpp
int main() {
	int score = 0;
	cout << "请输入考试分数：" << endl;
	cin >> score;

	if (score > 600)
	{
		cout << "我考上了一本大学" << endl;
		if (score > 700)
		{
			cout << "我考上了北大" << endl;
		}
		else if (score > 650)
		{
			cout << "我考上了清华" << endl;
		}
		else
		{
			cout << "我考上了人大" << endl;
		}
	}
	else if (score > 500)
	{
		cout << "我考上了二本大学" << endl;
	}
	else if (score > 400)
	{
		cout << "我考上了三本大学" << endl;
	}
	else
	{
		cout << "我未考上本科" << endl;
	}

	system("pause");
	return 0;
}
```

#### 三目运算符

**作用：** 通过三目运算符实现简单的判断。

**语法：**`表达式1 ? 表达式2 ：表达式3`

- 如果表达式1的值为真，执行表达式2，并返回表达式2的结果。

- 如果表达式1的值为假，执行表达式3，并返回表达式3的结果。

```cpp
int main() {
	int a = 10;
	int b = 20;
	int c = 0;

	c = a > b ? a : b;
	cout << "c = " << c << endl;

	(a > b ? a : b) = 100;
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;
	cout << "c = " << c << endl;

	system("pause");

	return 0;
}
```

#### switch语句

**作用：**执行多条件分支语句。

```cpp
int main() {
	int score = 0;
	cout << "请给电影打分: " << endl;
	cin >> score;

	switch (score)
	{
        case 10:
        case 9:
            cout << "经典" << endl;
            break;
        case 8:
            cout << "非常好" << endl;
            break;
        case 7:
        case 6:
            cout << "一般" << endl;
            break;
        default:
            cout << "烂片" << endl;
            break;
	}

	system("pause");
	return 0;
}
```

> `switch`与多行`if`的区别：
>
> - `switch` 适合单一变量与多个明确值的比较；`if` 适合范围判断或复杂条件
> - `switch` 通常执行效率略高，因为编译器可以优化为跳转表

### 循环结构

#### while循环语句

**作用：**满足循环条件，执行循环语句。

**语法：**` while(循环条件){ 循环语句 }`

```cpp
int main() {
	int num = 0;
	while (num < 10)
	{
		cout << "num = " << num << endl;
		num++;
	}
	
	system("pause");
	return 0;
}
```

#### dowhile循环语句

**作用：** 满足循环条件，执行循环语句

**语法：** `do{ 循环语句 } while(循环条件);`

```cpp
int main() {
	int num = 0;
	do
	{
		cout << num << endl;
		num++;

	} while (num < 10);
	
	
	system("pause");
	return 0;
}
```

> dowhile循环与while循环区别在于，do...while先执行一次循环语句，再判断循环条件

#### for循环语句

**作用：** 满足循环条件，执行循环语句。

**语法：**` for(起始表达式;条件表达式;末尾循环体) { 循环语句; }`

```cpp
int main() {

	for (int i = 0; i < 10; i++)
	{
		cout << i << endl;
	}
	
	system("pause");

	return 0;
}
```

### 跳转语句

#### break语句

**作用:** 用于**跳出**选择结构或者循环结构。

* 出现在switch条件语句中，作用是终止case并跳出switch。

  ```cpp
  int main() {
  	cout << "请选择您挑战副本的难度：" << endl;
  	cout << "1、普通" << endl;
  	cout << "2、中等" << endl;
  	cout << "3、困难" << endl;
  
  	int num = 0;
  	cin >> num;
  
  	switch (num)
  	{
  	case 1:
  		cout << "您选择的是普通难度" << endl;
  		break;
  	case 2:
  		cout << "您选择的是中等难度" << endl;
  		break;
  	case 3:
  		cout << "您选择的是困难难度" << endl;
  		break;
  	}
  
  	system("pause");
  	return 0;
  }
  ```

* 出现在循环语句中，作用是跳出当前的循环语句。

  ```cpp
  int main() {
  	for (int i = 0; i < 10; i++)
  	{
  		if (i == 5)
  		{
  			break;
  		}
  		cout << i << endl;
  	}
  
  	system("pause");
  	return 0;
  }
  ```

* 出现在嵌套循环中，跳出最近的内层循环语句。

  ```cpp
  int main() {
  	for (int i = 0; i < 10; i++)
  	{
  		for (int j = 0; j < 10; j++)
  		{
  			if (j == 5)
  			{
  				break;
  			}
  			cout << "*" << " ";
  		}
  		cout << endl;
  	}
  	
  	system("pause");
  
  	return 0;
  }
  ```

#### continue语句

**作用：**在循环语句中，跳过本次循环中余下尚未执行的语句，继续执行下一次循环。

```cpp
int main() {
	for (int i = 0; i < 100; i++)
	{
		if (i % 2 == 0)
		{
			continue;
		}
		cout << i << endl;
	}
	
	system("pause");
	return 0;
}
```

#### goto语句

**作用：**可以无条件跳转语句

**语法：** `goto 标记;`，如果标记的名称存在，执行到goto语句时，会跳转到标记的位置。

```cpp
int main() {
	cout << "1" << endl;

	goto FLAG;

	cout << "2" << endl;
	cout << "3" << endl;
	cout << "4" << endl;

	FLAG:

	cout << "5" << endl;
	
	system("pause");
	return 0;
}
```

## 数组

### 概述

数组就是一个集合，里面存放了相同类型的数据元素。

- 数组中的每个数据元素都是相同的数据类型。
- 数组是由连续的内存位置组成的。

### 一维数组

#### 一维数组的定义方式

一维数组定义的三种方式：

1. ` 数据类型  数组名[ 数组长度 ]; `
2. `数据类型  数组名[ 数组长度 ] = { 值1，值2 ...};`
3. `数据类型  数组名[ ] = { 值1，值2 ...};`

```cpp
int main() {
	// 数据类型 数组名[元素个数];
	int score[10];
	score[0] = 100;
	score[1] = 99;
	score[2] = 85;
	cout << score[0] << endl;
	cout << score[1] << endl;
	cout << score[2] << endl;


	// 数据类型  数组名[ 数组长度 ] = { 值1，值2 ...};
	int score2[10] = { 100, 90,80,70,60,50,40,30,20,10 };
	for (int i = 0; i < 10; i++)
	{
		cout << score2[i] << endl;
	}

	// 数据类型 数组名[] =  {值1，值2 ，值3 ...};
	int score3[] = { 100,90,80,70,60,50,40,30,20,10 };
	for (int i = 0; i < 10; i++)
	{
		cout << score3[i] << endl;
	}

	system("pause");
	return 0;
}
```

#### 一维数组的数组名

一维数组名称的用途：

1. 可以统计整个数组在内存中的长度
2. 可以获取数组在内存中的首地址

```cpp
int main() {
	int arr[10] = { 1,2,3,4,5,6,7,8,9,10 };

	cout << "整个数组所占内存空间为： " << sizeof(arr) << endl;
	cout << "每个元素所占内存空间为： " << sizeof(arr[0]) << endl;
	cout << "数组的元素个数为： " << sizeof(arr) / sizeof(arr[0]) << endl;

	cout << "数组首地址为： " << (int)arr << endl;
	cout << "数组中第一个元素地址为： " << (int)&arr[0] << endl;
	cout << "数组中第二个元素地址为： " << (int)&arr[1] << endl;

	system("pause");
	return 0;
}
```

### 二维数组

#### 二维数组定义方式

二维数组定义的四种方式：

1. ` 数据类型  数组名[ 行数 ][ 列数 ]; `
2. `数据类型  数组名[ 行数 ][ 列数 ] = { {数据1，数据2 } ，{数据3，数据4 } };`
3. `数据类型  数组名[ 行数 ][ 列数 ] = { 数据1，数据2，数据3，数据4};`
4. ` 数据类型  数组名[  ][ 列数 ] = { 数据1，数据2，数据3，数据4};`

```cpp
int main() {
	//数组类型 数组名 [行数][列数]
	int arr[2][3];
	arr[0][0] = 1;
	arr[0][1] = 2;
	arr[0][2] = 3;
	arr[1][0] = 4;
	arr[1][1] = 5;
	arr[1][2] = 6;

	//数据类型 数组名[行数][列数] = { {数据1，数据2 } ，{数据3，数据4 } };
	int arr2[2][3] =
	{
		{1,2,3},
		{4,5}
	};

	//数据类型 数组名[行数][列数] = { 数据1，数据2 ,数据3，数据4  };
	int arr3[2][3] = { 1,2,3,4 };

	//数据类型 数组名[][列数] = { 数据1，数据2 ,数据3，数据4  };
	int arr4[][3] = { 1,2,3,4,5 };

	for (int i = 0; i < 2; i++)
	{
		for (int j = 0; j < 3; j++)
		{
			cout << arr3[i][j] << " ";
		}
		cout << endl;
	}

	system("pause");
	return 0;
}
```

#### 二维数组数组名

二维数组名称的用途：

* 查看二维数组所占内存空间
* 获取二维数组首地址

```cpp
int main() {
	int arr[2][3] =
	{
		{1,2,3},
		{4,5,6}
	};

	cout << "二维数组大小： " << sizeof(arr) << endl;
	cout << "二维数组一行大小： " << sizeof(arr[0]) << endl;
	cout << "二维数组元素大小： " << sizeof(arr[0][0]) << endl;

	cout << "二维数组行数： " << sizeof(arr) / sizeof(arr[0]) << endl;
	cout << "二维数组列数： " << sizeof(arr[0]) / sizeof(arr[0][0]) << endl;

	cout << "二维数组首地址：" << (int)arr << endl;
	cout << "二维数组第一行地址：" << (int)arr[0] << endl;
	cout << "二维数组第二行地址：" << (int)arr[1] << endl;

	cout << "二维数组第一个元素地址：" << (int)&arr[0][0] << endl;
	cout << "二维数组第二个元素地址：" << (int)&arr[0][1] << endl;

	system("pause");
	return 0;
}
```

## 函数

### 定义和使用

**作用：**将一段经常使用的代码封装起来，减少重复代码。一个较大的程序，一般分为若干个程序块，每个模块实现特定的功能。

**语法：** 

* 返回值类型 ：函数返回的值的数据类型。
* 函数名：函数的名称。
* 参数列表：使用该函数时传入的数据。
* 函数体语句：函数内需要执行的语句。
* return表达式： 和返回值类型挂钩，函数执行完后，返回相应的数据。

```
返回值类型 函数名 （参数列表）
{
       函数体语句
       return表达式
}
```

**示例：**定义一个加法函数，实现两个数相加。

```C++
int add(int num1, int num2)
{
	int sum = num1 + num2;
	return sum;
}
```
### 函数的调用

**形参**是函数声明或定义时括号内列出的参数，用于接收外部传入的值，**实参**是调用函数时实际传递给形参的值或变量。

1. 当函数调用时，实参的值会传递给形参。
2. 实参的类型必须与形参兼容（或可隐式转换）。
3. 有三种参数传递方式：
   1. **按值传递**（默认）：形参是实参的副本，修改形参不影响实参。
   2. **按引用传递**：形参是实参的别名，修改形参会影响实参。
   3. **按指针传递**：通过地址间接操作实参。

**语法：**` 函数名（参数）`

```C++
// 函数定义
int add(int num1, int num2) {
	int sum = num1 + num2;
	return sum;
}

int main() {
	int a = 10;
	int b = 10;
	// 函数调用
	int sum = add(a, b);
	cout << "sum = " << sum << endl;

	a = 100;
	b = 100;

	sum = add(a, b);
	cout << "sum = " << sum << endl;

	system("pause");
	return 0;
}
```

### 函数的常见样式

常见的函数样式有4种：

1. 无参无返
2. 有参无返
3. 无参有返
4. 有参有返

```cs
//1、 无参无返
void test01()
{
	cout << "this is test01" << endl;
}

//2、 有参无返
void test02(int a)
{
	cout << "this is test02" << endl;
	cout << "a = " << a << endl;
}

//3、无参有返
int test03()
{
	cout << "this is test03 " << endl;
	return 10;
}

//4、有参有返
int test04(int a, int b)
{
	cout << "this is test04 " << endl;
	int sum = a + b;
	return sum;
}
```

### 函数的声明

**作用：**告诉编译器函数的存在。函数的**声明可以多次**，但**定义只能有一次**。部分编译器（如Visual Studio 2022）在函数调用之前必须先找到函数的声明或定义，否则会无法生成。

```csharp
// 声明
int max1(int a, int b);
int max1(int a, int b);

int main() {
	int a = 100;
	int b = 200;

	cout << max1(a, b) << endl;

	system("pause");
	return 0;
}

// 定义
int max1(int a, int b)
{
	return a > b ? a : b;
}
```

### 函数的分文件编写

**作用：**让代码结构更加清晰。

函数分文件编写一般有4个步骤：

1. 创建后缀名为.h的**头文件**
2. 创建后缀名为.cpp的**源文件**
3. 在头文件中写函数的声明
4. 在源文件中写函数的定义

```C++
// swap.h文件
#include<iostream>
using namespace std;

void swap(int a, int b);
```

```C++
// swap.cpp文件
#include "swap.h"
void swap(int a, int b)
{
	int temp = a;
	a = b;
	b = temp;

	cout << "a = " << a << endl;
	cout << "b = " << b << endl;
}
```

```C++
// main函数文件
#include "swap.h"
int main() {
	int a = 100;
	int b = 200;
	swap(a, b);

	system("pause");
	return 0;
}
```

## 指针

### 定义和使用

**定义：**指针是一个变量，存储的是另一个变量的**内存地址**（而非值本身）。

**作用：**可以通过指针间接访问内存。

```cpp
int x = 10;      // 定义一个普通变量
int *ptr = &x;   // ptr是指针，存储x的地址（&x取地址）

cout << x;       // 输出x的值：10
cout << &x;      // 输出x的地址（如0x7ffd...）
cout << ptr;     // 输出ptr存储的地址（即&x）
cout << *ptr;    // 输出ptr指向的值（即x的值：10）
```

> `*ptr` 中的 `*` 是**解引用**操作符，表示“取指针指向的值”。

指针变量和普通变量的区别

* 普通变量存放的是数据,指针变量存放的是地址
* 指针变量可以通过" * "操作符，操作指针变量指向的内存空间，这个过程称为解引用

### 指针占的内存空间

所有类型的指针在32位操作系统下占4个字节，在64位操作系统下占8个字节。

```cPp
int main() {
	int a = 10;
	int * p;
	p = &a;

	cout << sizeof(p) << endl;
	cout << sizeof(char *) << endl;
	cout << sizeof(float *) << endl;
	cout << sizeof(double *) << endl;

	system("pause");
	return 0;
}
```

### 空指针和野指针

**空指针**：指针变量指向内存中编号为0的空间

**用途：**初始化指针变量

**注意：**空指针指向的内存是**不可访问**的，访问时程序会报错“读取/写入访问权限冲突”。

```C++
int main() {
	// 指针变量p指向内存地址编号为0的空间
	int * p = NULL;

	// 访问空指针报错：内存编号0 ~255为系统占用内存，不允许用户访问
	cout << *p << endl;

	system("pause");
	return 0;
}
```

**野指针**：指针变量指向非法的内存空间

**注意：**野指针指向的内存是**不可访问**的，访问时程序会报错“读取/写入访问权限冲突”。

```cpp
int main() {
	// 指针变量p指向内存地址编号为0x1100的空间
	int * p = (int *)0x8888;
	// 访问野指针报错 
	cout << *p << endl;

	system("pause");
	return 0;
}
```

### const修饰指针

const修饰指针有三种情况：

1. const修饰指针——常量指针；指针的指向可以修改，指针指向的值不可以修改（编译时报错）
2. const修饰常量——指针常量；指针的指向不可以修改，指针指向的值可以修改（编译时报错）
3. const既修饰指针，又修饰常量；指针的指向和指针指向的值都不可以修改

```cpp
int main() {

	int a = 10;
	int b = 10;

	// const修饰的是指针，指针指向可以改，指针指向的值不可以更改
	const int* p1 = &a;
	p1 = &b; // 正确
	//*p1 = 100; 错误


	// const修饰的是常量，指针指向不可以改，指针指向的值可以更改
	int* const p2 = &a;
	//p2 = &b; 错误
	*p2 = 100; // 正确

	// const既修饰指针又修饰常量
	const int* const p3 = &a;
	//p3 = &b; // 错误
	//*p3 = 100; // 错误

	system("pause");

	return 0;
}
```

### 指针和数组

**作用：**利用指针访问数组中元素

```cpp
int main() {
	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };
	int* p = arr;

	cout << "第一个元素： " << arr[0] << endl;
	cout << "指针访问第一个元素： " << *p << endl;

	for (int i = 0; i < 10; i++)
	{
		// 利用指针遍历数组
		cout << *p << endl;
		p++;
	}

	system("pause");
	return 0;
}
```

### 地址传递

**作用：**利用指针作函数参数，可以修改实参的值

```cpp
void swap1(int a, int b)
{
	int temp = a;
	a = b;
	b = temp;
}
// 地址传递
void swap2(int* p1, int* p2)
{
	int temp = *p1;
	*p1 = *p2;
	*p2 = temp;
}

// 引用传递
void swap3(int& p1, int& p2)
{
	int temp = p1;
	p1 = p2;
	p2 = temp;
}

int main() {
	int a = 10;
	int b = 20;

	swap1(a, b); // 值传递不会改变实参
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;

	swap2(&a, &b); // 地址传递会改变实参
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;

	swap3(a, b); // 引用传递会改变实参
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;

	system("pause");
	return 0;
}
```

## 结构体

### 定义和使用

**定义：**结构体是**用户自定义**的复合数据类型，用于将不同类型的数据组合成一个逻辑单元。

通过结构体创建变量的方式有三种：

* struct 结构体名 变量名
* struct 结构体名 变量名 = { 成员1值 ， 成员2值...}
* 定义结构体时顺便创建变量

```cpp
// 定义
struct Person{
	string name;
	int age;
	float height;
}p3; // 声明

int main() {
	Person p1 = { "Alice", 25, 1.65f }; // 声明
	Person p2; // 声明
	p2.name = "Bob";
	p2.age = 30;

	p3.name = "Mike";
	p3.age = 40;
	p3.height = 1.70f;

	cout << " name: " << p1.name << " age: " << p1.age << " height: " << p1.height << endl;
	cout << " name: " << p2.name << " age: " << p2.age << " height: " << p2.height << endl;
	cout << " name: " << p3.name << " age: " << p3.age << " height: " << p3.height << endl;

	system("pause");
	return 0;
}
```

### 结构体数组

**作用：**结构体数组是存储多个相同结构体类型数据的集合，适合管理一组具有相同属性的数据（如学生信息、坐标点等）。

```cpp
int main() {
	Student students_1[3];
	students_1[0] = { "Alice", 10 };
	students_1[1] = { "Bob", 11 };
	students_1[2] = { "Charlie", 12 };


	Student students_2[3] = {
		{"Alice", 20},
		{"Bob", 21},
		{"Charlie", 22}
	};

	Student students_3[3] = { {"Alice"}, {"Bob", 31} };

	for (int i = 0; i < 3; i++) {
		cout << "Name: " << students_1[i].name
			<< ", Score: " << students_1[i].score << endl;
	}

	cout << '\n' << endl;

	for (int i = 0; i < 3; i++) {
		cout << "Name: " << students_2[i].name
			<< ", Score: " << students_2[i].score << endl;
	}

	cout << '\n' << endl;

	for (int i = 0; i < 3; i++) {
		cout << "Name: " << students_3[i].name
			<< ", Score: " << students_3[i].score << endl;
	}

	system("pause");
	return 0;
}
```

### 结构体指针

**作用：**通过指针访问结构体中的成员，利用操作符 `-> `可以通过结构体指针访问结构体属性。

```cpp
struct Student {
	string name;
	int score;
};

int main() {
	Student student = { "Charlie", 78 };
	Student students[3] = {
		{"Alice", 90},
		{"Bob", 85},
	};

	Student* ptr1 = &student; // 指向结构体对象student
	cout << "Name: " << ptr1->name
		<< ", Score: " << ptr1->score << endl;

	Student* ptr2 = students; // 指向数组首元素
	cout << "Name: " << ptr2->name
		<< ", Score: " << ptr2->score << endl;

	ptr2++; // 移动到数组下一个元素
	cout << "Name: " << ptr2->name
		<< ", Score: " << ptr2->score << endl;

	system("pause");
	return 0;
}
```

### 嵌套结构体

**定义：**嵌套结构体是指在一个结构体内部定义另一个结构体，用于构建更复杂的数据结构，嵌套结构体有两种定义方式：

1. 内部定义嵌套结构体

   ```cpp
   struct Outer {
       int outerData;
       
       struct Inner {  // 内部定义的结构体
           int innerData;
       };
       
       Inner innerObj; // 嵌套结构体成员
   };
   ```

2. 外部定义嵌套结构体

   ```cpp
   struct Inner {  // 先定义内部结构体
       int innerData;
   };
   
   struct Outer {
       int outerData;
       Inner innerObj;  // 使用已定义的结构体
   };
   ```

**访问：**通过多级`.`运算符可访问内部结构体成员。

```cpp
int main() {
	Outer outer;
	outer.outerData = 10;
	outer.innerObj.innerData = 20;  // 通过.运算符访问嵌套成员

	system("pause");
	return 0;
}
```

**初始化：**有嵌套初始化和分段初始化两种方式。

```cpp
Outer outer = {10, {20}};
```

```cpp
Outer outer;
outer.outerData = 10;
outer.innerObj.innerData = 20;
```

**指针：**嵌套结构体也可通过指针访问嵌套成员。

```cpp
Outer outer;
Outer* ptr = &outer;
ptr->innerObj.innerData = 30;  // 通过指针访问嵌套成员
```

### 作为函数参数

结构体作为函数参数有3中传递方式：

1. 传值：创建结构体的完整**副本**，函数内修改**不影响**原结构体

   ```cpp
   struct Point {
   	int x;
   	int y;
   };
   
   void printPoint(Point p) {
   	p.x += 1;
   	cout << "Copy: (" << p.x << ", " << p.y << ")" << endl;
   }
   int main() {
   	Point p = { 10, 20 };
   	printPoint(p); // Copy: (11, 20)
   	cout << p.x << endl; // 10
   }
   ```

2. 传引用：直接操作原结构体，无复制开销

   ```cpp
   struct Point {
   	int x;
   	int y;
   };
   
   void movePoint(Point& p, int dx, int dy) {
   	p.x += dx;
   	p.y += dy;
   }
   
   int main() {
   	Point p = { 10, 20 };
   	movePoint(p, 5, -5);
   	cout << "(" << p.x << ", " << p.y << ")" << endl; // (15, 15)
   }
   ```

   也可传常量引用防止意外修改：

   ```cpp
   struct Student {
       string name;
       int scores[3];
   };
   
   void displayStudent(const Student& s) {
       cout << s.name << "'s scores: ";
       for (int score : s.scores) { // 只能读取，不能修改
           cout << score << " ";
       }
       cout << endl;
   }
   
   int main() {
       Student stu = { "Alice", {90, 85, 88} };
       displayStudent(stu); // 安全高效地访问
   }
   ```

3. 传指针：显式传递地址

   ```cpp
   struct Point {
       int x;
       int y;
   };
   
   void scalePoint(Point* p, float factor) {
       if (p != nullptr) {
           p->x *= factor;
           p->y *= factor;
       }
   }
   
   int main() {
       Point p = { 10, 20 };
       scalePoint(&p, 1.5f); // 传递地址
       cout << "(" << p.x << ", " << p.y << ")" << endl; // (15, 30)
   }
   ```

   也可传常量指针防止意外修改：

   ```cpp
   struct Point {
       int x;
       int y;
   };
   
   void printPoint(const Point* p) {
       cout << "(" << p->x << ", " << p->y << ")" << endl;
       return;
   }
   
   int main() {
       Point p = { 10, 20 };
       printPoint(&p); // 传递地址
   }
   ```

## 程序内存模型

C++程序将**内存**分为4个区域：

- 代码区：存放二进制代码，由操作系统进行管理
- 全局区：存放全局**变量**、**静态变量**和**部分常量（全局常量和字符串常量）**，程序启动时分配，结束时释放
- 栈区：由编译器**自动**分配和释放，存放函数的参数、返回值、局部变量等，超出栈容量会导致内存溢出
- 堆区：**手动**分配（通过`new`/`malloc`申请）和释放（通过`delete`/`free`释放），若不释放，程序结束时由操作系统回收

### 程序运行前

程序运行前只有**静态分配**的区域确定：

- 代码区
  - 存放编译好的二进制代码（机器指令）
  - 只读，内容在运行前固定
  - 共享，内存中只有一份代码，多开的引用进程会共享一份代码
- 全局区
  - **初始化**的**全局变量/静态变量**存放在 `.data` 段
  - **未初始化**的**全局变量/静态变量**存放在 `.bss` 段
  - `const`修饰的**全局常量**和**字符串常量**存放在 `.rodata`（只读数据段）
  - 大小在编译时确定，无动态内存

```cpp
int g_a = 10; // 全局变量
const int c_g_a = 10; // 全局常量

int main() {
	int a = 10; // 局部变量
	cout << "【栈区】局部变量a的地址： " << (long long)&a << endl;
	cout << "【全局区】全局变量g_a的地址: " << (long long)&g_a << endl;

	static int s_a = 10; // 静态变量
	cout << "【全局区】静态变量s_a的地址: " << (long long)&s_a << endl;

	cout << "【全局区】全局常量c_g_a的地址: " << (long long)&c_g_a << endl;

	cout << "【全局区】字符串常量str_a的地址: " << (long long)&"hello world" << endl; // 字符串常量

	const int c_l_a = 10; // 局部常量
	cout << "【栈区】局部常量c_l_a的地址: " << (long long)&c_l_a << endl;

	system("pause");
	return 0;
}
```

### 程序运行后

内存分区开始动态变化，新增**运行时分配**的内容：

- 栈区（Stack）

  - 函数调用时的局部变量、参数、返回地址
  - 嵌套函数调用形成的**栈帧**

  - 自动分配/释放（如函数结束时栈帧弹出）
  - 可能发生栈溢出
  - 注意：**不要返回局部变量的地址**，栈区开辟的数据由编译器自动释放

  ```cpp
  int* func()
  {
  	int a = 10;
  	return &a;
  }
  
  int main() {
  	int* p = func();
  
  	cout << *p << endl; // 第一次能打印正确数字，因为编译器做了保留
  	cout << *p << endl; // 第二次无法打印正确数字（x86架构），因为栈区数据释放
  
  	system("pause");
  	return 0;
  }
  ```

- 堆区（Heap）

  - 通过 `new`/`malloc` 动态分配的内存
  - 需手动释放（`delete`/`free`），否则内存泄漏

  ```cpp
  int* func()
  {
  	int* a = new int(10); // 利用new关键字将数据开辟到堆区
  	return a;
  }
  
  int main() {
  	int* p = func();
  
  	cout << *p << endl;
  	cout << *p << endl;
  
  	delete p;
  	cout << *p << endl; // 运行时报错，因为释放的内存不可访问
  
  	system("pause");
  	return 0;
  }
  ```

### new操作符

C++中利用`new`操作符在**堆区**开辟数据：

- 利用new创建的数据，返回该数据类型的**指针**

- 手动开辟和释放，释放用操符`delete`
- 语法：` new 数据类型`

```cpp
int main() {
	int* arr = new int[10];
	for (int i = 0; i < 10; i++) {
		arr[i] = i + 100;
	}

	for (int i = 0; i < 10; i++) {
		cout << arr[i] << endl;
	}
	
	delete[] arr; //释放数组 delete 后加 []

	system("pause");
	return 0;
}
```

## 引用

### 定义

**定义：**引用是一个已存在变量的**别名**。引用在定义时**必须初始化**，且一旦绑定到一个变量后，**不能再指向其他变量**。

**作用：**它通过间接指向同一块内存地址的方式，为变量提供另一个名称。

**语法：**`数据类型& 别名 = 原名`

```cpp
int main() {
	int a = 10;
	int& b = a;

	cout << "a = " << a << endl; // a = 10
	cout << "b = " << b << endl; // b = 10

	b = 100;

	cout << "a = " << a << endl; // a = 100
	cout << "b = " << b << endl; // b = 100

	system("pause");
	return 0;
}
```

### 作为函数参数

**作用：**函数传参时，可以利用引用让形参修饰实参。

```cpp
void mySwap(int& a, int& b) {
	int temp = a;
	a = b;
	b = temp;
}

int main() {
	int a = 10;
	int b = 20;

	mySwap(a, b);
	cout << "a:" << a << " b:" << b << endl;

	system("pause");
	return 0;
}
```

### 作为返回值

**作用：**引用可以作为函数的返回值。

```cpp
int& test() {
	static int a = 10;
	return a;
}

int main() {
	int& ref = test();
	test() = 100;

	cout << "ref = " << ref << endl; // ref = 100

	system("pause");
	return 0;
}
```

### 引用的本质

引用在行为逻辑上等价于**指针常量**，且大多数编译器将引用底层实现为指针常量。

```cpp
// 编译器发现是引用，转换为 int* const ref = &a;
void func(int& ref){
	ref = 100; // 转换为*ref = 100
}
```

### 常量引用

**作用：**常量引用修饰函数形参，可以防止函数内部对实参进行修改。

```cpp
void showValue(const int& v) {
	// v += 10; 表达式必须是可修改的左值
	cout << v << endl;
}

int main() {
	int a = 10;
	showValue(a);

	system("pause");
	return 0;
}
```

## 函数默认参数

**定义：**函数的形参列表中的参数可以有默认值，函数的**声明和实现中只能有一个有默认参数**，否则会有**”二义性“**

**语法：**`返回值类型  函数名 （参数= 默认值）{}`

```cpp
int func1(int a, int b = 10, int c = 10) {
	return a + b + c;
}

// 如果函数声明有默认参数，实现时就不能有默认参数，否则运行会报“重定义默认参数”
int func2(int a = 10, int b = 10);
int func2(int a, int b) {
	return a + b;
}

int main() {
	cout << "ret = " << func1(20, 20) << endl; // ret = 50
	cout << "ret = " << func2(100) << endl; // ret = 110

	system("pause");
	return 0;
}
```

### 函数占位参数

**定义：**函数的形参列表中可以有占位参数，占位参数**省略参数名**，调用函数时必须填补该位置（除非占位参数有默认参数）

```cpp
void func(int a, int = 10) {
	cout << "this is a func" << endl;
}

int main() {
	func(10);

	system("pause");
	return 0;
}
```

### 函数重载

定义：**同一作用域**下，函数名相同，参数不同（**类型、个数**或**顺序**不同）的一组函数。

```cpp
void func()
{
	cout << "func 的调用" << endl;
}
void func(int a)
{
	cout << "func (int a) 的调用" << endl;
}
void func(double a)
{
	cout << "func (double a)的调用" << endl;
}
void func(int a, double b)
{
	cout << "func (int a ,double b) 的调用" << endl;
}
void func(double a, int b)
{
	cout << "func (double a ,int b)的调用" << endl;
}

int main() {
	func();
	func(10);
	func(3.14);
	func(10, 3.14);
	func(3.14, 10);

	system("pause");
	return 0;
}
```

引用可作为重载条件：

```cpp
void func(int &a) {
	cout << "func (int &a) 调用" << endl;
}

void func(const int &a) {
	cout << "func (const int &a) 调用" << endl;
}

int main() {
	int a = 10;
	func(a); // func (int &a) 调用
	func(10); // func (const int &a) 调用

	system("pause");
	return 0;
}
```

函数重载有默认参数，调用时不得有歧义：

```cpp
void func(int a, int b = 10) {
    cout << "func2(int a, int b = 10) 调用" << endl;
}

void func(int a) {
    cout << "func2(int a) 调用" << endl;
}

int main() {
    // func(10); 编译报错：有多个重载参数"func"实例于参数列表匹配
    func(10, 20);

    system("pause");
    return 0;
}
```

## 类和对象

面向对象三大特征：封装、继承、多态。

- **封装（Encapsulation）**：将属性和操作数据的方法（行为）捆绑为一个独立的单元（类），并隐藏内部实现细节，仅通过可控的接口与外界交互。
- **继承（Inheritance）**：子类继承父类的属性和方法，并可扩展或重写父类的功能。
- **多态（Polymorphism）**：同一操作作用于不同对象时，可产生不同的行为，如方法**重写**和**接口/抽象类**。

### 封装

**作用：**

* 将属性和行为作为一个整体
* 将属性和行为加以权限控制

**语法：** `class 类名{   访问权限： 属性  / 行为  };`

```cpp
const double PI = 3.14;
class Circle
{
public:
	int m_r;
	double GetPerimeter()
	{
		return 2 * PI * m_r;
	}
};

int main() {
	Circle c1;
	c1.m_r = 10;
	cout << "圆的周长为: " << c1.GetPerimeter() << endl;

	system("pause");
	return 0;
}
```

#### 访问修饰符

类在设计时，可以把属性和行为放在不同的权限下，访问权限有三种：

1. public：公共权限 ，类内可以访问，类外可以访问
2. protected：保护权限，类内和子类可以访问，类外不可访问
3. private：私有权限，类内可以访问，类外不可访问

```cpp
class Person
{
public:
	string m_Name;
protected:
	string m_Car;
private:
	int m_PassWord;
public:
	void Func()
	{
		m_Name = "Mike";
		m_Car = "BWM";
		m_PassWord = 123456;
	}
};

class Teacher: public Person {
public:
	void Func()
	{
		m_Name = "Tina";
		m_Car = "Avatar";
		//m_PassWord = 000000; 不可访问
	}
};

int main() {
	Person p;
	p.m_Name = "Alice";
	//p.m_Car = "Auto"; 不可访问
	//p.m_PassWord = 123456; 不可访问

	system("pause");
	return 0;
};
```

#### struct和class的区别

在C++中，`struct` 和 `class` 的**核心区别在于默认的成员访问权限和继承权限**，但它们的底层能力几乎完全相同。

- `struct`的成员默认权限为`public`
- `class`的成员默认权限为`private`

```cpp
class C1
{
	int  m_A; // 默认是private
};

struct C2
{
	int m_A;  // 默认是public
};

int main() {
	C1 c1;
	//c1.m_A = 10; 没有访问权限

	C2 c2;
	c2.m_A = 10;

	system("pause");
	return 0;
}
```

#### 构造函数

**作用：**在对象**创建时调用**，用于**初始化**对象的数据成员

**特点：**

- 与类同名，无返回类型（`void`也没有）
- 可以重载
- 如果没有显式定义，编辑器会生成一个空实现的**默认无参构造函数**

**语法：**`类名(){}`

```cpp
class MyClass {
public:
    int value;
    MyClass() : value(0) {}             // 默认构造函数
    MyClass(int v) : value(v) {}        // 带参构造函数
    MyClass(const MyClass& other) {      // 拷贝构造函数
        value = other.value;
    }
};
```

#### 析构函数

**作用：**在对象销毁时自动调用，用于释放资源（如动态内存、文件句柄等）

**特点：**

- 类名前加`~`，无返回类型和参数
- 不可重载，每个类只有一个析构函数
- 如果没有显式定义，编辑器会生成一个空实现的**默认析构函数**，但默认析构函数不会释放动态分配的资源

**语法：**`类名(){}`

```cpp
class MyClass {
public:
    int* ptr;
    MyClass() { ptr = new int(10); }    // 构造函数分配内存
    ~MyClass() { delete ptr; }           // 析构函数释放内存
};
```

#### 拷贝构造函数

**定义：**拷贝构造函数是一种特殊构造函数，用于创建一个新对象作为现有对象的**副本**，它在以下情况下被调用：

1. 用一个对象初始化另一个对象

   ```cpp
   void test() {
   	Person p1(100);
   	Person p2(p1);
   }
   ```

2. 对象作为函数参数按值传递

   ```cpp
   void doWork(Person p) {}
   void test() {
   	Person p;
   	doWork(p);
   }
   ```

3. 对象作为函数返回值按值返回

   ```cpp
   Person test()
   {
   	Person p;
   	cout << &p << endl;
   	return p;
   }
   ```

**特点：**

1. 参数必须是对**同类对象**的**常量引用**（`const T&`）
2. 如果没有显式定义，编译器会自动生成一个**默认拷贝构造函数**，执行**浅拷贝**

```cpp
class Person {
public:
    int m_Age;
    char* m_Name;

    Person(int age, const char* name) {
        cout << "有参构造函数" << endl;
        m_Age = age;
        m_Name = new char[strlen(name) + 1]; // C风格字符串末尾是'\0'
        strcpy_s(m_Name, strlen(name) + 1,  name);
    }
};

int main() {
	Person p1(100, "Alice"); // 调用有参构造函数，打印“有参构造函数”
	Person p2 = p1; // 调用 Person 默认的拷贝构造函数

    cout << "p1的m_Name地址: " << &p1.m_Name << endl;
    cout << "p2的m_Name地址: " << &p2.m_Name << endl;

	cout << "p2的m_Age: " << p2.m_Age << endl; // 100

    strcpy_s(p2.m_Name, strlen("Bob") + 1, "Bob");
    cout << "p1.m_Name: " << p1.m_Name << endl; // Bob

	system("pause");
	return 0;
}
```

用拷贝构造函数初始化对象有三种调用方式：

1. `Person p2 = p1;`：拷贝初始化，不会生成临时对象
2. `Person p2(p1);` ：直接初始化，不会生成临时对象
3. `Person p2 = Person(p1);` 显示构造+拷贝初始化，会产生临时匿名对象

```cpp
class Person {
public:
    int m_Age;

    Person(int age) {
        cout << "有参构造函数" << endl;
        m_Age = age;
    }

    ~Person() {
        cout << "析构函数" << endl;
    }
};

int main() {
    Person p1(100); // 调用有参构造函数，打印“有参构造函数”
    Person p2 = p1; // 拷贝初始化，不会生成临时对象
    Person p3(p1); // 直接初始化，不会生成临时对象，等价于拷贝初始化
    Person p4 = Person(p1); // 显示构造+拷贝初始化，会产生临时匿名对象，匿名对象释放前打印“析构函数”

    system("pause");
    return 0;
}
```

RVO/NRVO优化：在函数返回一个**临时对象**时，直接将该对象构造到调用者的目标内存中，**跳过拷贝/移动操作**。

- RVO（返回值优化）：当函数返回一个**匿名**临时对象时，编译器直接在调用者的栈帧上构造该对象，避免拷贝临时对象。
- NRVO（具名返回值优化）：当函数返回一个**具名**临时对象时，编译器尝试将该对象直接构造在调用者的栈帧上，避免拷贝临时对象。

```cpp
struct Test {
    Test() { cout << "构造函数\n"; }
    Test(const Test&) { cout << "拷贝构造\n"; }
    ~Test() { cout << "析构函数\n"; }
};

Test createTest() {
    return Test(); // RVO
}

Test createNamedTest() {
    Test t;
    return t; // NRVO
}


int main() {
    Test t1 = createTest(); // 打印"构造函数", 不打印"析构函数"，RVO生效
    Test t2 = createNamedTest(); // 打印"构造函数"，不打印"析构函数"，NRVO生效
    Test t3 = Test(t1); // 打印"拷贝构造", 不打印"析构函数"，RVO生效

    system("pause");
    return 0;
}
```

是否手动实现拷贝构造函数对RVO生效的影响：

| **情况**           | **`Person p2 = Person(p1);` 是否打印额外析构？** |
| ------------------ | ------------------------------------------------ |
| **未定义拷贝构造** | 是（调用临时对象的析构函数）                     |
| **定义拷贝构造**   | 否（优化跳过临时对象）                           |

未定义拷贝构造函数，不会进行RVO/NRVO优化：

```cpp
class Person {
public:
    int m_Age;

    Person(int age) {
        m_Age = age;
    }

    //Person(const Person& p) {
    //    m_Age = p.m_Age;
    //}

    ~Person() {
        cout << "析构函数" << endl;
    }
};

int main() {
    Person p1(100);
    Person p2 = Person(p1); // 打印“析构函数”

    system("pause");
    return 0;
}
```

手动实现了拷贝构造函数，编译器会认为这是一个 **“非平凡（non-trivial）”操作**，会进行RVO/NRVO优化：

```cpp
class Person {
public:
    int m_Age;

    Person(int age) {
        m_Age = age;
    }

    Person(const Person& p) {
        m_Age = p.m_Age;
    }

    ~Person() {
        cout << "析构函数" << endl;
    }
};

int main() {
    Person p1(100);
    Person p2 = Person(p1); // 不打印“析构函数”

    system("pause");
    return 0;
}
```

**根本原因：自定义的拷贝/移动构造函数触发了编译器优化策略**

- 当未显式定义拷贝构造函数时，编译器生成的默认拷贝构造函数是`trivial`（平凡的）
  - `trivial`拷贝构造的行为是逐字节复制
  - 此时`Person(p1)`会被视为一个临时对象，触发析构
- 当显式定义拷贝构造函数时：
  - 拷贝构造函数变为`non-trivial`（非平凡的，因为用户定义了行为）
  - 触发编译器拷贝省略策略，直接优化为在`p2`的地址构造`p1`（RVO生效）

#### 构造函数覆盖规则

- 如果定义了有参构造函数，编译器不再提供默认无参构造函数，但会提供默认拷贝构造函数

- 如果定义了拷贝构造函数，编译器不再提供其他构造函数

#### 深拷贝和浅拷贝

- 当类内包含指针成员且管理动态分配的内存时，若未自定义拷贝构造函数而使用编译器的默认拷贝构造函数，会导致**浅拷贝（Shallow Copy）**问题，进而可能引发**重复释放同一块堆内存**的未定义行为

- 自定义拷贝构造函数的本质是**确保每个对象拥有独立的资源副本**，避免多个对象共享同一资源导致的重复释放或数据竞争


#### 初始化列表

**作用：**C++提供了初始化列表语法，用来初始化属性

**语法：**`构造函数()：属性1(值1),属性2（值2）... {}`

```cpp
class Person {
public:
	Person(int a, int b, int c) :m_A(a), m_B(b), m_C(c) {}
	void PrintPerson() {
		cout << "m_A:" << m_A << endl;
		cout << "m_B:" << m_B << endl;
		cout << "m_C:" << m_C << endl;
	}
private:
	int m_A;
	int m_B;
	int m_C;
};

int main() {
	Person p(1, 2, 3);
	p.PrintPerson();

	system("pause");
	return 0;
}
```

#### 类作为类成员

- 按照成员在类中的**声明顺序（与初始化列表的顺序无关）**，先调用所有成员对象的构造函数。
- 在所有成员对象构造完成后，**再执行本类的构造函数**。
- 析构函数的调用顺序与构造函数的调用顺序**完全相反**，遵循“**后构造的对象先析构**”的原则（即栈的“后进先出”）

```cpp
class Member {
public:
    Member(int id) { cout << "Member " << id << " constructed" << endl; }
};

class MyClass {
    Member m1;
    Member m2;
public:
    MyClass() : m2(2), m1(1) {
        cout << "MyClass constructed" << endl;
    }
};

int main() {
    MyClass obj;
    // Member 1 constructed  m1 先构造（声明顺序优先）
	// Member 2 constructed  m2 后构造
	// MyClass constructed   最后调用本类的构造函数
    
    system("pause");
	return 0;
}
```

#### 静态成员

**定义：**静态成员就是在成员变量和成员函数前加上关键字`static`

- 静态成员变量：
  - 共享性：所有类对象共享**同一份**静态成员变量（储存在**全局区**）
  - 初始化：类内声明，**类外初始化**
  - 不依赖对象：即使没有创建对象，静态成员变量也存在（编译阶段就分配内存）
- 静态成员函数：
  - 共享性：所有类对象共享同一个函数
  - 访问对象：只能访问**静态成员变量**或其他**静态成员函数**
  - 不依赖对象：通过类名直接调用，无需创建对象

```cpp
class MyClass {
public:
    static void printCount() {
        cout << "Count: " << count; // 只能访问静态成员
    }
    static int count; // 类内声明
};
int MyClass::count = 0; // 类外初始化

int main() {
    MyClass::printCount(); // Count: 0
    MyClass c;
    c.count = 1; // 也可用类名访问静态成员变量，MyClass::count = 1
    
    c.printCount(); // Cout: 1
    
    system("pause");
	return 0;
}
```

#### 对象的内存占用

- 只有非静态成员变量占用对象的内存空间，每个对象都会包含这些成员的独立副本

- **静态成员变量**不占用对象的内存空间，储存在**静态区**，所有对象**共享**同一份静态成员变量
- **成员函数**不占用类的对象的内存空间，储存在**代码区**，所有对象**共享**同一份代码；非静态成员函数通过隐式的`this`指针访问对象数据

```cpp
class MyClass {
    int x;
    static int y; // 静态成员变量不占类对象内存
    void foo() {} // 非静态成员函数不占类对象内存
    static void bar() {} // 静态成员函数不占类对象内存
};

int MyClass::y = 0;

int main() {
    MyClass obj;
    std::cout << sizeof(obj) << std::endl; // 4（仅 int x 的大小）
    return 0;
}
```

#### this指针

**定义：**

- `this` 指针是一个**隐含的**、**非静态成员函数**自动拥有的指针，它**指向当前调用该成员函数的对象实例**，且不可修改指向；作用是让成员函数知道自己在操作哪个对象的数据

- 当通过对象调用成员函数时，`this` 自动绑定到该对象的地址

**作用：**

- 当形参和成员变量同名时，可用`this`指针来区分

  ```cpp
  class MyClass {
      int x;
  public:
      void setX(int x) {
          this->x = x;  // 明确指定成员变量而非参数
      }
  };
  ```

- 在类的非静态成员函数中返回对象本身，可使用`return *this`

  ```cpp
  class Calculator {
  public:
      Calculator& add(int n) {
          value += n;
          return *this;  // 返回当前对象的引用
      }
      int value = 0;
  };
  
  int main() {
      Calculator calc;
      calc.add(5).add(3);  // 链式调用
  
      cout << calc.value << endl; // 8
  	system("pause");
  	return 0;
  }
  ```

#### 常函数

**定义：**在成员函数声明和定义后加上`const`关键字

**语法：**`返回类型 函数名(参数列表) const;`

**特点：**

- 常函数内**不可修改**成员属性；但成员属性声明时加关键字`mutable`后，在常函数中依然可以修改

  ```cpp
  class Person {
  public:
  	Person(): m_A(0), m_B(0) {}
  
  	void SetPersonB() const {
  		// this->m_A = 100; 报错：表达式必须是可修改的左值 
  		this->m_B = 100;
  	}
      
      void SetPersonA() {
          this->m_A = 100;
      }
  public:
  	int m_A;
  	mutable int m_B; // 可变的
  };
  ```

- 常对象（用`const`修饰的对象）只能调用常函数

  ```cpp
  const Person p;
  // p.SetPersonA(); 报错：对象含有与成员函数不兼容的类型限定符
  ```

#### 友元

友元是一种机制，允许外部实体访问当前类的**私有（private）和受保护（protected）成员**。友元破坏了封装性，但能提供更高的灵活性。有三种类型的成员可以作为友元：

- **友元全局函数**

  - **作用**：允许一个**全局函数**访问类的私有或受保护成员
  - **语法**：在类内用 `friend` 声明全局函数，函数的定义可以在**类内或类外**

  ```cpp
  class Box {
  private:
      int width;
  
  public:
      Box(int w) : width(w) {}
  
      // 声明全局函数为友元，定义在类外
      friend void printWidth01(Box box);
      // 声明全局函数为友元，定义在类内
      friend void printWidth02(Box box) {
          cout << "Box width: " << box.width << endl;
      }
  };
  
  void printWidth01(Box box) {
      // 可以访问私有成员 width
      cout << "Box width: " << box.width << endl;
  }
  
  int main() {
      Box box(10);
      printWidth01(box); // 输出: Box width: 10
      printWidth02(box); // 输出: Box width: 10
  
      return 0;
  }
  ```

- **友元类**

  - **作用**：允许另一个类的**所有成员函数**访问当前类的私有或受保护成员
  - **语法**：在类内部用 `friend class` 声明友元类

  ```cpp
  class Box {
  private:
      int width;
  
  public:
      Box(int w) : width(w) {}
  
      // 声明 Printer 类为友元
      friend class Printer;
  };
  
  class Printer {
  public:
      void printWidth(Box box) {
          // Printer 的成员函数可以访问 Box 的私有成员
          cout << "Box width: " << box.width << endl;
      }
  };
  
  int main() {
      Box box(20);
      Printer printer;
      printer.printWidth(box); // 输出: Box width: 20
      return 0;
  }
  ```

- **友元成员函数**

  - **作用**：允许另一个类的**特定成员函数**访问当前类的私有或受保护成员
  - **语法：**在类内部用 `friend` 声明其他类的成员函数

  ```cpp
  class Box; // 前向声明
  class Printer {
  public:
      void printWidth(Box box);
  };
  
  class Box {
  private:
      int width;
  
  public:
      Box(int w) : width(w) {}
  
      // 声明 Printer 类的成员函数为友元
      friend void Printer::printWidth(Box box);
  };
  
  // Printer 成员函数的定义（需要 Box 的完整定义）
  void Printer::printWidth(Box box) {
      cout << "Box width: " << box.width << endl; // 可以访问 Box 类的私有成员
  }
  
  int main() {
      Box box(30);
      Printer printer;
      printer.printWidth(box); // 输出: Box width: 30
      return 0;
  }
  ```

#### 运算符重载

**定义：**一种特殊的函数重载，通过定义名为`operator@`的函数（`@`代表要重载的运算符），来指定该运算符在自定义类型上的行为。

- 后置递增/递减需要用`int`占位符；且返回的是对象的**值**，而非引用

```cpp
class Vector2D {
private:
    double x, y;

public:
    // 构造函数
    Vector2D(double x = 0, double y = 0) : x(x), y(y) {}

    // 获取坐标
    double getX() const { return x; }
    double getY() const { return y; }

    // 1. 加号运算符重载 (向量相加)
    Vector2D operator+(const Vector2D& other) const {
        return Vector2D(x + other.x, y + other.y);
    }

    Vector2D operator+(double scalar) const {
        return Vector2D(x + scalar, y + scalar);
    }

    // 2. 减号运算符重载 (向量相减)
    Vector2D operator-(const Vector2D& other) const {
        return Vector2D(x - other.x, y - other.y);
    }

    // 3. 左移运算符重载 (用于输出)
    friend ostream& operator<<(ostream& os, const Vector2D& vec) {
        os << "(" << vec.x << ", " << vec.y << ")";
        return os;
    }

    // 4. 递增运算符重载 (前缀++)
    Vector2D& operator++() {
        ++x;
        ++y;
        return *this;
    }

    // 4. 递增运算符重载 (后缀++)，返回递增之前的值，int是占位参数，编译器认为是后置递增
    Vector2D operator++(int) {
        Vector2D temp = *this;
        ++(*this); // 调用前缀++
        return temp;
    }

    // 4. 递减运算符重载 (前缀--)
    Vector2D& operator--() {
        --x;
        --y;
        return *this;
    }

    // 4. 递减运算符重载 (后缀--)，返回递增之前的值，int是占位参数，编译器认为是后置递减
    Vector2D operator--(int) {
        Vector2D temp = *this;
        --(*this); // 调用前缀--
        return temp;
    }

    // 5. 赋值运算符重载，返回引用支持链式调用
    Vector2D& operator=(const Vector2D& other) {
        if (this != &other) { // 比较地址，防止自赋值
            x = other.x;
            y = other.y;
        }
        return *this;
    }

    // 6. 关系运算符重载
    bool operator==(const Vector2D& other) const {
        return (x == other.x) && (y == other.y);
    }

    bool operator!=(const Vector2D& other) const {
        return !(*this == other);
    }

    bool operator<(const Vector2D& other) const {
        return (x * x + y * y) < (other.x * other.x + other.y * other.y);
    }

    bool operator>(const Vector2D& other) const {
        return other < *this;
    }

    bool operator<=(const Vector2D& other) const {
        return !(*this > other);
    }

    bool operator>=(const Vector2D& other) const {
        return !(*this < other);
    }
    
    // 7. 函数调用运算符重载
    // 示例1：缩放向量（返回缩放后的新向量）
    Vector2D operator()(double scale) const {
        return Vector2D(x * scale, y * scale);
    }

    // 示例2：计算与另一个向量的点积（返回标量）
    double operator()(const Vector2D& other) const {
        return x * other.x + y * other.y;
    }
};

int main() {
    Vector2D v1(3, 4);
    Vector2D v2(1, 2);

    // 1. 加号运算符
    Vector2D sum = v1 + v2;
    std::cout << "v1 + v2 = " << sum << std::endl; // 输出 (4, 6)

    Vector2D sum2 = v1 + 100;
    std::cout << "v1 + 100 = " << sum2 << std::endl; // 输出 (4, 6)

    // 2. 减号运算符
    Vector2D diff = v1 - v2;
    std::cout << "v1 - v2 = " << diff << std::endl; // 输出 (2, 2)

    // 3. 左移运算符
    std::cout << "v1: " << v1 << ", v2: " << v2 << std::endl;

    // 4. 递增运算符
    Vector2D v3 = v1;
    std::cout << "v3++ = " << v3++ << ", now v3 = " << v3 << std::endl;
    std::cout << "++v3 = " << ++v3 << std::endl;

    // 5. 赋值运算符
    Vector2D v4;
    v4 = v1;
    std::cout << "v4 = " << v4 << std::endl;

    // 6. 关系运算符
    std::cout << "v1 == v2? " << (v1 == v2) << std::endl; // 0 (false)
    std::cout << "v1 != v2? " << (v1 != v2) << std::endl; // 1 (true)
    std::cout << "v1 < v2? " << (v1 < v2) << std::endl;   // 0 (false)
    std::cout << "v1 > v2? " << (v1 > v2) << std::endl;   // 1 (true)
    
    // 7. 函数调用运算符
    Vector2D scaled = v1(2.0); // 缩放为原来的2倍
    std::cout << "v1 scaled by 2: " << scaled << std::endl; // 输出 (6, 8)
    double dotProduct = v1(v2); // v1和v2的点积
    std::cout << "v1 · v2 = " << dotProduct << std::endl; // 输出 3 * 1 + 4 * 2 = 11

    system("pause");
    return 0;
}
```

### 继承

**定义：**继承是指一个类（派生类/子类）可以继承另一个类（基类/父类）的属性和方法，同时可以添加自己的新特性。

**语法：**

```cpp
class BaseClass {
    // 基类成员
};

class DerivedClass : 访问控制符 BaseClass {
    // 派生类成员
};
```

#### 继承方式

C++中有三种继承方式，决定了基类成员在派生类中的访问权限：

1. **public继承**（最常用）
   - 基类的public成员在派生类中保持public
   - 基类的protected成员在派生类中保持protected
   - 基类的private成员不可直接访问
2. **protected继承**
   - 基类的public和protected成员在派生类中都变为protected
   - 基类的private成员不可直接访问
3. **private继承**
   - 基类的public和protected成员在派生类中都变为private
   - 基类的private成员不可直接访问

#### 构造顺序和析构顺序

一个派生类中的类对象的构造顺序如下：

1. 父类构造：先构造**最顶层**的基类，若基类有多个按继承**声明顺序**从左到右构造
2. 成员对象构造：按类定义中成员变量的**声明顺序**构造
3. 自身构造：执行自身的构造函数

析构顺序和构造顺序完全相反

```cpp
class Base {
public:
    Base() { cout << "Base constructed\n"; }
    ~Base() { cout << "Base destroyed\n"; } // 虚析构确保多态安全
};

class Member {
public:
    Member() { cout << "Member constructed\n"; }
    ~Member() { cout << "Member destroyed\n"; }
};

class Derived : public Base {
    Member m;
public:
    Derived() { cout << "Derived constructed\n"; }
    ~Derived() { cout << "Derived destroyed\n"; }
};

int main() {
    Derived d;
    return 0;
}
```

#### 同名成员和名字隐藏

当子类和父类出现同名成员变量时，默认情况下访问的是**子类的成员变量**；如子类需访问父类的同名成员变量，必须显式指定作用域

```cpp
class Base {
public:
    int value = 10;  // 父类成员变量
};

class Derived : public Base {
public:
    int value = 20;  // 子类同名成员变量
};

int main() {
    Derived d;
    cout << d.value << endl; // 20
    cout << d.Base::value << endl; // 10
    return 0;
}
```

当子类定义了与父类同名的函数（即使参数不同），父类的**所有同名函数都会被隐藏**；如子类需访问父类的同名成员函数必须显示指定作用域

```cpp
class Base {
public:
    void show() { cout << "Base::show()" << endl; }
    void show(int x) { cout << "Base::show(int)" << endl; } // 重载函数
};

class Derived : public Base {
public:
    void show() { cout << "Derived::show()" << endl; } // 隐藏父类所有 show()
};

int main() {
    Derived d;
    d.show();          // 输出 "Derived::show()"
    // d.show(10);     // 错误！父类的 show(int) 被隐藏
    d.Base::show();    // 输出 "Base::show()"
    d.Base::show(10);  // 输出 "Base::show(int)"
    return 0;
}
```

#### 多继承

**定义：**允许一个类同时继承多个基类

```cpp
class Derived : public Base1, public Base2, ... {
    // 派生类成员
};
```

**问题：**菱形继承问题，一个派生类通过**多条路径**继承**同一个基类**，会导致**数据冗余**和**二义性**；因此实际开发中尽量少用多继承，优先使用**组合**或**单继承+接口**的方式

```cpp
class A {
public:
    int value = 10;
};

class B : public A {};  // B 继承 A
class C : public A {};  // C 继承 A
class D : public B, public C {};  // D 继承 B 和 C（菱形继承）

int main() {
    D d;
    // 编译错误：不知道访问 B::A::value 还是 C::A::value
    cout << d.value << endl;

    // 必须明确指定路径
    cout << d.B::value << endl;  // 输出 10
    cout << d.C::value << endl;  // 输出 10
    return 0;
}
```

**解决方案：**虚继承，使用`virtual`关键字让两个派生类共享同一份基类的实例，虚继承会增加**虚基类指针**，略微影响性能。虚继承适用于派生类需要共享基类数据（如“人”作为“学生”和“老师”的共同基类）

```cpp
class A {
public:
    int value = 10;
};

class B : virtual public A {};  // 虚继承
class C : virtual public A {};  // 虚继承
class D : public B, public C {};

int main() {
    D d;
    cout << d.value << endl;  // 正确，输出 10
    return 0;
}
```

### 多态

**定义：**多态是面向对象编程的三大特性之一，指**同一操作**作用于**不同对象**时会产生不同的行为。多态分为**静态多态**和**动态多态**，核心区别在于**绑定时机**（编译期还是运行期）

|   **特性**   |     **静态多态**     |      **动态多态**      |
| :----------: | :------------------: | :--------------------: |
| **绑定时机** |        编译期        |         运行期         |
| **实现方式** |    函数重载、模板    |      虚函数、继承      |
|   **性能**   | 高效（无运行时开销） |  稍慢（需查虚函数表）  |
|  **灵活性**  |    依赖编译时类型    | 支持运行时类型动态替换 |

- 静态多态：在编译阶段确定具体调用的函数，通过**函数重载**和**模板**实现

  ```cpp
  // 函数重载（静态多态）
  void print(int a) { cout << "int: " << a; }
  void print(double a) { cout << "double: " << a; }
  
  // 模板（静态多态）
  template <typename T>
  void show(T val) { cout << val; }
  
  int main() {
      print(10);      // 调用 print(int)
      print(3.14);    // 调用 print(double)
      show("hello");  // 模板实例化为 show<const char*>
  }
  ```

- 动态多态：运行时通过**虚函数**和**继承关系**确定调用的具体函数

  ```cpp
  class Animal {
  public:
      virtual void speak() { cout << "Animal sound" << endl; }
  };
  
  class Dog : public Animal {
  public:
      void speak() override { cout << "Woof!" << endl; }
  };
  
  class Cat : public Animal {
  public:
      void speak() override { cout << "Meow!" << endl; }
  };
  
  int main() {
      Animal* pet = new Dog();
      pet->speak(); // 输出 "Woof!"（运行时决定调用Dog::speak）
  
      pet = new Cat();
      pet->speak(); // 输出 "Meow!"（运行时决定调用Cat::speak）
  }
  ```

#### 虚函数表和虚指针

动态多态的本质是通过**虚函数**和**继承机制**，在运行时动态决定调用哪个类的成员函数，其核心实现依赖于：

- **虚函数表(vtable)**
  - 如果一个类包含虚函数或继承自包含虚函数的基类，编译器会为该类生成一个虚函数表
  - 虚函数表是储存虚函数指针的数组，每个条目指向该类**实际实现**的虚函数地址
  - 派生类会继承基类的虚函数表，如果重写了虚函数，虚函数表中对应的条目会被**更新为派生类的函数地址**；未重写的虚函数保留基类的实现
- **虚指针(vptr)**
  - 如果一个对象的类包含虚函数或继承自包含虚函数的基类，编译器会为该对象生成一个虚指针，**指向**该对象所属类的**虚函数表**
  - 运行时通过基类指针调用虚函数时，程序**通过对象的虚指针找到虚函数表**，从虚函数表中查找虚函数的**实际地址**，调用该地址指向的函数（动态绑定）

#### 纯虚函数

**定义：**在基类中声明，但没有具体实现（用 `= 0` 标记）。

```cpp
virtual 返回类型 函数名(参数) = 0;
```

**特点：**

- 纯虚函数必须被派生类**重写**，如果派生类中没有重写全部纯虚函数，派生类依然是**抽象类**，创建对象时编译报错“纯虚拟函数没有强制替代项”

#### 抽象类

**定义：**包含**至少一个纯虚函数**的类称为抽象类

```cpp
class Shape { // 抽象类
public:
    virtual double area() const = 0;
    virtual ~Shape() = default; // 虚析构函数（推荐）
};
```

**特点：**

- 本身**不能实例化**，只能通过派生类实例化
- 通常用作**接口**，定义一组规范，**强制**派生类实现特定功能
- 可以包含普通成员函数和成员变量

```cpp
// 抽象类
class Animal {
public:
    virtual void speak() const = 0; // 纯虚函数
    virtual ~Animal() = default;    // 虚析构函数
};

// 派生类必须实现纯虚函数
class Dog : public Animal {
public:
    void speak() const {
        cout << "Woof!" << endl;
    }
};

class Cat : public Animal {
public:
    void speak() const {
        cout << "Meow!" << endl;
    }
};

int main() {
    Animal* animals[] = { new Dog(), new Cat() }; // 多态数组

    for (auto animal : animals) {
        animal->speak(); // 动态绑定到派生类方法
        delete animal;   // 正确调用派生类析构函数（虚析构）
    }

    return 0;
}
```

#### 纯虚析构函数

**定义：**纯虚析构函数是一种特殊的析构函数，它被声明为纯虚函数（=0），但**必须提供实现**。纯虚析构函数通常在抽象类中，确保派生类对象通过基类指针删除时能**正确调用析构函数链**；如果纯虚析构函数未提供实现，编译时链接器报错。

```cpp
class Base {
public:
    virtual ~Base() = 0; // 纯虚析构声明
};

// 纯虚析构函数必须提供实现
Base::~Base() {
    std::cout << "Base destructor called" << std::endl;
}

class Derived : public Base {
public:
    ~Derived() {
        std::cout << "Derived destructor called" << std::endl;
    }
};

int main() {
    Base* obj = new Derived();
    delete obj;
    return 0;
}
```

## 文件操作

程序运行时产生的数据属于临时数据，通过文件可以将数据持久化。文件分为两种：

1. 文本文件：文件以文本ASCII码的形式存储
2. 二进制文件：文件以二进制的形式存储

操作文件的三大类：

1. `ofstream`：仅写操作
2. `ifstream`：仅读操作
3. `fstream`：读写操作

### 文件打开模式

文件打开模式可以配合使用，用`|`操作符，如：`ios::binary | ios::out`

|  模式标志   |           描述           |
| :---------: | :----------------------: |
|   ios::in   |         读取模式         |
|  ios::out   |         写入模式         |
|  ios::app   |         追加模式         |
|  ios::ate   | 打开文件后定位到文件末尾 |
| ios::trunc  |  如果文件存在则清空内容  |
| ios::binary |        二进制模式        |

### 写文本文件

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
	ofstream ofs;
	ofs.open("test.txt", ios::out);
	ofs << "Hello World" << endl;
	ofs.close();
}
```

### 读文本文件

有四种方法可以读取文本文件

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
	ifstream ifs;
	ifs.open("test.txt", ios::in);
	if (!ifs.is_open()) {
		cout << "文件打开失败" << endl;
		return 0;
	}

	char buffer[1024] = { 0 };
	while (ifs >> buffer) {
		cout << buffer << endl; // 打印：Hello\nWorld，提取运算符(>>)读取文件内容时，会按照空白字符分割输入
	}

	while (ifs.getline(buffer, 1024)) {
		cout << buffer << endl; // 打印：Hello World
	}

	string buffer2;
	while (getline(ifs, buffer2)) {
		cout << buffer2 << endl; // 打印：Hello World
	}

	char c;
	while ((c = ifs.get()) != EOF) {
		cout << c;  // 打印：Hello World
	}

	ifs.close();
	return 0;
}
```

### 写二进制文件

打开方式指定为`ios::binary`，使用`ofstream& write(const char* buffer, int len)`函数写入二进制文件

```cpp
class Person {
public:
	char m_Name[64];
	int m_Age;
};

int main() {
	ofstream ofs;
	ofs.open("person.txt", ios::out | ios::binary);

	Person p = { "Alice", 18 };
	ofs.write((const char*)&p, sizeof(Person));
	ofs.close();
	return 0;
}
```

### 读二进制文件

打开方式指定为`ios::binary`，使用`istream& read(char* buffer, int len)`函数读取二进制文件

```cpp
class Person {
public:
	char m_Name[64];
	int m_Age;
};

int main() {
	ifstream ifs;
	ifs.open("person.txt", ios::in | ios::binary);
	if (!ifs.is_open()) {
		cout << "文件打开失败" << endl;
	}

	Person p;
	ifs.read((char*)&p, sizeof(Person));
	cout << "姓名: " << p.m_Name << endl; // 姓名: Alice
	cout << "年龄: " << p.m_Age << endl; // 年龄: 18

	return 0;
}
```

## 模板

C++ 模板是支持**泛型编程**的核心特性，允许编写与类型无关的代码

目的：避免重复代码，实现**与类型无关**的逻辑（如通用的排序、容器等）

原理：编译器在编译时根据具体类型**实例化**模板，生成对应的代码

### 函数模板

建立一个通用的函数，函数返回值类型和形参类型可以不具体指定，用一个**虚拟的类型**来代表

```cpp
template<typename/class T>
函数声明或定义
```

模板使用时可以**显式指定类型**，也可**自动推导类型**。

```cpp
template<typename T>
void mySwap(T& a, T& b) {
	T temp = a;
	a = b;
	b = temp;
}

int main() {
	int a = 10;
	int b = 20;
    
	mySwap<int>(a, b); // 显式指定类型
	mySwap(a, b); // 自动推导类型

	cout << "a = " << a << endl;
	cout << "b = " << b << endl;

	return 0;
}
```

所有模板参数必须可推导，如果模板参数无法从实参中推导，则需显式指定或通过默认值补充

```cpp
template <typename T>
void foo(T a, T b) {}

template <typename T>
void bar() {}

int main() {
	foo(3, 5);
	// foo(3, 5.0); 错误，T无法同时为int和double

	bar<int>();
	// bar(); 错误，无法推导T的具体类型

	return 0;
}
```

函数模板可以发生重载，分为**模板之间的重载**和**模板与普通函数的重载**。

- 模板之间的重载：多个函数模板同名，参数列表不同

```cpp
template <typename T>
void foo(T a) { std::cout << "单参数\n"; }

template <typename T>
void foo(T* a) { std::cout << "指针重载\n"; }

template <typename T, typename U>
void foo(T a, U b) { std::cout << "双参数\n"; }

int main() {
	int x = 10;

	foo(42); // 单参数
	foo(&x); // 指针重载
	foo(42, 3.14); // 双参数

	return 0;
}
```

- 模板与普通函数的重载：函数模板与普通函数同名

### 普通函数和函数模板

#### 区别

普通函数和函数模板的区别在于调用是能否发生**隐式类型转换**：

- 普通函数调用时可以发生隐式类型转换
- 函数模板调用时，如果利用自动类型推导，则不会发生隐式类型转换；如果利用显式指定类型，则可以发生隐式类型转换

```cpp
int myAdd01(int a, int b) {
	return a + b;
}

template<typename T>
T myAdd02(T a, T b) {
	return a + b;
}

int main() {
	int a = 10;
	char b = 'b';

	cout << myAdd01(a, b) << endl; // 打印：108
	cout << myAdd02<int>(a, b) << endl; // 打印108
	// cout << myAdd02(a, c) << endl; 错误：无法推导出T的具体类型

	return 0;
}
```

#### 调用规则

普通函数与函数模板**同名**时，编译器会根据一定规则决定调用哪一版本：

- **完全匹配时优先普通函数**：如果普通函数的参数类型**精确匹配**（不需要隐式类型转换），则优先调用普通函数
- **模板有更优匹配时优先模板**：如果普通函数的匹配需要隐式类型转换，而函数模板能产生更匹配的实例，则优先调用函数模板

```cpp
void foo(int a) { std::cout << "foo: 普通函数\n"; }

template <typename T>
void foo(T a) { std::cout << "foo: 函数模板\n"; }

void bar(double a) { std::cout << "bar: 普通函数\n"; }

template <typename T>
void bar(T a) { std::cout << "bar: 函数模板\n"; }

int main() {
	foo(420); // foo: 普通函数（普通函数能精确匹配）
	foo(3.1); // foo：函数模板（普通函数需要 double→int 的转换）
	
	bar(420); // bar: 函数模板（T=int 比 double 更匹配 int）
	bar(3.1); // bar: 普通函数

	return 0;
}
```

如果存在模板的全特化版本，优先级比普通模板高

```cpp
template <typename T>
void foo(T a) { std::cout << "普通函数模板\n"; }

template <>
void foo<int>(int a) { std::cout << "int特化模板\n"; }

int main() {
    foo(42); // int特化模板
}
```

模板解析的核心是”哪个更匹配就调哪个“，编译器始终选择当前上下文中**最匹配且代价最低**的版本

```tex
          [ 最精确匹配 ]
                ↑
普通函数（完全匹配） → 模板特化 → 通用模板
                ↑
          隐式转换代价更低者胜出
```

如果需要**强制调用**函数模板，可通过如下方式：

- 显式指定函数模板：显式告诉编译器调用函数模板版本
- 使用模板语法（空尖括号）：显式告诉编译器调用函数模板版本

```cpp
void foo(int a) { std::cout << "foo: 普通函数\n"; }

template <typename T>
void foo(T a) { std::cout << "foo: 函数模板\n"; }

int main() {
	foo<int>(42); // 强制调用模板版本（即使普通函数存在）
	foo<>(42); // 显式告知编译器使用模板推导

	return 0;
}
```

### 类模板

类模板允许在编写时处理多种数据类型，而不需要为每种类型重写代码

```cpp
template <typename T>
class Box {
private:
	T content;
public:
	void SetContent(const T& newContent) {
		content = newContent;
	}
	T getContent() const {
		return content;
	}
};

int main() {
	Box<int> intBox;
	intBox.SetContent(10);

	Box<string> strBox;
	strBox.SetContent("Hello");

	return;
}
```

类模板和函数模板有如下区别，最大的区别是**必须显式指定参数类型**。

|     特性     |   类模板 (Class Template)    | 函数模板 (Function Template) |
| :----------: | :--------------------------: | :--------------------------: |
|  **实例化**  |       必须显式指定类型       |       可以自动推导类型       |
|   **特化**   |      支持全特化和偏特化      |          支持全特化          |
| **默认参数** |       支持模板默认参数       |   C++11后支持默认模板参数    |
| **常见用途** | 容器类(如vector)、智能指针等 | 通用算法(如sort)、工具函数等 |

#### 类模板中的成员函数

类模板中的成员函数会**延迟实例化**：不会在类定义时立刻创建，而是在成员函数被实际使用时才实例化，这种机制也称为”按需实例化“或”惰性实例化“。实例化规则如下：

- 当实例化类模板时，只有被使用的成员函数才会实例化
- 未被使用的成员函数不会生成，意味着即使编译错误在生成时也不会报错

```cpp
template <typename T>
class Example {
public:
    void usedFunction() { /* 会被实例化 */ }
    void unusedFunction() { T::non_existent(); /* 不会被实例化，且错误代码不报错 */ }
};

int main() {
    Example<int> obj;
    obj.usedFunction();  // 只实例化usedFunction()
    //obj.unusedFunction();  // 如果取消注释，生成时会报错

    return 0;
}
```

#### 类模板对象作函数参数

类模板实例化出的对象向函数传递参数有三种传入方式：

1. 指定传入的类型：直接指定类模板的具体类型，函数接收**已实例化**的类模板对象，灵活性低，适用于明确需要某种具体类型（最常用）
2. 参数模板化：将函数定义为模板，通过参数推导**适配不同模板参数**的类实例，灵活性中，适配同一模板类的不同实例化
3. 整个类模板化：将**类模板本身作为模板参数**传递给函数，支持不同模板类的传递，灵活性高，适配不同类模板

```cpp
template <class T, class U>
class Example {
public:
    T m_T;
    U m_U;
};

// 1、指定传入类型
void func01(Example<string, int>& e) {}

// 2、参数模板化
template <class T, class U>
void func02(Example<T, U>& e) {}

// 3、整个类模板化
template<class T>
void func03(T& e) {}

int main() {
    Example<string, int> example01;
    func01(example01);

    Example<double, int> example02;
    func02(example02);

    Example<int, bool> example03;
    func03(example03);

    return 0;
}
```

#### 类模板的继承

类模板的继承符合以下几种情形和规则：

- **普通类继承类模板**：派生类可以继承一个**已实例化的类模板**（固定模板参数）
- **类模板继承类模板**：派生类本身也是模板，可以灵活传递基类的模板参数
- **多模板参数与默认参数**：基类和派生类可以有多个模板参数或使用默认参数
- **模板的模板参数继承**：模板参数本身可以是另一个类模板

```cpp
template <class T, class U>
class Base {
    T m_T;
    U m_U;
};

// 1.普通类继承类模板
class Derived01:public Base<int, bool> {

};

// 2.类模板继承类模板
template<class T, class U>
class Derived02:public Base<T, U> {

};

// 3.多模板参数与默认参数
template <class T>
class Derived03:public Base<T, int> {

};

// 4.模板的模板参数继承
template<template<class, class> class Container, class T, class U>
class Derived04 :public Container<T, U> {

};

int main() {
    Derived01 d1;
    Derived02<int, double> d2;
    Derived03<string> d3;
    Derived04<Base, int, bool> d4; // 继承 Base<int, double>

    return 0;
}
```

#### 类模板成员函数类外实现

板成员函数的类外实现需要以和类模板相同的参数列表开头

```cpp
template <class T, class U>
class Base {
public:
    Base(T t, U u); // 构造函数声明
    void Print(); // 成员函数声明

private:
    T m_T;
    U m_U;
};

// 构造函数实现
template <class T, class U>
Base<T, U>::Base(T t, U u) {
    this->m_T = t;
    this->m_U = u;
}

// 成员函数实现
template <class T, class U>
void Base<T, U>::Print() {
    cout << "m_T: " << this->m_T << endl;
    cout << "m_U" << this->m_U << endl;
}
```

#### 类模板份文件编写

类模板中的成员函数创建时机是在调用阶段，导致分文件编写时因为链接不到而**生成时报错**无法解析的外部符号，有两种解决方法：

- 调用函数的文件直接包含类的`.cpp`源文件
- 将函数声明和实现写在同一个文件中，更改后缀名为`.hpp`

#### 友元全局函数

如果友元函数**依赖类模板的模板参数**（即它本身是函数模板），则**定义时必须带模板参数**，否则生成时报错无法解析的外部符号

```cpp
template <class T, class U>
class TestClass
{
	// 1.全局函数作友元，类内声明和定义
	friend void PrintInsideClass(TestClass<T, U> t) {
		cout << "PrintInsideClass" << endl;
	}

	// 2.全局函数作友元，类内声明，类外定义
	template <class A, class B>
	friend void PrintOutsideClass(TestClass<A, B> t);

public:
	TestClass(T t, U u) : m_T(t), m_U(u) {}

private:
	T m_T;
	U m_U;
};

// 全局函数类外定义
template <class A, class B>
void PrintOutsideClass(TestClass<A, B> t) {
	cout << "PrintOutsideClass" << endl;
}
```

## STL

