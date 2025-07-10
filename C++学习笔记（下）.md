# C++学习笔记（下）

## 标准模板库

标准模板库(STL，Standard Template Library)是C++标准库的重要组成部分。STL 的设计遵循**泛型编程**思想，通过**模板**实现和类型无关的算法和数据结构，大大提高了代码的**复用性**和开发效率。提供了一系列通用的模板类和模板函数，主要包括以下三个核心组件：

- **容器（Containers）**：存储和管理数据的模板类
  - 序列容器：`vector`、`list`、`deque`、`array`（C++11）、`forward_list`（C++11）
  - 关联容器：`set`/`multiset`、`map`/`multimap`（基于红黑树，有序）
  - 无序关联容器：`unordered_set`/`unordered_map`（C++11，基于哈希表）
  - 容器适配器：`stack`、`queue`、`priority_queue`（基于其他容器封装）
- **算法（Algorithms）**：对**容器中的元素**进行操作，**算法通过迭代器和容器解耦**，不直接操作容器本身；包含约 100 种通用算法（如 `sort`、`find`、`copy`、`transform`）
- **迭代器（Iterators）**：作为**容器和算法之间的桥梁**，迭代器提供了统一的**访问容器元素**的方式；最常用的迭代器是双向迭代器和随机访问迭代器
  - 输入迭代器（只读）、输出迭代器（只写）
  - 前向迭代器（如`forward_list`）、双向迭代器（如`list`）、随机访问迭代器（如 `vector`）
- **仿函数（Functors）**和**匿名函数（Lambda）**：作为算法的策略（如自定义排序规则）
  - 仿函数（也称函数对象）是行为类似函数的对象，重载`operator()`的类
  - Lambda表达式为匿名函数对象
- **适配器（Adapters）**：对现有组件进行封装，提供不同的接口
  - 容器适配器：`stack`、`queue`、`priority_queue`
  - 迭代器适配器：`reverse_iterator`（反向迭代器）
  - 函数适配器：`bind`（C++11）、`function`（C++11）
- **分配器（Allocators）**：管理容器内存的分配与释放（默认使用 `allocator`），用户可以自定义分配器，但通常不需要直接使用，除非有特殊内存需求

### String容器

`string`是C++标准库中提供的字符串**类**，它封装了字符串的各种操作，比C风格的字符数组更安全、方便。

#### 构造函数

- `string()`：创建一个空字符串

- `string(const char* s)`：使用C风格字符串`s`初始化

- `string(const string& str)`：使用另一个`string`对象初始化（拷贝构造）

- `string(int n, char c)`：使用n个字符`c`构造

- `string(const char* s, int n)`：使用子序列构造，取前`n`个字符

- `string(const char* s, int pos, int len = npos)`或`string(const string& str, int pos, int len = npos)`：使用子序列构造，取从索引`pos`开始的`len`个字符，不传参数`len`时取到字符串末尾

```cpp
// 1. 创建空字符串
string str1;  // ""

// 2. 使用C风格字符串初始化
string str2("Hello");  // "Hello"

// 3. 拷贝构造
string str3(str2);  // "Hello"

// 4. 使用n个字符构造
string str4(5, 'A');  // "AAAAA"

// 5. 使用子序列构造（前n个字符）
string str5("Hello World", 5);  // "Hello"

// 6. 使用子序列构造（从pos开始取len个字符）
string str6("Programming", 3, 4);  // "gram"
string str7(str2, 1, 3);  // "ell"
```

#### 赋值操作

使用运算符`=`赋值：

- `string& operator=(const char* s)`：使用C风格字符串赋值给当前字符串

- `string& operator=(const string& str)`：把字符串`str`赋值给当前字符串

- `string& operator=(char c)`：把字符`c`赋值给当前字符串

使用方法`assign`赋值：

- `string& assign(const char* s)`：使用C风格字符串赋值给当前字符串

- `string& assign(const string& str)`：把字符串`str`赋值给当前字符串

- `string& assign(int n, char c)`：将n个字符`c`赋值给当前字符串

- `string& assign(const char* s, int n)`：把C风格字符串`s`的前`n`个字符赋值给当前字符串

- `string& assign(const char* s, int pos, int len = npos)`或`string& assign(const string& str, int pos, int len = npos)`：取从索引`pos`开始的`len`个字符赋值给当前字符串，不传参数`len`时取到字符串末尾

```cpp
string str;
// 1. 使用运算符=赋值
str = "Hello";
string str2;
str2 = str;
string str3;
str3 = 'H';

// 2. 使用assign方法赋值
str.assign("World");           // "World"
str.assign(str2);              // "Hello"
str.assign(5, 'X');            // "XXXXX"
str.assign("Hello World", 5);  // "Hello"
str.assign(str2, 1, 3);        // "ell"
str.assign("Hello", 1, 3);     // "ell"
```

#### 子串获取

子串获取主要通过`substr`方法实现：

- `string substr(int pos = 0, int n = npos) const`：获取从`pos`开始的`n`个字符构成的子串；不传则获取到末尾

```cpp
string str = "Hello World";

string sub1 = str.substr(6);  // "World"
string sub2 = str.substr(6, 3);  // "Wor"
```

#### 字符串拼接

使用运算符`+=`拼接：

- `string& operator+=(const char* s)`：拼接C风格字符串

- `string& operator+=(const char c)`：拼接单个字符`c`

- `string& operator+=(const string& str)`：拼接另一个字符串`str`

使用方法`append`拼接：

- `string& append(const char* s)`：拼接C风格字符串

- `string& append(const string& str)`：拼接另一个字符串`str`

- `string& append(const char* s, int n)`：拼接C风格字符串`s`的前`n`个字符

- `string& append(const char* s, int pos, int len = npos)`或`string& assign(const string& str, int pos, int len = npos)`：取从索引`pos`开始的`len`个字符拼接，不传参数`len`时取到字符串末尾

```cpp
string str;

// 1. 使用运算符+=拼接
str += "He";
str += 'l';
string str2("lo");
str += str2;

// 2. 使用append方法拼接
str.append("He");				// "HelloHe"
string str3("llo");
str.append(str3);				// "HelloHello"
str.append(" WWW", 2); 			// "HelloHello W"
str.append("Worlddd", 1, 4); 	// "HelloHello World"
string str4("??!??");
str.append(str4, 2, 1); 		// "HelloHello World!"
```

#### 字符串查找

正向查找用方法`find`：

