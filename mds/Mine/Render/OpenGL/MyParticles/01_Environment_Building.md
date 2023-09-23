# 环境配置

>对于我这个小白来说，想配一个OpenGL还是稍微花了不少时间的，这里记录一下，防止重蹈覆辙。

## IDE

使用了VS2019版本, 最开始用的VS2022，但不知道为啥，网上找的示例跑不起来，应该是各种各样的库不兼容导致的。

## GLFW

在我们画出出色的效果之前，首先要做的就是创建一个OpenGL上下文(Context)和一个用于显示的窗口。然而，这些操作在每个系统上都是不一样的，OpenGL有意将这些操作抽象(Abstract)出去。这意味着我们不得不自己处理创建窗口，定义OpenGL上下文以及处理用户输入。很多库可以帮我们解决这一点，GLFW就是其中之一。

[下载地址](http://www.glfw.org/download.html)下载源码包。

下载好源码包后，会有一个问题，也是很多开源代码的一个问题。
开放源代码所产生问题在于：并不是每个人都用相同的IDE或者构建系统来搞开发，因而提供的项目/解决方案文件可能和一些人的IDE不兼容。所以人们必须使用给定的.c/.cpp和.h/.hpp文件来自己建立项目/解决方案，这是一项很枯燥的工作。但因此也诞生了一个叫做CMake的工具。

## CMake

CMake是一个工程文件生成工具。用户可以使用预定义好的CMake脚本，根据自己的选择（像是Visual Studio, Code::Blocks, Eclipse）生成不同IDE的工程文件。这允许我们从GLFW源码创建一个Visual Studio 2019工程文件，之后进行编译。

这里使用CMake以GLFW源码库，创建了一个基于本机的lib文件。

[下载链接](http://www.cmake.org/cmake/resources/software.html)

## 创建工程并链接

在`项目设置/VC++目录`中，把GLFW的include文件夹，与libs文件夹分别挂载到`包含目录`和`库目录中`。
![设置链接](/images/Mine/OpenGL/Env_Building/vc_directories.png)
最后需要在Linker(链接器)选项卡里的Input(输入)选项卡里添加glfw3.lib这个文件：
![设置链接器](/images/Mine/OpenGL/Env_Building/linker_input.png)

这时如果一切妥当的话，可以使用以下：
```C++
#include <GLFW\glfw3.h>
```
引入头文件。

## GLAD

到这里还没有结束，我们仍然还有一件事要做。因为OpenGL只是一个标准/规范，具体的实现是由驱动开发商针对特定显卡实现的。由于OpenGL驱动版本众多，它大多数函数的位置都无法在编译时确定下来，需要在运行时查询。所以任务就落在了开发者身上，开发者需要在运行时获取函数地址并将其保存在一个函数指针中供以后使用，取得地址的方法因平台而异。

GLAD是一个[开源](https://github.com/Dav1dde/glad)的库，它能解决我们上面提到的那个繁琐的问题。GLAD的配置与大多数的开源库有些许的不同，GLAD使用了一个[在线服务](http://glad.dav1d.de/)。在这里我们能够告诉GLAD需要定义的OpenGL版本，并且根据这个版本加载所有相关的OpenGL函数。

打开GLAD的在线服务，将语言(Language)设置为C/C++，在API选项中，选择3.3以上的OpenGL(gl)版本（我们的教程中将使用3.3版本，但更新的版本也能用）。之后将模式(Profile)设置为Core，并且保证选中了生成加载器(Generate a loader)选项。现在可以先（暂时）忽略扩展(Extensions)中的内容。都选择完之后，点击生成(Generate)按钮来生成库文件。

GLAD现在应该提供给你了一个zip压缩文件，包含两个头文件目录，和一个glad.c文件。将两个头文件目录（glad和KHR）复制到你的Include文件夹中（或者增加一个额外的项目指向这些目录），并添加glad.c文件到你的工程中。

经过前面的这些步骤之后，你就应该可以将以下的指令加到你的文件顶部了：

```C++
#include <glad/glad.h> 
```