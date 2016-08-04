---
layout: post
title: 设计模式的前奏----UML和设计模式的原则
date: 2014-03-16 15:32:24.000000000 +09:00
---



>开篇我想上两幅图，是Objective-C 编程之道中的几个瞬间，不美丽，但做为开篇是合适的。至少我这样认为。

![](https://penglimin.github.io/assets/LeonpengPicture/类图.png)

![](https://penglimin.github.io/assets/LeonpengPicture/时序图.png)

>你能理解上面的图的大体意思吗？如果不能就不能好好理解设计模式，那么让我们学习认识这些图吧，下面我们开始这篇博客 ------`设计模式的前奏----UML`



UML(United Modeling Language),统一建模语言,是一种基于面向对象的可视化`建模语言`.
UML 采用了一组形象化的图形(如类图)符号作为建模语言, 使用这些符号可以形象地描述系统的各个方面
UML 通过建立图形之间的各种关系(如类与类之间的关系)来描述模型.

上面的几句话定义，可以不必深究，现在你只需要知道，UML能够表达类与类之间的关系就可以了。UML是可视化的，通过文档的方式呈现。总而言之，UML为面向对象开发系统的产品进行说明、可视化、和编制文档的一种标准语言。

### UML中的图
UML中的图大体可以分为两大类：
静态模型图：描述系统的静态结构。 包括：类图， 对象图， 包图，组件图，部署图
动态模型图：描述系统行为的各个方面。 包括：用例图，时序图，协作图，状态图，活动图。

### UML中的关系
UML 中的关系主要包括 4 种: 

关联关系(association)

依赖关系(dependency)

泛化关系(generalization)

实现关系(realization)


### UML建模工具
我使用的是MacBookPro,所以这里提供 StarUML的Mac版本，windows版本的有很多，自行下载吧，因为本人现在从事iOS开发工作。很抱歉啊。
[StarUML(Mac版本)](https://pan.baidu.com/s/1bPO3Zg)



### 1.用例图（Use Case diagram):
`概念`:是从软件需求分析到最终实现的第一步，它从客户的角度来描述系统功能，也称为用户模型图。

`描述方式(基本组件)`:用例图包含3个基本组件:参与者,用例,关系；

参与者(Actor):与系统`打交道的人`或其他系统(使用该系统的`人或事物`)，在UML中参与者用 `人形图标表示`。

用例:代表系统的某项完整的功能，在UML中使用一个`椭圆`来表示。 

关系:定义用例之间的关系 ----- 泛化关系(可以理解成继承关系)，扩展关系，包含关系。

`目的`:帮组开发团队以一种可视化的方式理解系统的功能需求.

让我们一起打开UML建模工具画一个用例图：

![](https://penglimin.github.io/assets/LeonpengPicture/UseCaseDiagram1.jpg)


#### 1.1用例之间的关系--泛化关系
泛化关系: 表示同一业务目的(父用例)的不同技术实现(各个子用例). 在 UML 中, 用例泛化用一个三角箭头从子用例指向父用例. 以下是某购物网站为用户提供不同的支付方式

表示方式：实线空三角箭头；箭头指向父用例
作用：子用例继承父用例所有的结构、行为和关系，是父用例的一种特殊形式.
![](https://penglimin.github.io/assets/LeonpengPicture/泛化关系.jpg)


#### 1.2用例之间的关系--包含关系
包含关系：一个用例可以包含其他用例具有的行为, 并把它包含的用例行为作为自身行为的一部分. 在 UML 中包含关系用虚线箭头加 “<<include>>”, 箭头指向被包含的用例
![](https://penglimin.github.io/assets/LeonpengPicture/包含关系.jpg)

#### 1.3用例之间的关系--扩展关系
如果在完成某个功能的时候偶尔会执行另外一个功能，则用扩展关系表示.在 UML 中扩展关系用虚线箭头加 “<<extend>>”, 箭头指向被扩展的用例。

![](https://penglimin.github.io/assets/LeonpengPicture/扩展关系.jpg)

### 用例图练习
下面是关于一个公司的人事管理系统的需求的简单描述, 建立其相应的用例模型: 该人事管理系统的用户是公司的人事管理干部. 该系统具有人事档案库, 保存员工的人事信息, 包括姓名, 性别, 出生年月, 健康状况, 文化程度, 学位, 职称, 岗位, 聘任时间, 任期, 工资, 津贴, 奖罚记录, 业绩, 论著和家庭情况等, 系统提供的基本服务有人事信息的管理, 包括人事规定的权调动与聘任, 职称评定, 奖罚等, 并且可以按照限查询人事信息, 生成与输出统计报表等. 该人事系统每月向公司的财务系统提供员工的工资, 津贴等数据.

![](https://penglimin.github.io/assets/LeonpengPicture/人事管理系统.jpg)

### 2.类图
类图是面向对象系统建模中最常用的图，是定义其他图的基础。
类图主要是用来显示系统中的类，接口以及他们之间的关系。
类图包含的主要元素有类，接口和关系，其中关系有泛化关系，关联关系，依赖关系和实现关系。在类图中也可以包含注释和约束。


类的表示法:类是类图的主要组件,由 3 部分组成: 类名, 属性和方法. 在 UML 中, 类用矩形来表示, 顶端部分存放类的名称, 中间部分存放类的属性, 属性的类型及值, 底部部分存放类的方法, 方法的参数和返回类型

在UML中可以根据实际情况有选择的隐藏属性部分或方法部分或两者都隐藏。
在UML中，共有类型有+表示（public），私有类型用-表示（private），保护类型用#表示（protected）。UML的工具开发商可以使用自己定义的符号表示不同的可见性。
![](https://penglimin.github.io/assets/LeonpengPicture/类图.jpg)
### 时序图
时序图用于描述对象之间的传递消息的时间顺序, 即用例中的行为顺序. 
当执行一个用例时, 时序图中的每条消息对应了一个类操作或者引起转换的触发事件.
在 UML 中, 时序图表示为一个二维的关系图, 其中, 纵轴是时间轴, 时间延竖线向下延伸. 横轴代表在协作中各个独立的对象. 当对象存在时, 生命线用一条虚线表示, 消息用从一个对象的生命线到另一个对象的生命线的箭头表示. 箭头以时间的顺序在图中上下排列.

### 时序图中的基本概念
对象: 时序图中对象使用矩形表示, 并且对象名称下有下划线. 将对象置于时序图的顶部说明在交互开始时对象就已经存在了. 如果对象的位置不在顶部, 表示对象是在交互的过程中被创建的.
生命线:  生命线是一条垂直的虚线. 表示时序图中的对象在一段生命周期内的存在. 每个对象底部中心的位置都带有生命线. 
消息: 两个对象之间的单路通信. 从发送方指向接收方. 在时序图中很少使用返回消息. 
激活: 时序图可以描述对象的激活和钝化. 激活表示该对象被占用已完成某个任务. 钝化指对象处于空闲状态, 等待消息. 在 UML 中, 对象的激活时将对象的生命线拓宽为矩形来表示的. 矩形称为计划条或控制期. 对象就是在激活条的顶部被激活的. 对象在完成自己的工作后被钝化.
对象的创建和销毁: 在时序图中, 对象的默认位置是在图的顶部. 这说明对象在交互开始之前就已经存在了. 如果对象是在交互过程中创建的, 那么就应该将对象放到中间部分. 如果要撤销一个对象, 在其生命线终止点处放置 “ X” 符号.

时序图练习:
	
	猜猜这个男人是谁？
	写到:
	有一个男人，他19岁娶了18岁的女友，
	24岁时和只有18岁的秘书交往并结婚，
	28岁见到1岁的女婴，开始光源氏计划，
	在31岁到日本旅游认识一名15岁的女仆，
	隔年认识10岁的萝莉，
	在日本旅行期间就周旋于女仆和萝莉之间
	38岁和萝莉结婚，39岁回到中国，
	49岁光源氏计划成功，把22岁的小妹妹带回家
	后来活到59岁死亡。
	请问这个人生的赢家是哪个历史人物？
	
	答案： 孙中山先生
	1885年， 19岁 与卢慕贞(18岁)结婚，后育有三子
	1891年， 24岁 认识陈粹芬(18岁)，后成为侧室
	1894年， 28岁 初次见到宋庆龄(1岁女婴)开始光源氏计划
	1897年， 31岁 流亡日本，认识浅田春(15岁女仆)
	1898年， 32岁 认识大月熏（10岁萝莉）
	1900年， 34岁 9月20日上午在神户市相生町加藤旅馆跟浅田春(18岁)...
	1901年， 35岁 向卢慕贞(34岁)提出离婚(当时似乎还没正式离婚)
	1902年， 36岁 向大月熏(14岁)父亲提亲被拒绝
	1903年， 37岁 8月与大月熏(15岁)订婚
	1904年， 38岁 7月19日与大月熏(16岁)正式成亲
	1915年， 49岁 与卢慕贞(48岁)正式离婚 与宋庆龄(22岁)结婚
	
	
![](https://penglimin.github.io/assets/LeonpengPicture/孙中山.png)

	
# 注意：我没有将UML图介绍完毕，你可以看看下面这个链接,进行学习。

[UML一系列教程](http://blog.csdn.net/jiuqiyuliang/article/details/8552956/)

当看过这些UML知识之后,我们就可以学习设计模式了。我们的设计模式之旅正式启程喽。

#### 设计模式
## 什么是设计模式
> Christopher Alexander说过:“每一个模式描述了一个在我们周围不断重复发生的问题, 以及该问题的解决方案的核心。这样,你就能一次又一次地使用该方案而不必做重复劳动”

### 1.1 历史由来
    模式是在某一场景下的问题解决方案。
    大白话：在一定环境下，用固定套路解决问题。
    模式一词，最早来源于建筑词汇，是千百年来，人们对构建生存环境得失总结。
    比如房屋要坐北朝南(在天朝)，目的是为了采光，要起脊，就是为了排水,要打地基,就是为了防风····· 
    这一系列的总结,就成了设计房屋的范式。
    范式再经过，整理，抽象，提升，就成了，今天所谓的设计模式。
    后来，这个概念，被引入到计算机领域，经过前人在软件实施中得到的经验，
    总结出了一套软件开发设计模式。
    这个模式实在是太抽象了，下面让我们来具体陈述一下，设计模式。或者说让我们描述一下模式的组成部分，或基本元素。

### 1.2 设计模式的四个基本要素

  一般而言,一个模式有四个基本要素:
  
    1. 模式名称(pattern name)  
      一个助记名,它用一两个词来描述模式的问题、解决方案和效果。
    2. 问题(problem) 描述了应该在何时使用模式。
    3. 解决方案(solution) 描述了设计的组成成分,它们之间的相互关系及各自的职责和协 作方式。
    4. 效果(consequences) 描述了模式应用的效果及使用模式应权衡的问题。

#### 设计模式(Design pattern)
     是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。
     使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代 码可靠性。
      毫无疑问，设计模式于己于他人于系统都是多赢的；设计模式使代码编制
      真正工程化；设计模式是软件工程的基石脉络，如同大厦的结构一样。
     在我们的研究设计模式的时候，通常会觉得简单的事情搞的很复杂！！！是的，
     从某种角度上说，设计模式把简单的问题复杂化（标准化），把环境中的各个部分进行抽象、归纳、解耦合。

#### 学习设计模式的意义
     做任何你认为有意义的事情，对你来说就是不辜负时光，学习设计模式的
     学习意义相对来说，就更加客观:设计模式是前人经验的摸索，和思想的固化，
     我们应该保持上进心去学习，另外，对于我们从事的行业来说，设计模式是一个
     中高级话题，关乎每个程序员的职业素养，和个人的长期长远发展。
     
 推荐书籍: Gang of Four 的“Design Patterns: Elements of Resualbel Software”, 如果你从事iOS开发 则推荐先看看 Objective-C 编程之道
     在 Gang of Four (四人帮or四人组)的书中，将设计模式归纳为三大类型，共23种。
     创建型模式：通常和对象的创建有关，涉及到对象实例化的方式。（共5种模式)
     结构型模式： 描述的是如何组合类和对象以获得更大的结构。(共7种模式)
     行为型模式： 用来对类或对象怎样交互和怎样分配职责进行描述。(共11种模式)
     
  这一系列博文，我将根据自己的理解，将这23种设计模式，一一陈述，作为个人总结，希望大神给与指教。相互进步。谢谢。
 
## 设计模式基本原则    
  模式化的东西,总会有一些，大大小小的规章制度，谈及做人，也要有原则，那么，我们的设计模式也不例外，有着自己的一些基本原则。这些原则的最终目的：`高内聚，低耦合`。
  
#### 1.开闭原则(开放封闭原则)
定义:OCP,Open For Extension, Closed For Modification Principle 一个软件实体如类、模块和函数应该对扩展开放,对修改关闭。

问题由来:
在软件的生命周期内,因为变化、升级和维护等原因需要对软件原有代码进行修改 时,可能会给旧代码中引入错误,也可能会使我们不得不对整个功能进行重构,并且需 要原有代码经过重新测试。

解决方案:
当软件需要变化时,尽量通过扩展软件实体的行为来实现变化,而不是通过修改已有的代码来实现变化。
> talk is cheap, show me the code
现在,我们去一个特别的银行，银行将存款，转账，缴费，理财产品购买，vip通道等业务设在同一柜台。这个柜台里的银行职员可以提供一条龙服务。这样显得杂乱。
	#import <Foundation/Foundation.h>
	@interface BankWorker : NSObject
	- (void)save;
	- (void)moveMoney;
	- (void)pay;
	@end
	@implementation BankWorker
	- (void)save
	{
	    NSLog(@"存款");
	}
	- (void)moveMoney
	{
	    NSLog(@"转账");
	}
	- (void)pay{
	    NSLog(@"缴费");
	}
	@end
	int main(int argc, const char * argv[]) {
	    @autoreleasepool {
		     BankWorker *bw = [[BankWorker alloc]init];
	        [bw moveMoney];
	        [bw save];
	        [bw pay];
	    }
	    return 0;
	}
	
让我们提出一个新的需求，银行的用户，想办理住房公积金提取，我们该怎样让BankWorker拥有提取住房公积金功能，那我们难道就要改变 BankWorker类中的代码吗？那如果又有新的需求呢？

现实生活中，我们去银行，总是会见到，理财产品柜台和普通存款业务柜台是分开的...普通用户柜台vip用户柜台是分开的。这样显得井井有条。


	#import <Foundation/Foundation.h>
	@interface BankWorker : NSObject
	- (void) dothing;
	@end
	@implementation BankWorker
	- (void) dothing{};
	@end

	@interface SaveBanker : BankWorker
	- (void) dothing;
	@end
	@implementation SaveBanker
	- (void) dothing{
	    NSLog(@"存款");
	};
	@end	

	@interface MoveBanker : BankWorker
	- (void) dothing;
	@end
	@implementation MoveBanker
	- (void) dothing{
	    NSLog(@"转账");
	};
	@end
	
	@interface AdvMoveBanker : MoveBanker
	- (void) dothing;
	@end
	@implementation AdvMoveBanker
	- (void) dothing{
	    NSLog(@"批量 转账");
	};
	
	@end
	
	int main(int argc, const char * argv[]) {
	    @autoreleasepool {
	        BankWorker *bw = NULL;
	        bw = [[MoveBanker alloc] init];
	        [bw dothing];  // 有多态发生
	        
	        bw = [[AdvMoveBanker alloc] init];
	        [bw dothing];
	        
            bw = [[SaveBanker alloc] init];
            [bw dothing];
            
       }
	    return 0;
	}
	
我们将银行职员分为 负责存款的银行职员，负责转账的银行职员，等等。。。。。。各自干各自的专项。比如现在有一个客户，要办理住房公积金提取业务。 我们就可以不再修改原有代码，只需要扩展出一个 负责 住房公积金提取 业务的银行职员类 就可以了。 

    #import <Foundation/Foundation.h>
	@interface BankWorker : NSObject
	- (void) dothing;
	@end
	@implementation BankWorker
	- (void) dothing{};
	@end
	@interface MoveBanker : BankWorker
	- (void) dothing;
	@end
	@implementation MoveBanker
	- (void) dothing{
	    NSLog(@"转账");
	};
	@end
	
	@interface SaveBanker : BankWorker
	- (void) dothing;
	@end
	@implementation SaveBanker
	- (void) dothing{
	    NSLog(@"存款");
	};
	@end
	
	@interface AdvMoveBanker : MoveBanker
	- (void) dothing;
	@end
	@implementation AdvMoveBanker
	- (void) dothing{
	    NSLog(@"批量 转账");
	};
	@end
	
	// 扩展的 负责住房公积金办理的 银行职员类
	@interface HouseBanker : BankWorker
	- (void) dothing;
	@end
	@implementation HouseBanker
	- (void) dothing{
	    NSLog(@"住房公积金办理");
	};
	
	
	@end
	
	int main(int argc, const char * argv[]) {
	    @autoreleasepool {
	        BankWorker *bw = NULL;
	        bw = [[MoveBanker alloc] init];
	        [bw dothing];  // 有多态发生
	        
	        bw = [[AdvMoveBanker alloc] init];
	        [bw dothing];
	        
	        bw = [[SaveBanker alloc] init];
	        [bw dothing];
	        
	        bw = [[HouseBanker alloc] init];
	        [bw dothing];
	
	    }
	    return 0;
	}
		
这样我们就可以面对各种业务需求，临危不乱，你来什么业务需求，我就扩展相应的类，负责处理你的业务需求，并且不会对原有的代码造成影响。这就是所谓的 开闭原则，对扩展开放，对修改关闭，扩展开放是可以理解为对类增加的开放，修改关闭可以理解为对原有类的修改关闭。并且你有没有发现，原有的框架调用了后来人的代码。另外个人感觉，多态是设计模式的基石，理解多态十分重要。

看看下面这段代码，你又有什么启发？？？ 在往常的编程中我们经常见到协议和代理同时出现。这导致了许多程序员,一提到协议就想起代理。现在是时候理解协议到底是什么了，其实协议可以说是一个接口，我们常说要面向接口编程，等等之类。好好理解一下。其实我这里想说的是,在c++中有抽象类的概念，为子类提供接口。在OC中可以利用协议实现，提供接口的功能。这是我个人的理解。

	#import <Foundation/Foundation.h>
	@protocol AAA
	- (void) dothing;
	@end
	
	@interface MoveBanker : NSObject<AAA>
	- (void) dothing;
	@end
	
	@implementation MoveBanker
	- (void) dothing{
	    NSLog(@"转账");
	};
	@end
	
	@interface SaveBanker : NSObject<AAA>
	- (void) dothing;
	@end
	@implementation SaveBanker
	- (void) dothing{
	    NSLog(@"存款");
	};
	@end
	
	@interface AdvMoveBanker : NSObject<AAA>
	- (void) dothing;
	@end
	@implementation AdvMoveBanker
	- (void) dothing{
	    NSLog(@"批量 转账");
	};
	@end
	
	// 扩展的 负责住房公积金办理的 银行职员类
	@interface HouseBanker : NSObject<AAA>
	- (void) dothing;
	@end
	@implementation HouseBanker
	- (void) dothing{
	    NSLog(@"住房公积金办理");
	};

	@end
	
	int main(int argc, const char * argv[]) {
	    @autoreleasepool {
	        
	        NSObject<AAA> *bw = NULL;
	        bw = [[MoveBanker alloc] init];
	        [bw dothing];  // 有多态发生
	        
	        bw = [[AdvMoveBanker alloc] init];
	        [bw dothing];
	        
	        bw = [[SaveBanker alloc] init];
	        [bw dothing];
	        
	        bw = [[HouseBanker alloc] init];
	        [bw dothing];
	
	    }
	    return 0;
	}






#### 2.依赖倒置原则

定义: DIP,Dependence Inversion Principle  高层模块不应该依赖低层模块,二者都应该依赖其抽象;抽象不应该依赖细节;细节应该依赖抽象。总而言之，依赖于抽象(接口),不要依赖具体的实现(类)，也就是针对接口编程。

问题由来:
类A直接依赖类B,假如要将类A改为依赖类C,则必须通过修改类 A 的代码来达成。这种场景下,类 A 一般是高层模块,负责复杂的业务逻辑;类 B 和类 C 是低层模 块,负责基本的原子操作;假如修改类 A,会给程序带来不必要的风险。

![](https://penglimin.github.io/assets/LeonpengPicture/依赖倒置1.png)
解决方案:
将类 A 修改为依赖接口 I,类 B 和类 C 各自实现接口 I,类 A 通过接口 I 间接与类 B或者类 C 发生联系,则会大大降低修改类 A 的几率。

![](https://penglimin.github.io/assets/LeonpengPicture/依赖倒置2.png)

下面让我们一起组装电脑。
我们组装电脑的时候，会选择CPU ,硬盘, 内存, 显示器......我们可以选择各种牌子的CPU(因特尔，AMD)， 可以选择各种牌子的硬盘(西部数据, 希捷),内存我们可以选择金士顿。等等。。。

实际上，我们可以想象，之所以我们能够有多重选择进行组装是因为，电脑的各个接口规格已经先指定好了, 各厂商针对接口进行制造产品, 组装者根据 接口选择遵守了接口的产品。
这个接口正是我们的抽象层。

这样就是所谓的,依赖于抽象(接口),不要依赖具体的实现(类)，也就是针对接口编程。

下面我们写出代码。


	#import <Foundation/Foundation.h>
	
	// 先定义抽象接口 我想先实现一个接口层，抽象层。
	@protocol HardDisk    //硬盘接口
	- (void)work;
	@end
	
	@protocol Memory      //内存接口
	- (void)work;
	@end
	
	@protocol Cpu         // cpu接口
	- (void)work;
	@end
	
	
	@interface InterCpu : NSObject<Cpu>
	
	- (void)work;
	
	@end
	@implementation InterCpu
	- (void)work
	{
	    NSLog(@"我是iterl cpu ");
	}
	@end
	
	@interface XSDisk : NSObject<HardDisk>
	
	- (void)work;
	
	@end
	@implementation XSDisk
	- (void)work
	{
	    NSLog(@"我是西数硬盘 ");
	}
	@end
	
	
	@interface JSDMem : NSObject<Memory>
	
	- (void)work;
	
	@end
	@implementation JSDMem
	- (void)work
	{
	    NSLog(@"我是金士顿内存 ");
	}
	@end
	
	
	@interface Computer : NSObject
	
	@property(nonatomic, strong)NSObject<HardDisk> *m_harddisk;
	@property(nonatomic, strong)NSObject<Memory> *m_memory;
	@property(nonatomic, strong)NSObject<Cpu> *m_cpu;
	
	- (void)work;
	
	@end
	@implementation Computer
	- (void)work
	{
	    [self.m_harddisk work];
	    [self.m_memory work];
	    [self.m_cpu work];
	}
	@end
	
	int main()
	{
	    NSObject<Cpu> *cpu = NULL;
	    NSObject<Memory> *memory = NULL;
	    NSObject<HardDisk> *harddisk = NULL;
	
	    cpu = [InterCpu new];
	    memory = [JSDMem new];
	    harddisk = [XSDisk new];
	    
	    Computer *mycomputer = [Computer new];
	    
	    mycomputer.m_cpu = cpu;
	    mycomputer.m_harddisk = harddisk;
	    mycomputer.m_memory = memory;
	    
	    [mycomputer work];
	
	    return 0;
	}


现在我不想用intel的cpu了，那我就可以创建一个 AMD类，让他遵守cpu接口协议，就可以按照自己的需求更换电脑的cpu了. 
仔细体会这就实现了，高层模块不应该依赖低层模块,二者都应该依赖其抽象;抽象不应该依赖细节;细节应该依赖抽象。总而言之，依赖于抽象(接口),不要依赖具体的实现(类)，也就是针对接口编程。非常利于扩展。仔细体会。


#### 3.迪米特法则
定义: LOD,Law of Demeter 一个对象应当对其他对象尽可能少的了解，从而降低各个对象之间的耦合，提高系统的可维护性。例如在一个程序中，各个模块之间相互调用时，通常会提供一个统一的接口来实现。这样其他模块不需要了解另外一个模块的内部实现细节，这样当一个模块内部的实现发生改变时，不会影响其他模块的使用。

问题的由来:
让我们举一个现实生活中的例子。
你的朋友有一个朋友，他和你没有见过面，非常陌生。你想和这个人进行通话。

不要和陌生人说话。


1. 直接和陌生人说话，有可能他是一个坏人。
2. 不和陌生人说话，让你的朋友帮忙传话。这样降低了你和陌生人之间的耦合，降低危险性。
3. 与依赖导致原则结合 某人和 抽象陌生人 说话 让某人和欧胜任进行解耦合。这里的抽象陌生人，是你判断一个人是否安全的接口，如果这个陌生人符合，他就是好人，可以直接对话。

#### 4.里氏替换原则
定义: LSP, Liskov Substitution Principle 如果对每一个类型为 T1 的对象 o1,都有类型为 T2 的对象 o2,使得以 T1 定义 的所有程序 P 在所有的对象 o1 都代换成 o2 时,程序 P 的行为没有发生变化,那 么类型 T2 是类型 T1 的子类型。   所有引用基类的地方必须能透明地使用其子类的对象。
问题由来:
当使用继承时,遵循里氏替换原则。类 B 继承类 A 时,除添加新的方法完成新增 功能 P2 外,尽量不要 shadow(遮盖)父类 A 的方法。 （shadow类似于重写。)
继承作为面向对象三大特性之一,在给程序设计带来巨大便利的同时,也带来了弊 端。比如使用继承会给程序带来侵入性,程序的可移植性降低,增加了对象间的耦合性, 如果一个类被其他的类所继承,则当这个类需要修改时,必须考虑到所有的子类,并且 父类修改后,所有涉及到子类的功能都有可能会产生故障。
解决方案:
里氏替换原则通俗的来讲就是:子类可以扩展父类的功能,但不能改变父类原有的功能。它包含以下 2 层含义:
  1.子类中可以增加自己特有的方法。  2.子类可以实现父类的抽象方法,但不能覆盖父类的非抽象方法。

	#import <Foundation/Foundation.h>
	
	@interface AAA : NSObject
	- (int)add:(int) a with:(int) b;
	@end
	@implementation AAA
	- (int)add:(int)a with:(int) b
	{
	    return a + b;
	}
	@end
	
	@interface BBB : AAA
	- (int)add:(int)a with:(int) b;
	@end
	
	@implementation BBB
	- (int)add:(int)a with:(int) b
	{
	    return a - b;
	}
	@end
	int main()
	{
	    AAA *a = [AAA new]; BBB *b=[BBB new];
	    int aa = [a add:3 with:5];
	    int bb = [b add:3 with:5];
	    NSLog(@"%d",aa);
	    NSLog(@"%d",bb);
	    return 0;
	}
	
这样真的好吗？？？

#### 5.单一职责原则
(SRP,Single Responsibility Principle) 类的职责要单一，对外只提供一种功能，而引起类变化的原因都应该只有一个。
#### 6.接口隔离原则 
(ISP,Interface Segegation Principle)不应该强迫客户的程序依赖他们不需要的接口方法。一个接口应该只提供一种对外功能，不应该把所有操作都封装到一个接口中去。

#### 7.优先使用组合而不是继承原则
 (CARP,Composite/Aggregate Reuse Principle)  如果使用继承，会导致父类的任何变换都可能影响到子类的行为。如果使用对象组合，就降低了这种依赖关系。
> 设计模式的前奏就写到这里吧,欢迎联系我,进行指正，谢谢大家。

