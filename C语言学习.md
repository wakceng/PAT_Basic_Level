## 一、概述

### 1、编程语言：

​		**定义**：通过”语言“来控制计算机，让计算机为我们做事情

​		**常见语言**：C语、C++、Java、C#、Python、PHP、JavaScript、Go语言、Objective-C、Swift、汇编语言等

​		**作用**：编程语言是用来控制计算机的一系列指令（Instruction），它有固定的格式和词汇（不同编程语言的格式和词汇不一样），必须遵守，否则就会出错，达不到我们的目的。



### 2、相关概念

​		**源代码、源码、代码**：这些具有特定含义的词汇、语句，按照特定的格式组织在一起，就构成了源代码

```c
#include <stdio.h>
int main(){
    puts("C语言中文网");
    return 0;
}
```

​		**语法**：规定了源代码中每个词汇、语句的含义，也规定了它们该如何组织在一起

​		**编程**：编写源代码的过程

### 3、进制

​		**二进制**	int a = 0b101;表示a=5

​		**八进制**	int a = 015;换算成十进制为 13

​		**十六进制**	int a = 0X2A;换算成十进制为 42

​		二进制、八进制和十六进制 转换成 十进制 用“**按权相加**”

```
八进制转换成十进制：
423.5176 = 4×8^2 + 2×8^1 + 3×8^0 + 5×8^-1 + 1×8^-2 + 7×8^-3 + 6×8^-4 = 275.65576171875（十进制）
小数部分和整数部分相反，要从左往右看，第1位的位权为 8^-1=1/8，第2位的位权为 8^-2=1/64，第3位的位权为 8^-3=1/512，第4位的位权为 8^-4=1/4096 …… 第m位的位权就为 8^-m。
```

​		十进制整数 转换为 N进制整数采用“**除 N 取余，逆序排列**”法

​		十进制小数 转换成 N进制小数采用“**乘 N 取整，顺序排列**”法

### 4、单位换算

```
1Byte = 8 bit
1KB = 1024Byte = 2^10Byte
1MB = 1024KB = 2^20Byte
1GB = 1024MB = 2^30Byte
1TB = 1024GB = 2^40Byte
1PB = 1024TB = 2^50Byte
1EB = 1024PB = 2^60Byte
```

### 5、ASCII编码

​		ASCII 是“American Standard Code for Information Interchange”的缩写，

​		翻译过来是“美国信息交换标准代码”。

​		数字0-9对应十进制的ASCII是48-57

​		字母A-Z对应十进制的ASCII是65-90

​		字母a-z对应十进制的ASCII是97-122

### 6、Unicode 字符集

​		**字符集**定义了字符和二进制的对应关系，为每个字符分配了唯一的编号。可以将字符集理解成一个很大的表格，它列出了所有字符和二进制的对应关系，计算机显示文字或者存储文字，就是一个查表的过程。

​		**字符编码**规定了如何将字符的编号存储到计算机中。如果使用了类似 GB2312 和 GBK 的变长存储方案（不同的字符占用的字节数不一样），那么为了区分一个字符到底使用了几个字节，就不能将字符的编号直接存储到计算机中，字符编号在存储之前必须要经过转换，在读取时还要再逆向转换一次，这套转换方案就叫做字符编码。

​		Unicode 可以使用的编码方案有三种，分别是：

​		UTF-8：一种变长的编码方案，使用 1~6 个字节来存储；

​		UTF-32：一种固定长度的编码方案，不管字符编号大小，始终使用 4 个字节来存储；

​		UTF-16：介于 UTF-8 和 UTF-32 之间，使用 2 个或者 4 个字节来存储，长度既固定又可变。

UTF 是 Unicode Transformation Format 的缩写，意思是“**Unicode转换格式**”，后面的数字表明至少使用多少个比特位（Bit）来存储字符。

只有 UTF-8 兼容 ASCII，UTF-32 和 UTF-16 都不兼容 ASCII，因为它们没有单字节编码。



## 二、入门

### 1、入门

```c
puts("C语言中文网");
```

​		在C语言中，字符串需要用双引号`" "`包围起来，`C语言中文网`什么也不是，计算机不认识它，`"C语言中文网"`才是字符串

​		在编写代码的时候必须使用**英文半角输入法**，尤其是标点符号

### 2、源文件

​		在开发软件的过程中，我们需要将编写好的代码（Code）保存到一个文件中，这样代码才不会丢失，才能够被编译器找到，才能最终变成可执行文件。这种用来保存代码的文件就叫做**源文件**（Source File）

### 3、编译

​		**编译器**：需要一个工具，将C语言代码转换成CPU能够识别的二进制指令，也就是将代码加工成 .exe 程序的格式；这个工具是一个特殊的软件，叫做**编译器（Compiler）**。

​		**编辑器**：用来编写代码，并且给代码着色，以方便阅读；

​		代码提示器：输入部分代码，即可提示全部代码，加速代码的编写过程；

​		调试器：观察程序的每一个运行步骤，发现程序的逻辑错误；

​		项目管理工具：对程序涉及到的所有资源进行管理，包括源文件、图片、视频、第三方库等；

​		漂亮的界面：各种按钮、面板、菜单、窗口等控件整齐排布，操作更方便。

​		**集成开发环境**：这些工具通常被打包在一起，统一发布和安装，例如 Visual Studio、Dev C++、Xcode、Visual C++ 6.0、C-Free、Code::Blocks 等，它们统称为**集成开发环境**（IDE，Integrated Development Environment）

### 4、工程、项目

​		为当前程序配备的专用文件夹，在 IDE 中也有一个专门的称呼，叫做“**Project**”，翻译过来就是“工程”或者“项目”。在 Visual C++ 6.0 下，这叫做一个“工程”，而在 Visual Studio 下，这又叫做一个“项目”，它们只是单词“Project”的不同翻译而已，实际上是一个概念。

### 5、三套标准

​		C89

​		C99

​		C11

### 6、头文件

​		引入头文件使用`#include`命令，并将文件名放在`< >`中，#include 和 < > 之间可以有空格，也可以没有。

### 7、空白符

```c
#include <stdio.h>
int main() {
    puts("a
         bc");
    return 0;
}
```

​		这样使用是错误的，以下的都是正确的

```c
#include<stdio.h>
int main()
{
    puts("C语言");
    puts("中文网");
    puts
    ("C语言中文网");
    puts
    (
    "C语言中文网"
    )
    ;
    puts   ("C语言中文网");
    puts    (    "C语言中文网"    )    ;
    return 0;
}
```



### 8、C标准库

<stdio.h>、<ctype.h>、<stdlib.h>、<string.h>

<assert.h>、<limits.h>、<stddef.h>、<time.h>

<float.h>、<math.h>、<error.h>、<locale.h>、<setjmp.h>、<signal.h>、<stdarg.h>





## 三、变量和数据类型

### 1、变量

```c
int a;
a=123;
//int a = 123;
```

​		这个语句的意思是：在内存中找一块区域，命名为 a，用它来存放整数。

​		赋值（Assign）：是指把数据放到内存的过程。

​		因为 a 的值可以改变，所以我们给它起了一个形象的名字，叫做**变量（Variable）**。

​		`int a;`创造了一个变量 a，我们把这个过程叫做**变量定义**。`a=123;`把 123 交给了变量 a，我们把这个过程叫做给**变量赋值**；又因为是第一次赋值，也称变量的初始化，或者赋初值。

### 2、数据类型

| 说  明           | 字符型 | 短整型 | 整型 | 长整型 | 单精度浮点型 | 双精度浮点型 | 无类型 |
| :--------------- | :----- | :----- | :--- | :----- | :----------- | :----------- | :----- |
| 数据类型         | char   | short  | int  | long   | float        | double       | void   |
| 长度（32位环境） | 1      | 2      | 4    | 4      | 4            | 8            |        |

​		只有 short 的长度是确定的，是两个字节，而 int 和 long 的长度无法确定，在不同的环境下有不同的表现，2 ≤ short ≤ int ≤ long

​		可以用sizeof()函数得到类型的长度，返回是int类型

