# iOS推送1.3.2及以前推送版本升级指导

因推送支持图片，GrowingPushExtensionKit中原有接口不支持弃用，需要修改为新接口。  
将原来的接口替换  
//旧接口`+ (void)sendNotificationRequest:(UNNotificationRequest *)request withCompletionHandler:(void (^)(id response))completionHandler;`

### 新接口

```objectivec

- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
    self.contentHandler = contentHandler;
    self.bestAttemptContent = [request.content mutableCopy];
 
    [GrowingPushExtensionKit handleNotificationRequest:request
                                        withCompletion:^(NSArray<UNNotificationAttachment *> * _Nullable attachments, NSArray<NSError *> * _Nullable errors) {
        NSLog(@"执行成功");
        NSLog(@"回调信息是 attachments = %@, error = %@", attachments, errors);
        
        // Modify the notification content here...
        self.bestAttemptContent.attachments = attachments;
        self.contentHandler(self.bestAttemptContent);
    }];
}
```

