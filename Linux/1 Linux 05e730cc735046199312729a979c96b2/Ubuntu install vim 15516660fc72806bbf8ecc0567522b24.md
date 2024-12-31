# Ubuntu install vim

## **1. 安装Vim**

Ubuntu默认可能带有轻量级的`vim-tiny`，建议安装完整版本的Vim。

1. 更新系统软件包列表：
    
    ```bash
    sudo apt update
    ```
    
2. 安装完整的Vim：
    
    ```bash
    sudo apt install vim -y
    ```
    
3. 验证安装：
    
    ```bash
    vim --version
    ```
    
    如果输出中显示`+syntax`，说明支持完整的Vim功能。
    

---

---

## **3. Vim的基本配置**

为更好地使用Vim，可以为`root`用户和普通用户设置通用配置。

### **3.1 创建配置文件**

编辑`vimrc`文件（所有用户通用）：

```bash
sudo vim /etc/vim/vimrc

```

或者编辑单个用户的配置文件：

```bash
vim ~/.vimrc

```

### **3.2 推荐的配置内容**

```
" 启用语法高亮
syntax on

" 设置行号
set number

" 显示匹配的括号
set showmatch

" 设置缩进
set tabstop=4
set shiftwidth=4
set expandtab

" 启用搜索高亮
set hlsearch

" 实时显示搜索结果
set incsearch

" 自动换行
set wrap

```

保存后，重新打开Vim即可生效。