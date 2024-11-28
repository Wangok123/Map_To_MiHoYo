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

# 具体服务

## 