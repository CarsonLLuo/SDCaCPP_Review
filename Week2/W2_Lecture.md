# 1. Functions

## Syntax

```c++
Return_type/void function_name(Arg_List){
	Function body;
}
```

1. **Return_type（返回类型）：** 这是指函数执行完毕后返回的数据类型。在你的例子中，返回类型是`int`，意味着函数会返回一个整数值。
2. **function_name（函数名）：** 这是函数的标识符，你可以通过这个名字来调用函数。在你的例子中，函数名是`TestFunction`。
3. **Arg_List（参数列表）：** 这是函数接受的输入值列表，参数是在函数被调用时传递给函数的值。在你的语法中，参数列表是用逗号分隔的参数，例如`int x`，这意味着函数接受一个整数作为参数。
4. **Function body（函数体）：** 这是函数的实际代码块，包含了函数的具体逻辑。在你的例子中，函数体是`return x+1;`，表示函数的任务是将输入的整数参数加一，并将结果返回。

## Example

```C++
int TestFunction(int x){
	return x+1;
}
```

# Passing Parameters

In C and C++ there are two methods of passing parameters to a function: Pass by value（按值传递） and Pass by reference（按引用传递）

1. **按值传递（Pass by value）：**
   - 参数的副本被传递给函数。函数内部使用的是参数的副本，而不是原始参数本身。
   - 函数内部无法修改原始参数的值，因为它只是操作参数的副本。
   - 这种传递方式保护了原始参数的值，确保在函数内部不会意外地修改外部的数据。
2. **按引用传递（Pass by reference）：**
   - 参数的内存地址被传递给函数。函数内部使用的是参数的内存地址，而不是参数的副本。
   - 函数内部可以直接修改原始参数的值，因为它操作的是参数的内存地址，所以对参数的修改会反映到函数外部。
   - 这种传递方式允许函数直接修改传入的参数，对于需要在函数内部改变参数值的情况非常有用。

## Pass by Value

```C
#include <stdio.h>

int addOneTo(int x) {
    x++;
    return x;
}

int main() {
    int x = 20;
    int y = addOneTo(x);
    printf("%i\n", x); // 输出：20，因为x的值在addOneTo函数中没有被修改
    printf("%i\n", y); // 输出：21，因为addOneTo函数将x加一后返回，并赋值给了y
    return 0;
}
```

## Passing by value

```C
#include <stdio.h>
int addOneTo(int *x) {
    *x = *x + 1;
    return *x;
}
int main() {
    int x = 20;
    int y = addOneTo(&x);
    printf("%i\n", x); // 输出：21，因为x的值在addOneTo函数中被修改为21
    printf("%i\n", y); // 输出：21，因为addOneTo函数返回的值是修改后的x的值
    return 0;
}
```

1. `addOneTo` 函数接受一个整型指针作为参数（`int *x`）。这意味着它期望传递一个整数变量的内存地址。函数内部使用指针解引用操作（`*x`）来访问该内存地址上的值，将其加一，并将修改后的值保存回原始的内存地址。函数返回修改后的值。
2. 在 `main` 函数中，定义了一个整数变量 `x` 并初始化为 `20`。然后，调用 `addOneTo` 函数，将 `x` 的地址（使用取地址符 `&`）传递给函数，并将返回值赋给另一个整数变量 `y`。
3. 在 `addOneTo` 函数中，`*x = *x + 1;` 的操作将 `x` 的值加一，由于传递的是指针，这个操作会修改 `main` 函数中 `x` 的实际值。
4. 最后，程序尝试打印 `x` 和 `y` 的值。由于 `addOneTo` 函数修改了 `x` 的实际值，所以 `printf` 语句中的 `x` 输出的是修改后的值，即 `21`。`y` 的值也是 `21`，因为它接收了 `addOneTo` 函数返回的值。

### & operator

在C和C++等编程语言中，`&` 操作符（取地址操作符）用于获取变量的内存地址。

1. **获取变量的地址：**
   如果 `var` 是一个变量，那么 `&var` 将返回该变量在内存中的地址。例如，如果有一个整数变量 `x`，`&x` 将返回 `x` 的内存地址。这个地址通常以十六进制数表示。

   ```c
   int x = 10;
   int *ptr = &x; // ptr保存了变量x的地址
   ```

