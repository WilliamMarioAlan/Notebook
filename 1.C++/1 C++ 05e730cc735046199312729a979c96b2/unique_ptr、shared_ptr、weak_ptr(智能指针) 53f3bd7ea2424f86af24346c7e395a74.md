# unique_ptr、shared_ptr、weak_ptr(智能指针)

### **`std::unique_ptr`**

**`std::unique_ptr`**是独占所有权的智能指针，它确保一个对象只有一个所有者。它不能被复制，但可以通过**`std::move`**进行移动。

### **`std::shared_ptr`**

**`std::shared_ptr`**是共享所有权的智能指针，多个**`std::shared_ptr`**可以共享同一个对象。当最后一个**`std::shared_ptr`**销毁时，对象才会被释放。

### **`std::weak_ptr`**

**`std::weak_ptr`**是一种不控制对象生命周期的智能指针，通常用于解决**`std::shared_ptr`**之间循环引用的问题。它必须从一个**`std::shared_ptr`**构造，可以通过调用**`lock`**方法获得一个指向该对象的**`std::shared_ptr`**。