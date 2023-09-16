# 内购相关

## C#端

项目内购使用Unity IAP直接对接。
其中，有一层代理层`PurchaseAgent`，其作为sdk的桥接口，并为业务端提供服务。

其中有以下内容：

### 实现IStoreListener接口

`IStoreListener`接口是Unity IAP提供的接口，用于初始化与返回向服务器申请购买操作状态。

### 定义了购买状态码

成功，本地错误，远端错误。

