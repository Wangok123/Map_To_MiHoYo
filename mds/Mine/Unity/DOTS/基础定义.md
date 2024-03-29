# DOTS 组成

- C# Job System
- ECS
- Burst Compiler

## C# Job System

可以利用多核处理器，同时运行多个任务。以Job的形式，代替了直接操作thread控制。

## ECS

一种新的代码思维方式, 举例:
![ECS举例](./imgs/ECS.png)

## Burst Compiler

可以将C#代码，转化编译成适合优化的机器代码，尤其适合于Job System