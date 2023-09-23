# 内购相关

## C#端

项目内购使用Unity IAP直接对接。
其中，有一层代理层`PurchaseAgent`，其作为sdk的桥接口，并为业务端提供服务。

[查看Unity-IAP官方教程](https://docs.unity3d.com/Packages/com.unity.purchasing@4.0/manual/Overview.html)

其中有以下内容：

### 实现IStoreListener接口

`IStoreListener`接口是Unity IAP提供的接口，用于初始化与返回向服务器申请购买操作状态。

### 定义了购买状态码

成功，本地错误，远端错误。

### 初始化


```C#
private IGooglePlayConfiguration _googlePlayConfiguration;
private AppStore _appStore;

public void Init(LuaTable products, string guId = null){
    var module = StandardPurchasingModule.Instance();
    var builder = ConfigurationBuilder.Instance(module);
    _appStore = module.appStore;

    builder.Configure<IMicrosoftConfiguration>().useMockBillingSystem = false;
    _googlePlayConfiguration = builder.Configure<IGooglePlayConfiguration>();

    SetGoogleObfuscatedAccountId(guId); //功能存疑
    _guId = guId;

    products.ForEach<int, LuaTable>((k, v) =>
        {
            string productId = v.Get<string>("buyId");
            bool isSubscribe = v.Get<bool>("isSubscribe");
            if (isSubscribe)
                builder.AddProduct(productId, ProductType.Subscription);
            else
                builder.AddProduct(productId, ProductType.Consumable);
        });

    UnityPurchasing.Initialize(this, builder);
}

```

其中这里使用IAP内部接口，初始化了关于商店配置相关。同时，初始化Ｐｒｏｄｕｃｔ相关内容。最后调用`Initialize`。

