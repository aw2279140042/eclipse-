# typora画图

```mermaid
%%饼图
pie
	title Pie chart
	"Dogs":386
	"Cats":85
	"Rats":150
```

```mermaid
%%状态图
stateDiagram
	[*] -->Still: ss
	Still -->[*]
	
	Still --> Moving
	Moving --> Still
	Moving --> Crash
	Crash --> [*]
```

```mermaid
%%类图
classDiagram
	Animal <|-- Duck
	Animal <|-- Fish
	Animal : +int age
	Animal : +String gender
	Animal : +isMammal()
	Animal : +mate()
	class Duck{
		+String beakColor
		+swim()
		+quack()
	}
	class Fish{
		-int sizeInFeet
		-canEat()
	}
```

```mermaid
graph LR
A[Hard edge] -->B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
    C -->|Three| A
    C -->|Four| C
```

```mermaid
%% 顺序图
  sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    alt is sick
    Bob->>Alice: Not so good :(
    else is well
    Bob->>Alice: Feeling fresh like a daisy
    end
    opt Extra response
    Bob->>Alice: Thanks for asking
    end
```

```flow
%%流程
st=>start: Start
op=>operation: Your Operation
cond=>condition: Yes or No?
sub1=>subroutine: 子流程
io=>inputoutput: 输入输出框
e=>end

st->op->cond
cond(yes)->io->e
cond(no)->sub1(top)->op
```

时序图（不支持%%注释）

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
Note over Alice,Bob: over
```

```mermaid
%% 时序图例子,-> 直线，-->虚线，->>实线箭头

  sequenceDiagram

    participant 张三

    participant 李四

    张三->王五: 王五你好吗？

    loop 健康检查

        王五->王五: 与疾病战斗

    end

    Note right of 王五: 合理 食物 <br/>看医生...

    李四-->>张三: 很好!

    王五->李四: 你怎么样?

    李四-->王五: 很好!
```

```mermaid
%% 语法示例

        gantt

        dateFormat  YYYY-MM-DD

        title 软件开发甘特图

        section 设计
        需求                      :done,    des1, 2014-01-06,2014-01-08
        原型                      :active,  des2, 2014-01-09, 3d
        UI设计                     :         des3, after des2, 5d
        未来任务                     :         des4, after des3, 5d
        section 开发
        学习准备理解需求                      :crit, done, 2014-01-06,24h
        设计框架                             :crit, done, after des2, 2d
        开发                                 :crit, active, 3d
        未来任务                              :crit, 5d
        耍                                   :2d  
        section 测试
        功能测试                              :active, a1, after des3, 3d
        压力测试                               :after a1  , 20h
        测试报告                               : 48h
```