​		short、int 和 long 类型默认都是带符号位的，符号位以外的内存才是数值位。如果只考虑正数，那么各种类型能表示的数值范围（取值范围）就比原来小了一半。在很多情况下，我们非常确定某个数字只能是正数，比如班级学生的人数、字符串的长度、内存地址等，这个时候符号位就是多余的了，就不如删掉符号位，把所有的位都用来存储数值，这样能表示的数值范围更大（大一倍）。**unsigned int b = 1002;**如果将一个数字分为符号和数值两部分，那么不加 unsigned 的数字称为有符号数，能表示正数和负数，加了 unsigned 的数字称为无符号数，只能表示正数，如果是`unsigned int`类型，那么可以省略 int ，只写 **unsigned b = 1002;**

### 3、输出

​		**puts** 只能用来输出**字符串**，不能输出整数、小数、字符等

​		**printf** 不仅可以输出字符串，还可以输出整数、小数、单个字符等，并且输出格式可以自定义

​		puts 输出完成后会自动换行，而 printf 不会，要自己添加换行符\n

​		%d：来输出 int 类型，d 是 decimal 的简写。

​		%hd：用来输出 short int 类型，hd 是 short decimal 的简写

​		%ld用来输出 long int 类型，ld 是 long decimal 的简写。

​		%c：输出一个字符。c 是 character 的简写。

​		%s：输出一个字符串。s 是 string 的简写。

​		%f：输出一个小数。f 是 float 的简写。

​		%f 以十进制形式输出 float 类型；

​		%lf 以十进制形式输出 double 类型；

​		%e 以指数形式输出 float 类型，输出结果中的 e 小写；

​		%E 以指数形式输出 float 类型，输出结果中的 E 大写；

​		%le 以指数形式输出 double 类型，输出结果中的 e 小写；

​		%lE 以指数形式输出 double 类型，输出结果中的 E 大写。

​		当使用`%d`输出 short，或者使用`%ld`输出 short、int 时，不管值有多大，都不会发生错误，因为格式控制符足够容纳这些值。当使用`%hd`输出 int、long，或者使用`%d`输出 long 时，如果要输出的值比较小（就像上面的情况），一般也不会发生错误，如果要输出的值比较大，就很有可能发生错误。

​		在 puts 函数中，可以将一个较长的字符串分割成几个较短的字符串，这样会使得长文本的格式更加整齐。这只是形式上的分割，编译器在编译阶段会将它们合并为一个字符串，它们放在一块连续的内存中。

```c
#include <stdio.h>
int main()
{
    puts(
        "C语言中文网，一个学习C语言和C++的网站，他们坚持用工匠的精神来打磨每一套教程。"
        "坚持做好一件事情，做到极致，让自己感动，让用户心动，这就是足以传世的作品！"
        "C语言中文网的网址是：http://c.biancheng.net"
    );
    return 0;
}
```

```c
#include <stdio.h>
int main()
{
    short a = 0b1010110;  //二进制数字
    int b = 02713;  //八进制数字
    long c = 0X1DAB83;  //十六进制数字
    printf("以八进制输出a=%ho, b=%o, c=%lo\n", a, b, c);  //以八进制形似输出
    printf("以十进制输出a=%hd, b=%d, c=%ld\n", a, b, c);  //以十进制形式输出
    printf("以十六进制输出（字母小写）a=%hx, b=%x, c=%lx\n", a, b, c);  //以十六进制形式输出（字母小写）
    printf("以十六进制输出（字母大写）a=%hX, b=%X, c=%lX\n", a, b, c);  //以十六进制形式输出（字母大写）
    printf("******************\n");
    printf("a=%#ho, b=%#o, c=%#lo\n", a, b, c);  //以八进制形似输出
    printf("a=%hd, b=%d, c=%ld\n", a, b, c);  //以十进制形式输出
    printf("a=%#hx, b=%#x, c=%#lx\n", a, b, c);  //以十六进制形式输出（字母小写）
    printf("a=%#hX, b=%#X, c=%#lX\n", a, b, c);  //以十六进制形式输出（字母大写）
    return 0;
}
```

​		结果如下

```
以八进制输出a=126, b=2713, c=7325603
以十进制输出a=86, b=1483, c=1944451
以十六进制输出（字母小写）a=56, b=5cb, c=1dab83
以十六进制输出（字母大写）a=56, b=5CB, c=1DAB83
******************
a=0126, b=02713, c=07325603
a=86, b=1483, c=1944451
a=0x56, b=0x5cb, c=0x1dab83
a=0X56, b=0X5CB, c=0X1DAB83
```

### 4、字符

```c
//正确的写法
char a = '1';
char b = '$';
char c = 'X';
char d = ' ';  // 空格也是一个字符

//错误的写法
char x = '中';  //char 类型不能包含 ASCII 编码之外的字符
char y = 'Ａ';  //A 是一个全角字符
char z = "t";  //字符类型应该由单引号包围
```

```c
#include <stdio.h>
int main() {
    char a = '1';
    char b = '$';
    char c = 'X';
    char d = ' ';

    //使用 putchar 输出
    putchar(a); putchar(d);
    putchar(b); putchar(d);
    putchar(c); putchar('\n');
    //使用 printf 输出
    printf("%c %c %c\n", a, b, c);

    return 0;
}
```

​		putchar 函数每次只能输出一个字符，输出多个字符需要调用多次。

​		当给c赋值一个字符时，字符会先转换成 ASCII 码再存储；printf("%d",c);能输出c的ASCII对应的整数。

### 5、字符串

```c
char str1[] = "http://c.biancheng.net";
char *str2 = "C语言中文网";
```

​		用以上方式都能表示字符串，可以用puts和printf("%s");输出。

### 6、加减乘除

|       | 加法 | 减法 | 乘法 | 除法 | 求余数（取余） |
| ----- | ---- | ---- | ---- | ---- | -------------- |
| 数学  | +    | -    | ×    | ÷    | 无             |
| C语言 | +    | -    | *    | /    | %              |

​		当除数和被除数都是整数时，运算结果也是整数；如果不能整除，那么就直接丢掉小数部分，只保留整数部分；除数和被除数中有一个是小数，那么运算结果也是小数，并且是 double 类型的小数。

​		取余，也就是求余数，使用的运算符是 %。C语言中的取余运算只能针对整数，也就是说，% 的两边都必须是整数，不能出现小数，否则编译器会报错；余数可以是正数也可以是负数，由 % 左边的整数决定：如果 % 左边是负数，那么余数也是负数。

​		简写：a = a # b的意思与a #= b的意思相同。

​		a++后自增：先进行其他操作，再进行自增运算。

​		++a前自增：先进行自增运算，再进行其他操作。

### 7、变量的定义位置以及初始值

​		在函数外部定义的变量在函数内部也可以使用。

​		**全局变量**：在函数外部定义的变量

​		**局部变量**：在函数内部定义的变量

​		定义变量时，最好顺便给他一个初值。

### 8、运算优先级、结合型

### 9、强制类型转换

```c
(float) a;  //将变量 a 转换为 float 类型
```





## 四、输入输出

### 1、printf的格式控制符

| 格式控制符                      | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| %c                              | 输出一个单一的字符                                           |
| %hd、%d、%ld                    | 以十进制、有符号的形式输出 short、int、long 类型的整数       |
| %hu、%u、%lu                    | 以十进制、无符号的形式输出 short、int、long 类型的整数       |
| %ho、%o、%lo                    | 以八进制、不带前缀、无符号的形式输出 short、int、long 类型的整数 |
| %#ho、%#o、%#lo                 | 以八进制、带前缀、无符号的形式输出 short、int、long 类型的整数 |
| %hx、%x、%lx %hX、%X、%lX       | 以**十六进制、不带前缀**、无符号的形式输出 short、int、long 类型的整数。如果 x 小写，那么输出的十六进制数字也小写；如果 X 大写，那么输出的十六进制数字也大写。 |
| %#hx、%#x、%#lx %#hX、%#X、%#lX | 以**十六进制、带前缀**、无符号的形式输出 short、int、long 类型的整数。如果 x 小写，那么输出的十六进制数字和前缀都小写；如果 X 大写，那么输出的十六进制数字和前缀都大写。 |
| %f、%lf                         | 以十进制的形式输出 float、double 类型的小数                  |
| %e、%le %E、%lE                 | 以指数的形式输出 float、double 类型的小数。如果 e 小写，那么输出结果中的 e 也小写；如果 E 大写，那么输出结果中的 E 也大写。 |
| %g、%lg %G、%lG                 | 以十进制和指数中较短的形式输出 float、double 类型的小数，并且小数部分的最后不会添加多余的 0。如果 g 小写，那么当以指数形式输出时 e 也小写；如果 G 大写，那么当以指数形式输出时 E 也大写。 |
| %s                              | 输出一个字符串                                               |