- `int find(const string& str, int pos = 0) const`或`int find(const char* s, int pos = 0) const`：从`pos`开始，**向后**查找字符串`str`/`s`在给定字符串中的位置

反向查找用`rfind`：

- `int rfind(const string& str, int pos = npos) const`或`int rfind(const char* s, int pos = npos) const`：从`pos`开始，**向前**查找字符串`str`/`s`在给定字符串中的位置

正向查找任意匹配字符用`find_first_of()`：

- `int find_first_of(const string& str, int pos = 0) const`：查找任意匹配字符在字符串中的位置

反向查找任意匹配字符用`find_last_of()`：

- `int find_last_of(const string& str, int pos = npos) const`：查找任意匹配字符在字符串中的位置

查找任意不匹配字符用`find_first_not_of()`：

- `int find_first_not_of(const string& str, int pos = 0) const`：查找任意不匹配字符在字符串中的位置

```cpp
string str = "Hello World Hello";
int pos;

// 1. 正向查找替换
pos = str.find("Hello");    // 返回0（首次出现位置）
pos = str.find("World");    // 返回6
pos = str.find("hello");    // 返回-1（未找到）
pos = str.find("Hello", 1); // 从位置1开始找，返回12

// 2. 反向查找替换
pos = str.rfind("Hello");   // 返回12（最后一次出现位置）
pos = str.rfind("ll", 5);    // 返回2

// 3. 正向查找匹配任意字符
pos = str.find_first_of("aeiou");  // 返回1（'e'所在的位置）

// 4. 反向查找匹配任意字符
pos = str.find_last_of("aeiou"); // 返回15（最后一个'o'所在的位置）

// 5. 查找任意不匹配字符
pos = str.find_first_not_of("Helo "); // 返回6（第一个不匹配字符'W'所在的位置）
```

#### 字符串替换

字符串替换主要通过`replace`方法实现：

- `string& replace(int pos, int len, const string& str)`或`string& replace(int pos, int len, const char* s)`：从`pos`位置开始，将`len`长度的子串替换为`str`/`s`

- `string& replace(int pos, size_t len, const string& str, int subpos, int sublen)`：使用`str`的子串进行替换

- `string& replace(int pos, int len, int n, char c)`：用`n`个字符`c`替换

- `string& replace(iterator i1, iterator i2, const string& str)`：使用迭代器范围指定替换位置

- `string& replace(iterator i1, iterator i2, int n, char c)`：用`n`个字符`c`填充

```cpp
string str = "I like Java";

// 1. 替换子串
str.replace(7, 4, "C++");  // "I like C++"
str.replace(2, 4, "love");  // "I love C++"

// 2. 用子串替换子串
string repl = "Python/JavaScript";
str.replace(7, 3, repl, 7, 10);  // "I love JavaScript"

// 3. 用指定个数字符替换
str.replace(0, 1, 3, '*');  // "*** love JavaScript"

// 4. 迭代器范围指定替换
string::iterator it = str.begin() + 4;
str.replace(it, it+4, "hate");  // "*** hate JavaScript"

// 5. 迭代器范围指定填充
str.replace(str.end()-10, str.end(), 5, '!');  // "*** hate !!!!!"
```

#### 字符串插入

在字符串的指定位置插入内容主要用`insert`方法：

- `string& insert(int pos, const char* s)`：在`pos`位置插入C风格字符串

- `string& insert(int pos, const string& str)`：在`pos`位置插入字符串

- `string& insert(int pos, const char* s, int len)`：在`pos`位置插入C风格字符串的前`len`个字符

- `string& insert(int pos, const string& str, int pos2, int count = npos)`：在`pos`位置插入另一个字符串的子串

- `string& insert(int pos, int n, char c)`：在`pos`位置插入`n`个字符`c`

- `iterator insert(iterator pos, char c)`：在迭代器位置前插入字符`c`

- `void insert(iterator pos, int n, char c)`：在迭代器位置前插入`n`个字符`c`

```cpp
string str("HelloWorld");
// 1. 插入C风格字符串
str.insert(5, " "); // Hello World

// 2. 在指定位置插入字符串
string str2("Hello");
str.insert(6, str2); // Hello HelloWorld

// 3. 在指定位置插入指定个数的C风格字符串
str.insert(11, "***", 1); // Hello Hello*World

// 4. 在指定位置插入另一个字符串的子串
string str3("Say Hi");
str.insert(0, str3, 0, 4); // Say Hello Hello*World

// 5. 在指定位置插入指定个数的字符
str.insert(15, 2, '*'); // Say Hello Hello***World

// 6. 在迭代器位置前插入字符
str = "Warning";
str.insert(str.begin(), '!'); // !Warning

// 7. 在迭代器位置前插入指定个数的字符
str.insert(str.end(), 2, '?'); // !Warning??
```

#### 字符串删除

字符串删除通过`erase`方法实现：

- `string& erase(int pos = 0, int n = npos)`：删除从`pos`开始的`n`个字符，不指定则删除到末尾

- `iterator erase(iterator pos)`：删除迭代器指向的字符

- `iterator erase(iterator first, iterator last)`：删除迭代器范围[first, last)的字符


```cpp
string str("Hello, World!");
// 1. 删除指定位置指定个数字符
str.erase(7, 5); // Hello, !

// 2. 删除迭代器指向字符
str = "Programming";
auto it = str.erase(str.begin() + 3); // Proramming

// 3. 删除迭代器范围的字符
str = "This is an example";
it = str.erase(str.begin() + 5, str.begin() + 11); // This example
```

#### 字符访问

在C++中，访问字符串中的单个字符主要有两种方式，使用下标运算符`[]`和使用`at()`成员函数

- `char& operator[] (int pos)`或`const char& operator[] (int pos) const`：直接通过索引访问，不进行边界检查

  ```cpp
  string str = "Hello";
  str[0] = 'h';
  ```

- `char& at(int pos)`或`const char& at(int pos) const`：进行边界检查，如果越界则抛异常

  ```cpp
  string str = "World";
  str.at(0) = 'w';
  ```

#### 字符串比较

`string`提供了`>`、`<`、`==`、`>=`、`<=`、`!=`等比较运算符，还提供了`compare()`函数，支持多参数处理，支持用索引值和长度截取子串进行比较

- `int compare(const string& str) const`或`int compare(const char* s) const`：完整字符串比较

- `int compare(int pos, int len, const string& str) const`或`int compare(int pos, int len, const char* s) const`：子串比较

