# cordova

## cordova简介
1. codovaiOS9之后加载网页使用的是Wkwebview大大的减少了内存的占用。

## 在原有的项目里添加cordova
1. 安装一些插件
  1. 安装Node.js命令 ：brew install node
  1. 安装cordova命令： sudo npm install–g cordova
  1. 创建一个叫CordovaDemo的ios工程 命令：cordova create cordovaDemo com.example.cordovaDemo CordovaDemo
1. 然后添加平台支持，以iOS为例子
  * 添加iOS端 命令：cordova platform add ios
  * 这样在platforms中会多一个ios的文件夹以及内容
1. 将cordova的相关文件copy到自己的工程中： cordova,CordovaLib,platform_www ,www
1. 将CordovaLib.xcodeproj 添加到DemoTest工程中，右键选择Add Files To 你的工程名
1. 添加www到工程中，勾选Create folder references
1. 添加config.xml到工程中
1. 工程中BuildSettings->Other Link Flags设置-Objc -all_load
1. 选择BuildPhases->New Run Script Phase，将新增New Run Script Phase命名为copy www directory
1. 粘贴到下面的方框
```
NODEJS_PATH=/usr/local/bin;NVM_NODE_PATH=~/.nvm/versions/node/`nvm version 2>/dev/null`/bin; N_NODE_PATH=`find/usr/local/n/versions/node/* -maxdepth 0-type d 2>/dev/null | tail -1`/bin; XCODE_NODE_PATH=`xcode-select--print-path`/usr/share/xcs/Node/bin;PATH=$NODEJS_PATH:$NVM_NODE_PATH:$N_NODE_PATH:$XCODE_NODE_PATH:$PATH &&node cordova/lib/copy-www-build-step.js
```
1. Build Phases->Link Binary WithLibraries中添加libCordova.a,MobileCoreServices,AssetsLibrary
1. BuildSettings->HeaderSearch Paths 中添加$(OBJROOT)/UninstalledProducts/include解决该问题连接.（如果不添加这步会报错：Cordova/CDVViewController.h file not found)

1. 配置项目
config.xml 文件的配置，插件的制作和使用

## 参考
* http://blog.csdn.net/u011619283/article/details/52700601
