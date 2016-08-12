---
layout: post
title: DP之观察者模式
date: 2014-04-10 15:32:24.000000000 +09:00
---



### 首先我想以一份简单代码开始这篇blog。


	#import <Foundation/Foundation.h>
	
	@interface B : NSObject
	{
	    int _a;
	}
	- (void)update:(int)a;
	@end
	@implementation B
	
	- (void)update:(int )a
	{
	    _a = a;
	    _a += 10;
	    NSLog(@"B:%d",_a);
	}
	@end
	
	@interface C : NSObject
	{
	    int _a;
	}
	
	- (void)update:(int) a;
	
	@end
	@implementation C
	
	- (void)update:(int) a
	{
	    _a = a;
	    _a += 20;
	    NSLog(@"C:%d",_a);
	}
	
	@end
	
	@interface A : NSObject
	{
	    int _a;
	}
	- (void)update:(B *)pb : (C *)pc :(int) a;
	@end
	@implementation A
	- (void)update:(B *)pb : (C *)pc :(int) a
	{
	    _a = a;
	
	    NSLog(@"A:%d",_a);
	    [pb update:_a];
	    [pc update:_a];
	}
	@end
	
	int main(int argc, const char * argv[]) {
	    @autoreleasepool {
	        B *pb = [B new];
	        C *pc = [C new];
	        
	        A *a = [A new];
	        [a update:pb :pc :18];
	    }
	    return 0;
	}


上述小案例，主要是想表达，当A 类对象的 _a 成员发生变化时，同时让 B 类 和 C类对象的_a 成员作出各自相应的变化。事实上，我们确实实现了这个功能。但是，你发现没有，耦合性太高了。A 类提供的API 	- (void)update:(B *)pb : (C *)pc :(int) a; 就可以看出，耦合性太高了。遥想想当年，设计模式产生之前，肯定大师们也发现了这样的问题，他们是怎么解决的呢，下面引出我们的使用很广泛的设计模式 --- 观察者模式。

### 观察者模式 observer

	Observer模式是行为模式之一，它的作用是当一个对象的状态发生变化时，能够自动通知其他关联对象，自动刷新对象状态。
	Observer模式提供给关联对象一种同步通信的手段，使某个对象与依赖它的其他对象之间保持状态同步。

#####  定义：
> 定义对象间一种一对多的依赖关系,当一个对象的状态发生改变时,所有依赖于它的 对象都得到通知并被自动更新。观察者处于被动地位,被观察者处于主动地位。这种交互也称为发布-订阅(publish-subscribe)。
#####   角色和职责
![](https://penglimin.github.io/assets/LeonpengPicture/DesignPattern/观察者模式相关/struct.png)


	Subject（被观察者):
	被观察的对象。当需要被观察的状态发生变化时，需要通知队列中所有观察者对象。 
	被观察者知道他的观察者，可以有任意多个观察者观察同一个目标。
	提供注册和删除观察者对象的接口。
	    
	ConcreteSubject(具体被观察者):
            将有关状态存入各ConcreteObserver对象。
            当他的状态发生改变时，向他的各个观察者发出通知。 	    	被观察者的具体实现。包含一些基本的属性状态及其他操作。
	Observer（观察者）:
	        为那些在被观察者发生改变时需获得通知的对象定义一个更新接口。 	    	接口或抽象类。当Subject的状态发生变化时，Observer对象将通过一个callback函数得到通知。
	ConcreteObserver: 	    	观察者的具体实现。得到通知后将完成一些具体的业务逻辑处理。
	        维护一个指向ConcreteSubject对象的引用。
	        存储有关状态，这些状态应与目标的状态保持一致。
	        实现Observer的更新接口以使自身状态与目标的状态保持一致。
  
### 典型应用
 - 侦听事件驱动程序设计中的外部事件
- 侦听/监视某个对象的状态变化
- 发布者/订阅者(publisher/subscriber)模型中，当一个外部事件（新的产品，消息的出现等等）被触发时，通知邮件列表中的订阅者

适用于：
	定义对象间一种一对多的依赖关系，使得每一个对象改变状态，则所有依赖于他们的对象都会得到通知。

### 使用场景：
比如有一个世界时钟程序,有多个图形时钟去显示比如北京时区,巴黎时区,等等。 如果设置一个北京时间,那么其他时钟图形都需要更新(加上或者减去时差值)。典型 的图形界面设计随处可见,一个温度程序,在温度湿度等条件改变时,要更新多种显示 图形来呈现。

