# 当private member中含有pointer

在 C++ 中，当类中有指向动态内存的指针（即指针成员变量）时，通常需要自己编写以下三个函数以确保类的正确行为和内存管理：

1. **拷贝构造函数**（Copy Constructor）
2. **赋值运算符重载**（Copy Assignment Operator）
3. **析构函数**（Destructor）

这三个函数通常被称为“三大法则”（Rule of Three）。如果类中有资源管理（例如，指向动态内存的指针），而没有正确管理这些资源，就可能导致内存泄漏、双重释放（double free）等问题。

下面是一个包含指针成员变量的类示例，以及如何实现“三大法则”：

```cpp
#include <iostream>
#include <cstring>

class MyClass {
private:
    char* data;
    
public:
    // 默认构造函数
    MyClass(const char* str = "") {
        data = new char[strlen(str) + 1];
        strcpy(data, str);
    }

    // 拷贝构造函数
    MyClass(const MyClass& other) {
        data = new char[strlen(other.data) + 1];
        strcpy(data, other.data);
    }

    // 赋值运算符重载
    MyClass& operator=(const MyClass& other) {
        if (this == &other) return *this; // 防止自我赋值
        delete[] data; // 释放已有的资源
        data = new char[strlen(other.data) + 1];
        strcpy(data, other.data);
        return *this;
    }

    // 析构函数
    ~MyClass() {
        delete[] data;
    }

    // 一个打印内容的函数
    void print() const {
        std::cout << data << std::endl;
    }
};

int main() {
    MyClass obj1("Hello");
    MyClass obj2 = obj1; // 调用拷贝构造函数
    MyClass obj3;
    obj3 = obj1; // 调用赋值运算符重载

    obj1.print();
    obj2.print();
    obj3.print();

    return 0;
}

```

### 解释

1. **默认构造函数**：在初始化对象时为 `data` 分配动态内存并复制字符串。
2. **拷贝构造函数**：在使用另一个对象初始化新对象时被调用。它为新对象分配新的动态内存，并复制源对象的数据。
3. **赋值运算符重载**：在将一个对象赋值给另一个现有对象时被调用。它首先检查自我赋值，然后释放现有对象的内存，分配新的动态内存，并复制源对象的数据。
4. **析构函数**：在对象销毁时被调用。它释放分配给 `data` 的动态内存。

通过正确实现这些函数，确保了 `MyClass` 对象的动态内存管理是安全和正确的，防止了内存泄漏和其他潜在问题。