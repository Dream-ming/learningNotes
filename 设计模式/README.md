# 设计模式

* 内容参考：深入设计模式 v2020-1-20

* 设计模式六大原则
* 设计模式详解

## 一、前置知识

* 面向对象编程的四个基本概念
  * 抽象：反映真实世界对象的特定内容，忽然不要需要的内容
  * 封装：一个对象对其他对象隐藏部分状态，仅暴漏有限接口
  * 继承：根据已有类创建新的类，复用一些已有的内容
  * 多态：程序能够检测对象的实际类，调用对应的接口
* 对象之间的关系（从强到弱，每一级都是后一级的强化版）
  * 继承：类 A 继承类 B 的接口和实现，并扩展内容
  * 实现：类 A 实现类 B 的接口内容，类 B 通常是纯虚类
  * 组合：对象 A 知道对象 B，成员中有 B，且管理着 B 的生命周期
  * 聚合：对象 A 知道对象 B，通过指针调用 B，但是 B 独立存在
  * 关联：对象 A 知道对象 B
  * 依赖：对类 B 进行修改会影响到类 A

##  二、六大设计原则（SOLID + 最少知道原则）
### 1、单一职责原则

* 每一个类只实现一个功能
* 例：“文件处理”需求
  * 违反原则：fileManager 类中写三个函数，分别是读文件、写文件、打日志
  * 遵循原则：将三个函数写成三个类，fileManager 类调用这三个类
* 优势：更清晰的职责分离，容易扩展、方便维护
* 劣势：不要过度拆分，否则得不偿失

###  2、开闭原则

* 类的拓展是开放的，类的修改是封闭的
* 例：订单类中，需要一个计算运费功能
  * 违反原则：一个计费功能，内部硬编码： if (陆运) 、if (海运)，需要添加空运功能的时候，要修改历史代码
  * 遵循原则：实现一个计费功能接口，陆运、海运通过继承实现具体内容，需要添加空运时，拓展一个子类即可
* 优势：当系统经常需要扩展功能时，十分使用
* 劣势：需要投入时间增加抽象层次

### 3、里氏替换原则

* 子类可以实现父类的抽象方法（多态），增加自己的方法，但不可以更改父类的方法
* 例：一个正方形类，继承矩形类。矩形类两个参数 w 、h，面积 s = w * h
  * 违反原则：正方形类中，s = w * w，修改了父类的
  * 遵循原则：在正方形类中也使用 w 、h 两个参数。或者抽象出一个 shape 类，然后将矩形和正方形当成平行的子类
* 优势：确保继承体系中子类和父类行为一致，防止不规范的多态产生的矛盾
* 劣势：不允许子类重写父类已声明的方法

###  4、接口隔离原则

* 接口应该尽量小而精，将一个通用接口拆分成多个专用接口
* 例子：一个关于动物行为的接口，内部有 eat、run、fly、swim 这几个纯虚函数，现在要定义 狗、猫、鱼、鸟，这几个动物类
  * 违反原则：纯虚函数要求子类继承时必须实现，导致每个动物都有浪费的地方，比如鱼不需要 run 功能、鸟不需要 swim 功能
  * 遵循原则：将接口中的每一个函数都拆成一个单独的接口，每个动物按需自取
* 优势：减少依赖、更灵活、风险更低、可读性更强

###  5、依赖倒置原则

* 高层模块不直接依赖底层模块，只依赖于底层模块封装出来的抽象接口
* 例子：类 A 依赖类 B，现在想要改为依赖类 C。A是高层模块，负责负责的业务逻辑。B 和 C 是底层模块，负责基本的原子操作
  * 违反原则：直接修改类 A，会造成不必要的风险
  * 遵循原则：类 A 在实现时，就使用抽象类，而抽象类通过 B 和 C 实现
* 优点：底层模块的修改不影响高层模块。支持面向接口编程

###  6、最少知道原则