2. **指针变量声明：**
   在指针变量的声明中，`&` 用于指定一个指针，该指针将保存另一个变量的地址。例如，`int *ptr = &x;` 将创建一个整型指针 `ptr`，并将它初始化为变量 `x` 的地址。

   ```c
   int x = 10;
   int *ptr = &x; // ptr保存了变量x的地址
   ```

通过 `&` 操作符，程序可以在需要时获取变量的内存地址，这对于涉及指针和内存操作的情况非常有用。指针允许程序直接访问内存中的数据，这对于动态分配内存、函数参数传递以及数据结构的实现非常重要。

### * operator	

`*` 操作符有两种主要用途，分别是指针声明和解引用。

1. **指针声明：**
   在变量声明时，`*` 操作符用于定义一个指针变量。指针是一个特殊类型的变量，它存储了另一个变量的内存地址。例如，`int *ptr;` 定义了一个整型指针变量 `ptr`，它可以存储一个整数变量的地址。

   ```c
   int x = 10;
   int *ptr = &x; // ptr保存了变量x的地址
   ```

2. **解引用操作：**
   在指针变量前面放置 `*` 操作符可以用于访问指针所指向的内存地址上的值。这个过程被称为解引用。例如，`*ptr` 表示指针 `ptr` 所指向的内存地址上的值。

   ```c
   int x = 10;
   int *ptr = &x; // ptr保存了变量x的地址
   int value = *ptr; // value现在包含了ptr所指向的内存地址上的值，即x的值，也就是10
   ```

   在一些情况下，解引用操作符还可以用于修改指针所指向的内存地址上的值：

   ```c
   int x = 10;
   int *ptr = &x; // ptr保存了变量x的地址
   *ptr = 20; // 修改ptr所指向的内存地址上的值，即修改了x的值为20
   ```

这两种用途使得 `*` 操作符在指针和内存操作中非常重要。它允许程序直接访问和修改内存中的数据，这对于动态内存分配、函数参数传递以及数据结构的实现非常有用。



# Store Variable

* 创建变量：编译器分配内存空间
* 当后续引用这个变量时：
  * 可以引用变量的实际数值。这意味着你可以使用该变量存储的数据，无论是数字、文本还是其他类型的信息。
  * 可以引用变量在内存中的位置，即变量的地址或引用：
    * 通过这个地址，你可以找到存储在该变量中的实际数值。这种方式允许你直接访问变量的内存位置，以便读取或修改其中的数据。

在C++中，当你创建一个变量时，编译器会为该变量分配内存空间。例如，如果你声明一个整数变量：

```cpp
int number = 42;
```

在这个例子中，`number` 是一个整数变量，被赋值为 `42`。在内存中，编译器会分配足够的空间来存储整数值 `42`。

你可以通过变量名 `number` 引用这个整数的实际值。例如，你可以将这个值输出到屏幕上：

```cpp
#include <iostream>
using namespace std;

int main() {
    int number = 42;
    cout << "The value of number is: " << number << endl;
    return 0;
}
```

在这个例子中，`cout` 语句用于输出 `number` 的值。编译器会将 `number` 的值（即 `42`）复制到输出流，最终显示在屏幕上。

同时，你也可以通过取地址运算符 `&` 获取 `number` 变量的内存地址：

```cpp
#include <iostream>
using namespace std;

int main() {
    int number = 42;
    cout << "The address of number is: " << &number << endl;
    return 0;
}
```

在这个例子中，`&number` 返回了 `number` 变量在内存中的地址。输出语句会显示这个地址的十六进制表示形式。

当你将一个变量传递给一个函数时，必须传递该变量的**副本（copy）**，因为函数需要知道在内存中的哪个位置可以找到这个变量的值。这是因为函数在执行时需要访问这个变量的值，但为了确保程序的安全性和可预测性，不应该直接在函数内修改原始变量的值。因此，将变量的副本传递给函数，函数在副本上进行操作，不影响原始变量的值。

举例来说，假设你有一个函数 `doubleValue`，用来将一个整数变量的值加倍，并且你想要将变量 `x` 的值传递给这个函数：

