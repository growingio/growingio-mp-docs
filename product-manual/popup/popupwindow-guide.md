# 弹窗注册至今使用

![](../../.gitbook/assets/image%20%28119%29.png)

注册至今是我们预定义的一个事件  
需要在代码设置一下注册日期 CreateAt，需要保证key 是 CreateAt , 值是YYYYMMDD  
iOS 示例

```text
    [Growing setUserId:@"zhangsan"];
// 登陆用户属性 注册至今 需设置CreateAt，值必须用YYYYMMDD 的方式上传，否则无法生效  要求SDK1.2.0及以上
    [Growing setPeopleVariable:@{@"CreateAt":@"20191219"}];
```

