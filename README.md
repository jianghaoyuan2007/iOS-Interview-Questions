# iOS Interview Questions

这个 repo 的主要目的收集和整理与 iOS 相关的面试题。

## Table of Contents

1. Memory Management

2. Runtime

3. Run Loop 

4. GCD

5. KVO & KVC

6. UIKit

7. Debugging

### Memory Management

1. 什么情况使用 `weak` 关键字，相比 `assign` 有什么不同？

2. 怎么用 `copy` 关键字？

3. 这个写法会出什么问题：`@property (copy) NSMutableArray *array;`

4. 如何让自己的类用 `copy` 修饰符？如何重写带 `copy` 关键字的 `setter`？

5. `@property` 的本质是什么？`ivar`、`getter`、`setter` 是如何生成并添加到这个类中的？

6. `@protocol` 和 `category` 中如何使用 `@property`？

7. `Runtime` 如何实现 `weak` 属性？

8. `@property` 中有哪些属性关键字？/ `@property` 后面可以有哪些修饰符？

9. `weak` 属性需要在 `dealloc` 中置 `nil` 么？

10. `@synthesize` 和 `@dynamic` 分别有什么作用？

11. `ARC` 下，不显式指定任何属性关键字时，默认的关键字都有哪些？

12. 用 `@property` 声明的 `NSString`（或 `NSArray`，`NSDictionary`）经常使用`copy` 关键字，为什么？如果改用 `strong` 关键字，可能造成什么问题？

13. `@synthesize` 合成实例变量的规则是什么？假如 `property` 名为 `foo`，存在一个名为 `_foo` 的实例变量，那么还会自动合成新变量么？

14. 在有了自动合成属性实例变量之后，`@synthesize` 还有哪些使用场景？

15. `objc` 使用什么机制管理对象内存？

16. `ARC` 通过什么方式帮助开发者管理内存？

17. 不手动指定 `Autorelease Pool` 的前提下，一个 `Autorelease Pool` 对象在什么时刻释放？（比如在一个 `vc` 的 `viewDidLoad` 中创建）

18. `BAD_ACCESS` 在什么情况下出现？

19. 苹果是如何实现 `Autorelease Pool` 的？

20. 使用 `block` 时什么情况会发生引用循环，如何解决？

21. 在 `block` 内如何修改 `block` 外部变量？

22. 使用系统的某些` block api`（如 `UIView` 的 `block` 版本写动画时），是否也考虑引用循环问题？

### Runtime

1. `Objective-C` 中向一个 `nil` 对象发送消息将会发生什么？

2. `Objective-C` 中向一个对象发送消息 `[obj foo]` 和 `objc_msgSend()` 函数之间有什么关系？

3. 什么时候会报 `unrecognized selector` 的异常？

4. 一个 `Objective-C` 对象如何进行内存布局？（考虑有父类的情况）

5. 一个 `Objective-C` 对象的 `isa` 的指针指向什么？有什么作用？

6. 下面的代码输出什么？  

```objective-c
   @implementation Son : Father
   - (id)init
   {
       self = [super init];
       if (self) {
           NSLog(@"%@", NSStringFromClass([self class]));
           NSLog(@"%@", NSStringFromClass([super class]));
       }
       return self;
   }
   @end
```
7. 使用 `Runtime Associate` 方法关联的对象，需要在主对象 `dealloc` 的时候释放么？

8. `Objective-C` 中的类方法和实例方法有什么本质区别和联系？

9. `_objc_msgForward` 函数是做什么的，直接调用它将会发生什么？

10. `Runtime` 如何实现 `weak` 变量的自动置 `nil`？

11. 能否向编译后得到的类中增加实例变量？能否向运行时创建的类中添加实例变量？为什么？

### Run Loop

1. `Run Loop` 和线程有什么关系？

2. `Runloop` 的 `Mode` 作用是什么？

3. 以 `+ scheduledTimerWithTimeInterval...` 的方式触发的 `timer`，在滑动页面上的列表时，`timer` 会暂定回调，为什么？如何解决？

4. `Run Loop` 内部是如何实现的？ 

### GCD

1. `GCD` 的队列（ `dispatch_queue_t` ）分哪两种类型？

2. 如何用 `GCD` 同步若干个异步调用？（如根据若干个 `url` 异步加载多张图片，然后在都下载完成后合成一张整图）

3. `dispatch_barrier_async` 的作用是什么？

4. 苹果为什么要废弃 `dispatch_get_current_queue` ？

5. 以下代码运行结果如何？

```objective-c
- (void)viewDidLoad
{
    [super viewDidLoad];
    NSLog(@"1");
    dispatch_sync(dispatch_get_main_queue(), ^{
        NSLog(@"2");
    });
    NSLog(@"3");
}
```
### KVO & KVC

1. `addObserver:forKeyPath:options:context:` 各个参数的作用分别是什么，`observer` 中需要实现哪个方法才能获得 `KVO` 回调？

2. 如何手动触发一个 `value` 的 `KVO`？

3. 若一个类有实例变量 `NSString *_foo`，调用 `setValue:forKey:` 时，可以以 `foo` 还是 `_foo` 作为 `key`？

4. `KVC` 的 `keyPath` 中的集合运算符如何使用？

5. `KVC` 和 `KVO` 的 `keyPath` 一定是属性么？

6. 如何关闭默认的 `KVO` 的默认实现，并进入自定义的 `KVO` 实现？

7. `Apple` 用什么方式实现对一个对象的 `KVO`？

### UIKit

1. `IBOutlet` 连出来的视图属性为什么可以被设置成 `weak` ?

2. `IB` 中 `User Defined Runtime Attributes` 如何使用？

### Debugging

1. 如何调试 `BAD_ACCESS` 错误

2. `lldb`（ `gdb` ）常用的调试命令？

## References

* [《招聘一个靠谱的 iOS》—参考答案（上）](https://github.com/ChenYilong/iOSInterviewQuestions/blob/master/01%E3%80%8A%E6%8B%9B%E8%81%98%E4%B8%80%E4%B8%AA%E9%9D%A0%E8%B0%B1%E7%9A%84iOS%E3%80%8B%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%82%E8%80%83%E7%AD%94%E6%A1%88/%E3%80%8A%E6%8B%9B%E8%81%98%E4%B8%80%E4%B8%AA%E9%9D%A0%E8%B0%B1%E7%9A%84iOS%E3%80%8B%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%82%E8%80%83%E7%AD%94%E6%A1%88%EF%BC%88%E4%B8%8A%EF%BC%89.md)



