# Service

> 服务作为模块的最小单元

# 接口

```C#
public interface IService {
}
```

仅仅是个标签，没有任何实际内容

# 具体实现

## ConstStateService

基本都是配置数据

## RandomService

使用自定义[LFloat](./LFloat.md)类型的一个随机库

## CommonStateService

一些通用的参数，如：Tick，DeltaTime等

## SimulatorService

## NetworkService

## IdService

Id生成器

## GameResourceService

资源加载器