# 知识

## 资料
* [Python之父Guido推荐的开发规范](https://www.cnblogs.com/v394435982/p/5909072.html)，[PEP8](https://www.jianshu.com/p/52f4416c267d)
* [异常](http://www.cnblogs.com/wj-1314/p/8707804.html)
* [函数注释](https://blog.csdn.net/liang19890820/article/details/74264380)
* [一篇文章搞懂Python中的进程和线程](http://yangcongchufang.com/%E9%AB%98%E7%BA%A7python%E7%BC%96%E7%A8%8B%E5%9F%BA%E7%A1%80/python-process-thread.html)
* [Python多进程使用](https://www.cnblogs.com/weiman3389/p/6044936.html)
* 某些编辑器运行时找不到系统模块，如pandas：设置系统变量PYTHONPATH="\Python\Python38\Lib\site-packages"

## 日志
* [python logging日志模块以及多进程日志](http://python.jobbole.com/87300/)，多进程时rotating会在切换时异常
* [log](http://www.zlovezl.cn/articles/replacing-print-simple-introduction-to-logging/)
* [教程](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)

## pandas
* [21天pandas入门手册(1) - 10分钟入门1](https://www.jianshu.com/p/d630c14d3ea0)
* [shutil文件操作](https://www.jianshu.com/p/b4c87aa6fd24)

## numpy
* [numpy.array](https://blog.csdn.net/sinat_34474705/article/details/74458605)

## 语法
* json字段检查 : if 'data' in result:
* 变量存在 : if data:
* log打印：print ('标题 : var1[{0}], var2[{1}]'.format(var1, var2))
* 文件操作
```
for root, dirs, files in os.walk(path):
for file in fnmatch.filter(files, '*.py'):
path=os.path.join(root,file)
```
* 执行命令：ret = os.system('ping %s' % (ip))
* 函数默认值(1是默认值)：def fn(param1 = 1):

### 集合操作
* [列表和字典](https://pythonmana.com/2021/06/20210628184617643E.html)
* [列表遍历](https://blog.csdn.net/whatday/article/details/100557888)
* 遍历int转换成str：num_list_new = [str(x) for x in num_list]

## 单元测试
```
import unittest

from pilib.src.util import pi_security

class Test(unittest.TestCase):
    def test_sha1_file(self):
        self.assertEqual('6d518be97631a3cb58fe30eab7a7e3c017a23ca7', pi_security.sha1_file('../data/_series.txt'))

    def test_byte_hex(self):
        self.assertEqual('786D616E', pi_security.byte_hex(b'xman'))

if __name__ == "__main__":
    unittest.main()
```