```cpp
#include <iostream>
using namespace std;

void doubleValue(int num) {
    num = num * 2;
}

int main() {
    int x = 5;
    cout << "Original value of x: " << x << endl;
    
    doubleValue(x);
    
    cout << "Value of x after calling doubleValue function: " << x << endl;
    
    return 0;
}
```

在这个例子中，`x` 是一个整数变量，初始值为 `5`。当你调用 `doubleValue(x)` 时，`x` 的值被传递到 `num` 参数中。函数内部会将 `num` 的值加倍，但这不会影响到原始的 `x` 变量。因此，尽管函数内部对 `num` 进行了操作，但在 `main` 函数中输出的 `x` 的值仍然是 `5`，没有被改变。

这种传递变量副本的方式确保了函数的操作不会意外地改变原始变量的值，从而增加了程序的可维护性和安全性。

# Reference

在C和C++中，引用（reference）是一种在变量声明时创建的别名。引用允许你使用**原始变量的名称**来访问**相同的内存位置**，从而实现对**原始变量的间接访问**。引用提供了一种更直观的方法来操作变量，同时避免了复制变量值的开销。在C++中，引用通常用于函数参数、函数返回值和复杂数据结构（如类对象）。

**在C++中的引用示例：**

```cpp
#include <iostream>
using namespace std;

int main() {
    int original = 42;
    int &ref = original; // 创建一个对变量original的引用，即引用original的地址

    cout << "Original value: " << original << endl;
    cout << "Value through reference: " << ref << endl;

    ref = 99; // 通过引用修改原始变量的值
    cout << "Modified value through reference: " << original << endl;

    return 0;
}
```

**输出如下：**

```
Original value: 42
Value through reference: 42
Modified value through reference: 99
```

在这个例子中，`ref` 是对整数变量 `original` 的引用。通过引用 `ref`，我们可以直接操作 `original` 的值，而不需要使用 `original` 的名称。在修改 `ref` 的值时，`original` 的值也会被修改，因为它们实际上指向相同的内存位置。

引用的一个主要优势是在函数参数中的使用，它允许你传递参数的引用而不是参数的副本，从而避免了复制大块数据的开销，提高了程序的效率。以下是一个函数中使用引用的例子：

```cpp
#include <iostream>
using namespace std;

void modifyValue(int &num) {
    num = num * 2;
}

int main() {
    int x = 5;
    cout << "Original value of x: " << x << endl;

    modifyValue(x);

    cout << "Value of x after modification: " << x << endl;

    return 0;
}
```

在这个例子中，`modifyValue` 函数接受一个整数的引用作为参数，并将参数的值加倍。通过引用，函数可以直接修改 `x` 的值，而不需要返回一个新的值或通过指针操作。这种方式更直观，同时避免了指针操作所涉及的语法复杂性。

# dereferencing

在C和C++中，解除引用（dereferencing）是指使用指针访问其所指向的内存地址上的值。通过解除引用，你可以获取或修改指针指向的实际数据。在C和C++中，解除引用是通过使用星号 `*` 运算符来完成的。

在C++中，解除引用通常与指针一起使用，如下所示：

```cpp
int x = 42;
int *ptr = &x; // ptr是一个指向整数的指针，指向变量x的地址

int value = *ptr; // 解除引用ptr，获取ptr指向的内存位置上的值，即x的值（42）

*ptr = 99; // 解除引用ptr，修改ptr指向的内存位置上的值，即将x的值改为99
```

在这个例子中，`*ptr` 表示解除引用，它允许你访问指针 `ptr` 所指向的内存地址上的值。在第一行中，`*ptr` 获取了指针 `ptr` 所指向的内存位置上的值（即变量 `x` 的值），并将其赋值给 `value`。在第二行中，`*ptr` 也被用来修改指针 `ptr` 所指向的内存位置上的值，将 `x` 的值改为99。

在C语言中同样可以使用星号 `*` 运算符进行解引用，语法和上述示例类似。

需要注意的是，解引用操作需要在合法的内存地址上进行。如果你尝试在未初始化的指针上进行解引用，或者解引用一个空指针，将会导致未定义的行为。因此，在解引用之前，通常需要确保指针指向了有效的内存地址。

