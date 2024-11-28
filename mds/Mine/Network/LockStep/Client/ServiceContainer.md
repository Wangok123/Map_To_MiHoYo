# ServiceContainer：服务容器

所有相关服务都继承了`IService`接口，由此容器`IServiceContainer`管理。

# 服务接口

## IGameViewService

```C#
    public interface IServiceContainer {
        T GetService<T>() where T : IService;
        IService[] GetAllServices();
    }
```

# 具体服务容器

## BaseGameServicesContainer

单独把构造函数拉出来而已，初始化了一些默认的服务

## UnityServiceContainer

主要容器

## PureServiceContainer

不知道干嘛的