- `int compare(int pos, int len, const string& str, int subpos, int sublen) const`或`int compare(int pos, int len, char* s, int subpos, int sublen) const`：子串和子串比较

- `int compare(int pos, int len, const char* s, int = npos) const`：与C风格字符串子串比较


```cpp
string s = "Hello World";
// 1.完整字符串比较
s.compare("Hello World");  // 返回0

// 2.子串比较
s.compare(6, 5, "World"); // 比较"World"和"World"，返回0

// 3.子串和子串比较
s.compare(0, 5, "Hello Earth", 0, 5); // 比较"Hello"和"Hello"，返回0

// 4.与C风格字符串比较
s.compare(0, 11, "Hello!", 5); // 返回>0（"Hello World" > "Hello"）
```

### vector容器

vector是C++标准模板库中最常用的容器之一，提供了**动态数组**的功能，能够自动管理内存并在需要时动态调整大小（并不是在原有空间后续接新空间，而是找一块更大的内存空间将原数据拷贝到新空间，并释放原有空间）

#### 构造函数

- `vector()`：默认构造函数，构造空容器
- `vector(int n)`：用`n`个默认值构造队列
- `vector(int n, const T& value = T())`：用`n`个`value`构造容器
- `vector(InputIterator first, InputIterator last)`：用其他容器的范围构造新容器
- `vector(const vector& x)`：拷贝构造函数
- `vector(vector&& x) `：移动拷贝构造函数(C++11)
- `vector(initializer_list<T> il)`：初始化列表构造函数(C++11)

```cpp
// 1. 默认构造函数：创建空vector
vector<int> v1;

// 2. 指定大小和初始值：创建包含n个元素的vector，每个元素初始化为val
vector<int> v2(5);       // 5个0
vector<int> v3(5, 10);   // 5个10

// 3. 范围构造函数：用迭代器范围[first,last)初始化
vector<int> v4(v3.begin(), v3.end());

// 4. 拷贝构造函数：用另一个vector初始化
vector<int> v5(v4);

// 5. 列表初始化 (C++11)
vector<int> v6 = {1, 2, 3, 4, 5};

// 6. 移动构造函数 (C++11)
vector<int> v7(move(v6)); // v6现在为空
```

#### 赋值操作

可以用`=`运算符进行赋值：

- `vector& operator=(const vector& x)`：拷贝赋值
- `vector& operator=(vector&& x)`：移动拷贝赋值(C++11)
- `vector& operator=(initializer_list<T> il)`：初始化列表赋值(C++11)
- `void assign(InputIterator first, InputIterator last)`：用另一个容器的范围赋值

也可以用assign方法赋值：

- `void assign(int n, const T& value)`：用`n`个`value`填充容器
- `void assign(initializer_list<T> il)`：初始化列表赋值(C++11)

```cpp
vector<int> v1 = {1, 2, 3};
vector<int> v2;

// 1. 拷贝赋值
v2 = v1;

// 2. 移动赋值 (C++11)
v2 = move(v1); // v1现在为空

// 3. 范围赋值：用迭代器范围[first,last)赋值
vector<int> v3;
v3.assign(v2.begin(), v2.end());

// 4. 填充赋值：用n个val赋值
v3.assign(5, 10); // 5个10

// 5. 列表赋值 (C++11)
v3 = {1, 2, 3, 4, 5};
```

#### 容量和大小

`vector`容器提供了多种查询和修改容量的方法：

- `int size() const`：返回元素数量
- `int max_size() const`：返回最大可能元素数量的理论值
- `int capacity() const`：返回当前分配的存储容量
- `bool empty() const`：检查是否为空
- `void resize(int newsize)`：调整容器大小，不足的元素用默认值补齐
- `void resize(int newsize, const T& value)`：调整容器大小，不足的元素用`value`补齐
- `void reserve(int n)`：预留存储空间，避免频繁重新分配
- `void shrink_to_fit()`：减少容量以适应大小(C++11)

```cpp
vector<int> v = { 1, 2, 3, 4, 5 };

// 1. 当前元素数量
cout << v.size() <<endl;      // 输出5

// 2. 最大可能元素数量
cout << v.max_size() << endl;  // 取决于系统和实现

// 3. 当前分配的存储容量
cout << v.capacity() << endl;  // ≥5

// 4. 检查是否为空
cout << v.empty() << endl;     // 0 (false)

// 5. 调整大小
v.resize(10);         // 大小变为10，新增元素初始化为0
v.resize(15, 100);    // 大小变为15，新增元素初始化为100
v.resize(3);          // 大小变为3，多余元素被删除

// 6. 预留空间
v.reserve(100);       
cout << v.capacity() << endl;  // 100
```

#### 元素插入

- `void push_back(const T& value)`：在尾部插入元素
- `void push_back(T&& value)`：在尾部移动插入元素(C++11)
- `iterator insert(const_iterator position, const T& value)`：在迭代器指定位置插入元素
- `iterator insert(const_iterator position, T&& value)`：在迭代器指定位置移动插入元素(C++11)
- `iterator insert(const_iterator position, int n, const T& value)`：在迭代器指定位置插入n个元素value
- `iterator insert(const_iterator position, InputIterator first, InputIterator last)`：在迭代器指定位置插入另一个迭代器范围
- `iterator insert(const_iterator position, initializer_list<T> il)`：在迭代器指定位置插入初始化列表(C++11)

```cpp
vector<int> v = {1, 2};

// 1. 尾部添加元素
v.push_back(3);       // v: {1,2,3}

// 2. 在指定位置插入元素
v.insert(v.begin(), 0);       // v: {0,1,2,3}
v.insert(v.begin()+2, 5);     // v: {0,1,5,2,3}
v.insert(v.end(), 3, 10);     // v: {0,1,5,2,3,10,10,10}

// 3. 插入范围
vector<int> v2 = {7,8,9};
v.insert(v.begin()+1, v2.begin(), v2.end()); // v: {0,7,8,9,1,5,2,3,10,10,10}
```

#### 元素删除

- `void pop_back()`：在尾部删除元素

- `iterator erase(const_iterator position)`：删除迭代器指定位置元素

  `iterator erase(const_iterator first, const_iterator last)`：删除迭代器指定位置

- `void clear()`：清空容器

```cpp
vector<int> v = {1, 2, 3, 4, 5, 6};

// 1. 尾部删除元素
v.pop_back();         // v: {1,2,3,4,5}

// 2. 删除指定位置元素
v.erase(v.begin());           		// v: {2,3,4,5}
v.erase(v.begin()+1, v.begin()+3); 	// v: {2,5}

// 3. 清空vector
v.clear();            // v: {}
```

