# C++学习笔记

## C++入门

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

示例：

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

- 代码区：存放二进制代码**，由操作系统进行管理
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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

**示例：**

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

## 函数重载

## 类和对象

