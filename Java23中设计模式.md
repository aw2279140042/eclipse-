# 23中设计模式

## 类之间的关系

### 泛化关系（generalization）

类的集成结构表现在UML中为：泛化（generalize）与实现（realize）；

泛化关系用一条带有空心的箭头直接表示；

继承关系为（A继承自B）

![_images/uml_generalization.jpg](https://design-patterns.readthedocs.io/zh_CN/latest/_images/uml_generalization.jpg)

**注：**最终代码中，泛化关系表现为继承非抽象类

### 实现关系（realize）

实现关系用一条带有空心箭头的虚线表示，图中小汽车和自行车实现了车；

![_images/uml_realize.jpg](https://design-patterns.readthedocs.io/zh_CN/latest/_images/uml_realize.jpg)

**注：**最终代码中，实现关系表现为继承抽象类、实现接口。

### 聚合关系（aggregation）

聚合关系用一条带空心菱形箭头的直线表示，如下图表示A聚合到B上，或者说B由A组成；

![_images/uml_aggregation.jpg](https://design-patterns.readthedocs.io/zh_CN/latest/_images/uml_aggregation.jpg)

聚合关系用于表示实体对象之间的关系，表示整体由部分构成的语义；例如一个部门由多个员工组成；与组合关系不同的是，整体和部分不是强依赖的，即使整体不存在，部分依然存在；

### 组合关系（composition）

组合关系用一条带实心菱形箭头直线表示，如下图表示A组成B，或B由A组成；

![_images/uml_composition.jpg](https://design-patterns.readthedocs.io/zh_CN/latest/_images/uml_composition.jpg)

与聚合关系一样，组合关系同样表示整体由部分构成的语义；但组合关系是一种强依赖关系，如果整体不存在了，部分也不存在。

### 关联关系（association）

关联关系用一条直线表示；它描述不同类的对象之间的结构关系；它是一种静态关系，通常与云心状态无关。关联关系默认不强调防线，表示对象互相知道；如果特别强调方向，如下图，A知道B，但是B不知道A；

![_images/uml_association.jpg](https://design-patterns.readthedocs.io/zh_CN/latest/_images/uml_association.jpg)

**注：**在最终代码中，关联对象通常是以成员变量的形式实现的；

### 依赖关系（dependency）

依赖关系是用一套带箭头的虚线表示的；如下图表示A依赖于B；它描述一个对象在运行期间会用到另一个对象的关系；

![_images/uml_dependency.jpg](https://design-patterns.readthedocs.io/zh_CN/latest/_images/uml_dependency.jpg)



与关联关系不同的是，它是一种临时性的关系，通常在运行期间产生，并且随着运行时的变化依赖关系也可能发生变化；

显然，依赖也有方向，双向依赖时一种非常糟糕的结构，我们重视应该保持单向依赖，杜绝双向依赖的产生。

**注：**在最终代码中，依赖关系体现为类构造方法以及类方法的传入参数，箭头的指向为条用关系；依赖关系除了零时知道对方外，还是“使用”对方的方法和属性；

## 创建型模式

创建型模式（creational pattern）对类的实例化过程进行了抽象，能够将软件模块中对象的创建和对象的使用分离。为了使软件的结构更加清晰，外界对于这些对象只需要知道它们共同的接口，而不清楚其具体的实现细节，使整个系统的设计更加符合单一职责原则。

创建型模式在创建什么（what），由谁创建（who），何时创建（when）等方面都为软件设计者提供了尽最大可能的灵活性。创建型模式隐藏了类的实例的创建细节，通过隐藏对象如何被创建和组合在一起达到了使整个系统独立的目的。

包含模式

- 简单工厂模式（simple factory）
- 工厂方法模式（factory method）
- 抽象工厂模式（abstract factory）
- 建造者模式（builder）
- 原型模式（prototype）
- 单例模式（singleton）

### 简单工厂（simple factory pattern）

简单工厂模式：又被称为静态工厂方法（static factory method）模式，他属于类创建型模式。在简单工厂模式中，可以根据参数的不同返回不同类的实例。简单工厂模式专门定义一个类来负责创建其他类的实例，被创建的实例通常具有共同的父类。

简单工厂模式包含如下角色：

- Factory：工厂角色
  工厂角色负责实现创建所有实例的内部逻辑
- Product：抽象产品角色
  抽象产品角色是所创建的所有对象的父类，负责描述所有实例所共有的公共接口
- ConcreteProduct：具体产品角色
  具体产品角色是创建目标，所有创建的对象都充当这个角色的某个具体类的实例

![../_images/SimpleFactory.jpg](https://design-patterns.readthedocs.io/zh_CN/latest/_images/SimpleFactory.jpg)

时序图

![../_images/seq_SimpleFactory.jpg](https://design-patterns.readthedocs.io/zh_CN/latest/_images/seq_SimpleFactory.jpg)

**模式分析**

- 将对象的创建和对象本身业务处理分离可以降低系统的耦合度，使得两者修改起来都相对容易。
- 在调用工厂类的工厂方法时，由于工厂方法时静态方法，使用起来很方便，可通过类名直接调用，而且只需要传入一个简单的参数即可，在实际开发中，还可以在调用时将所传入的参数保存在XML等格式的配置文件中，修改参数时无需修改任何源码。
- 最大的问题在于工厂类的职责相对过重，增加新的产品需要修改工厂类的判断逻辑，这一点与开闭原则相违背。
- 箱单工厂模式的要点在于，当你需要什么，只需要传入一个正确的参数，就可以获取你所需要的对象，而无需知道其创建细节。