#### 数据访问

用下标运算符`[]`访问数据：

- `reference operator[](int n)`或`const_reference operator[](int n) const`：通过下标访问元素，不检查边界

用`at`方法访问：

- `reference at(int n)`或`const_reference at(int n) const`：访问指定索引的元素，检查边界

用`front`方法和`end`方法访问首尾元素：

- `reference front()`或`const_reference front() const`：访问第一个元素
- `reference back()`或`const_reference back() const`：访问最后一个元素

```cpp
vector<int> v = {1, 2, 3, 4, 5};

// 1. 下标访问 (不检查边界)
cout << v[2] << endl;        // 输出3
v[1] = 10;           		 // v: {1,10,3,4,5}

// 2. at()访问 (越界抛异常)
cout << v.at(3) << endl;     // 输出4

// 3. 访问首尾元素
cout << v.front() << endl;   // 输出1
cout << v.back() << endl;    // 输出5

// 4. 获取底层数组指针
int* p = v.data();   		 // 指向第一个元素的指针
cout << *p << endl;          // 输出1
```

#### 互换容器

用`swap`方法交换两个vector的内容：

- `void swap(vector& other)`：交换容器内容(C++11)

```cpp
vector<int> v1 = { 1, 2, 3 };
vector<int> v2 = { 4, 5, 6, 7 };

cout << "交换前:" << endl;
cout << "v1: "; for (int i : v1) cout << i << " "; cout << endl;
cout << "v2: "; for (int i : v2) cout << i << " "; cout << endl;

v1.swap(v2);  // 交换v1和v2的内容

cout << "n交换后:" << endl;
cout << "v1: "; for (int i : v1) cout << i << " "; cout << endl;
cout << "v2: "; for (int i : v2) cout << i << " "; cout << endl;
```

### deque容器

`deque`（双端队列）是C++标准模板库中的一个重要容器，通过动态分配固定大小的块和维护一个中央索引表实现（内存块内连续、块间不连续），支持在**两端**高效地插入和删除元素

#### 构造函数

- `deque()`：默认构造函数，构造空队列
- `deque(int n)`：用`n`个默认值构造队列
- `deque(int n, const T& value = T())`：用`n`个`value`构造
- `deque(InputIterator first, InputIterator last)`：用其他容器的范围构造新容器
- `deque(const deque& x)`：拷贝构造函数
- `deque(const deque&& x)`：移动拷贝构造函数(C++11)
- `deque(initializer_list<T> il)`：初始化列表构造函数(C++11)

```cpp
// 1. 默认构造
deque<int> dq1;

// 2. 填充构造
deque<int> dq2(5);         // 5个0
deque<int> dq3(5, 10);     // 5个10

// 3. 范围构造
int arr[] = { 1, 2, 3, 4, 5 };
deque<int> dq4(arr, arr + 3);  // 1,2,3

// 4. 拷贝构造
deque<int> dq5(dq4);       // 1,2,3

// 5. 初始化列表构造
deque<int> dq7 = { 6, 7, 8, 9 };

// 6. 移动拷贝构造
deque<int> dq6(move(dq5)); // dq5现在为空
```

#### 赋值操作

可以用运算符`=`进行赋值：

- `deque& operator=(const deque& other)`：拷贝赋值
- `deque& operator=(deque&& other)`：移动赋值(C++11)
- `deque& operator=(initializer_list<T> ilist)`：初始化列表赋值

```cpp
// 1. 拷贝赋值
deque<int> dq1 = {1, 2, 3};
deque<int> dq2;
dq2 = dq1;  // 拷贝赋值

// 2. 移动赋值
deque<int> dq3;
dq3 = move(dq1);  // dq1现在为空

// 3. 初始化列表赋值
deque<int> dq4;
dq4 = {4, 5, 6, 7};
```

也可以用`assign`方法进行赋值：

- `void assign(int n, const T& value)`：用`n`个`value`构造
- `void assign(InputIt first, InputIt last)`：把其他容器的范围赋值给容器
- `void assign(initializer_list<T> ilist)`：初始化列表赋值函数(C++11)

```cpp
deque<int> dq;
    
// 1. 填充赋值
dq.assign(5, 10);  // 5个10
for (auto i : dq) cout << i << " ";  // 输出: 10 10 10 10 10

// 2. 范围赋值
int arr[] = {1, 3, 5, 7, 9};
dq.assign(arr, arr + 3);
for (auto i : dq) cout << i << " ";  // 输出: 1 3 5

// 3. 初始化列表赋值
dq.assign({2, 4, 6, 8});
for (auto i : dq) cout << i << " ";  // 输出: 2 4 6 8
```

#### 容量和大小

- `int size() const`：返回容器中当前元素的数量
- `bool empty() const`：检查容器是否为空
- `int max_size() const`：返回可容纳的最大元素数量的理论值
- `void resize(int count)`：改变容器中元素的数量
- `void resize(int count, const T& value)`：改变容器中元素的数量，不足的元素用`value`填充

```cpp
deque<int> dq = { 1, 2, 3, 4, 5 };

// 1. size()
cout << dq.size() << endl;  // 输出: 5

// 2. empty()
cout << dq.empty() << endl;  // 输出: false

// 3. max_size()
cout << dq.max_size() << endl;  // 输出: 一个很大的数

// 4. resize() - 扩大
dq.resize(7);
for (auto i : dq) cout << i << " ";  // 输出: 1 2 3 4 5 0 0

// 5. resize() - 缩小
dq.resize(3);
for (auto i : dq) cout << i << " ";  // 输出: 1 2 3

// 6. resize() - 带默认值
dq.resize(5, 10);
for (auto i : dq) cout << i << " ";  // 输出: 1 2 3 10 10
```

#### 元素插入

- `void push_back(const T& value)`：在末尾插入一个元素
- `void push_back(T&& value)`：在末尾移动插入一个元素(C++11)
- `void emplace_back(Args&&... args)`：在末尾构造一个元素(C++11)
- `void push_front(const T& value)`：在头部插入一个元素
- `void push_front(T&& value)`：在头部移动插入一个元素(C++11)
- `void emplace_front(Args&&... args)`：在头部构造一个元素(C++11)
- `iterator insert(const_iterator pos, const T& value)`：在迭代器的`pos`位置插入一个元素
- `iterator insert(const_iterator pos, T&& value)`：在迭代器的`pos`位置移动插入一个元素(C++11)
- `iterator insert(const_iterator pos, int count, const T& value)`：在迭代器的`pos`位置插入`n`个`value`
- `iterator insert(const_iterator pos, InputIt first, InputIt last)`：在迭代器的`pos`位置插入多个元素
- `iterator insert(const_iterator pos, initializer_list<T> ilist)`：在迭代器的`pos`位置插入(C++11)
- `iterator emplace(const_iterator pos, Args&&... args)`：在迭代器的`pos`位置构造一个元素(C++11)

