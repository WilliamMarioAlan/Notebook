# 1.isdigit(判断是否为数字)

```cpp
bool my_isdigit(char c) {
	// 判断字符是否在 '0' 到 '9' 的 ASCII 值范围内
	return c >= '0' && c <= '9';
}
```