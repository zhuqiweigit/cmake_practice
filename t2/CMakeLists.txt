cmake_minimum_required(VERSION 3.10)
#project 名称建立后，会自动建立两个内部变量 NAME_BINARY_DIR 和 NAME_SOURCE_DIR;
#或者是PROJECT_BINARY_DIR 和 PROJECT_SOURCE_DIR
#binary dir 是目标文件生成的目录，随着外部编译或者内部编译有所不同；source dir是源代码的目录，一般就是根项目的cmakeLists的位置
#cmake指令不区分大小写；但变量区分大小写
project(hello)

#message 的格式，STATUS固定，表示输出带-的信息；还有FATEL_ERROR等，可以终止项目编译
message(STATUS "this is binary dir " ${PROJECT_BINARY_DIR})
message(STATUS "this is src dir" ${PROJECT_SOURCE_DIR})

#add_subdirectory，前一个参数表示子目录名字，后一个参数表示子目录代码要生成的目标文件的存放相对位置
#这个相对位置是相对于 PROJECT_BINAYR_DIR来说的
#cmake会自动去子目录搜索子目录的cmakelists，并执行
add_subdirectory(src bin)
add_subdirectory(doc)

#install指令安装文本文件、sh脚本、二进制目标文件、整个目录等
#FILES、PROGRAMS表示安装的是什么；后面跟安装的文件或目录；如果是目录，目录/表示安装目录下的内容，目录表示带着目录一起安装
#DESTINATION 表示安装位置；这是相对路径，前缀由执行cmake时的参数-DCMAKE_INSTALL_PREFIX=/tmp/t2/usr 给出
#完整的安装过程是：cmake -DCMAKE_INSTALL_PREFIX=/tmp/t2/usr ..
#               make
#               make install
#如果不定义-DCMAKE_INSTALL_PREFIX=安装前缀，则默认安装到/usr/local/
install(FILES COPYRIGHT.txt README.md DESTINATION share/doc/cmake/t2)
install(PROGRAMS runHello.sh DESTINATION bin)


#关于内部编译和外部编译
#外部编译，即不在原代码根目录的cmakelists处生成目标文件，而在其他文件夹生成；
#方法是：新建一个build目录，在build目录内部使用cmake指令