```cpp
// 1. 尾部插入
dq.push_back(5);       // {2, 3, 4, 5}
dq.emplace_back(6);    // {2, 3, 4, 5, 6}

// 2. 头部插入
dq.push_front(1);      // {1, 2, 3, 4, 5, 6}
dq.emplace_front(0);   // {0, 1, 2, 3, 4, 5, 6}

// 3. 任意位置插入
auto it = dq.begin() + 3;
dq.insert(it, 99);     // {0, 1, 2, 99, 3, 4, 5, 6}

// 插入多个相同元素
dq.insert(dq.end(), 3, 7);  // {0, 1, 2, 99, 3, 4, 5, 6, 7, 7, 7}

// 插入范围
int arr[] = { 10, 11, 12 };
dq.insert(dq.begin() + 5, arr, arr + 3);  // {0, 1, 2, 99, 3, 10, 11, 12, 4, 5, 6, 7, 7, 7}

// emplace构造
dq.emplace(dq.begin() + 2, 55);  // {0, 1, 55, 2, 99, 3, 10, 11, 12, 4, 5, 6, 7, 7, 7}
```

#### 元素删除

- `void pop_back()`：删除末尾的元素
- `void pop_front()`：删除开头的元素
- `iterator erase(const_iterator pos)`：删除指定位置的元素
- `iterator erase(const_iterator first, const_iterator last)`：删除指定迭代器范围的元素
- `void clear()`：清空容器

```cpp
deque<int> dq = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };

// 1. 尾部删除
dq.pop_back();
for (auto i : dq) cout << i << " ";  // 0 1 2 3 4 5 6 7 8

// 2. 头部删除
dq.pop_front();
for (auto i : dq) cout << i << " ";  // 1 2 3 4 5 6 7 8

// 3. 删除单个元素
auto it = dq.begin() + 3;
dq.erase(it);
for (auto i : dq) cout << i << " ";  // 1 2 3 5 6 7 8

// 4. 删除范围元素
dq.erase(dq.begin() + 1, dq.begin() + 4); // 删除2,3,5
for (auto i : dq) cout << i << " ";  // 1 6 7 8

// 5. 清空整个deque
dq.clear();
```

#### 数据访问

使用下标运算符`[]`访问元素：

- `reference operator[](int n)`或`const_reference operator[](int n) const`：通过下标访问元素，不检查边界

用`at`方法访问：

- `reference at(int n)`或`const_reference at(int n) const`：访问指定索引的元素，检查边界

用`front`方法和`end`方法访问首尾元素：

- `reference front()`或`const_reference front() const`：访问第一个元素
- `reference back()`或`const_reference back() const`：访问最后一个元素

```cpp
deque<int> dq = { 1, 2, 3, 4, 5 };

// 1. 下标访问 (不检查边界)
cout << dq[2] << endl;        // 输出3
dq[1] = 10;           		  // dq: {1,10,3,4,5}

// 2. at()访问 (越界抛异常)
cout << dq.at(3) << endl;     // 输出4

// 3. 访问首尾元素
cout << dq.front() << endl;   // 输出1
cout << dq.back() << endl;    // 输出5
```

### list容器

`list`是C++标准模板库中的**双向循环链表**，由一系列**节点**构成，支持高效地双向遍历和任意位置插入删除。具有如下特征：

- **双向链表**：每个节点包含指向前驱节点和后继结点的指针
- **循环结构**：尾结点的后继结点是头结点，头结点的前驱节点是尾节点
- **非连续内存**：元素分散存储在内存中
- **高效插入删除**：在任何位置插入删除都是O(1)事件复杂度
- **低效随机访问**：不支持快速随机访问，访问元素需要遍历

#### 构造函数

- `list()`：默认构造空链表
- `explicit list(int n)`：构造包含`n`个默认初始化元素的链表
- `list(int n, const T& value)`：构造包含`n`个`value`的链表
- `list(InputIt first, InputIt last)`：用迭代器范围构造
- `list(const list& other)`：拷贝构造
- `list(list&& other)`：移动构造(C++11)
- `list(initializer_list<T> init)`：初始化列表构造(C++11)

```cpp
list<int> l1; // 空链表
list<int> l2(5); // 5个0
list<int> l3(3, 10); // [10,10,10]
vector<int> v {1,2,3};
list<int> l4(v.begin(), v.end()); // [1,2,3]
list<int> l5 {7,8,9}; // [7,8,9]
```

#### 元素访问

- `reference front()` 或 `const_reference front() const`：访问首元素
- `reference back()` 或`const_reference back() const`：访问尾元素

```cpp
list<int> l {10,20,30};
cout << l.front() << endl; // 10
cout << l.back() << endl;  // 30
```

#### 迭代器

- `iterator begin()`或`const_iterator begin() const`：前向迭代器的首元素位置
- `iterator end()` 或`const_iterator end() const`：前向迭代器的尾元素位置
- `reverse_iterator rbegin()` 或`const_reverse_iterator rbegin() const`：反向迭代器的首元素位置
- `reverse_iterator rend()`或`const_reverse_iterator rend() const`：反向迭代器的尾元素位置

```cpp
list<int> l {1,2,3};
for(auto it = l.begin(); it != l.end(); ++it) {
    cout << *it << " "; // 1 2 3
}
cout << endl;
for(auto rit = l.rbegin(); rit != l.rend(); ++rit) {
    cout << *rit << " "; // 3 2 1
}
```

#### 容量和大小

- `bool empty() const`：检查是否为空
- `int size() const`：返回元素数量
- `int max_size() const`：返回可容纳的最大元素数量的理论值
- `void resize(int newsize)`：调整容器大小，不足的元素用默认值补齐
- `void resize(int newsize, const T& value)`：调整容器大小，不足的元素用`value`补齐