```c
#include <stdio.h>
int main()
{
    int a1=20, a2=345, a3=700, a4=22;
    int b1=56720, b2=9999, b3=20098, b4=2;
    int c1=233, c2=205, c3=1, c4=6666;
    int d1=34, d2=0, d3=23, d4=23006783;
    printf("%-9d %-9d %-9d %-9d\n", a1, a2, a3, a4);
    printf("%-9d %-9d %-9d %-9d\n", b1, b2, b3, b4);
    printf("%-9d %-9d %-9d %-9d\n", c1, c2, c3, c4);
    printf("%-9d %-9d %-9d %-9d\n", d1, d2, d3, d4);
    return 0;
}
```

​		输出结果：

```
20        345       700       22
56720     9999      20098     2
233       205       1         6666
34        0         23        23006783
```

​		`%-9d`中，`d`表示以十进制输出，`9`表示最少占9个字符的宽度，宽度不足以空格补齐，`-`表示左对齐。综合起来，`%-9d`表示以十进制输出，左对齐，宽度最小为9个字符。

​		printf() 格式控制符的完整形式如下：

```c
%[flag][width][.precision]type
```

​		type 表示输出类型，比如 %d

​		width 表示最小输出宽度，至少占用几个字符的位置；printf("%10d%12f%4c%8s", n, f, c, str);

​		.precision 表示输出精度，也就是**小数**的位数。用于**整数**时，.precision 表示最小输出宽度。与 width 不同的是，整数的宽度不足时会在左边补 0，而不是补空格。用于**字符串**时，.precision 表示最大输出宽度，或者说截取字符串。当字符串的长度大于 precision 时，会截掉多余的字符；当字符串的长度小于 precision 时，.precision 就不再起作用。

​		flag 是标志字符。例如，`%#x`中 flag 对应 #，`%-9d`中 flags 对应`-`。

| 标志字符 | 含  义                                                       |
| :------: | :----------------------------------------------------------- |
|    -     | `-`表示左对齐。如果没有，就按照默认的对齐方式，默认一般为右对齐。 |
|    +     | 用于整数或者小数，表示输出符号（正负号）。如果没有，那么只有负数才会输出符号。 |
|   空格   | 用于整数或者小数，输出值为正时冠以空格，为负时冠以负号。     |
|    #     | 对于八进制（%o）和十六进制（%x / %X）整数，# 表示在输出时添加前缀；八进制的前缀是 0，十六进制的前缀是 0x / 0X。对于小数（%f / %e / %g），# 表示强迫输出小数点。如果没有小数部分，默认是不输出小数点的，加上 # 以后，即使没有小数部分也会带上小数点。 |

### 2、scanf读取从键盘输入的数据

​		scanf()： 可以输入多种类型的数据。

​		getchar()、getche()、getch()：这三个函数都用于输入单个字符。

​		gets()：获取一行数据，并作为字符串处理。

​		scanf的变量前要带一个`&`符号。`&`称为取地址符，也就是获取变量在内存中的地址。

```c
scanf("%d %d", &a, &b);  // 获取用户输入的两个整数，分别赋值给变量 a 和 b
```

​		从本质上讲，我们从键盘输入的数据并没有直接交给 scanf()，而是放入了缓冲区中，直到我们按下回车键，scanf() 才到缓冲区中读取数据。如果缓冲区中的数据符合 scanf() 的要求，那么就读取结束；如果不符合要求，那么就继续等待用户输入，或者干脆读取失败。

| 格式控制符   | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| %c           | 读取一个单一的字符                                           |
| %hd、%d、%ld | 读取一个十进制整数，并分别赋值给 short、int、long 类型       |
| %ho、%o、%lo | 读取一个八进制整数（可带前缀也可不带），并分别赋值给 short、int、long 类型 |
| %hx、%x、%lx | 读取一个十六进制整数（可带前缀也可不带），并分别赋值给 short、int、long 类型 |
| %hu、%u、%lu | 读取一个无符号整数，并分别赋值给 unsigned short、unsigned int、unsigned long 类型 |
| %f、%lf      | 读取一个十进制形式的小数，并分别赋值给 float、double 类型    |
| %e、%le      | 读取一个指数形式的小数，并分别赋值给 float、double 类型      |
| %g、%lg      | 既可以读取一个十进制形式的小数，也可以读取一个指数形式的小数，并分别赋值给 float、double 类型 |
| %s           | 读取一个字符串（以空白符为结束）                             |

​		scanf() 控制字符串的完整写法为：

```c
%{*} {width} type
```

​		`type`表示读取什么类型的数据，例如 %d、%s、%[a-z]、%[ ^\n] 等；type 必须有。

​		`width`表示最大读取宽度，可有可无。

​		`*`表示丢弃读取到的数据，可有可无。





## 五、循环结构和选择结构

### 1、if else语句

```c
if(判断条件1){
    语句块1
} else  if(判断条件2){
    语句块2
}else  if(判断条件3){
    语句块3
}else  if(判断条件m){
    语句块m
}else{
     语句块n
}
```

| 运算符 | 说明                           | 结合性 | 举例                   |
| ------ | ------------------------------ | ------ | ---------------------- |
| &&     | 与运算，双目，对应数学中的“且” | 左结合 | 1&&0、(9>3)&&(b>a)     |
| \|\|   | 或运算，双目，对应数学中的“或” | 左结合 | 1\|\|0、(9>3)\|\|(b>a) |
| !      | 非运算，单目，对应数学中的“非” | 右结合 | !a、!(2<5)             |

​		&和&&都可以用作逻辑与的运算符，表示逻辑与（and），当运算符两边的表达式的结果都为true时，整个运算结果才为true，否则，只要有一方为false，则结果为false。&&还具有短路的功能，即如果第一个表达式为false，则不再计算第二个表达式。



### 2、switch case语句

```c
switch(表达式){
    case 整型数值1: 语句 1;
    case 整型数值2: 语句 2;
    ......
    case 整型数值n: 语句 n;
    default: 语句 n+1;
}
```

1) 首先计算“表达式”的值，假设为 m。

2) 从第一个 case 开始，比较“整型数值1”和 m，如果它们相等，就执行冒号后面的所有语句，也就是从“语句1”一直执行到“语句n+1”，而不管后面的 case 是否匹配成功。

3) 如果“整型数值1”和 m 不相等，就跳过冒号后面的“语句1”，继续比较第二个 case、第三个 case……一旦发现和某个整型数值相等了，就会执行后面所有的语句。假设 m 和“整型数值5”相等，那么就会从“语句5”一直执行到“语句n+1”。

4) 如果直到最后一个“整型数值n”都没有找到相等的值，那么就执行 default 后的“语句 n+1”，default 不是必须的。当没有 default 时，如果所有 case 都匹配失败，那么就什么都不执行。

​		**当和某个整型数值匹配成功后，会执行该分支以及后面所有分支的语句！！！**



### 3、?和:语句		

```c
if(a>b){
    max = a;
}else{
    max = b;
}

//和以下语句实现的功能一样
max = (a>b) ? a : b;
```

### 4、while语句

```c
while(表达式){
    语句块
}
```

​		**先计算“表达式”的值**，当值为真（非0）时， 执行“语句块”；执行完“语句块”，再次计算表达式的值，如果为真，继续执行“语句块”……这个过程会一直重复，直到表达式的值为假（0），就退出循环，执行 while 后面的代码。

### 5、do while语句

```c
do{
    语句块
}while(表达式);//注意while(i<=100);最后的分号;，这个必须要有。
```

​		**先执行“语句块”**，然后再判断表达式是否为真，如果为真则继续循环；如果为假，则终止循环。因此，do-while 循环至少要执行一次“语句块”。

### 6、for语句

```c
for(表达式1; 表达式2; 表达式3)//for(初始化语句; 循环条件; 自增或自减)
{
    语句块
}
```

1) 先执行“表达式1”。

2) 再执行“表达式2”，如果它的值为真（非0），则执行循环体，否则结束循环。

3) 执行完循环体后再执行“表达式3”。

4) 重复执行步骤 2) 和 3)，直到“表达式2”的值为假，就结束循环

   上面的步骤中，2) 和 3) 是一次循环，会重复执行，for 语句的主要作用就是不断执行步骤 2) 和 3)。

