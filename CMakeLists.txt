#设置工程名称
PROJECT(CMAKEDemo)
#自己定制
SET(MY_TARGET demo)
SET(MY_LINK threadpool pthread) 
SET(MY_INC inc )
SET(MY_LINK_INC lib )


#设置CMAKE最小版本
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
#设置编译器
SET(CMAKE_CXX_COMPILER "g++")
#设置构建类型，及相应的编译选项
SET(CMAKE_BUILD_TYPE "Debug")
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")

#设置执行文件输出目录
SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#设置库输出路径
SET(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

MESSAGE("++++++++++++++Start Build+++++++++++++++++")

#当前目录的文件
AUX_SOURCE_DIRECTORY(. SRC_LIST)
#添加子目录
ADD_SUBDIRECTORY(src)

#头文件搜索目录
INCLUDE_DIRECTORIES(${MY_INC})
#链接库搜索路径
LINK_DIRECTORIES(${MY_LINK_INC})
#设置链接库
#SET(EXTRA_LIBS ${EXTRA_LIBS} test1 test2)
SET(EXTRA_LIBS ${EXTRA_LIBS} ${MY_LINK})

#生成可执行文件
ADD_EXECUTABLE(${MY_TARGET} ${SRC_LIST})
#执行文件链接属性
TARGET_LINK_LIBRARIES(${MY_TARGET} ${EXTRA_LIBS})