```cpp
list<int> nums;

// 1. 检查是否为空
if (nums.empty()) {
    cout << "链表为空" << endl;  // 输出：链表为空
}

// 2. 获得元素个数
nums.assign(3, 100);
cout << "当前大小: " << nums.size() << endl;  // 输出：当前大小: 3

// 3. 最大可能大小（理论值）
cout << "最大容量: " << nums.max_size() << endl;  // 输出一个很大的数值

// 4. 调整大小
nums.resize(5);      // [100, 100, 100, 0, 0]
nums.resize(2);      // [100, 100]
nums.resize(4, 99);  // [100, 100, 99, 99]
```

#### 修改操作

- `void push_front(const T& value)`：头部插入
- `void pop_front()`：头部删除
- `void push_back(const T& value)`：尾部插入
- `void pop_back()`：尾部删除
- `iterator insert(const_iterator pos, const T& value)`：在`pos`前插入
- `iterator erase(const_iterator pos)`：删除`pos`处元素
- `void clear()`：清空链表

```cpp
list<int> l;
l.push_back(10);  // [10]
l.push_front(5);  // [5,10]
l.insert(++l.begin(), 7); // [5,7,10]
l.erase(l.begin()); // [7,10]
l.resize(4); // [7,10,0,0]
l.clear(); //[]
```

- `void swap(list& other)`：交换两个链表的内容

```cpp
list<int> list1 {1, 3, 5};
list<int> list2 {2, 4, 6};

list1.swap(list2); //list1: [2, 4, 6] list2: [1, 3, 5]
```

#### 特殊操作

- `void remove(const T& value)`：删除所有等于value的元素
- `void splice(const_iterator pos, list& other)`：移动`other`的所有元素到`pos`前
- `void unique()`：删除连续重复元素
- `void sort()`：排序
- `void reverse()`：反转链表

```cpp
list<int> l1 {1,2,3}, l2 {4,5};
l1.splice(l1.end(), l2); // l1:[1,2,3,4,5], l2:[]
l1.remove(3); // [1,2,4,5]
l1.sort(); // [1,2,4,5]
l1.reverse(); // [5,4,2,1]
```

### stack容器

`stack`是C++标准模板库中的一个**容器适配器**，提供了**先进后出(FILO, First In Last Out)**的数据结构功能，底层实现可以是`vector`、`deque`（默认）或`list`

#### 构造函数

- `stack()`：默认构造函数
- `explicit stack(const Container& cont)`：使用已有容器构造
- `explicit stack(Container&& cont)`：使用已有容器移动构造(C++11)
- `stack(const stack& other)`：拷贝构造
- `stack(stack&& other)`：移动拷贝构造(C++11)

```cpp
stack<int> s1; // 默认构造空栈
deque<int> d {1, 2, 3};
stack<int> s2(d); // 使用deque构造栈
stack<int> s3(s2); // 拷贝构造
```

#### 元素访问

- `reference top()`或`const_reference top() const`：访问栈顶元素

```cpp
stack<int> s;
s.push(10);
s.push(20);
cout << s.top(); // 输出20
```

#### 容量操作

- `int size() const`：返回栈中元素数量
- `bool empty() const`：检查栈是否为空

```cpp
stack<int> s;
if (s.empty()) {
    cout << "Stack is empty" << endl; // 输出Stack is empty
}

s.push(1);
s.push(2);
cout << s.size() << endl; // 输出2
```

#### 修改操作

- `void push(const T& value)`：将元素压入栈顶
- `void pop()`：移除栈顶元素
- `void swap(stack& other)`：交换两个栈的内容

```cpp
stack<int> s1;
s1.push(10); // 压入10
s1.push(20); // 压入20

stack<int> s2;
s2.push(30);
s2.push(40);
s2.pop(); // 移除栈顶元素40

s1.swap(s2); // 现在s1包含30，s2包含10和20
```

### queue容器

`queue`是C++标准模板库中的一个**容器适配器**，提供了**先进先出(FIFO, First In First Out)**的数据结构功能，底层可以是`deque`（默认）或`list`

#### 构造函数

- `queue()`：默认构造函数
- `explicit queue(const Container& cont)`：使用已有容器构造
- `explicit queue(Container&& cont)`：使用已有容器移动构造(C++)
- `queue(const queue& other)`：拷贝构造
- `queue(queue&& other)`：移动拷贝构造

```C++
queue<int> q1; // 默认构造空队列
deque<int> d {1, 2, 3};
queue<int> q2(d); // 使用deque构造队列
queue<int> q3(q2); // 拷贝构造
```

#### 容量和大小

- `int size() const`：返回队列中元素数量
- `bool empty() const`：检查队列是否为空

```cpp
queue<int> q;
if (q.empty()) {
    cout << "Queue is empty"; // 输出Queue is empty
}

queue<int> q;
q.push(1);
q.push(2);
cout << q.size() << endl; // 输出2
```

#### 元素访问

- `reference front()`或`const_reference front() const`：访问队首元素
- `reference back()`或`const_reference back() const`：访问队尾元素

```cpp
queue<int> q;
q.push(10);
q.push(20);
cout << q.front() << endl; // 输出10
cout << q.back() << endl;  // 输出20
```

#### 修改操作

- `void push(const T& value)`：将元素插入队尾
- `void pop()`：移除队首元素
- `void swap(queue& other)`：交换两个队列的内容

```cpp
queue<int> q1;
q1.push(10); // 压入10
q1.push(20); // 压入20

queue<int> q2;
q2.push(30);
q2.push(40);
q2.pop(); // 移除队首元素30

q1.swap(q2); // 现在q1包含30，q2包含10和20
```

### set/multiset容器

`set`是C++标准模板库中的关联容器，基于**红黑树**实现，具有以下特征：

- **唯一键**：每个元素必须唯一
- **自动排序**：元素总是按照特定排序准则自动排序
- **高效查找**：基于红黑树实现，查找时间复杂度为O(log n)
- **不可修改元素**：元素的值不能被直接修改，只能删除后重新插入

`multise`t的特性和`set`类似，除了：

- **允许重复键**：可以包含多个值相同的元素

#### 构造函数

- `set()`：默认构造函数
- `explicit set(const Compare& comp)`：指定比较函数的构造函数
- `set(InputIterator first, InputIterator last)`：用迭代器范围构造函数
- `set(InputIterator first, InputIterator last, const Compare& comp)`：指定比较函数的迭代器范围构造函数
- `set(initializer_list<T> init)`：初始化列表构造函数(C++11)
- `set(const set& other)`：拷贝构造函数
- `set(set&& other)`：移动拷贝构造函数(C++11)

