## Object-C 学习

#### 类

- @property
- @synthesize
- @class 



#### NSMutableDictionary

**NSMutableDictionary** 和 **Dictionary** 类型转换

```objective-c
      NSMutableDictionary* dictionary = [NSMutableDictionary dictionary];
      [dictionary setObject:@40001 forKey:@"key1"];

      NSNumber* num = [dictionary objectForKey:@"key1"];
      
      if ([num integerValue] == 40001) {
          NSLog(@" == ");
      } else {
          NSLog(@"not ==");
      }
```