# Reference and Pointer

### 1. 引用（Reference）：

- **别名：** 引用是变量的别名，它提供了一个已存在变量的名称，通过该名称可以直接访问变量的值。引用在声明时必须初始化，一旦引用被初始化为某个变量，它将一直引用该变量，无法改变引用的目标。

  ```cpp
  int num = 10;
  int &ref = num; // ref是num的引用
  ```

- **语法简洁：** 引用的语法更简洁，不需要使用解引用操作符，直接使用引用就可以访问变量的值。

- **安全性：** 引用在被创建时必须初始化，并且无法在引用的生命周期中引用其他变量，这样可以避免空引用的问题。

### 2. 指针（Pointer）：

- **存储地址：** 指针是一个变量，其存储的是另一个变量的内存地址。指针可以指向任何数据类型，包括基本数据类型、对象、函数等。

  ```cpp
  int num = 10;
  int *ptr = &num; // ptr是指向num的指针
  ```

- **需要解引用：** 在使用指针访问目标变量的值时，需要使用解引用操作符`*`。

  ```cpp
  int value = *ptr; // 解引用ptr，获取存储在ptr指向地址的值（即num的值）
  ```

- **灵活性：** 指针具有更高的灵活性，可以在运行时改变指向的对象，也可以指向空（nullptr），但这也增加了一些潜在的错误和安全隐患。

# Array

在C语言中，数组（array）是一种用于存储相同数据类型的多个元素的数据结构。根据你提供的描述，当在C中声明一个数组时，编译器会执行以下操作：

1. **计算数组的总大小：** 首先，编译器会根据数组的大小（比如，20个元素）和所需的数据类型的大小来计算数组的总大小。这个大小是数组中所有元素所占内存的总和。例如，如果每个数组元素的大小是4个字节，一个包含20个元素的整数数组将占用80个字节的内存空间。

2. **在程序的静态数据区中分配内存：** 编译器会在程序的静态数据区（static data area）分配足够大小的内存，以便存储整个数组。这个内存空间在程序运行期间保持固定，即它是静态分配的，而不是在运行时动态分配的。数组的元素在这块内存中是依次排列的。

3. **存储内存地址：** 编译器会将该内存区域的起始地址存储下来。这个地址表示数组在内存中的位置。当你使用数组的变量名（例如，`scores`）时，编译器会将其解释为该内存地址，从而能够访问数组的元素。

例如，如果你声明了一个包含20个整数的数组：

```c
int scores[20];
```

编译器将会分配足够的内存空间来存储20个整数，计算出这块内存的起始地址，并将其关联到变量名`scores`。这样，当你使用`scores`时，编译器会将其解释为数组的起始地址，允许你访问数组的各个元素。

当你在C语言中声明一个数组时，你可以选择使用数组的元素类型和指定数组的大小。以下是一个整数数组的例子，它包含5个元素：

```c
#include <stdio.h>

int main() {
    // 声明一个包含5个整数的数组
    int numbers[5] = {1, 2, 3, 4, 5};
    
    // 访问数组的元素并输出它们的值
    printf("Element 0: %d\n", numbers[0]); // 输出第一个元素的值
    printf("Element 1: %d\n", numbers[1]); // 输出第二个元素的值
    printf("Element 2: %d\n", numbers[2]); // 输出第三个元素的值
    printf("Element 3: %d\n", numbers[3]); // 输出第四个元素的值
    printf("Element 4: %d\n", numbers[4]); // 输出第五个元素的值
    
    return 0;
}
```

在上面的例子中，`int numbers[5]` 声明了一个包含5个整数的数组。这个数组的元素分别是1, 2, 3, 4, 和 5。在程序中，我们使用数组的下标（从0到4）来访问不同位置的元素，并通过`printf`函数输出它们的值。数组的下标从0开始，所以`numbers[0]`表示数组的第一个元素，`numbers[1]`表示第二个元素，依此类推。

# Strings

## C

在C语言中，字符串是字符数组的一种形式，以空字符（'\0'，也称为null字符或空终止符）结尾，表示字符串的结束。字符串常用于表示文本数据。

### 字符串的声明和初始化：