```cpp
bool myCompare(int a, int b) {
    return a > b; // 降序排序
}

// 1. 默认构造
set<int> s1;

// 2. 指定比较函数
set<int, bool(*)(int, int)> s2(myCompare);

// 3. 迭代器范围构造
vector<int> v = {3,1,4,2};
set<int> s3(v.begin(), v.end());

// 4. 初始化列表构造
set<int> s4 = {5,2,8,3};

// 5. 拷贝构造
set<int> s5(s4);
```

#### 容量和大小

- `bool empty() const`：判断是否为空
- `int size() const`：返回元素个数
- `int max_size() const`：返回最大可能元素数量的理论值

```cpp
set<int> nums = { 5, 2, 8, 1 };

// empty() 检查
if (!nums.empty()) {
    cout << "元素数量: " << nums.size() << endl;  // 输出: 元素数量: 4
}

// max_size() 示例
cout << "理论最大容量: " << nums.max_size() << endl;  // 输出一个很大的数值
```

#### 元素访问

- `iterator find(const T& value)`：查找值为`value`的元素
- `int count(const T& value) const`：返回值为`value`的元素个数
- `iterator lower_bound(const T& value)`：返回第一个不小于`value`的元素
- `iterator upper_bound(const T& value)`：返回第一个大于`value`的元素
- `pair<iterator,iterator> equal_range(const T& value)`：返回等于`value`的范围

```cpp
set<string> words = { "apple", "banana", "cherry" };

// 1. find() 查找元素
auto it = words.find("banana");
if (it != words.end()) {
    cout << "找到: " << *it << endl;  // 输出: 找到: banana
}

// 2. count() 统计 (set只会返回0或1)
cout << "apple出现次数: " << words.count("apple") << endl;  // 输出: 1

// 3. lower_bound()/upper_bound()
set<int> nums = { 10, 20, 30, 40, 50 };
auto lb = nums.lower_bound(25);  // 第一个 >=25 的元素
auto ub = nums.upper_bound(35);  // 第一个 <=35 的元素
for (auto i = lb; i != ub; ++i) {
    cout << *i << " ";  // 输出: 30
}
cout << endl;

// 4. equal_range()查找相同元素的范围
multiset<int> mnums = { 1, 2, 2, 2, 3 };
auto range = mnums.equal_range(2);
for (auto i = range.first; i != range.second; ++i) {
    cout << *i << " ";  // 输出: 2 2 2
}
```

#### 元素修改

- `pair<iterator,bool> insert(const T& value)`：插入元素，返回`pair`
- `iterator insert(iterator hint, const T& value)`：带提示插入（插入提示是给容器的一个建议位置，告诉容器“新元素应该插入在这个位置附近”，不是一个强制要求，主要用于性能优化）
- `void erase(iterator pos)`：删除`pos`位置的元素
- `void erase(InputIterator first, InputIterator last)`：删除迭代器范围内的元素
- `int erase(const T& value)`：删除所有值为`value`的元素，返回删除元素个数
- `void swap(set& other)`：交换两个容器
- `void clear()`：清空容器

```cpp
set<int> nums;

// 1. insert()插入
auto ret = nums.insert(10);
if (ret.second) {
    cout << "插入成功: " << *ret.first << endl;
}

// 2. 带提示插入
auto hint = nums.begin();
nums.insert(hint, 100);  // 快速插入提示

// 3. erase()删除
nums.erase(5);  // 通过值删除
auto it = nums.find(10);
if (it != nums.end()) {
    nums.erase(it);  // 通过迭代器删除
}

// 4. multiset的erase()删除
multiset<int> mnums = { 1, 1, 2, 2, 2, 3 };
int erased = mnums.erase(2);  // 删除所有2
cout << "\n删除了 " << erased << " 个2" << endl;  // 输出: 删除了 3 个2

// 5. swap()交换两个集合
set<int> new_nums;
nums.swap(new_nums);

// 6. clear()清空
mnums.clear();
cout << "清空后大小: " << mnums.size() << endl;  // 输出: 0
```

### map/multimap容器

`map`和`multimap`是C++标准模板库中的关联容器，基于**红黑树**实现，用于储存键值对，具有以下特征：

- **唯一键**：每个键只能出现一次
- **自动排序**：元素总是按照键的特定排序准则自动排序
- **高效查找**：基于红黑树实现，查找时间复杂度为O(log n)
- **键不可修改**：键的值不能被直接修改，只能删除后重新插入

`multimap`的特性和`map`类似，除了：

- **允许重复键**：可以包含多个键相同的元素
- **没有`operator[]`和`at()`**：因为键不唯一，无法直接通过键访问值

#### 构造函数

- `map()`：默认构造函数
- `explicit map(const Compare& comp)`：指定比较函数的构造函数
- `map(InputIterator first, InputIterator last)`：用迭代器范围构造函数
- `map(InputIterator first, InputIterator last, const Compare& comp)`：指定比较函数的迭代器范围构造函数
- `map(initializer_list<pair<const Key, T>> init)`：初始化列表构造函数(C++11)
- `map(const map& other)`：拷贝构造函数
- `map(map&& other)`：移动拷贝构造函数(C++11)

```cpp
bool myCompare(const string& a, const string& b) {
    return a.length() < b.length();
}

// 1. 默认构造
map<string, int> m1;

// 2. 指定比较函数
map<string, int, bool(*)(const string&, const string&)> m2(myCompare); // 按键长度排序

// 3. 迭代器范围构造
vector<pair<string, int>> v = { {"apple", 5}, {"banana", 3} };
map<string, int> m3(v.begin(), v.end());

// 4. 初始化列表构造
map<string, int> m4 = { {"apple", 5}, {"banana", 3} };

// 5. 拷贝构造
map<string, int> m5(m4);
```

#### 容量和大小

- `bool empty() const`：判断是否为空
- `int size() const`：返回元素个数
- `int max_size() const`：返回最大可能元素数量的理论值

```cpp
map<string, int> fruits = {{"apple", 5}, {"banana", 3}};

if (!fruits.empty()) {
    cout << "元素数量: " << fruits.size() << endl;  // 输出: 元素数量: 2
}

cout << "理论最大容量: " << fruits.max_size() << endl;  // 输出一个很大的数值
```

#### 元素访问

