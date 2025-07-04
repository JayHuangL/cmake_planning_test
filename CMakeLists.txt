# 指定 CMake 最低版本要求，确保使用的功能可用
cmake_minimum_required(VERSION 3.20.0)

# 自动获取当前目录名称作为项目名称（例如：/path/to/my_project → 项目名=my_project）
get_filename_component(PROJECT_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)

# 设置项目名称
project(${PROJECT_NAME})

# 设置 C++ 标准为 C++17，并要求编译器强制使用该标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 设置可执行文件的输出路径为项目根目录下的 bin 目录
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)


file(GLOB_RECURSE SRC_LIST 
    ${PROJECT_SOURCE_DIR}/*.cpp      # 主源代码目录
)

# 排除 CMake 生成的目录
list(FILTER SRC_LIST EXCLUDE REGEX "${PROJECT_BINARY_DIR}/.*")

# 生成可执行文件，链接所有收集到的源文件
add_executable(${PROJECT_NAME} ${SRC_LIST})