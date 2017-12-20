---
layout: post
title: pod install VS. pod update
date: 2017-12-20 15:32:24.000000000 +09:00
---

pod install 和 pod update 之间的不同之处？
什么时候使用pod install？
什么时候使用pod update?
......

#  1.介绍一下
许多开发者 使用`CocoaPods` 时，似乎认为`pod install` 只用于第一次建立使用CocoaPods的工程，而在这之后要用`pod update`，但事实并非如此。

这篇引导的目的就是解释什么该使用`pod install`,什么时候该使用`pod update`。

简单的说就是(总结精华)：
1.  使用pod install在你的工程里安装新的pods。尽管你已经有了一个Podfile并且之前运行过pod install；
尽管你只是在已经使用了CocoaPods的工程中添加/移除了pod，你都要使用pod install。

2.  只有在你想要更新pods到新的版本时才使用pod update [PODNAME]。

#### 小贴士：
注意：install和update这两个词实际上并不是CocoaPods独有的。它们也被许多其他依赖的管理器推荐使用，
如bundler，RubyGems或者composer，它们都有类似的命令，并且有与本文描述完全相同的行为和意图。


# 2. 命令的详细介绍
##### 2.1 pod install
用于工程中第一次 在工程中 安装初始化pods， 也用于每次编辑Podfile添加、更新或移除pod时。
Podfile.lock 文件介绍，这个文件会保持对每个pod已安装的版本的跟踪，并且锁定这些版本。
每次运行pod install命令时——下载和安装新的pods——并将每个已经安装的pods的版本号写入Podfile.lock文件。
当你运行pod install时，它只会处理没有被记录在Podfile.lock文件中的pods的依赖。

1.  对于已经记录在Podfile.lock中的pods，会下载记录在Podfile.lock文件中的准确版本，而不去检查是否有新版本可用。
2.  对于没有记录在Podfile.lock文件中的pods，会查找匹配Podfile中描述的版本（如pod ‘MyPod’, ‘~>1.2’）。


##### 2.2 pod outdated
当你运行pod outdated命令，CocoaPods会列出所有有新版本的pods，
新版本是指比记录在Podfile.lock文件中的版本（即当前每个pod安装的版本）更新的版本。
这意味着如果你对这些pod运行pod update PODNAME，
它们将会更新——只要这些版本仍然满足如pod ‘MyPod’, ‘~>x.y’这样设置在Podfile中的约束。

#####2.3 pod update
当你运行pod update PODNAME命令，CocoaPods将会尝试找到PODNAME指定pod的更新版本，
而不会顾及Podfile.lock文件中记录的版本。它将会更新pod的最新可用版本
（只要满足Podfile中的版本约束）。


如果你运行`pod update`而不带pod名称，`CocoaPods`将会更新`Podfile`文件中记录的每一个`pod`到最新可用版本。


# 3.用途

使用pod update PODNAME，你可以只更新指定的pod（检查是否存在新版本并相应的更新这个pod）。
相反pod install不会尝试更新已经安装的pod的版本。

当你添加一个pod到你的Podfile，你应该运行pod install，而不是pod update——才能安装这个新的pod，
同时不会带来在同一个处理过程中更新已存在的pod的风险。

当你想要更新指定pod（或所有pod）的版本时，应该只使用pod update。


# 4. 提交Podfile.lock文件

小贴士：

作为提醒，除非你的策略是不能提交Pods文件夹到共享仓库，否则你应该总是提交并推送你的Podfile.lock文件。
否则，你将会打破上述关于pod install将会锁定你的pods的已安装版本的整个逻辑。


# 5. 场景示例

以下是一些场景例子列举了在工程周期中可能遭遇的各种使用情况。


##### 场景1：用户1创建工程

用户1创建了一个工程，并想使用pods A、B、C。他创建了这些pods的Podfile，然后运行pod install。
这将会安装pods A、B、C，我们假定它们都是版本1.0.0.

Podfile.lock文件将会持续跟踪，并记住A、B和C都已经安装为版本1.0.0。

另外，由于这是第一次运行pod install，并且Pods.xcodeproj工程并不存在，
该命令也会创建Pods.xcodeproj和.xcworkspace，但这只是该命令的副作用而非主要功能。

##### 场景2：用户1添加了新的pod

随后，用户1想要添加pod D到他们的Podfile。

他们在这之后也应该运行pod install，因此即使pod B的维护者在第一次执行pod install之后发布了版本1.1.0，
这个工程也将继续使用版本1.0.0——因为用户1只想要添加pod D，而不想有意外的更新了pod B的风险。


小贴士：

tip：这就是一些人错误的地方，
因为他们在这里使用了pod update——可能认为这就是“用新的pods更新工程”的意思？——而不是使用pod install——才能在工程中安装新的pods。

##### 场景3：用户2加入到工程中

然后用户2，一个以前从未参与过这个工程的人，加入到团队之中。他克隆了仓库，然后使用pod install。

Podfile.lock文件（应该被提交到git仓库中）的内容会保证用户2能获得完全相同的pods，以及与用户1使用的完全相同的版本。

尽管pod C的1.2.0版本现在已经可用，用户2仍将获得pod C的1.0.0版本。
因为这就是写在Podfile.lock中的内容。pod C被Podfile.lock文件锁在了1.0.0版本（因此这个文件叫这个名字）。


#### 场景4：检查pod的新版本

后来，用户1想要检查这些pods是否有更新可以用。他运行了pod outdates，这个命令会告诉他pod B有新的1.1.0版本且pod C有新的1.2.0版本。

用户1决定他们要更新pod B，但是不更新pod C；因此他运行pod update B，
让B从版本1.0.0升到版本1.1.0（同时Podfile.lock文件也随之更新），但是将pod C保持在1.0.0版本（不会更新到1.2.0）。


# 5. 在Podfile中使用准确版本号是不够的

有些人可能想通过在他们的Podfile中指定pods的准确版本号，如pod ‘a’, ‘1.0.0’，就能够保证团队中的其他人拥有相同的版本。

然后他们即使使用了pod update，即使添加了新的pod，认为这将不会有更新到其他pods的风险，因为他们已经在Podfile中绑定到指定的版本了。

但实际上，这不足以保证我们在上面场景中提到的用户1和用户2总能得到所有pods的相同版本。

一个典型的例子是，如果pod A依赖了A2——在A.podspec中有声明dependency ‘A2’, ‘~> 3.0’。
此时，在Podfile中使用pod ‘A’,’1.0.0’，确实会强制用户1和用户2都总是使用pod A的1.0.0版本，但是：

用户1可能最后得到pod A2的3.4版本（因为这是A2那时的最新版本），而当用户2在之后加入工程运行pod install时，
他可能得到pod A2的3.5版本（因为A2的维护者可能在这段时间里发布了新的版本）。

这就是为什么确保每一个团队成员都能在各自的电脑上使用相同版本的pod库的唯一方法就是使用Podfile.lock，
并且正确的使用pod install和pod update。

