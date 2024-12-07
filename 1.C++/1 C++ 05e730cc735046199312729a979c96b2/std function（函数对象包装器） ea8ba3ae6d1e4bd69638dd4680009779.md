# std::function（函数对象包装器）

`std::function` 是 C++ 标准库中提供的一个模板类，用于存储、复制和调用任意可调用对象（如普通函数、lambda 表达式、函数对象和成员函数）。它提供了一个统一的接口来处理不同类型的可调用对象，使得代码更加灵活和易于维护。

### `std::function` 的定义和用法

### 定义

`std::function` 是一个模板类，可以用来存储具有特定签名的可调用对象。例如，`std::function<void(int)>` 可以存储任何接受一个 `int` 参数并返回 `void` 的可调用对象。

```cpp
#include <iostream>
#include <functional>

void freeFunction(int x) {
    std::cout << "Free function called with " << x << std::endl;
}

int main() {
    // 定义一个 std::function 接受一个 int 参数并返回 void
    std::function<void(int)> func;

    // 将自由函数赋值给 std::function
    func = freeFunction;
    func(10);  // 输出: Free function called with 10

    // 使用 lambda 表达式
    func = [](int x) {
        std::cout << "Lambda called with " << x << std::endl;
    };
    func(20);  // 输出: Lambda called with 20

    return 0;
}

```

### 捕获外部变量的 lambda 表达式

`std::function` 特别有用的一个场景是需要捕获外部变量的 lambda 表达式：

```cpp
#include <iostream>
#include <functional>

int main() {
    int factor = 5;

    std::function<int(int)> multiply = [factor](int x) -> int {
        return x * factor;
    };

    std::cout << multiply(2) << std::endl;  // 输出: 10

    return 0;
}

```

### `std::function` 的常见用途

1. **回调函数**：在事件驱动编程或异步操作中，`std::function` 常用于定义回调函数。可以方便地将不同类型的函数（如普通函数、成员函数或 lambda 表达式）传递给需要回调的接口。
2. **存储和调用异构函数**：在模板类或通用算法中，可以使用 `std::function` 来存储和调用不同类型的函数，而不需要知道这些函数的具体类型。
3. **实现策略模式**：通过将不同策略封装为可调用对象，并使用 `std::function` 来存储和调用这些策略，可以方便地实现策略模式。
4. **递归**：在递归算法中，通过使用 `std::function` 可以方便地定义和调用递归 lambda 表达式。

### 例子：递归

以下是一个递归生成子集的例子，展示了 `std::function` 的灵活性：

```cpp
#include <iostream>
#include <vector>
#include <functional>

class Solution {
public:
    std::vector<std::vector<int>> subsets(std::vector<int>& nums) {
        std::vector<std::vector<int>> ans;
        std::vector<int> path;
        int n = nums.size();

        std::function<void(int)> dfs = [&](int i) {
            if (i == n) {
                ans.push_back(path);
                return;
            }
            dfs(i + 1);  // 不选当前元素
            path.push_back(nums[i]);
            dfs(i + 1);  // 选当前元素
            path.pop_back();  // 撤销选择
        };

        dfs(0);
        return ans;
    }
};

int main() {
    Solution solution;
    std::vector<int> nums = {1, 2, 3};
    std::vector<std::vector<int>> result = solution.subsets(nums);

    for (const auto& subset : result) {
        std::cout << "[ ";
        for (int num : subset) {
            std::cout << num << " ";
        }
        std::cout << "]\\n";
    }

    return 0;
}

```

在这个例子中，`std::function<void(int)> dfs` 用于存储捕获了外部变量的 lambda 表达式，从而实现了递归算法。

### 总结

`std::function` 是一个非常有用的工具，可以显著提高代码的灵活性和可维护性。通过使用 `std::function`，你可以将不同类型的可调用对象统一处理，使代码更加简洁和通用。