```c
#include <stdio.h>
int main(){
    int i, sum=0;
    for(i=1; i<=100; i++){
        sum+=i;
    }
    printf("%d\n",sum);
    return 0;
}
```



### 7、break和continue用法（跳出循环）

​		在多层循环中，一个 break 语句只向外跳一层

​		continue语句的作用是**跳过循环体中剩余的语句**而**强制进入下一次循环**。continue语句只用在 while、for 循环中，常与 if 条件语句一起使用，判断条件是否成立。

​		break与continue的对比：break 用来结束所有循环，循环语句不再有执行的机会；continue 用来结束本次循环，直接跳到下一次循环，如果循环条件成立，还会继续循环。



## 六、C语言数组

### 注意：C语言数组是静态的，不能插入或删除元素

### 1、C语言数组定义

​		我们把这样的一组数据的集合称为**数组（Array）**，它所包含的每一个数据叫做数组元素（Element），所包含的数据的个数称为数组长度（Length），例如`int a[4];`就定义了一个长度为4的整型数组，名字是`a`。

​		数组中每个元素的数据类型必须相同，对于`int a[4];`，每个元素都必须为 int。

```c
int a[10]={12, 19, 22 , 993, 344};
```

​		表示只给 a[0]~a[4] 5个元素赋值，而后面 5 个元素自动初始化为 0，（对于char，就是字符 '\0'；对于float、double，就是小数 0.0。）



### 2、C语言二维数组的定义

​		在C语言中，二维数组是按行排列的。



### 3、C语言字符数组和字符串

```c
char a[10];  //一维字符数组
char b[5][10];  //二维字符数组
char c[20]={'c', '  ', 'p', 'r', 'o', 'g', 'r', 'a','m'};  // 给部分数组元素赋值
char d[]={'c', ' ', 'p', 'r', 'o', 'g', 'r', 'a', 'm' };  //对全体元素赋值时可以省去长度
char str[30] = {"c.biancheng.net"};
char str[30] = "c.biancheng.net";  //这种形式更加简洁，实际开发中常用
char str[] = {"c.biancheng.net"};
char str[] = "c.biancheng.net";  //这种形式更加简洁，实际开发中常用
```

​		字符数组只有在定义时才能将整个字符串**一次性地**赋值给它，一旦定义完了，就只能一**个字符一个字符地赋值**了。

​		printf() 输出字符串时，会从第 0 个元素开始往后检索，直到遇见`'\0'`才停止，然后把`'\0'`前面的字符全部输出，这就是 printf() 输出字符串的原理

​		在C语言中，我们使用`string.h`头文件中的 strlen() 函数来求字符串的长度



​		scanf()：通过格式控制符`%s`输入字符串。除了字符串，scanf() 还能输入其他类型的数据。取字符串时以空格为分隔，遇到空格就认为当前字符串结束了，所以无法读取含有空格的字符串。

​		gets()：直接输入字符串，并且只能输入字符串。gets() 认为空格也是字符串的一部分，只有遇到回车键时才认为字符串输入结束，所以，不管输入了多少个空格，只要不按下回车键，对 gets() 来说就是一个完整的字符串。换句话说，gets() 用来读取一整行字符串。



### 4、字符串处理

```c
strcat(arrayName1, arrayName2);
```

​		strcat() 将把 arrayName2 连接到 arrayName1 后面，并删除原来 arrayName1 最后的结束标志`'\0'`。这意味着，arrayName1 必须足够长，要能够同时容纳 arrayName1 和 arrayName2，否则会越界。



```c
strcpy(arrayName1, arrayName2);
```

​		strcpy() 会把 arrayName2 中的字符串拷贝到 arrayName1 中，字符串结束标志`'\0'`也一同拷贝。



```c
strcmp(arrayName1, arrayName2);
```

​		strcmp() 以各个字符对应的 ASCII 码值进行比较。strcmp() 从两个字符串的第 0 个字符开始比较，如果它们相等，就继续比较下一个字符，直到遇见不同的字符，或者到字符串的末尾。返回值：若 arrayName1 和 arrayName2 相同，则返回0；若 arrayName1 大于 arrayName2，则返回大于 0 的值；若 arrayName1 小于 arrayName2，则返回小于0 的值。



### 5、对数组元素冒泡排序

```c
#include <stdio.h>
int main(){
    int nums[10] = {4, 5, 2, 10, 7, 1, 8, 3, 6, 9};
    int i, j, temp, isSorted；
    //优化算法：最多进行 n-1 轮比较
    for(i=0; i<10-1; i++){
        isSorted = 1;  //假设剩下的元素已经排序好了
        for(j=0; j<10-1-i; j++){
            if(nums[j] > nums[j+1]){
                temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
                isSorted = 0;  //一旦需要交换数组元素，就说明剩下的元素没有排序好
            }
        }
        if(isSorted) break; //如果没有发生交换，说明剩下的元素已经排序好了
    }
    for(i=0; i<10; i++){
        printf("%d ", nums[i]);
    }
    printf("\n")
    return 0;
}
```



## 七、C语言函数

### 1、概念

​		常用的功能，一个程序可能会用到很多次，如果每次都写这样一段重复的代码，不但费时费力、容易出错，而且交给别人时也很麻烦，所以C语言提供了一个功能，允许我们将常用的代码以固定的格式封装（包装）成一个独立的模块，只要知道这个模块的名字就可以重复使用它，这个模块就叫做**函数（Function）**。

