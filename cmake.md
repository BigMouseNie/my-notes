# cmake

## 🏗️ 项目基本配置

```cmake
cmake_minimum_required(VERSION 3.16)
project(MyProject LANGUAGES CXX)

```



## 📌 C++ 标准设置

```cmake
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)  # 必须支持该标准
set(CMAKE_CXX_EXTENSIONS OFF)        # 禁用 g++ 扩展，如使用 -std=c++17 而非 -std=gnu++17

```



## 📂 通用模板结构

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