####  show me the code

	#import <Foundation/Foundation.h>
	
	@interface Observer : NSObject
	
	- (void)updateHour:(int)h minute:(int )m second:(int )s;
	
	@end
	
	@implementation Observer
	
	- (void)updateHour:(int)h minute:(int )m second:(int )s{}
	
	@end
	
	
	@interface Subject : NSObject
	
	@property (nonatomic, strong) NSMutableArray *observerList;
	
	- (void) registerObserver:(Observer *)observer;
	- (void) removeObserver:(Observer *)observer;
	
	@end
	
	@implementation Subject
	
	- (NSMutableArray *)observerList
	{
	    if (_observerList == NULL) {
	        _observerList = [NSMutableArray array];
	    }
	    return _observerList;
	}
	
	
	- (void) registerObserver:(Observer *)observer
	{
	    [self.observerList addObject:observer];
	}
	- (void) removeObserver:(Observer *)observer
	{
	    [self.observerList removeObject:observer];
	}
	
	@end
	
	
	
	@interface PekingTimeSubject : Subject
	{
	    int _hour;
	    int _min;
	    int _sec;
	}
	
	- (void)notify;
	
	- (void)getTime;
	
	- (void)setTime:(int) h minute:(int) m second:(int) s;
	
	
	@end
	
	@implementation PekingTimeSubject
	- (void)notify
	{
	    for (Observer *ob in self.observerList) {
	        [ob updateHour:_hour minute:_min second:_sec];
	    }
	
	}
	
	- (void)getTime
	{
	    NSLog(@"北京:%d:%d:%d\n",_hour,_min,_sec);
	}
	
	- (void)setTime:(int) h minute:(int) m second:(int) s
	{
	    _hour = h;
	    _min = m;
	    _sec = s;
	    [self getTime];
	    [self notify];
	}
	
	@end
	
	
	@interface USATimeObserver : Observer
	{
	    int _hour;
	    int _min;
	    int _sec;
	}
	
	- (void)updateHour:(int)h minute:(int )m second:(int )s;
	- (void)dis;
	
	@end
	
	@implementation USATimeObserver
	
	- (void)updateHour:(int)h minute:(int )m second:(int )s{
	    _hour = h + 2;
	    _min = m + 12;
	    _sec = s;
	
	    [self dis];
	}
	
	- (void)dis
	{
	    NSLog(@"美国:%d:%d:%d\n",_hour,_min,_sec);
	}
	
	@end
	
	
	@interface EuropeTimeObserver : Observer
	{
	    int _hour;
	    int _min;
	    int _sec;
	}
	
	- (void)updateHour:(int)h minute:(int )m second:(int )s;
	- (void)dis;
	
	@end
	
	@implementation EuropeTimeObserver
	
	- (void)updateHour:(int)h minute:(int )m second:(int )s{
	    _hour = h = 3;
	    _min = m +10;
	    _sec = s;
	    
	    [self dis];
	}
	
	- (void)dis
	{
	    NSLog(@"欧洲:%d:%d:%d\n",_hour,_min,_sec);
	}
	
	@end
	
	int main(int argc, const char * argv[]) {
	    @autoreleasepool {
	        
	        PekingTimeSubject  *pkt =  [PekingTimeSubject new];
	        USATimeObserver    *ust =  [USATimeObserver new];
	        EuropeTimeObserver *ert =  [EuropeTimeObserver new];
	    
	        [pkt registerObserver:ust];
	        [pkt registerObserver:ert];
	        [pkt setTime:12 minute:23 second:45];
	        
	        
	        [pkt removeObserver:ust];
	        [pkt setTime:10 minute:10 second:23];
	    }
	    return 0;
	}
	
仔细阅读上述代码。并在自己的Xcode中自行调试。设计模式本来就是极其抽象的。☺ ↖(^ω^)↗ ☺


![](https://penglimin.github.io/assets/LeonpengPicture/DesignPattern/观察者模式相关/observer.jpg)

原本是子类间进行耦合，把子类间的耦合提升到父类中去，这样父类中一次耦合关系，使得众子类耦合关系得到了解耦。从uml 也可以看的出来，父类间是紧耦合的，而子类中却是松耦合的。



### 上述介绍，只是实现了传统意义上的的观察者模式。万变不离其宗，要多加体会。

在Cocoa Touch 框架中 用了两种技术改写了观察者模式 ---- 通知和键值观察(Key-Value Observing).尽管是两种不同过得Cocoa技术，两者都实现了观察者模式。他们有各自的特征以及差别。

##### 1. 通知
Cocoa Touch框架使用 NSNotificationCenter 和 NSNotifiCation 对象实现了一对多的发布-订阅模型。他们允许subject与observer以一种松耦合的方式通信.两者在通信时对另一方无需多少了解。
subject要notify其他对象时，需要创建一个可通过全局的名字来识别的通知对象，然后把它投递到通知中心。通知中心，查明特定的通知的观察者，然后通过消息把通知发送给他们。

##### 2. 键-值观察
Cocoa(包括Cocoa Touch)提供了一种称为键-值观察的机制，对象可以通过它得到其他对特定属相的变更通知。这种机制在模型-视图-控制器模式的场景中尤其重要，因为它让视图对象可以经由控制器层观察模型对象的变更。
这里我们提到了MVC，其实观察者模式对MVC设计模式的运作，是不可或缺的，从某种意义上说构成了Model和Controller进行主动通信的桥梁。稍过些日子可能会有一篇关于MVC的总结。

##### 3. 更多的KVO和通知的介绍和剖析这里暂时不进行叙述了。不过我提供了一篇博文供大家参考及研究。链接如下:

[南峰子的技术博客--Foundation: NSKeyValueObserving(KVO)](http://southpeak.github.io/blog/2015/04/23/cocoa-foundation-nskeyvalueobserving/)

如果您有更多的优秀资源学习资源要推荐请麻烦您，[联系我](mailto:iOS_leonpeng@163.com)。共同进步，thanks a lot!



