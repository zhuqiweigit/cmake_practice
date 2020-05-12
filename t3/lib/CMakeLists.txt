set(LIBHELLO_SRC hello.cpp)

#添加库文件，SHARED表示动态链接文件，STATIC表示静态文件；
#由于目标名不能重复，因此第二个不用hello而用hello_static
ADD_LIBRARY(hello SHARED ${LIBHELLO_SRC})
ADD_LIBRARY(hello_static STATIC ${LIBHELLO_SRC})

#为了生成两个一样名字的动态库和静态库，我们更改第二个库的名字
#set_target_properties 可以设置目标文件的属性；格式是 目标1， 目标2， PROPERTIES 属性1 值1 属性2 值2
set_target_properties(hello_static PROPERTIES OUTPUT_NAME "hello")

#获取目标文件的属性, 格式是 变量，目标文件名，属性
get_target_property(VALUE hello_static OUTPUT_NAME)
message(STATUS "value: " ${VALUE})