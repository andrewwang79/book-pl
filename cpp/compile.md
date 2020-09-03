# 编译原理
## 步骤
预编译 -> 编译 -> 汇编 -> 链接

## 静态库与动态库的区别
库是编译汇编后的产物

| 项 | 说明 |
| :-: |  |
| 静态库 | 静态链接，链接时重定位。在链接阶段进入可执行程序，自身依赖的动态库需可执行程序动态加载 |
| 动态库 | 动态链接，运行重定位。运行时动态加载，可以同时被多个程序共享内存 |

* https://juejin.im/post/6844904002438561805
* https://blog.csdn.net/yzy1103203312/article/details/80821883
* [GOT PLT](https://blog.csdn.net/u011987514/article/details/67716639)
* [PIC技术](https://blog.csdn.net/loushuai/article/details/50493603)

## ELF文件
| 项 | 说明 |
| :-: |  |
| data | 已初始化的全局数据 |
| bss | 未初始化的全局数据，不分配空间，只是记录数据所需空间的大小 |
| text | 代码 |
| 堆(Heap) | 局部变量。不存在于ELF |
| 栈(Stack) | 函数调用参数。不存在于ELF |

* [ELF文件结构](http://chuquan.me/2018/05/21/elf-introduce/)
* [elf文件格式和运行时内存布局](http://blog.sina.com.cn/s/blog_4ed962ae01013vhr.html)

## 内存分配
* [内存分配(brk/mmap)](https://blog.csdn.net/yusiguyuan/article/details/39496057)