* 只和自己直接持有的对象交互，不通过链式调用访问其他对象，不依赖全局变量
* 例子：类 A、B、C中，A 有一个 B 的对象，B 有一个 C 的对象
  * 违反原则：A.B.C.par 访问了非直接拥有的对象
  * 遵循原则：在 B 中实现一个函数 返回 C.par，然后 A.B.func 实现目标
* 低耦合、高内聚



## 二、创建型模式

### 1、单例模式

* 在全局只有一个对象，禁止其他对象调用构造函数
  * 场景：线程池对象、任务队列对象
  * 实现：
    * 将默认构造函数设为**私有**
    * 将拷贝构造函数设为**私有或禁止**
    * 将唯一的实例指针设为静态私有，仅允许类静态构造一个
    * 实现一个公共函数，返回该实例的指针，供全局使用

  * 饿汉模式：
    * 写完类之后，就直接实例化一个对象出来

  * 懒汉模式：
    * 在有对象访问这个单例的时候，才去做实例化。需要在调用的函数中判断是否已经实例化，若没有，则创建一个
    * 线程安全问题：单例做为公共资源，要防止被重复创建
      * 单层锁：加锁，再判断是否为空。每个线程每次来都要等锁，太慢
      * 双重锁：先判断，再加锁，再判断。只有第一次需要等锁，后续在第一次判断就跳出。但是机器编译会打乱顺序，导致问题
      * 原子变量：将对象指针放在原子变量里，编译阶段默认顺序执行
      * 静态局部对象


### 2、工厂模式

* 简单工厂模式：
  * 场景：产品类型不多，且创建逻辑相对固定。比如加减乘除等运算对象
  * 实现
    * 产品类为抽象类，多态出多个子类，表示不同的产品。其中，父类的析构函数要声明为虚函数，才可以释放子类的资源
    * 产品子类实现具体的产品内容
    * 工厂类定义一个生产函数，传入产品的具体类型，判断并返回父类指针
  * 缺点：有新的产品时，需要修改工厂类，违反开闭原则
* 工厂模式
  * 场景：使用产品类型较多，每个产品类型有差异时。比如不同的商单（电子产品、服装、食品等）
  * 实现
    * 工厂修改为抽象类 + 子类的模式
    * 使用时，先 new 一个子工厂，再调用子工厂的 create，生产一个产品
    * 工厂基类不再检查产品类型，添加新产品时不需要修改基类
  * 优势：解决简单工厂模式，不满足封闭开放原则

### 3、抽象工厂模式
  * 场景：生产一系列的产品。比如家具城中的（床、凳子、椅子等）每一个系列又有多种产品
  * 实现
    * 在工厂模式的基础上，对工厂类进行修改。
    * 由原来的一个抽象类派生多个具体子类，然后子类生产产品。
    * 变为一个抽象类聚合多个抽象类，每个抽象类又派生多个子类，再生产产品（对应场景案例中的系列和种类）
    * 父工厂内部会调用每一个子工厂，然后子工厂多态生产
  * 误区：抽象工厂符合开闭原则。尽管增加一个系列的时候，父工厂需要修改代码，但是不认为这违背开闭原则。这种行为视为对系统功能的重大改变，而不是简单的拓展功能

### 4、生成器 / 创造者模式

* 场景：造一艘船，里面有很多部件（甲板、船舱、引擎、武器等很多）。光是构造函数就需要很多。将构造函数单独拉出来做一个生成器类
* 实现：
  * 两个船的类，实现功能。构造交给生成器
  * (Builder) 抽象生成器类 + 两个生成器子类
  * (ABuilder、BBuilder) 具体生成器内部提供多个函数，用于指定每一个部件
  * (Director) 主管类，提供几套不同的方案，在内部以不同的方式调用 Builder
* 使用流程
  * 创建一个 Director ，传入一个 Builder，然后按需求调用 builder 提供的部件
* 优势
  * 在对象过于繁杂时，可以使用此模式，生产对象

## 三、结构型模式






## 四、行为模式
