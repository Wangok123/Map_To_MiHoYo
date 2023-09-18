# 第一个窗口

之前已经使用GLFW帮助我们初始化窗口了，这里直接分析一下其基础内容功能。

```C++
int main()
{
    glfwInit();
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
    //glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);   //Mac系统用

    return 0;
}
```

1. 使用`glfwInit()`来初始化
2. 使用`glfwWindowHint()`来做基础配置
   1. `GLFW_CONTEXT_VERSION_MAJOR`、`GLFW_CONTEXT_VERSION_MINOR`分别代表主版本号，次要版本号，如本次用的是3.3。
   2. `GLFW_OPENGL_PROFILE`设置核心模式。 

创建一个窗口对象，这个窗口对象存放了所有和窗口相关的数据，而且会被GLFW的其他函数频繁地用到。
```C++
GLFWwindow* window = glfwCreateWindow(800, 600, "LearnOpenGL", NULL, NULL);
if (window == NULL)
{
    std::cout << "Failed to create GLFW window" << std::endl;
    glfwTerminate();
    return -1;
}
glfwMakeContextCurrent(window);
```