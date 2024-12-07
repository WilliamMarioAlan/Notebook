# lambda expression(匿名函数）

Lambda 表达式（也称为匿名函数）是 C++11 中引入的一种简洁的方式来定义函数对象。它们可以捕获周围作用域中的变量，并允许在需要传递函数或回调的地方使用。这是一个简短但功能强大的特性，特别适用于需要在短时间内定义小型函数的场合，如排序、查找、算法等。

### Lambda 表达式的基本语法

```cpp
[capture](parameters) -> return_type { body }
```

- **capture**：捕获列表，用于指定哪些外部变量可以在 lambda 表达式中使用。
- **parameters**：参数列表，与普通函数参数列表类似。
- **return_type**：返回类型，可选。如果可以从 `body` 推断出返回类型，可以省略。
- **body**：函数体，包含具体的操作。

### 详细解释

### 1. 捕获列表（Capture List）

捕获列表用于指定 lambda 表达式可以使用哪些外部变量。可以按值捕获，也可以按引用捕获：

- [ ]  `[ ]`：不捕获任何外部变量。
- [ ]  `[x]`：按值捕获变量 `x`。
- `[&x]`：按引用捕获变量 `x`。
- `[=]`：按值捕获所有外部变量。
- `[&]`：按引用捕获所有外部变量。
- `[this]`：捕获当前对象的 `this` 指针（适用于类成员函数）。

### 2. 参数列表（Parameters）

参数列表与普通函数的参数列表类似：

- `(int a, int b)`：两个整型参数 `a` 和 `b`。
- `()`：无参数。

### 3. 返回类型（Return Type）

返回类型可以省略，如果可以从函数体中推断出来。否则，使用 `-> return_type` 指定返回类型：

- `> int`：返回类型为 `int`。
- 省略：编译器自动推断。

### 4. 函数体（Body）

函数体包含具体的操作，与普通函数的函数体类似。

### 示例

### 示例 1：简单的 Lambda 表达式

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // 包含 std::sort

int main() {
    std::vector<int> numbers = {5, 2, 9, 1, 5, 6};

    // 使用 lambda 表达式进行升序排序
    std::sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return a < b;
    });

    // 输出排序后的向量
    for (int n : numbers) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    return 0;
}

```

### 示例 2：捕获外部变量

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // 包含 std::sort

int main() {
    std::vector<int> numbers = {5, 2, 9, 1, 5, 6};
    int threshold = 4;

    // 使用 lambda 表达式，按值捕获 threshold
    numbers.erase(std::remove_if(numbers.begin(), numbers.end(), [threshold](int n) {
        return n < threshold;
    }), numbers.end());

    // 输出筛选后的向量
    for (int n : numbers) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    return 0;
}

```

### 示例 3：按引用捕获外部变量并修改

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // 包含 std::sort

int main() {
    std::vector<int> numbers = {5, 2, 9, 1, 5, 6};
    int increment = 10;

    // 使用 lambda 表达式，按引用捕获 increment 并修改它
    std::for_each(numbers.begin(), numbers.end(), [&increment](int &n) {
        n += increment;
    });

    // 输出修改后的向量
    for (int n : numbers) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    return 0;
}

```

### 示例 4：带有返回类型的 Lambda 表达式

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // 包含 std::sort

int main() {
    std::vector<int> numbers = {5, 2, 9, 1, 5, 6};

    // 使用 lambda 表达式指定返回类型
    std::sort(numbers.begin(), numbers.end(), [](int a, int b) -> bool {
        return a > b; // 降序排序
    });

    // 输出排序后的向量
    for (int n : numbers) {
        std::cout << n << " ";
    }
    std::cout << std::endl;

    return 0;
}

```

### 总结

- **捕获列表**：指定 lambda 表达式可以使用哪些外部变量，可以按值捕获或按引用捕获。
- **参数列表**：与普通函数的参数列表类似。
- **返回类型**：如果可以从函数体中推断出来，可以省略，否则使用 `> return_type` 指定。
- **函数体**：包含具体的操作。

Lambda 表达式在 C++ 中非常强大和灵活，可以用于各种场合，如排序、查找、算法等场景中，非常方便快捷。通过以上示例，你可以快速掌握 lambda 表达式的基本用法和高级用法。