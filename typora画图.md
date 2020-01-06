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
	[*] -->Still
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
e=>end

st->op->cond
cond(yes)->e
cond(no)->op
```

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

