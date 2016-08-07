---
layout: post
title: DP之工厂模式
date: 2014-04-1 15:32:24.000000000 +09:00
---

> 今天我们来看看工厂的一系列模式
简单工厂模式 - 工厂模式 - 抽象工厂模式

一个引子：
   
    在OC开发中，我们已经知道常见的两段式对象创建法，[[SomeClass alloc]init],
    有时，我们已经注意到有一些“便利”方法返回类的实例。例如我们的NSNumber 类，
     通过类方法numberWith****方法创建NSNumber对象。比如，我们可以向NSNumber
     发送[NSNumber numberWithBool:bool],以获得与传入参数同类型的各种NSNumber实例。与如何创建NSNumber的具体子类型的实例有关的所有细节，都由NSNumber的类
     工厂方法负责。仔细想想，我们有没有看到具体的创建过程，具体子类是什么？[NSNumber numberWithBool:bool]的情况是，方法接受值bool，并把NSNumber的
     内部子类的一个实例初始化，让他能够反映传入的值bool。
    
	@interface NSNumber (NSNumberCreation)
	
	+ (NSNumber *)numberWithChar:(char)value;
	+ (NSNumber *)numberWithUnsignedChar:(unsigned char)value;
	+ (NSNumber *)numberWithShort:(short)value;
	+ (NSNumber *)numberWithUnsignedShort:(unsigned short)value;
	+ (NSNumber *)numberWithInt:(int)value;
	+ (NSNumber *)numberWithUnsignedInt:(unsigned int)value;
	+ (NSNumber *)numberWithLong:(long)value;
	+ (NSNumber *)numberWithUnsignedLong:(unsigned long)value;
	+ (NSNumber *)numberWithLongLong:(long long)value;
	+ (NSNumber *)numberWithUnsignedLongLong:(unsigned long long)value;
	+ (NSNumber *)numberWithFloat:(float)value;
	+ (NSNumber *)numberWithDouble:(double)value;
	+ (NSNumber *)numberWithBool:(BOOL)value;
	+ (NSNumber *)numberWithInteger:(NSInteger)value NS_AVAILABLE(10_5, 2_0);
	+ (NSNumber *)numberWithUnsignedInteger:(NSUInteger)value NS_AVAILABLE(10_5, 2_0);
	
	@end


## 简单工厂模式
### 1.什么是简单工厂模式
简单工厂模式属于类的创建型模式，又叫静态工厂方法模式。通过专门一个类来负责创建其他类的实例，被创建的实例通常都具有共同的父类。


### 2.模式中包含的角色以及其职责
1. 工厂角色：
       简单工厂模式的核心，他负责实现创建所有实例的内部逻辑。工厂类可以被外界直接调用，创建所需的产品对象。
2. 抽象角色：
       简单工厂模式所创建的所有对象的父类，它负责描述所有实例所共有的公共接口。
3. 具体产品角色：
       简单工厂模式所创建的具体实例对象。
       
       
