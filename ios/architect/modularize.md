## 组件化 与 插件化

组件化的首先，是对人的组件化.

简单来看，MVC是常用的分层结构，而组件化，需要同时关注分层、分模块，比如一个业务组件A，它包括UI层、逻辑层、数据层。

这里有句话，来理解“模块”与“组件”的：要区分代码块（模块）、运行时块（组件）、硬件组（网络节点或环境要素）。你还需要识别并掌握每个系统运用的架构模式，了解每种模式能够满足哪些质量属性，这样才能判断客户端-服务器系统比映射-还原（map-reduce）系统具有更少的延迟时间。—— 摘自《恰如其分的软件架构，风险驱动的设计方法》

### 代码组件化 之 language

1. 前端组件

2. 本地组件

### 组件 之 定义 【参考：《风险驱动的软件架构》】

1. 组件
2. 端口
3. 连接器

### 代码组件 之 usage

0. 功能组件：带UI属性的独立业务模块。
1. 业务组件：不具备UI属性的独立业务模块。
2. UI组件：不具备业务场景的独立UI模块。
3. 工具组件：不具备业务场景的功能模块。

或这么看：

0. 独立业务组件
1. 基础业务组件
2. 基础通用组件
3. UI组件

### 动态插件式

1. [iOS 利用 framework 进行动态更新](https://yq.aliyun.com/articles/3024)
2. [IOS-使用framework实现功能模块动态更新](http://blog.csdn.net/like7xiaoben/article/details/44081257)
3. http://blog.csdn.net/u012907783/article/details/53158657
4. http://blog.csdn.net/YCM1101743158/article/details/61925145

### TODO

1. 2017 年前，完成代码级别的组件化尝试
2. 2017 年3月，完成组件化的完整支持，从代码，到工程组织，到版本管理
3. 2017 年6月，支持组件的动态更新机制

### 参考

  * 1. [wequick/Small](https://github.com/wequick/Small)
    - gradle-small插件：Small中的一个gradle自定义插件，用于打包组件
    - aapt：用于分离资源文件，重设资源id等等
    - 插件类的加载：动态加载.so包
    - 插件资源id冲突问题
    - Activity启动和生命周期问题

  * 2. [对组件化架构的再思考](http://blog.sina.com.cn/s/blog_493a845501012c1p.html)
    - 组件，要关注分模块，模块内分层（UI层、逻辑层、数据层）
    - 依赖原则：
      > 上层调用下层，不可逆；模块间
      > 业务组件间的调用，或说跨模块的调用需要通过服务组件暴露的服务接口进行，跨模块调用建议尽量是同层调用为主，即A模块的逻辑层只能调用B模块的逻辑层，而不能调用B模块的数据层。如果存在对B模块数据层的调用应该转化为B模块的业务服务后暴露到逻辑层。
      > 对于数据库也需要考虑隔离和解耦，为了达到这点，尽量减少对数据库存储过程和关联视图的使用，数据库基本不承载任何的业务规则和逻辑。对数据库中的公用基础数据剥离到公用业务组件中。
      > 对于系统管理，组织，权限，流程等转化为独立的平台层基础组件，为各个业务组件都需要依赖的组件。基础平台层能力如权限，安全，流程，日志等一定要抽取为公用的独立基础组件，业务组件不在承担这部分内容。
      > 不一定要引入复杂的ESB，但是系统内部基于IOC或OSGI模式来实现总线式集成和组件热插拔。
      > 各层提供的服务存在分级，数据层提供数据服务，逻辑层提供业务服务，UI层提供UI组件服务。平台层提供基础的技术服务和流程服务等。下层对上层的依赖，则：依赖注入。
      > 如果在DDD领域驱动架构设计下，数据层转化为基础架构层，业务层转化为领域层，整体思路仍然不变。而领域驱动设计中的应用层转化为组件集成和整合层。
      > 将跨系统的流程整合的概念引入到系统内部，各个业务组件即可以理解为独立的子系统，可以考虑这些子系统间如何通过服务组装和集成解决流程整合的问题，但是并不一定要用到BPEL。

  * 3. [组件化架构漫谈](http://blog.csdn.net/fallenink/article/details/52895417)，比较老的文章了
    > 组件化的粒度与分类：
      ** 蘑菇街：地图模块、聊天模块、用户模块、首页模块、设置模块，分类为业务模块、基础模块（资源、网络、缓存）
      ** casatwy：跟上面差不多
    > 组件组织、协议和间通信
      ** 蘑菇街：中间件（集中式，router），Url（引申出 短链管理），Protocol
      ** casatwy：远程调用（openURL）、本地调用（performTarget，易于追踪或调试）
      ** casatwy：他提出去model化！个人觉得，模块间通信，还是不要model，可以采取通用容器，键值协议；模块内部，采取易用性强的model化；同时嘛，如果保持model层、control层扁平、耦合，采取更细粒度的组件，则可以将model跨层使用，还是看业务需求和人员配置。
      ** 总线设计：URL路由+服务+消息。统一所有组件的通信标准，各个业务间通过总线进行通信。
    > 组件内结构
      ** 可以异构化：MVVM，MVC，MVCS
    > 组件化的project实现（这个还是请移步原文去看看）
      ** 采用cocoapods、carthage
      ** 每个组件工程有两个target，一个负责编译当前组件和运行调试，另一个负责打包framework。

  * 4. [滴滴的组件化实践与优化](http://blog.csdn.net/fallenink/article/details/52905347)，写的很仔细、细心可以一看。大致讲了结合业务实施的组件化方案，其中说清楚了组件组织、通信方式，另外配的图也说明了应用的多层结构；专项技术里头，有业务接入方式、页面结构、界面导航管理组件、共享地图背景、业务可扩展的地图的解决方案、灰度测试、app瘦身、启动速度优化、降低崩溃、模块优化。
  * 5. [iOS App组件化开发实践](http://blog.csdn.net/fallenink/article/details/52905701)，没有使用过多的架构视图，从实施层面一步步讲解了他们的组件化具体实现和指导思想，还可以。
    > [YTXModule](https://github.com/mdsb100/YTXModule/blob/master/Example/Tests/TestYTXModuleSpec.m)

  * 6. [ iOS组件化实践方案－LDBusMediator炼就](http://blog.csdn.net/fallenink/article/details/52905760)，服务总线的一个实现方式
    > [LDBusMeiator](https://github.com/Lede-Inc/LDBusMediator.git)

  * 7. [糯米移动组件架构演进之路](http://blog.csdn.net/fallenink/article/details/52905833)
  * 8. [iOS 组件化方案探索](http://blog.csdn.net/fallenink/article/details/52905854)
  * 9. [APP组件化之路](http://blog.csdn.net/fallenink/article/details/52905874)，蘑菇街的组件化方案，贡献出了：MGJRouter
  * 10. [一个iOS模块化开发解决方案](http://blog.csdn.net/fallenink/article/details/53063823)
    > 问题域：页面耦合严重，多个app下相同模块重复开发，等，讲了一些模块化过程中的细节点，可以看看。
    > 他们使用了，router，巧叔的YTKNetwork，热更新。

  * 11. [iOS组件化思路－大神博客研读和思考](http://blog.csdn.net/fallenink/article/details/53127082), 实际项目中的组件化问题,这段说的很中肯。

  * 12. [iOS组件化方案](http://mrpeak.cn/blog/module/?utm_source=tuicool&utm_medium=referral), 枚举了这些组件类型：【用户登录】，【内存管理】，【日志打点系统】，【个人Profile模块】。它除了对个别其他组件化方案的评估，同时给出了组件接口定义的案例：
    ```
    @protocol IAppModule <NSObject>
    //module life cycle
    - (void)initModule;
    - (void)destroyModule;
    //common behavior
    - (NSString*)getModuleVersion;
    - (BOOL)handleUrl:(NSString*)url;
    - (UIViewController*)getDefaultController;
    @end
    ```
    > 最后作者提到的Dependency Hell，其实是依赖性下的版本控制问题，独立业务模块对基础业务模块，是多对一关系，但是版本控制，让这个拓扑变成了多对多，复杂性增加了。。【我建议对基础业务模块的设计，采用长时间设计，少部分时间打磨，迭代过程中争取通用化，这样对外接口保持干净不变，更新与部署也会一步到位。】

  * 13. []()
