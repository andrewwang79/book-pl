# CMAKE
## 用法
* MESSAGE( STATUS "SOURCE_FILES = ${SOURCE_FILES}.") // 提示信息
* list(REMOVE_ITEM ${CONAN_LIBS_RELEASE} "aaa") // 移除列表项

## 资料
* [CMAKE介绍](https://www.hahack.com/codes/cmake/)
* [cmake使用示例与整理总结](https://blog.csdn.net/wzzfeitian/article/details/40963457)
* [CMAKE自定义模块](https://www.kancloud.cn/itfanr/cmake-practice/82991)
* [cmake指令详解](https://blog.csdn.net/bytxl/article/details/50635016)
* [cmake常用工程示例大集合](https://blog.csdn.net/FreeApe/article/details/52567087)
* [列表操作](https://blog.csdn.net/fuyajun01/article/details/9036477)

### 编译类型
四种：Debug Release RelWithDebInfo MinSizeRel
```
两种设置方式：
cmake -DCMAKE_BUILD_TYPE=Debug ..
SET(CMAKE_BUILD_TYPE "Debug”)
相关参数设置：
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
```

## 加入conan支持
```
编辑“CMakeLists.txt”
include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

foreach(_LIB ${CONAN_LIBS_RELEASE})
  target_link_libraries(widget optimized ${_LIB})
endforeach()
```