![](https://penglimin.github.io/assets/LeonpengPicture/DesignPattern/工厂模式相关1/简单工厂.jpg)

// 依赖关系： 一个类的对象，当另一个类的函数参数或者 是返回值。

### 3.简单工厂的优缺点
在这个设计模式中，工厂类是整个模式的关键所在。在包含必要的逻辑判断，能够根据外界给定的信息，决定究竟应该创建哪个具体类的对象。用户 在使用时可以直接根据工厂类去创建所需的实例，而无需了解谢谢对象是如何创建以及如何组织的，有利于整个软件体系结构的优化，不难发现，简单工厂模式的缺点也正体现在其工厂类上，由于工厂类集中了所有实例的创建逻辑，所以，高内聚方面做得并不好，另外，当系统中的具体产品类不断增多时，可能会出现要求工厂类也要做相应的修改，扩展性并不很好。

### talk is cheap， Show me the code.

	#import <Foundation/Foundation.h>
	typedef enum FruitType
	{
	    BananaType,
	    PearType,
	    AppleType
	}FruitType;
	
	@interface Fruit : NSObject
	- (void) getFruit;
	@end
	@implementation Fruit
	- (void) getFruit{
	
	}
	@end
	
	@interface Banana : Fruit
	- (void) getFruit;
	
	@end
	@implementation Banana
	
	- (void) getFruit
	{
	    NSLog(@"香蕉");
	}
	@end
	@interface Pear : Fruit
	- (void) getFruit;
	
	@end
	@implementation Pear
	
	- (void) getFruit
	{
	    NSLog(@"梨子");
	}
	@end
	@interface Apple : Fruit
	- (void) getFruit;
	
	@end
	@implementation Apple
	
	- (void) getFruit
	{
	    NSLog(@"苹果");
	}
	@end
	
	
	@interface Factory : NSObject
	
	+ (Fruit *)CreteFruit:(FruitType) type;
	
	@end
	@implementation Factory
	+ (Fruit *)CreteFruit:(FruitType) type
	{
	    if(type == BananaType)
	    {	        return [Banana new];
	    }	    if(type == PearType)
	    {	        return [Pear new];
	    }	    if(type == AppleType)
	    {	        return [Apple new];
	    }
	    return NULL;
	}
	
	@end
	
	int main(int argc, const char * argv[]) {
	    Fruit *fruit1 = [Factory CreteFruit:AppleType];
	    [fruit1 getFruit];
	    Fruit *fruit2 =[Factory CreteFruit:BananaType];
	    [fruit2 getFruit];
	    return 0;
	}


// 简单工厂主要用于创建对象，新添加类时，不会影响以前的系统代码。核心思想是用一个工厂来根据输入的条件产生不同的类，然后根据不同类的函数得到不同的结果。

优点：适用于不同情况创建不同的类。
缺点：客户端必须要知道基类和工厂类，耦合性太差，你可以把客户端当做main函数，也就是调用创建的地方。


## 工厂模式
### 1.概念：
工厂方法模式同样属于类的创建模式，又被称为多态工厂模式。工厂方法模式的意义是定义一个创建产品对象的工厂接口，将实际创建工作推迟到子类当中。核心工厂类不再负责产品的创建，这样核心类成为一个抽象工厂角色，仅负责具体工厂子类必须实现的接口，这样进一步抽象化的好处是使得工厂方法模式可以使系统在不修改具体工厂角色的情况下引进新的产品。

### 2.类图角色和职责
抽象工厂（Creator）角色
工厂方法模式的核心，任何工厂类都必须实现这个接口。

具体工厂（ Concrete  Creator）角色
具体工厂类是抽象工厂的一个实现，负责实例化产品对象。

抽象（Product）角色    
工厂方法模式所创建的所有对象的父类，它负责描述所有实例所共有的公共接口。

具体产品（Concrete Product）角色
工厂方法模式所创建的具体实例对象

![](https://penglimin.github.io/assets/LeonpengPicture/DesignPattern/工厂模式相关1/工厂模式.jpg)
### 3.工厂方法模式和简单工厂模式比较

工厂方法模式与简单工厂模式在结构上的不同不是很明显。工厂方法类的核心是一个抽象工厂类，而简单工厂模式把核心放在一个具体类上。  

工厂方法模式之所以有一个别名叫多态性工厂模式是因为具体工厂类都有共同的接口，或者有共同的抽象父类。

当系统扩展需要添加新的产品对象时，仅仅需要添加一个具体对象以及一个具体工厂对象，原有工厂对象不需要进行任何修改，也不需要修改客户端，很好的符合了“开放－封闭”原则。而简单工厂模式在添加新产品对象后不得不修改工厂方法，扩展性不好。工厂方法模式退化后可以演变成简单工厂模式。

“开放－封闭”通过添加代码的方式，不是通过修改代码的方式完成功能的增强。

	### talk is cheap， Show me the code.
	
	#import <Foundation/Foundation.h>
	@interface Fruit : NSObject
	- (void) sayname;
	@end
	@implementation Fruit
	- (void) sayname{
	    
	}
	@end
	
	@interface FruitFactory : NSObject
	- (Fruit *) getFruit;
	@end
	@implementation FruitFactory
	- (Fruit *) getFruit{
	    
	    return  [Fruit new];
	}
	@end
	
	
	@interface Banana : Fruit
	- (void) sayname;
	@end
	@implementation Banana
	- (void) sayname{
	    NSLog(@"Banana \n");
	}
	@end
	
	@interface BananaFactory : FruitFactory
	- (Fruit *) getFruit;
	@end
	@implementation BananaFactory
	- (Fruit *) getFruit{
	    return  [Banana new];
	}
	@end
	
	@interface Apple : Fruit
	- (void) sayname;
	@end
	
	@implementation Apple
	- (void) sayname{
	    NSLog(@"Apple \n");
	}
	@end
	
	@interface AppleFactory : FruitFactory
	- (Fruit *) getFruit;
	@end
	
	@implementation AppleFactory
	- (Fruit *) getFruit{
	    
	    return  [Apple new];
	}
	
	@end
	
	int main()
	{
	    
	    FruitFactory *ff = NULL;
	    Fruit *fruit = NULL;
	    
	    ff = [BananaFactory new];
	    fruit = [ff getFruit];
	    [fruit sayname];
	    
	    // 苹果
	    ff = [AppleFactory new];
	    fruit = [ff getFruit];
	    [fruit sayname];
	    
	    return 0;
	}

发现了，设计模式就是让简单的代码复杂化。但是当我们搭好了这样的框架，后期的维护和扩展，简直就像是在做配置一样，随手就来。

## 抽象工厂
### 1.概念：
抽象工厂模式是所有形态的工厂模式中最为抽象的。抽象工厂模型可以向客户端提供一个接口，使得客户端在不必指定产品的具体类型的情况下，能够创建多个产品族的产品对象。

### 2.注解：
工厂模式：要么生产香蕉、要么生产苹果、要么生产西红柿；但是不能同时生产一个产品组。
抽象工厂：能同时生产一个产品族。这就是抽象工厂存在原因


解释:
具体工厂在开闭原则下,​​能生产香蕉/苹果/梨子;  
​抽象工厂:在开闭原则下,​​能生产：南方香蕉/苹果/梨子 (产品族)  ​​​​​​​​​​北方香蕉/苹果/梨子

重要区别
工厂模式只能生产一个产品。（要么香蕉、要么苹果）
抽象工厂可以一下生产一个产品族（里面有很多产品组成）

### 2.模式中包含的角色及其职责
1. 抽象工厂（Creator）角色
抽象工厂模式的核心，包含对多个产品结构的声明，任何工厂类都必须实现这个接口。

2. 具体工厂（ Concrete  Creator）角色
具体工厂类是抽象工厂的一个实现，负责实例化某个产品族中的产品对象。

3. 抽象（Product）角色
抽象模式所创建的所有对象的父类，它负责描述所有实例所共有的公共接口。

4. 具体产品（Concrete Product）角色
抽象模式所创建的具体实例对象


![](https://penglimin.github.io/assets/LeonpengPicture/DesignPattern/工厂模式相关1/抽象工厂.png)


### talk is cheap， Show me the code.

	#import <Foundation/Foundation.h>
	@interface Fruit : NSObject
	- (void) sayname;
	@end
	@implementation Fruit
	- (void) sayname{
	    
	}
	@end
	
	@interface FruitFactory : NSObject
	- (Fruit *) getApple;
	- (Fruit *) getBanana;
	
	@end
	@implementation FruitFactory
	- (Fruit *) getApple{
	    
	    return  [Fruit new];
	}
	- (Fruit *) getBanana{
	    
	    return  [Fruit new];
	}
	@end
	
	
	@interface SouthBanana : Fruit
	- (void) sayname;
	@end
	@implementation SouthBanana
	- (void) sayname{
	    NSLog(@"SouthBanana \n");
	}
	@end
	
	
	@interface SouthApple : Fruit
	- (void) sayname;
	@end
	@implementation SouthApple
	- (void) sayname{
	    NSLog(@"SouthApple \n");
	}
	@end
	
	
	@interface NorthApple : Fruit
	- (void) sayname;
	@end
	@implementation NorthApple
	- (void) sayname{
	    NSLog(@"NorthApple \n");
	}
	@end
	
	
	@interface NorthBanana : Fruit
	- (void) sayname;
	@end
	@implementation NorthBanana
	- (void) sayname{
	    NSLog(@"NorthBanana \n");
	}
	@end
	
	
	@interface SourthFruitFactory : FruitFactory
	- (Fruit *) getApple;
	- (Fruit *) getBanana;
	
	@end
	@implementation SourthFruitFactory
	- (Fruit *) getApple
	{
	    return [SouthApple new];
	}
	- (Fruit *) getBanana
	{
	    return [SouthBanana new];
	}
	@end
	
	@interface NorthFruitFactory : FruitFactory
	- (Fruit *) getApple;
	- (Fruit *) getBanana;
	
	@end
	@implementation NorthFruitFactory
	- (Fruit *) getApple
	{
	    return [NorthApple new];
	}
	- (Fruit *) getBanana
	{
	    return [NorthBanana new];
	}
	@end
	
	
	int main()
	{
	    
	    FruitFactory *ff = NULL;
	    Fruit *fruit = NULL;
	    
	    ff = [SourthFruitFactory new];
	    fruit = [ff getApple];
	    [fruit sayname];
	    fruit = [ff getBanana];
	    [fruit sayname];
	
	    // 苹果
	    ff = [NorthFruitFactory new];
	    fruit = [ff getBanana];
	    [fruit sayname];
	    fruit = [ff getApple];
	    [fruit sayname];
	    
	    return 0;
	}

理解概念是第一步，在日常开发中，如何其一反三的使用，需要多加练习和斟酌。