在C语言中，你可以使用字符数组来表示字符串。以下是字符串的基本声明和初始化方法：

```c
char str1[] = "Hello, World!"; // 自动计算字符串长度并分配内存
char str2[12] = "Hello"; // 明确指定数组大小，并初始化部分字符串
char str3[20]; // 声明一个字符数组，稍后可以使用strcpy等函数进行赋值
```

在上述例子中，`str1`、`str2`和`str3`都是字符串。`str1`会自动分配足够的内存以存储字符串 "Hello, World!"，`str2`明确指定了数组大小为12，并初始化了部分字符串，`str3`只是声明了一个字符数组，需要在后续使用字符串赋值函数（例如`strcpy`）进行赋值。

### 字符串相关函数：

在C语言中，有许多内置的字符串处理函数，这些函数可以帮助你执行各种字符串操作。以下是其中一些常用的字符串函数：

1. **strcpy(char *dest, const char *src):** 复制字符串。将源字符串(src)的内容复制到目标字符串(dest)中。

   ```c
   char source[] = "Hello, World!";
   char destination[20];
   strcpy(destination, source);
   ```

2. **strcat(char *dest, const char *src):** 字符串连接。将源字符串(src)的内容追加到目标字符串(dest)的末尾。

   ```c
   char str1[] = "Hello, ";
   char str2[] = "World!";
   strcat(str1, str2);
   ```

3. **strlen(const char *str):** 返回字符串的长度，不包括空终止符('\0')。

   ```c
   char str[] = "Hello, World!";
   int length = strlen(str);
   ```

4. **strcmp(const char *str1, const char *str2):** 比较两个字符串。如果两个字符串相等，返回0；如果第一个字符串小于第二个字符串，返回负数；如果第一个字符串大于第二个字符串，返回正数。

   ```c
   char str1[] = "apple";
   char str2[] = "orange";
   int result = strcmp(str1, str2);
   ```

这些函数都在C标准库（`<string.h>`头文件）中定义。请确保在使用这些函数之前包含该头文件。需要注意的是，在处理字符串时，请确保足够的内存分配以存储字符串及其空终止符。

## C++

在C++中，字符串（String）是一个标准库类型，不同于C语言中的字符数组，它提供了更多的功能和便利性。C++中的字符串类型是`std::string`，它被定义在 `<string>` 头文件中。

### 声明和初始化字符串：

在C++中，你可以使用`std::string`类型来声明和初始化字符串：

```cpp
#include <string>
#include <iostream>

int main() {
    std::string str1 = "Hello, World!"; // 初始化字符串
    std::string str2("C++ String"); // 使用构造函数初始化字符串
    
    std::cout << str1 << std::endl;
    std::cout << str2 << std::endl;
    
    return 0;
}
```

### 字符串相关操作和函数：

C++的字符串类提供了丰富的操作函数，允许你进行字符串的连接、比较、查找等操作，而无需手动处理内存分配和空终止符。

1. **字符串连接：**
   ```cpp
   std::string str1 = "Hello, ";
   std::string str2 = "World!";
   std::string result = str1 + str2; // 字符串连接
   ```

2. **字符串比较：**
   ```cpp
   std::string str1 = "apple";
   std::string str2 = "orange";
   if (str1 == str2) {
       // 字符串相等
   } else {
       // 字符串不相等
   }
   ```

3. **获取字符串长度：**
   ```cpp
   std::string str = "Hello, World!";
   int length = str.length(); // 获取字符串长度
   ```

4. **查找子串：**
   ```cpp
   std::string str = "Hello, World!";
   size_t pos = str.find("World"); // 查找子串的位置
   ```

5. **提取子串：**
   ```cpp
   std::string str = "Hello, World!";
   std::string subStr = str.substr(7, 5); // 从位置7开始提取5个字符（"World"）
   ```

6. **插入和删除操作：**
   ```cpp
   std::string str = "Hello!";
   str.insert(5, " World"); // 在位置5插入字符串
   str.erase(6, 1); // 从位置6删除1个字符
   ```

这些函数是`std::string`类的成员函数，可以直接在字符串对象上调用。C++标准库还提供了更多的字符串操作函数，可以帮助你更方便地处理字符串。









