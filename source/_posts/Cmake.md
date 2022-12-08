---
title: Cmake入门和MindsporeLite Cmake文件分析
toc: true
copyright: true
date: 2021-11-29 20:30:18
tags:
    - CMake
    - CPP
categories:
    - 《栈溢出工程师》
reward:
---
对于没有接触Cmake的同学而言，刚接触Cmake难免一脸懵逼,我刚开始实习时也是第一次接触到Cmake，原来CPP开发也一直是在Visual Studio环境下进行，对Liunx环境下的CPP开发并不熟悉，对于Liunx环境的CPP开发而言，CMake和MakeFile是必须掌握的，本文将简单介绍Cmake的原理和使用方法，并以[mindsporelite](https://gitee.com/mindspore/mindspore)作为案例讲解一个大型项目的Cmake写法。

---
# MakeFile和Cmake简介
对于一个C++或者C程序的编译分为预处理、编译、汇编、链接四个过程，比如对于单文件`"hello.cpp",`
生成hello（hello.exe）所需要执行的bash命令：

    gcc -v -o hello hello.c

但当涉及多文件编译时，我们的命令会十分复杂，比如一个`main.cpp`文件依赖于`Foo1.cpp`,`Foo2.cpp`,...`Foo10`,我们需要先将这10个文件编译成`.o`文件，再将各`.o`文件和`main.o`进行链接，代码如下

    g++ -std=c++17 -O2 -o Foo1.o -c Foo1.cpp
    g++ -std=c++17 -O2 -o Foo2.o -c Foo2.cpp
    g++ -std=c++17 -O2 -o Foo3.o -c Foo3.cpp
    g++ -std=c++17 -O2 -o Foo4.o -c Foo4.cpp
    g++ -std=c++17 -O2 -o Foo5.o -c Foo5.cpp
    g++ -std=c++17 -O2 -o Foo6.o -c Foo6.cpp
    g++ -std=c++17 -O2 -o Foo7.o -c Foo7.cpp
    g++ -std=c++17 -O2 -o Foo8.o -c Foo8.cpp
    g++ -std=c++17 -O2 -o Foo9.o -c Foo9.cpp
    g++ -std=c++17 -O2 -o Foo10.o -c Foo10.cpp
    g++ -std=c++17 -O2 -o main.o -c main.cpp
    g++ -std=c++17 -O2 main.o Foo1.o Foo2.o Foo3.o Foo4.o Foo5.o Foo6.o Foo7.o Foo8.o Foo9.o Foo10.o -o main


上述编译过程还算简单，因为各子文件还不相互依赖，但如果子文件有相互依赖关系，比如`foo1.cpp`依赖于`foo10.cpp`我们编译的顺序有必须更改，在文件数目更大的工程中，一行一行输入命令进行编译是不现实的，所以我们引入了Makefile,对于上述编译任务，我们的MakeFile如下，我们只需输入`make`一句命令即可完成编译

    COMPILER = g++ -std=c++17 -O2 -I./include  
    OBJECTS = Foo1.o Foo2.o Foo3.o Foo4.o Foo5.o Foo6.o Foo7.o Foo8.o Foo9.o Foo10.o main.o
    TARGET = main
    
    $(TARGET): $(OBJECTS)
        $(COMPILER) -o $@ $^ -lprotobuf
    $(OBJECTS): %.o: %.cpp
        $(COMPILER) -o $@ -c $<
    $(DEPENDENCIES): %.d: %.cpp
        $(COMPILER) -o $@ -MM $<
    
    include $(DEPENDENCIES)
    
    .PHONY: clean
    clean:
        rm $(OBJECTS) $(DEPENDENCIES) $(TARGET)


Makefile 规定了一套编译规则，使用什么编译器，编译器使用什么样的编译选项，每个文件都有什么依赖关系。在编译的时候，能够直接根据 makefile 来确定哪些文件依赖于其他的哪些文件，从而把编译顺序、需不需要重新编译以及链接都自动检测出来,在Linux环境下，MakeFile本身可以看做一个shell脚本。

既然我们有了MakeFile，又为什么需要Cmake工具？对于不同环境下的编译，有着多种Make工具，比如 GNU Make ，QT 的 qmake ，微软的 MS nmake，BSD Make（pmake），Makepp，等等。这些 Make 工具遵循着不同的规范和标准，所执行的 Makefile 格式也千差万别。这样就带来了一个严峻的问题：如果软件想跨平台，必须要保证能够在不同平台编译。而如果使用上面的 Make 工具，就得为每一种标准写一次 Makefile。

CMake 就是针对上面问题所设计的工具：它首先允许开发者编写一种平台无关的 CMakeList.txt 文件来定制整个编译流程，然后再根据目标用户的平台进一步生成所需的本地化 Makefile 和工程文件，如 Unix 的 Makefile 或 Windows 的 Visual Studio 工程。从而做到“Write once, run everywhere”。显然，CMake 是一个比上述几种 make 更高级的编译配置工具。对于深度学习框架而言，跨平台是一件非常重要的事，因为深度学习模型可能在不同的环境下运行，可能是x86的Linux或者Windows，也可能是ARM，涉及到跨平台交叉编译。

# MindSporeLite Cmake详解
## 生成可执行文件或库
在 linux 平台下使用 CMake 生成 Makefile 并编译的流程如下：

+ 编写 CMake 配置文件 CMakeLists.txt 。
+ 执行命令 cmake PATH 或者 ccmake PATH 生成 Makefile（ccmake 和 cmake 的区别在于前者提供了一个交互式的界面）。其中， PATH 是 CMakeLists.txt 所在的目录。
+ 使用 make 命令进行编译。

下面是一个最简单的单文件CmakeLists,执行命令后会编译一个名为Demo的 `exe`文件

    # CMake 最低版本号要求
    cmake_minimum_required (VERSION 2.8)
    
    # 项目信息
    project (mindsporelite)
    
    # 指定生成目标
    add_executable(mindsporelite main.cc)

如果把`add_executable`改成[add_library](https://cmake.org/cmake/help/v3.20/command/add_library.html),那么会生成一个的静态或者动态库


    # 生成动态库
    add_library(mindsporelite SHARED main.cc)
    # 生成静态库
    add_library(mindsporelite STATIC main.cc)


## 多文件编译
对于多文件的情况，我们可以通过在`add_library`或`add_executable`的目标后意义列出所有文件，如下

    # 生成动态库
    add_library(mindsporelite SHARED main.cc a.cc b.cc)
    # 生成静态库
    add_library(mindsporelite STATIC main.cc a.cc b.cc)

但是对于一个较大的工程，一一列举会显得Cmake代码十分冗长，我们可以用`set`设置一个变量，包含所有需要的`.cc`或`.cpp`文件

    set(LITE_SRC
            ${API_SRC}
            ${CMAKE_CURRENT_SOURCE_DIR}/common/context_util.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/common/file_utils.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/common/config_file.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/common/utils.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/common/graph_util.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/common/log.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/common/lite_utils.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/common/prim_util.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/common/tensor_util.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/runtime/inner_allocator.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/runtime/runtime_allocator.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/runtime/infer_manager.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/schema_tensor_wrapper.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/tensor.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/ms_tensor.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/executor.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/inner_context.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/lite_model.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/kernel_registry.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/inner_kernel.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/lite_kernel.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/lite_kernel_util.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/sub_graph_kernel.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/scheduler.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/lite_session.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/errorcode.cc
            ${CMAKE_CURRENT_SOURCE_DIR}/cpu_info.cc
            )

    # 生成动态库
    add_library(mindsporelite SHARED ${LITE_SRC})
    # 生成静态库
    add_library(mindsporelite STATIC ${LITE_SRC})

当然除了动态库和静态库，我们还可以选择将代码编译成未链接的`.o`中间文件，在`add_library`使用`OBJECT`参数，使用方法如下

    add_library(<name> OBJECT [<source>...])
    add_library(... $<TARGET_OBJECTS:objlib> ...)
    add_executable(... $<TARGET_OBJECTS:objlib> ...)
    
    
对于生成的中间产物，这些文件并未被链接，所以并不能作为库或执行，我们对这些中间产物还可以进行如`add_dependencies`的操作，`add_dependencies()`会为顶层目标添加一个依赖关系，可以保证某个目标在其他的目标之前被构建。比如`mindsporelite`依赖于[flatbuffers](https://github.com/google/flatbuffers)（一个谷歌开源的序列化库）生成的`fbs`文件


    ms_build_flatbuffers_lite(FBS_FILES ${CMAKE_CURRENT_SOURCE_DIR}/schema/ fbs_src ${CMAKE_BINARY_DIR}/schema "")

    #生成中间文件
    add_library(lite_src_mid OBJECT ${LITE_SRC})
    #添加依赖
    add_dependencies(lite_src_mid fbs_src)

    # 生成动态库
    add_library(mindsporelite SHARED $<TARGET_OBJECTS:lite_src_mid>)
    # 生成静态库
    add_library(mindsporelite STATIC $<TARGET_OBJECTS:lite_src_mid>)


## 生成多个库或者可执行文件

有时我们希望在一个项目中能编译多个独立的库或者可执行文件，比如在`mindsporelite`中,我们总共会生成以下可执行文件和动静态库



+ Mindsporelite
    + runtime
        + libminddata-lite.a (数据加载静态库）     
        + libmindspore-lite-train.a（端侧训练静态库）
        + libmindspore-lite.a （端侧推理静态库）   
        + libminddata-lite.so (数据加载动态库）     
        + libmindspore-lite-train.so（端侧训练动态库）
        + libmindspore-lite.so （端侧推理动态库）  
    + tools
        + benchmark（基准测试·工具）
        + cropper（裁剪工具）
        + converter（模型转化工具）
        + benchmark_train（训练基准测试工具）
        + codegen（代码生成工具）

而对于每个库或者可执行文件，一般在其相关的`.cc`文件目录下有一个`CmakeLists`文件，在最外侧目录的`CmakeLists`中通过`add_subdirectory`命令，指明本项目包含一个子目录 ，这样子目录下的 CMakeLists.txt 文件和源代码也会被处理，通过多层的`CmakeLists`我们一一构建各层的库和依赖。以下代码表示添加一个
`src`的子目录


    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/src)




## 链接库
`add_subdirectory`往往和`target_link_libraries`一起使用，在我们编译好一个可执行文件或者库时，如果它依赖其他库,我们可以使用`target_link_libraries`将其链接其他库，方法如下



    # 生成动态库
    add_library(mindsporelite SHARED $<TARGET_OBJECTS:lite_src_mid>)
    # 生成静态库
    add_library(mindsporelite-static STATIC $<TARGET_OBJECTS:lite_src_mid>)
    # 生成可执行文件
    add_executable(benchmark main.cc)
    # 动态链接
    target_link_libraries(benchmark mindsporelite）
    #静态链接
    target_link_libraries(benchmark mindsporelite-static)
    
mindsporelite中的基准测试工具依赖于mindsporelite runtime库，链接代码如上，链接又分为动态链接和静态链接，静态链接会将库中所有的代码一起编译到可执行文件中，运行时速度更快，但包的大小更大，动态链接不会将库的代码编译到可执行文件中，文件更小，但在运行时会搜索动态库，运行速度慢。如果在系统目录和环境变量中找不到动态库，那么在运行时会报错，在Linux环境中，可以通过设置环境变量`LD_LIBRARY_PATH`指定动态库目录


    export LD_LIBRARY_PATH=/path/to/lib:${LD_LIBRARY_PATH}


这里有在链接库时，Cmake是如何找到对应库的位置的？在Cmake中，我们一般在文件开始添加 [include_directories](https://cmake.org/cmake/help/v3.20/command/add_compile_definitions.html)（包含指定目录）或aux_source_directory（包含所有子目录）命令，Cmake会在这些目录下进行搜索。



    add_library (MathFunctions ${DIR_LIB_SRCS})
 

## 编译选项和编译宏
对于跨平台的项目，我们往往要进行交叉编译，针对不同环境的代码和功能可能有所不同，
我们往往通过`option`确定编译选项，[add_compile_definitions](https://cmake.org/cmake/help/v3.20/command/add_compile_definitions.html)来增加编译宏定义，不同平台编译的代码用宏进行隔离，同时编译宏也可以决定某部分代码是否编译，是否包含某个功能，对一些还不稳定的特性进行隔离，

比如,在mindsporelilte中，通过设置`MSLITE_ENABLE_SHARING_MEM_WITH_OPENGL`来确定是否编译OpenGL相关代码


    option(MSLITE_ENABLE_SHARING_MEM_WITH_OPENGL "enable sharing memory with OpenGL" on)

    if(DEFINED ENV{MSLITE_ENABLE_SHARING_MEM_WITH_OPENGL})
        set(MSLITE_ENABLE_SHARING_MEM_WITH_OPENGL $ENV{MSLITE_ENABLE_SHARING_MEM_WITH_OPENGL})
    endif()

    if(MSLITE_ENABLE_SHARING_MEM_WITH_OPENGL)
        add_definitions(-DENABLE_OPENGL_TEXTURE)
    endif()

在相关cpp文件中用宏`ENABLE_OPENGL_TEXTURE`隔离相关代码


    #ifdef ENABLE_OPENGL_TEXTURE
      if (!lite::opencl::LoadOpenGLLibrary(&gl_handle_)) {
        MS_LOG(ERROR) << "Load OpenGL symbols failed!";
        return RET_ERROR;
      }
    #endif


对于任何跨平台的Cpp项目，其Cmake的架构基本大同小异，按层级结构一一编译各个动静态库，最后链接成一个可执行文件或者库。

# 参考文献

+ [CMake 入门实战](https://www.hahack.com/codes/cmake/)
+ [Effective Modern CMake](https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1)
+ [Cmake官方文档](https://cmake.org/cmake/help/v3.20/)