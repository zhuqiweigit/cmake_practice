# 加入非标准库的头文件搜索路径
include_directories(../../t3/lib)

#加入非标准库的库文件搜索路径
link_directories(/Users/zhuqiwei/CLionProjects/cpp_primer/cmakePractice/t3/lib)

add_executable(main main.cpp)

#为目标文件进行库链接
target_link_libraries(main hello)