​		**库（Library）**是编程中的一个基本概念，可以简单地认为它是一系列函数的集合，在磁盘上往往是一个文件夹。C语言自带的库称为标准库（S[tan](http://c.biancheng.net/ref/tan.html)dard Library），其他公司或个人开发的库称为第三方库（Third-Party Library）。

​		函数的一个明显特征就是使用时带括号`( )`，有必要的话，括号中还要包含数据或变量，称为**参数（Parameter）**。参数是函数需要处理的数据。

​		函数**返回值**有固定的数据类型（int、char、float等），用来接收返回值的变量类型要一致。

​		函数定义时给出的参数称为形式参数，简称形参；函数调用时给出的参数（也就是传递的数据）称为实际参数，简称实参。函数调用时，将实参的值传递给形参，相当于一次赋值操作。

​		return 语句是提前结束函数的唯一办法。return 后面可以跟一份数据，表示将这份数据返回到函数外面；return 后面也可以不跟任何数据，表示什么也不返回，仅仅用来结束函数。



### 2、函数原型

​		函数声明给出了函数名、返回值类型、参数列表（重点是参数类型）等与该函数有关的信息，称为**函数原型（Function Prototype）**。函数原型的作用是告诉编译器与该函数有关的信息，让编译器知道函数的存在，以及存在的形式，即使函数暂时没有定义，编译器也知道如何使用它。

​		在实际开发中，往往都是几千行、上万行、百万行的代码，将这些代码都放在一个源文件中简直是灾难，不但检索麻烦，而且打开文件也很慢，所以必须将这些代码分散到多个文件中。对于多个文件的程序，通常是将函数定义放到源文件（`.c`文件）中，将函数的声明放到头文件（`.h`文件）中，使用函数时引入对应的头文件就可以，编译器会在链接阶段找到函数体。



### 3、全局变量和局部变量

​		当全局变量和局部变量同名时，在局部范围内全局变量被“屏蔽”，不再起作用。或者说，变量的使用遵循就近原则，如果在当前作用域中存在同名变量，就不会向更大的作用域中去寻找变量。

​		给全局变量加上 **static** 关键字，它的作用域就变成了当前文件，在其它文件中就无效了。

​		变量 i 定义在循环条件里面，所以是一个块级变量，它的作用域就是当前 for 循环，出了 for 循环就无效了。

```c
#include <stdio.h>
int main(){
    int n = 22;  //编号①
    //由{ }包围的代码块
    {
        int n = 40;  //编号②
        printf("block n: %d\n", n);
    }
    printf("main n: %d\n", n);
   
    return 0;
}


//运行结果
//block n: 40
//main n: 22
```





### 八、C语言预处理

### 1、使用

​		预处理主要是处理以`#`开头的命令，例如`#include <stdio.h>`等。预处理命令要放在所有函数之外，而且一般都放在源文件的前面。

​		预处理是C语言的一个重要功能，由**预处理程序**完成。当对一个源文件进行编译时，系统将自动调用预处理程序对源程序中的预处理部分作处理，处理完毕自动进入对源程序的编译。

```c
#include <stdio.h>

//不同的平台下引入不同的头文件
#if _WIN32  //识别windows平台
#include <windows.h>
#elif __linux__  //识别linux平台
#include <unistd.h>
#endif
int main() {
    //不同的平台下调用不同的函数
    #if _WIN32  //识别windows平台
    Sleep(5000);
    #elif __linux__  //识别linux平台
    sleep(5);
    #endif
    puts("http://c.biancheng.net/");
    return 0;
}
```

### 2、#include的用法

```c
#include <stdHeader.h>
#include "myHeader.h"
```

​		使用尖括号`< >`，编译器会到**系统路径**下查找头文件；

​		而使用双引号`" "`，编译器首先在**当前目录**下查找头文件，如果没有找到，再到系统路径下查找。



### 3、#define的用法

​		**宏定义命令**：`#define N 100`就是宏定义，`N`为宏名，`100`是宏的内容（宏所表示的字符串）。在预处理阶段，对程序中所有出现的“宏名”，预处理器都会用宏定义中的字符串去代换，这称为“宏替换”或“宏展开”。

​		宏定义是用宏名来表示一个字符串，在宏展开时又以该字符串取代宏名，这只是一种简单粗暴的替换。字符串中可以含任何字符，它可以是常数、表达式、if 语句、函数等，预处理程序对它不作任何检查，如有错误，只能在编译已被宏展开后的源程序时发现。

​		宏定义不是说明或语句，在行末不必加分号，如果加上分号则连分号也一起替换。代码中的宏名如果被引号包围，那么预处理程序不对其作宏代替。宏定义允许嵌套，在宏定义的字符串中可以使用已经定义的宏名，在宏展开时由预处理程序层层代换。

​		 宏定义必须写在函数之外，其作用域为宏定义命令起到源程序结束。如要终止其作用域可使用`#undef`命令。例如：表示 PI 只在 main() 函数中有效，在 func() 中无效。

```c
#define PI 3.14159
int main(){
    // Code
    return 0;
}
#undef PI
void func(){
    // Code
}
```

​		宏定义只是简单的字符串替换，由预处理器来处理；而 typedef 是在编译阶段由编译器处理的，它并不是简单的字符串替换，而给原有的数据类型起一个新的名字，将它作为一种新的数据类型。

```c
//带参数的宏定义
#include <stdio.h>
#define MAX(a,b) (a>b) ? a : b
int main(){
    int x , y, max;
    printf("input two numbers: ");
    scanf("%d %d", &x, &y);
    max = MAX(x, y);
    printf("max=%d\n", max);
    return 0;
}
```

​		宏和函数只是在形式上相似，本质上是完全不同的。

​		记住，宏定义只是把参数带入。



### 4、##的用法

​		`##`称为连接符，用来将宏参数或其他的串连接起来。

```c
#include <stdio.h>
#define CON1(a, b) a##e##b
#define CON2(a, b) a##b##00
int main() {
    printf("%f\n", CON1(8.5, 2));
    printf("%d\n", CON2(12, 34));
    return 0;
}
//运行结果：
//850.000000
//123400
```



### 5、#if的用法

​		如常“表达式1”的值为真（非0），就对“程序段1”进行编译，否则就计算“表达式2”，结果为真的话就对“程序段2”进行编译，为假的话就继续往下匹配，直到遇到值为真的表达式，或者遇到 #else。这一点和 if else 非常类似。\#elif 和 #else 也可以省略。

```c
#if 整型常量表达式1
    程序段1
#elif 整型常量表达式2
    程序段2
#elif 整型常量表达式3
    程序段3
#else
    程序段4
#endif
```



### 6、#ifdef

​		它的意思是，如果当前的宏已被定义过，则对“程序段1”进行编译，否则对“程序段2”进行编译。

```c
#ifdef  宏名
    程序段1
#else
    程序段2
#endif
```



### 7、#ifndef

​		与 #ifdef 相比，仅仅是将 #ifdef 改为了 #ifndef。它的意思是，如果当前的宏未被定义，则对“程序段1”进行编译，否则对“程序段2”进行编译，这与 #ifdef 的功能正好相反。

```c
#ifndef 宏名
    程序段1 
#else 
    程序段2 
#endif
```



### 8、#error

​		\#error 指令用于在编译期间产生错误信息，并阻止程序的编译；例如，我们的程序针对 Linux 编写，不保证兼容 Windows，那么可以这样做：

```c
#ifdef WIN32
#error This programme cannot compile at Windows Platform
#endif
```



### 9、总结

| 指令     | 说明                                                      |
| -------- | --------------------------------------------------------- |
| #        | 空指令，无任何效果                                        |
| #include | 包含一个源代码文件                                        |
| #define  | 定义宏                                                    |
| #undef   | 取消已定义的宏                                            |
| #if      | 如果给定条件为真，则编译下面代码                          |
| #ifdef   | 如果宏已经定义，则编译下面代码                            |
| #ifndef  | 如果宏没有定义，则编译下面代码                            |
| #elif    | 如果前面的#if给定条件不为真，当前条件为真，则编译下面代码 |
| #endif   | 结束一个#if……#else条件编译块                              |





## 八、C语言指针

### 1、指针（地址）概念

​		数据在内存中的地址也称为[指针](http://c.biancheng.net/c/80/)，如果一个变量存储了一份数据的指针，我们就称它为**指针变量**。		

​		我们将内存中字节的编号称为**地址（Address）或指针（Pointer）**。地址从 0 开始依次增加，对于 32 位环境，程序能够使用的内存为 4GB，最小的地址为 0，最大的地址为 0XFFFFFFFF。

```c
#include <stdio.h>

int main(){
    int a = 100;
    char str[20] = "c.biancheng.net";
    printf("%#X, %#X\n", &a, str);
    return 0;
}
```

​		`%#X`表示以十六进制形式输出，并附带前缀`0X`。a 是一个变量，用来存放整数，需要在前面加`&`来获得它的地址；str 本身就表示字符串的首地址，不需要加`&`。

​		CPU 只能通过地址来取得内存中的代码和数据，程序在执行过程中会告知 CPU 要执行的代码以及要读写的数据的地址。

​		CPU 访问内存时需要的是地址，而不是变量名和函数名！变量名和函数名只是地址的一种助记符，当源文件被编译和链接成可执行程序后，它们都会被替换成地址。编译和链接过程的一项重要任务就是找到这些名称所对应的地址。



### 2、指针变量的定义和使用

​		定义

```c
datatype *name;
datatype *name = value;
//*表示这是一个指针变量，datatype表示该指针变量所指向的数据的类型 。例如：
int *p1;
int a = 100;
int *p_a = &a;//在定义指针变量 p_a 的同时对它进行初始化，并将变量 a 的地址赋予它，此时 p_a 就指向了 a。值得注意的是，p_a 需要的一个地址，a 前面必须要加取地址符&，否则是不对的。
p1=&a;//*是一个特殊符号，表明一个变量是指针变量，定义 p1、p2 时必须带*。而给 p1、p2 赋值时，因为已经知道了它是一个指针变量，就没必要多此一举再带上*，后边可以像使用普通变量一样来使用指针变量。也就是说，定义指针变量时必须带*，给指针变量赋值时不能带*

```

​		使用

```c
#include <stdio.h>

int main(){
    int a = 15;
    int *p = &a;
    printf("%d, %d\n", a, *p);  //两种方式都可以输出a的值
    return 0;
}
```

​		使用指针是间接获取数据，使用变量名是直接获取数据，前者比后者的代价要高。指针除了可以获取内存上的数据，也可以修改内存上的数据。

```c
#include <stdio.h>

int main(){
    int a = 15, b = 99, c = 222;
    int *p = &a;  //定义指针变量
    *p = b;  //通过指针变量修改内存上的数据
    c = *p;  //通过指针变量获取内存上的数据
    printf("%d, %d, %d, %d\n", a, b, c, *p);
    return 0;
}
//运行结果：
//99, 99, 99, 99
```

​		*p 代表的是 a 中的数据，它等价于 a，可以将另外的一份数据赋值给它，也可以将它赋值给另外的一个变量。

​		`*`在不同的场景下有不同的作用：`*`可以用在指针变量的定义中，表明这是一个指针变量，以和普通变量区分开；使用指针变量时在前面加`*`表示获取指针指向的数据，或者说表示的是指针指向的数据本身：***p 代表的是指针p指向的地址上的数据**。

```c
int *p = &a,b,c,*px;  //指针p指向a的地址
p = &a;				//指针p指向a的地址
*p = b;       //指针p指向的地址上的数据变为b的数值
c = *p;       //c的数值变为指针p指向的地址上的数值
y = *px + 5;  //y的数值变为指针px指向的地址上的数值 再加上5
```

​		`*&a`可以理解为`*(&a)`，`&a`表示取变量 a 的地址（等价于 pa），`*(&a)`表示取这个地址上的数据（等价于 *pa），绕来绕去，又回到了原点，`*&a`仍然等价于 a。（ int 类型的变量 a，pa 是指向它的指针）

​		`&*pa`可以理解为`&(*pa)`，`*pa`表示取得 pa 指向的数据（等价于 a），`&(*pa)`表示数据的地址（等价于 &a），所以`&*pa`等价于 pa。 （int 类型的变量 a，pa 是指向它的指针）

​		当对指针变量进行比较运算时，比较的是指针变量本身的值，也就是数据的地址。如果地址相等，那么两个指针就指向同一份数据，否则就指向不同的数据。



### 3、星号*总结

​		表示乘法，例如`int a = 3, b = 5, c;  c = a * b;`；

​		表示定义一个指针变量，以和普通变量区分开，例如`int a = 100;  int *p = &a;`；

​		**表示获取指针指向的数据**，是一种间接操作，例如`int a, b, *p = &a;  *p = 100;  b = *p;`。



### 4、指针与数组

```c
int arr[] = { 99, 15, 100, 888, 252 };
int len = sizeof(arr) / sizeof(int);  //求数组长度，sizeof(p) 求得的是 p 这个指针变量本身所占用的字节数，而不是整个数组占用的字节数。
int *p = arr;
```

​		**arr 本身就是一个指针，可以直接赋值给指针变量 p**。arr 是数组第 0 个元素的地址，所以`int *p = arr;`也可以写作`int *p = &arr[0];`。也就是说，arr、p、&arr[0] 这三种写法都是等价的，它们都指向数组第 0 个元素，或者说指向数组的开头。

​		如果一个指针指向了数组，我们就称它为**数组指针（Array Pointer）**。数组指针指向的是数组中的一个具体元素，而不是整个数组，所以数组指针的类型和数组元素的类型有关，上面的例子中，p 指向的数组元素是 int 类型，所以 p 的类型必须也是`int *`。



### 5、访问数组元素的两个方法

​		1）使用下标：采用 arr[i] 的形式访问数组元素。如果 p 是指向数组 arr 的指针，那么也可以使用 p[i] 来访问数组元素，它等价于 arr[i]。

​		2）使用指针：使用 *(p+i) 的形式访问数组元素。另外数组名本身也是指针，也可以使用 *(arr+i) 来访问数组元素，它等价于 *(p+i)。

​		*p++ 等价于 *(p++)，表示先取得第 n 个元素的值，再将 p 指向下一个元素。

​		*++p 等价于 *(++p)，会先进行 ++p 运算，使得 p 的值增加，指向下一个元素，整体上相当于 *(p+1)，所以会获得第 n+1 个数组元素的值。

​		(*p)++ 就非常简单了，会先取得第 n 个元素的值，再对该元素的值加 1。假设 p 指向第 0  个元素，并且第 0 个元素的值为 99，执行完该语句后，第 0  个元素的值就会变为 100。



### 6、指针输出字符串

```c
#include <stdio.h>
#include <string.h>

int main(){
    char str[] = "http://c.biancheng.net";
    char *pstr = str;
    int len = strlen(str), i;

    //使用*(pstr+i)
    for(i=0; i<len; i++){
        printf("%c", *(pstr+i));
    }
    printf("\n");
  
    //使用pstr[i]
    for(i=0; i<len; i++){
        printf("%c", pstr[i]);
    }
    printf("\n");
  
    //使用*(str+i)
    for(i=0; i<len; i++){
        printf("%c", *(str+i));
    }
    printf("\n");

  	//使用str[i]
    for(i=0; i<len; i++){
        printf("%c", str[i]);
    }
    printf("\n");
    return 0;
}
```

​		除了字符数组，C语言还支持另外一种表示字符串的方法，就是直接使用一个指针指向字符串

```c
char *str = "http://c.biancheng.net";
char *str;
str = "http://c.biancheng.net";
```

```c
#include <stdio.h>
#include <string.h>

int main(){
    char *str = "http://c.biancheng.net";
    int len = strlen(str), i;
   
    //直接输出字符串
    printf("%s\n", str);
    //使用*(str+i)
    for(i=0; i<len; i++){
        printf("%c", *(str+i));
    }
    printf("\n");
    //使用str[i]
    for(i=0; i<len; i++){
        printf("%c", str[i]);
    }
    printf("\n");

    return 0;
}
```

​		上面两种根本的区别是**在内存中的存储区域不一样**，字符数组存储在全局数据区或栈区，指针指向字符串形式的字符串存储在常量区。全局数据区和栈区的字符串（也包括其他数据）有读取和写入的权限，而常量区的字符串（也包括其他数据）只有读取权限，没有写入权限。

​		内存权限的不同导致的一个明显结果就是，字符数组在定义后可以读取和修改每个字符，而对于指针指向字符串形式的字符串，一旦被定义后就只能读取不能修改，任何对它的赋值都是错误的。（不能赋值其中某个字符！！！）

```c
#include <stdio.h>
int main(){
    char *str = "Hello World!";
    str = "I love C!";  //正确
    str[3] = 'P';  //错误
    return 0;
}
```

```c
#include <stdio.h>
#include <stdlib.h>

int main(){
    char str[20] = {0};
    int i;
    for(i=0; i<10; i++){
        *(str+i) = 97+i;  // 97为字符a的ASCII码值
    }
    printf("%s\n", str);//abcdefghij
    printf("%s\n", str+2);//cdefghij
    printf("%c\n", str[2]);//c
    printf("%c\n", (str+2)[2]);//e
    return 0;
}
```

​		如果是%s那么是从指针开始的位置到'\0'中间的字符串。



### 7、指针用作函数的参数

​		传入函数的参数不仅可以是整数、小数、字符等具体的数据，还可以是指向它们的[指针](http://c.biancheng.net/c/80/)。用指针变量作函数参数可以将函数外部的地址传递到函数内部，使得在函数内部可以操作函数外部的数据，并且这些数据不会随着函数的结束而被销毁。（不用return来得到结果。）

```c
//以下的形式是一样的
void func(int *parr){ ...... }
void func(int arr[]){ ...... }
void func(int arr[5]){ ...... }
```

​		数组是一系列数据的集合，无法通过参数将它们一次性传递到函数内部，如果希望在函数内部操作数组，必须传递数组指针。参数 intArr 仅仅是一个数组指针，在函数内部无法通过这个指针获得数组长度，必须将数组长度作为函数参数传递到函数内部。

```c
#include <stdio.h>

int max(int *intArr, int len){     //int max(int intArr[], int len){
    int i, maxValue = intArr[0];  //假设第0个元素是最大值
    for(i=1; i<len; i++){
        if(maxValue < intArr[i]){
            maxValue = intArr[i];
        }
    }
   
    return maxValue;
}

int main(){
    int nums[6], i;
    int len = sizeof(nums)/sizeof(int);
    //读取用户输入的数据并赋值给数组元素
    for(i=0; i<len; i++){
        scanf("%d", nums+i);
    }
    printf("Max value is %d!\n", max(nums, len));

    return 0;
}
```

​		`int intArr[6]`这种形式只能说明函数期望用户传递的数组有 6 个元素，并不意味着数组只能有 6 个元素，真正传递的数组可以有少于或多于 6 个的元素。



### 8、指针用作函数的返回值

​		C语言允许函数的返回值是一个指针（地址），我们将这样的函数称为指针函数。下面的例子定义了一个函数 strlong()，用来返回两个字符串中较长的一个：

```c
#include <stdio.h>
#include <string.h>

char *strlong(char *str1, char *str2){
    if(strlen(str1) >= strlen(str2)){
        return str1;
    }else{
        return str2;
    }
}

int main(){
    char str1[30], str2[30], *str;
    gets(str1);
    gets(str2);
    str = strlong(str1, str2);
    printf("Longer string: %s\n", str);

    return 0;
}
```

​		用指针作为函数返回值时需要注意的一点是，函数运行结束后会销毁在它内部定义的所有局部数据，包括局部变量、局部数组和形式参数，函数返回的指针请尽量不要指向这些数据，C语言没有任何机制来保证这些数据会一直有效，它们在后续使用过程中可能会引发运行时错误。



### 9、C语言二级指针（指向指针的指针）

​		定义：指针可以指向一份普通类型的数据，例如 int、double、char 等，也可以指向一份指针类型的数据，例如 int *、double *、char * 等。如果一个指针指向的是另外一个指针，我们就称它为二级指针，或者指向指针的指针。C语言不限制指针的级数，每增加一级指针，在定义指针变量时就得增加一个星号`*`。p1 是一级指针，指向普通类型的数据，定义时有一个`*`；p2 是二级指针，指向一级指针 p1，定义时有两个`*`。

```c
int a =100;
int *p1 = &a;
int **p2 = &p1;
int ***p3 = &p2;//***p3等价于*(*(*p3))
int ****p4 = &p3;
```

​		p3 得到的是 p2 的值，也即 p1 的地址；(p3) 得到的是 p1 的值，也即 a 的地址；经过三次“取值”操作后，((p3)) 得到的才是 a 的值。



### 10、C语言空指针NULL以及void指针

```c
#include <stdio.h>

int main(){
    char *str = NULL;
    gets(str);
    printf("%s\n", str);
    return 0;
}
```

​		运行程序后发现，还未等用户输入任何字符，printf() 就直接输出了`(null)`。我们有理由据此推断，gets() 和 printf() 都对空指针做了特殊处理：

​		gets() 不会让用户输入字符串，也不会向指针指向的内存中写入数据；

​		printf() 不会读取指针指向的内容，只是简单地给出提示，让程序员意识到使用了一个空指针。



​		`void *`表示一个有效指针，它确实指向实实在在的数据，只是数据的类型尚未确定，在后续使用过程中一般要进行强制类型转换。C语言动态内存分配函数 malloc() 的返回值就是`void *`类型，在使用时要进行强制类型转换。

```c
#include <stdio.h>

int main(){
    //分配可以保存30个字符的内存，并把返回的指针转换为 char *
    char *str = (char *)malloc(sizeof(char) * 30);
    gets(str);
    printf("%s\n", str);
    return 0;
}
```



### 11、数组和指针绝不等价，数组是另外一种类型

​		数组和指针不等价的一个典型案例就是求数组的长度，这个时候只能使用数组名，不能使用数组指针。

```c
#include <stdio.h>

int main(){
    int a[6] = {0, 1, 2, 3, 4, 5};
    int *p = a;
    int len_a = sizeof(a) / sizeof(int);
    int len_p = sizeof(p) / sizeof(int);
    printf("len_a = %d, len_p = %d\n", len_a, len_p);
    return 0;
}
//len_a = 6, len_p = 1
```

​		数组是一系列数据的集合，没有开始和结束标志，p 仅仅是一个指向 int 类型的指针，编译器不知道它指向的是一个整数还是一堆整数，对 p 使用 sizeof 求得的是指针变量本身的长度。也就是说，编译器并没有把 p 和数组关联起来，p 仅仅是一个指针变量，不管它指向哪里，sizeof 求得的永远是它本身所占用的字节数。

​		对数组的引用 a[i] 在编译时总是被编译器改写成`*(a+i)`的形式，C语言标准也要求编译器必须具备这种行为。



### 12、C语言指针数组（数组每个元素都是指针）

​		如果一个数组中的所有元素保存的都是[指针](http://c.biancheng.net/c/80/)，那么我们就称它为指针数组。指针数组的定义形式一般为：

```c
dataType *arrayName[length];//[ ]的优先级高于*，该定义形式应该理解为：dataType *(arrayName[length]);
```

```c
#include <stdio.h>
int main(){
    char *str[3] = {
        "c.biancheng.net",
        "C语言中文网",
        "C Language"
    };
    printf("%s\n%s\n%s\n", str[0], str[1], str[2]);
    return 0;
}
```

```c
#include <stdio.h>
int main(){
    char *str0 = "c.biancheng.net";
    char *str1 = "C语言中文网";
    char *str2 = "C Language";
    char *str[3] = {str0, str1, str2};
    printf("%s\n%s\n%s\n", str[0], str[1], str[2]);
    return 0;
}
```



### 13、指针数组和二级指针

```c
		char *string0 = "COSC1283/1284";
    char *string1 = "Programming";
    char *string2 = "Techniques";
    char *string3 = "is";
    char *string4 = "great fun";
   
    char *lines[5];
    lines[0] = string0;
    lines[1] = string1;
    lines[2] = string2;
    lines[3] = string3;
    lines[4] = string4;
```

​		`char *lines[5]`定义了一个指针数组，它的每个元素的类型都是`char *`。在表达式中使用 lines 时，它会转换为一个类型为`char **`的指针，这样`*lines`就表示一个指向字符的指针，而`**lines`表示一个具体的字符。



### 14、C语言二维数组指针（指向二维数组的指针）

```c
int *(p1[5]);  //指针数组，可以去掉括号直接写作 int *p1[5];
int (*p2)[5];  //二维数组指针，不能去掉括号
```



### 15、C语言函数指针

​		我们可以把函数的这个首地址（或称入口地址）赋予一个[指针](http://c.biancheng.net/c/80/)变量，使指针变量指向函数所在的内存区域，然后通过指针变量就可以找到并调用该函数。这种指针就是函数指针。

```c
returnType (*pointerName)(param list);
```

​		returnType 为函数返回值类型，pointerName 为指针名称，param list 为函数参数列表。参数列表中可以同时给出参数的类型和名称，也可以只给出参数的类型，省略参数的名称，这一点和函数原型非常类似。

```c
#include <stdio.h>

//返回两个数中较大的一个
int max(int a, int b){
    return a>b ? a : b;
}

int main(){
    int x, y, maxval;
    //定义函数指针
    int (*pmax)(int, int) = max;  //也可以写作int (*pmax)(int a, int b)
    printf("Input two numbers:");
    scanf("%d %d", &x, &y);
    maxval = (*pmax)(x, y);
    printf("Max value: %d\n", maxval);

    return 0;
}
```

​		maxval = (*pmax)(x, y);对函数进行了调用。pmax 是一个函数指针，在前面加 * 就表示对它指向的函数进行调用。注意`( )`的优先级高于`*`，第一个括号不能省略。



### 16、C语言指针总结

```c
int *p1[6];  //指针数组
int *(p2[6]);  //指针数组，和上面的形式等价
int (*p3)[6];  //二维数组指针
int (*p4)(int, int);  //函数指针
```

​		int *p1[6];  //指针数组

​		从 p1 开始理解，它的左边是 *，右边是 [ ]，[ ] 的优先级高于 *，所以编译器先解析`p1[6]`，p1 首先是一个拥有 6 个元素的数组，然后再解析`int *`，它用来说明数组元素的类型。从整体上讲，p1 是一个拥有 6 个 int * 元素的数组，也即指针数组。



​		int (*p3)[6];  //二维数组指针

​		从 p3 开始理解，( ) 的优先级最高，编译器先解析`(*p3)`，p3 首先是一个指针，剩下的`int [6]`是 p3 指向的数据的类型，它是一个拥有 6 个元素的一维数组。从整体上讲，p3 是一个指向拥有 6 个 int 元素数组的指针，也即二维数组指针。



​		int (*p4)(int, int);  //函数指针

​		从 p4 开始理解，( ) 的优先级最高，编译器先解析`(*p4)`，p4 首先是一个指针，它后边的 ( ) 说明 p4 指向的是一个函数，括号中的`int, int`是参数列表，开头的`int`用来说明函数的返回值类型。整体来看，p4 是一个指向原型为`int func(int, int);`的函数的指针。



| 定  义       | 含  义                                                       |
| ------------ | ------------------------------------------------------------ |
| int *p;      | p 可以指向 int 类型的数据，也可以指向类似 int arr[n] 的数组。 |
| int **p;     | p 为二级指针，指向 int * 类型的数据。                        |
| int *p[n];   | p 为指针数组。[ ] 的优先级高于 *，所以应该理解为 int *(p[n]); |
| int (*p)[n]; | p 为[二维数组](http://c.biancheng.net/c/array/)指针。        |
| int *p();    | p 是一个函数，它的返回值类型为 int *。                       |
| int (*p)();  | p 是一个函数指针，指向原型为 int func() 的函数。             |

1) 指针变量可以进行加减运算，例如`p++`、`p+i`、`p-=i`。指针变量的加减运算并不是简单的加上或减去一个整数，而是跟指针指向的数据类型有关。

2) 给指针变量赋值时，要将一份数据的地址赋给它，不能直接赋给一个整数，例如`int *p = 1000;`是没有意义的，使用过程中一般会导致程序崩溃。

3) 使用指针变量之前一定要初始化，否则就不能确定指针指向哪里，如果它指向的内存没有使用权限，程序就崩溃了。对于暂时没有指向的指针，建议赋值`NULL`。

4) 两个指针变量可以相减。如果两个指针变量指向同一个数组中的某个元素，那么相减的结果就是两个指针之间相差的元素个数。

5) 数组也是有类型的，数组名的本意是表示一组类型相同的数据。在定义数组时，或者和 sizeof、& 运算符一起使用时数组名才表示整个数组，表达式中的数组名会被转换为一个指向数组的指针。



## 九、C语言结构体

### 1、定义

​		在C语言中，可以使用**结构体（Struct）**来存放一组不同类型的数据。结构体的定义形式为：

```c
//struct 结构体名{
//    结构体所包含的变量或数组
//};
struct stu{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在学习小组
    float score;  //成绩
};				//注意大括号后面的分号;不能少，这是一条完整的语句。
```

​		stu 为结构体名，它包含了 5 个成员，分别是 name、num、age、group、score。结构体成员的定义方式与变量和数组的定义方式相同，只是不能初始化。



### 2、结构体变量

```c
struct stu stu1, stu2;
```

​		定义了两个变量 stu1 和 stu2，它们都是 stu 类型，都由 5 个成员组成。注意关键字`struct`不能少。

​		也可以在定义结构体的同时定义结构体变量：

```c
struct stu{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在学习小组
    float score;  //成绩
} stu1, stu2;		//将变量放在结构体定义的最后即可。
```



### 3、成员的获取和赋值

结构体和数组类似，也是一组数据的集合，整体使用没有太大的意义。数组使用下标`[ ]`获取单个元素，结构体使用点号`.`获取单个成员。获取结构体成员的一般格式为：结构体变量名.成员名;

```c
    stu1.name = "Tom";
    stu1.num = 12;
    stu1.age = 18;
    stu1.group = 'A';
    stu1.score = 136.5;

    //读取结构体成员的值
    printf("%s的学号是%d，年龄是%d，在%c组，今年的成绩是%.1f！\n", stu1.name, stu1.num, stu1.age, stu1.group, stu1.score);
```

```c
struct{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在小组
    float score;  //成绩
} stu1, stu2 = { "Tom", 12, 18, 'A', 136.5 };
```



### 4、C语言结构体数组

```c
struct stu{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在小组 
    float score;  //成绩
}class[5];
```

```c
//初始化
struct stu{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在小组 
    float score;  //成绩
}class[5] = {       //5也可以不写，不给出数据长度
    {"Li ping", 5, 18, 'C', 145.0},
    {"Zhang ping", 4, 19, 'A', 130.5},
    {"He fang", 1, 18, 'A', 148.5},
    {"Cheng ling", 2, 17, 'F', 139.0},
    {"Wang ming", 3, 17, 'B', 144.5}
};


class[0].group = 'B';//修改 Li ping 的学习小组
```



### 5、C语言结构体指针

​		定义

```c
struct stu{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在小组
    float score;  //成绩
} stu1 = { "Tom", 12, 18, 'A', 136.5 };
//结构体指针
struct stu *pstu = &stu1;
```

​		也可以

```c
struct stu{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在小组
    float score;  //成绩
} stu1 = { "Tom", 12, 18, 'A', 136.5 }, *pstu = &stu1;
```

​		结构体变量名和数组名不同，数组名在表达式中会被转换为数组指针，而结构体变量名不会，无论在任何表达式中它表示的都是整个集合本身，要想取得结构体变量的地址，必须在前面加`&`，所以给 pstu 赋值只能写作：` struct stu *pstu = &stu1; `

​		通过结构体指针可以获取结构体成员，一般形式为：`(*pointer).memberName`

​		或者`pointer->memberName`

```c
#include <stdio.h>
int main(){
    struct{
        char *name;  //姓名
        int num;  //学号
        int age;  //年龄
        char group;  //所在小组
        float score;  //成绩
    } stu1 = { "Tom", 12, 18, 'A', 136.5 }, *pstu = &stu1;

    //读取结构体成员的值
    printf("%s的学号是%d，年龄是%d，在%c组，今年的成绩是%.1f！\n", (*pstu).name, (*pstu).num, (*pstu).age, (*pstu).group, (*pstu).score);
    printf("%s的学号是%d，年龄是%d，在%c组，今年的成绩是%.1f！\n", pstu->name, pstu->num, pstu->age, pstu->group, pstu->score);

    return 0;
}
```



### 6、结构体指针作为函数参数

​		结构体变量名代表的是整个集合本身，作为函数参数时传递的整个集合，也就是所有成员，而不是像数组一样被编译器转换成一个指针。如果结构体成员较多，尤其是成员为数组时，传送的时间和空间开销会很大，影响程序的运行效率。所以最好的办法就是使用结构体指针，这时由实参传向形参的只是一个地址，非常快速。

```c
#include <stdio.h>

struct stu{
    char *name;  //姓名
    int num;  //学号
    int age;  //年龄
    char group;  //所在小组
    float score;  //成绩
}stus[] = {
    {"Li ping", 5, 18, 'C', 145.0},
    {"Zhang ping", 4, 19, 'A', 130.5},
    {"He fang", 1, 18, 'A', 148.5},
    {"Cheng ling", 2, 17, 'F', 139.0},
    {"Wang ming", 3, 17, 'B', 144.5}
};

void average(struct stu *ps, int len);

int main(){
    int len = sizeof(stus) / sizeof(struct stu);
    average(stus, len);
    return 0;
}

void average(struct stu *ps, int len){
    int i, num_140 = 0;
    float average, sum = 0;
    for(i=0; i<len; i++){
        sum += (ps + i) -> score;
        if((ps + i)->score < 140) num_140++;
    }
    printf("sum=%.2f\naverage=%.2f\nnum_140=%d\n", sum, sum/5, num_140);
}
```



### 7、C语言枚举类型（C语言enum用法）

```c
#include <stdio.h>

int main(){
    enum week{ Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun } day;
    scanf("%d", &day);
    switch(day){
        case Mon: puts("Monday"); break;
        case Tues: puts("Tuesday"); break;
        case Wed: puts("Wednesday"); break;
        case Thurs: puts("Thursday"); break;
        case Fri: puts("Friday"); break;
        case Sat: puts("Saturday"); break;
        case Sun: puts("Sunday"); break;
        default: puts("Error!");
    }
    return 0;
}
```

​		枚举列表中的 Mon、Tues、Wed 这些标识符的作用范围是全局的（严格来说是 main() 函数内部），不能再定义与它们名字相同的变量。Mon、Tues、Wed 等都是常量，不能对它们赋值，只能将它们的值赋给其他的变量。

​		枚举和宏其实非常类似：宏在预处理阶段将名字替换成对应的值，枚举在编译阶段将名字替换成对应的值。我们可以将枚举理解为编译阶段的宏。

​		Mon、Tues、Wed 这些名字都被替换成了对应的数字。这意味着，Mon、Tues、Wed 等都不是变量，它们不占用数据区（常量区、全局数据区、栈区和堆区）的内存，而是直接被编译到命令里面，放到代码区，所以不能用`&`取得它们的地址。这就是枚举的本质。



### 8、C语言共用体（C语言union用法）

​		共用体在一般的编程中应用较少，在单片机中应用较多。



### 9、位运算

| 运算符 | &      | \|     | ^        | ~    | <<   | >>   |
| ------ | ------ | ------ | -------- | ---- | ---- | ---- |
| 说明   | 按位与 | 按位或 | 按位异或 | 取反 | 左移 | 右移 |













