# C++知识
## 编译原理
### 步骤
预编译 -> 编译 -> 汇编 -> 链接
### 静态库与动态库的区别
库是编译汇编后的产物

| 项 | 说明 |
| :-: | |
| 静态库 | 静态链接，链接时重定位。在链接阶段进入可执行程序，自身依赖的动态库需可执行程序动态加载 |
| 动态库 | 动态链接，运行重定位。运行时动态加载，可以同时被多个程序共享内存 |

* https://juejin.im/post/6844904002438561805
* https://blog.csdn.net/yzy1103203312/article/details/80821883
* [GOT PLT](https://blog.csdn.net/u011987514/article/details/67716639)
* [PIC技术](https://blog.csdn.net/loushuai/article/details/50493603)

### ELF文件
| 项 | 说明 |
| :-: | |
| data | 已初始化的全局数据 |
| bss | 未初始化的全局数据，不分配空间，只是记录数据所需空间的大小 |
| text | 代码 |
| 堆(Heap) | 局部变量。不存在于ELF |
| 栈(Stack) | 函数调用参数。不存在于ELF |

* [ELF文件结构](http://chuquan.me/2018/05/21/elf-introduce/)
* [elf文件格式和运行时内存布局](http://blog.sina.com.cn/s/blog_4ed962ae01013vhr.html)

### 内存分配
* [内存分配(brk/mmap)](https://blog.csdn.net/yusiguyuan/article/details/39496057)

## 编译安装整体流程
https://www.cnblogs.com/tinywan/p/7230039.html
1. 安装依赖库：conan install
1. 生成Makefile文件
  1. cmake .
  1. configure  
1. 编译：make -j 8
1. 安装：make install

## 工具
* 重新加载库：ldconfig /usr/local/lib
* 查看依赖库：ldd xxx.so
* 查看符号：nm xxx.so

## boost
* [C++使用Boost实现HTTP服务端——同步、异步、协程](https://blog.csdn.net/luchengtao11/article/details/100928141)
* [Boost Beast要点解析](https://blog.csdn.net/guxch/article/details/106780832)

## CMAKE
### 用法
* MESSAGE( STATUS "SOURCE_FILES = ${SOURCE_FILES}.") // 提示信息

### 资料
* [CMAKE介绍](https://www.hahack.com/codes/cmake/)
* [cmake使用示例与整理总结](https://blog.csdn.net/wzzfeitian/article/details/40963457)
* [CMAKE自定义模块](https://www.kancloud.cn/itfanr/cmake-practice/82991)
* [cmake指令详解](https://blog.csdn.net/bytxl/article/details/50635016)
* [cmake常用工程示例大集合](https://blog.csdn.net/FreeApe/article/details/52567087)

### 加入conan支持
```
编辑“CMakeLists.txt”
include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

foreach(_LIB ${CONAN_LIBS_RELEASE})
  target_link_libraries(widget optimized ${_LIB})
endforeach()
```

## conan
### 安装
```
Conan的使用需基于Python, 安装方式很简单:
pip install conan=1.17.0
```

### 常用命令
```
conan remote add <server_name> <sever_url> // 将远端conan服务器加入本地列表
conan install . -s arch=x86_64 -s os=Linux -r cloud // Linux初始化
conan install . -s arch=x86_64 -s os=Windows -r cloud // Windows初始化
conan upload rapidjson/1.1.0@Common/stable -r cloud --all // 提交
conan search -r cloud rapidjson/1.1.0@Common/stable // 查看特定库的详细信息
```

### 资料
* [Conan打包](https://www.cnblogs.com/xl2432/p/11901089.html)
* conan打包脚本：https://chromium.googlesource.com/external/github.com/google/flatbuffers/+/c0698cc33f1e534bb59c455909b88cc2726089af/conanfile.py

## UT
* [在 Visual Studio 中编写 C/C++ 单元测试](https://docs.microsoft.com/zh-cn/visualstudio/test/writing-unit-tests-for-c-cpp?view=vs-2019)
* [玩转Google开源C++单元测试框架Google Test系列(gtest)(总)](https://www.cnblogs.com/coderzh/archive/2009/04/06/1426755.html)
* Boost：https://www.jianshu.com/p/9a87918023fb
* [指定case测试](https://www.boost.org/doc/libs/1_47_0/libs/test/doc/html/utf/user-guide/runtime-config/run-by-name.html)：./ut --run_test=Suite/Case

## 规范
1. [editorconfig](https://juejin.im/post/5b9cba4c6fb9a05cf67a79a4)

## 方案
### Linux直接编译程序
```
cd 代码目录
conan install ../ -s arch=x86_64 -s os=Linux -r cloud --update
cmake .
make -j 8
```

### 在Windows开发调试Linux上运行的程序

### 库调用无效的解决
```
nm -D baseLib1.so 查看symbol
symbol找不到(有，但加了装饰)的解决：
头文件定义：
extern "C" {
double power1(double base, int exponent);
}
```