- `T& operator[](const Key& key)`：通过键访问值，如果键不存在则插入
- `T& at(const Key& key)`：通过键访问值，如果键不存在则抛出异常
- `iterator find(const Key& key)`：查找键为`key`的元素
- `int count(const Key& key) const`：返回键为`key`的元素个数
- `iterator lower_bound(const Key& key)`：返回第一个键不小于`key`的元素
- `iterator upper_bound(const Key& key)`：返回第一个键大于`key`的元素
- `pair<iterator,iterator> equal_range(const Key& key)`：返回键等于`key`的范围

```cpp
map<string, int> fruits = { {"apple", 5}, {"banana", 3} };

// 1. operator[]访问
fruits["apple"] = 10;  // 修改已有键的值
fruits["orange"] = 7;  // 插入新键值对

// 2. at()访问
try {
    cout << "banana: " << fruits.at("banana") << endl;  // 输出: 3
    cout << fruits.at("pear") << endl;  // 抛出out_of_range异常
} catch (const out_of_range& e) {
    cout << "键不存在: " << e.what() << endl;
}

// 3. find()查找
auto it = fruits.find("apple");
if (it != fruits.end()) {
    cout << "找到: " << it->first << " => " << it->second << endl;
}

// 4. count()统计
cout << "apple出现次数: " << fruits.count("apple") << endl;  // 输出: 1

// 5. lower_bound()/upper_bound()
auto lb = fruits.lower_bound("a");       // 第一个键 >= "a" 的元素
auto ub = fruits.upper_bound("banana");  // 第一个键 <= "banana" 的元素
for (auto i = lb; i != ub; ++i) {
    cout << i->first << " : " << i->second << endl;
}

// 6. equal_range()查找相同元素的范围
auto range = fruits.equal_range("apple");
for (auto i = range.first; i != range.second; ++i) {
    cout << i->first << " : " << i->second << endl;
}
```

#### 元素修改

- `pair<iterator,bool> insert(const value_type& value)`：插入元素，返回pair
- `iterator insert(iterator hint, const value_type& value)`：带提示插入
- `void erase(iterator pos)`：删除pos位置的元素
- `void erase(iterator first, iterator last)`：删除迭代器范围内的元素
- `int erase(const Key& key)`：删除键为key的元素，返回删除元素个数
- `void swap(set& other)`：交换两个容器
- `void clear()`：清空容器

```cpp
map<string, int> fruits;

// 1. insert()插入
auto ret = fruits.insert({ "apple", 5 });
if (ret.second) {
    cout << "插入成功: " << ret.first->first << " : " << ret.first->second << endl;
}

// 2. 带提示插入
auto hint = fruits.begin();
fruits.insert(hint, { "banana", 3 });

// 3. emplace()直接构造元素(C++11)
fruits.emplace("orange", 7);

// 4. erase()删除
fruits.erase("apple");  // 通过键删除
auto it = fruits.find("banana");
if (it != fruits.end()) {
    fruits.erase(it);  // 通过迭代器删除
}

// 5. swap()交换两个容器
map<string, int> new_fruits;
fruits.swap(new_fruits);

// 6. clear()清空
fruits.clear();
```

#### multimap特有操作

- **没有`operator[]`和`at()`**：因为键不唯一，无法直接通过键访问值

```cpp
multimap<string, int> fruits = {
    {"apple", 5}, {"apple", 7}, {"banana", 3}
};

// 1. 查找所有相同键的元素
auto range = fruits.equal_range("apple");
for (auto it = range.first; it != range.second; ++it) {
    cout << it->first << " : " << it->second << endl;
}

// 2. 统计相同键的数量
cout << "apple出现次数: " << fruits.count("apple") << endl;  // 输出: 2
```

### 函数对象

**函数对象(Function Object)**，也称为**仿函数(Functor)**，本质上是一个类对象，重载了函数调用运算符`operator()`，使得对象可以像函数一样被调用

函数对象有如下优势：

- **可以保持状态：**与普通函数不同，函数对象可以在调用之间保持状态
- **灵活性：**可以作为参数传递给其他函数
- **效率：**编译器可以更好地优化函数对象

```cpp
class MyPrint {
public:
    MyPrint() { this->count = 0; }
    void operator()(string test) {
        cout << test <<endl;
    }

    int count;
};

int main() {
    MyPrint myPrint;  // 创建函数对象
    for (int i = 0; i < 4; i++) {
        myPrint("I love coding!");
    }

    cout << myPrint.count << endl;

    return 0;
}
```

**Lambda表达式**是C++11引入的一个重要特性，提供了一种简洁的方式来创建**匿名函数对象**（也称为**闭包**）。Lambda可以捕获作用域中的变量，并像普通函数一样被调用

- `capture`：捕获列表，指定哪些外部变量可以在lambda体内使用
- `parameters`：参数列表，与普通函数的参数列表类似
- `return_type`：返回类型（可以省略，编译器会自动推导）
- `{}`：函数体

```cpp
[capture](parameters) -> return_type { 
    // 函数体
}
```

编译器会将lambda表达式转换为一个匿名类的函数对象，例如：

```
auto lambda = [](int x) { return x * 2; };
```

会被转换成类似：

```cpp
class __AnonymousClass {
public:
    int operator()(int x) const { return x * 2; }
};
```

#### Lambda捕获变量

Lambda可以通过捕获列表访问外部变量

- 值捕获：创建变量的副本

  ```cpp
  int x = 10;
  auto lambda = [x]() { cout << x << endl; };
  ```

- 引用捕获：通过引用访问变量

  ```cpp
  int y = 20;
  auto lambda = [&y]() { y++; };
  lambda();
  
  cout << y << endl; // 21
  ```

- 值捕获的变量在Lambda内是`const`的，使用`mutable`关键字可以修改值捕获的变量

  ```cpp
  int count = 0;
  auto increment = [count]() mutable { return ++count; };
  ```

#### 谓词

谓词是返回**布尔值**的可调用对象（函数、函数对象或Lambda表达式），可以是：

1. 一个返回`bool`类型或可以隐式转换为`bool`类型的函数
2. 一个重载了`operator()`并返回`bool`的函数对象
3. 一个返回`bool`的Lambda表达式

**一元谓词(Unary Predicate)**是接收一个参数并返回`bool`的谓词，**二元谓词(Binary Predicate)**是接收两个参数并返回`bool`的谓词，谓词在STL算法中广泛使用，具有以下特征：

1. **纯函数性**：谓词通常应该是**无状态**的，或者状态不影响结果
2. **不修改参数**：谓词通常不应该修改其参数
3. **性能**：简单的谓词通常会被编译器内联，性能很好
