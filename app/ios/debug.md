# 调试

## 调试  
1. 普通断点调试
在代码的中间添加断点，当程序运行到这里时会暂停运行，再配合log输出异常。
1. 异常断点输出
断点的功能不限于上面所述。开发iOS知道，如果我们因为异常然后程序crash了，代码就直接跑到main.m的main函数中去了。为什么就不能跑到出现异常的代码中呢？？？异常断点就为我们解决该问题，程序就会在异常出现的那行代码终止。
通过添加Add Exception Breakpoint 这样碰到crash就可以定位到crash的地方了
1. profle检查器
最重要的也是最好使用的检测内存跟异常的工具。
通过 Product--》Profile 打开
选择leaks进行项目运行调试

## 日志打印
1. 重新定义系统的NSLog，__OPTIMIZE__ 是release 默认会加的宏

```
#ifndef __OPTIMIZE__  
#define NSLog(...) NSLog(__VA_ARGS__)  
#else  
#define NSLog(...){}  
#endif
```
1. 直接自己写#define,当release版本的时候把#define 注释掉即可

```
#define IOS_DEBUG

#ifdef IOS_DEBUG  
#define NSLog(...) NSLog(__VA_ARGS__)  
#endif  
```
1. 演示

```
#ifdef DEBUG    
# define DLog(format, ...) NSLog((@"[文件名:%s]" "[函数名:%s]" "[行号:%d]" format), __FILE__, __FUNCTION__, __LINE__, ##__VA_ARGS__);    
#else    
# define DLog(...);    
#endif    
```
这种方式需要修改项目的配置，使得在debug编译的时候，编译DLog的宏，产生详细的日志信息，而release的时候，不产生任何控制台输出
