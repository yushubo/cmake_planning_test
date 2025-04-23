cmake_minimum_required(VERSION 3.29.0)
project(planning)
set(CMAKE_CXX_STANDARD 17)
#设置可执行文件和动态库输出路径  动态库dll和exe都放在bin目录下
#CMAKE_RUNTIME_OUTPUT_DIRECTORY  这个设置适用于windows平台
#CMAKE_LIBRARY_OUTPUT_DIRECTORY  这个设置适用于Linux平台 设置动态库和可执行文件生成目录
#CMAKE_LIBRARY_OUTPUT_DIRECTORY  这个设置适用于Linux平台 但是只设置静态库，不会管可执行文件
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)  #这个设置适用于windows平台


#动态库
#获取源文件目录
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LIST)
#生成动态链接库文件
add_library(common
    SHARED
    ${SRC_LIST}
)
#设置动态库包含的头文件目录
include_directories(common
    PUBLIC
    ${PROJECT_SOURCE_DIR}/include
)

#可执行文件
#生成可执行文件
add_executable(planning_main planning_main.cpp)
#设置可执行文件包含的头文件目录
include_directories(planning_main
    PUBLIC
    ${PROJECT_SOURCE_DIR}/include
)

#链接
#可执行文件链接动态库
target_link_libraries(planning_main
    PUBLIC
    common
)


