# cmake

## 项目基本配置

```cmake
cmake_minimum_required(VERSION 3.16)
project(MyProject LANGUAGES CXX)

```



## C++ 标准设置

```cmake
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)  # 必须支持该标准
set(CMAKE_CXX_EXTENSIONS OFF)        # 禁用 g++ 扩展，如使用 -std=c++17 而非 -std=gnu++17

```



## 通用模板结构

```cmake
cmake_minimum_required(VERSION 3.16)
project(MyApp LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_executable(MyApp
    src/main.cpp
    src/foo.cpp
)

target_include_directories(MyApp PRIVATE include)
target_compile_options(MyApp PRIVATE -Wall -Wextra)
```



## header-only 生成库

```cmake
cmake_minimum_required(VERSION 3.14)
project(base)

# header-only
# 接口库（INTERFACE） 是一种特殊的库类型
# 不生成任何编译产物（如 .lib、.a 文件）
# 只携带编译选项、包含路径、宏定义等，供其他 target 依赖使用
# 适合用于 header-only 的库
add_library(base INTERFACE)

# target_include_directories：给 base 库指定头文件搜索路径
# 由于 base 是 INTERFACE 类型，所以用的是 INTERFACE 关键字（不能用 PUBLIC 或 PRIVATE）
# 它设置了两个不同的路径，根据使用场景自动切换

# 1. $<BUILD_INTERFACE:...>：
# 当你在构建阶段使用这个库（比如 add_subdirectory 或 FetchContent_MakeAvailable），会使用这个路径；
# 它告诉依赖方：“你要包含这个路径”

# 2. $<INSTALL_INTERFACE:...>：
# 当你安装这个库到系统目录（比如 /usr/local/include）之后再使用，会用这个路径
# 常见于执行 make install 后，系统安装的路径
target_include_directories(base INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

```



## FetchContent 使用

```cmake
include(FetchContent)

FetchContent_Declare(
    base
    GIT_REPOSITORY https://github.com/BigMouseNie/base.git
    GIT_TAG        v1.0.0	# 可以是 commitid
)

FetchContent_MakeAvailable(base)

add_executable(myproject main.cpp)

# 让 playback-node 拿到 base 的头文件目录
# 应用 base 的编译选项 / 宏定义（如果有）
# 链接 base 的二进制库（如果它是静态/动态库）
# 如果 base 是 INTERFACE（header-only），仅处理头文件、编译选项，无需编译链接；
target_link_libraries(myproject PRIVATE base)
```

