# 安装

## 安装
1. [CentOS安装Python3.6](http://blog.csdn.net/u011404495/article/details/54883310)
1. [Ubuntu安装Python3.5](http://blog.csdn.net/bebemo/article/details/51350484)

## 语法
1. 获取环境变量：os.getenv('INTRANET_HOST')

## 命令
```
python3, exit()
pip3 install
```

## pip
### 安装
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python get-pip.py
```

### 使用
```
pip list
pip show numpy
```

### 安装基于pip的软件包
* pip -vvv install python-scipy // -vvv详细信息
* pip --trusted-host pypi.python.org install requests // --trusted-host 信任网站
* pip install jinja2==2.3 # 指定软件的版本升级

## conda
* python环境，可以有不同的python和库
```
conda info --envs // 看所有环境
source activate xyz // 创建环境xyz
```
