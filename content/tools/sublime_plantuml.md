Title: 使用 Sublime + PlantUML 高效地画图
Date: 2015-12-10 22:52
Modified: 2015-12-10 22:52
Tags: sublime, uml
Slug: sublime-plantuml
Authors: Joey Huang
Summary: 本文介绍如何使用 Sublime + PlantUML 的插件画流程图，状态图，时序图等

## 什么是 PlantUML

PlantUML 是一个画图脚本语言，用它可以快速地画出：

* 时序图
* 流程图
* 用例图
* 状态图
* 组件图

简单地讲，我们使用 visio 画图时需要一个一个图去画，但使用 PlantUML 只需要用文字表达出图的内容，然后就可以直接生成图片。看一个最简单的例子：

```
Bob -> Alice : Hello, how are you
Alice -> Bob : Fine, thank you, and you?
```

![demo](http://plantuml.com/plantuml/png/SyfFKj2rKt3CoKnELR1Iy4ZDoSdNKSZ8BrT8B4fLgCmlvO980TKu0PLQARXbvgNgA9Ha9EPbWwHr51BpKa0CUm00)

## 软件安装

这些软件全部是开源或共享软件，不存在版权问题，可以放心使用。

* 安装 [Sublime][2]
  Sublime 是个强大的可扩展的文本编辑器。进入[官网][2]下载对应操作系统下的版本安装即可。
* 安装 [graphviz][3]
  graphviz 是个开源的图片渲染库。安装了这个库才能在 Windows 下实现把 PlantUML 脚本转换为图片。
* 安装 [PlantUML for Sublime][4] 插件
  有了这个插件后，我们就可以在 Sublime 里写 PlantUML 脚本，然后直接通过一个快捷键生成图片。安装步骤如下
    * [下载插件][5]，并解压
    * 通过 `Preferences -> Browse Packages ...` 打开 sublime 的 `Packages` 目录，解压后的插件放在 `Packages` 目录下
    * 重启 Sublime

为了简化使用，可以在 Sublime 里配置个快捷键。打开 `Preferences -> Key Binding - User`，添加一个快捷键：

```
{ "keys": ["alt+d"], "command": "display_diagrams"}
```

上面的代码配置成按住 `Alt + d` 来生成 PlantUML 图片，你可以修改成你自己喜欢的按键。

**效果检验**

最后检验一下工作安装是否正确。打开 Sublime 输入：

```
Bob -> Alice : Hello, how are you
Alice -> Bob : Fine, thank you, and you?
```

选中这些文本内容，按 Alt + d 会在当前工作目录下生成这个图片文件，同时自动弹出窗口显示图片。

## PlantULM 快速入门

### 时序图

```
@startuml

title 时序图

== 鉴权阶段 ==

Alice -> Bob: 请求
Bob -> Alice: 应答

== 数据上传 ==

Alice -> Bob: 上传数据
note left: 这是显示在左边的备注

Bob --> Canny: 转交数据
... 不超过 5 秒钟 ...
Canny --> Bob: 状态返回
note right: 这是显示在右边的备注

Bob -> Alice: 状态返回

== 状态显示 ==

Alice -> Alice: 给自己发消息

@enduml
```

![sequence diagram](http://plantuml.com/plantuml/png/RO_DIiD058Ntzodk2vYTcq84zKbKeWP22fADE-iFqK89beYfzMyHj8WsbjQ9HarU9dCpUGkdCoeKihkSUyxvEE3PdcCXNJAU1NoO0vWcrcSpkZcg8qRZDpHDW5N7th9mQGNNsfij54bAaqEGzrnIlnRoBAnUGXMdYrVgZSltRlbrtn3N3sq2j-rPw5ZRdgmj1XGb5ELLdF7h4KyVHFvHNHtpsAVf23HFbgnlkEw-j7y_brdyMsCOXkpj2NOY2X-NiNhir_qxb38ekmegUjLbTD0HHSY7jvg-P-_iDk23QGF-V-v2pNoq5dHySVHVudCW_2UUJdXmJkoKEWdy0000)

TIPS：

* 使用 `title` 来指定标题
* '->' 和 '-->' 来指示线条的形式
* 在每个时序后面加冒号 `:` 来添加注释
* 使用 `note` 来显示备注，备注可以指定显示在左边或右边
* 使用 `== xxx ==` 来分隔时序图
* 使用 `...` 来表示延迟省略号
* 节点可以给自己发送消息，方法是发送方和接收方使用同一个主体即可

### 用例图

```
@startuml

left to right direction
actor 消费者
actor 销售员
rectangle 买单 {
消费者 -- (买单)
(买单) .> (付款) : include
(帮助) .> (买单) : extends
(买单) -- 销售员
}

@enduml
```

![use case](http://plantuml.com/plantuml/png/oqbDAr4eoLSeoapFA558oInAJIx9pC_ZIamkoIzIUBQjuyMMdIyQMg7ybrCQdavPztJY32wGkiIyz9nKXISxDppjdQfGpGLNhA2hgw014TRaWZ4KzEo0WhjdF5kpJrF1IY4pBpcdD2MLI-FfZdLFkrP2fQ5AhHHIAqfIyrAA4Rg1HY8ih-K20000)

TIPS：

* 用例图
    * 用例图是指由参与者（Actor）、用例（Use Case）以及它们之间的关系构成的用于描述系统功能的静态视图
    * [百度百科][6]上有简易的入门资料，其中用例之间的关系 (include, extends) 是关键
* 使用 `actor` 来定义参与者
* 使用括号 `(xxx)` 来表示用例，用例用椭圆形表达
* 使用不同的线条表达不同的关系。包括参与者与用例的关系，用例与用例的关系

### 流程图

```
@startuml

title 流程图

(*) --> "步骤1处理"
--> "步骤2处理"
if "条件1判断" then
    ->[true] "条件1成立时执行的动作"
    if "分支条件2判断" then
        ->[no] "条件2不成立时执行的动作"
        -> === 中间流程汇总点1 ===
    else
        -->[yes] === 中间流程汇总点1 ===
    endif
    if "分支条件3判断" then
        -->[yes] "分支条件3成立时执行的动作"
        --> "Page.onRender ()" as render
        --> === REDIRECT_CHECK ===
    else
        -->[no] "分支条件3不成立时的动作"
        --> render
    endif
else
    -->[false] === REDIRECT_CHECK ===
endif

if "条件4判断" then
    ->[yes] "条件4成立时执行的动作"
    --> "流程最后结点"
else
endif
--> "流程最后结点"
-->(*)

@enduml
```

![activity diagram](http://plantuml.com/plantuml/png/uoh9BCb9LNYsjV7vYkwdi_TnSMbeQIhewjefA3rRk_JbgYM6JvUqF9_GfiI596O44yjC0mhDNVXazpR3fnrBdarRgwHGaf6QnwK01BfsqIL5fQcnS1NFEYOyNztzRFgsPvtBNopiUJwhvMdNYYTxvoY1bOECUjhHzcpAUeXo8mm3eORcvSEDD7goenU_gH0z2hQsjWfFTgnzENqBnAFFDhO_QzZzl6cd8KWAh38rfpWLeGLeJsLgSInH6lDICjEmUi4OknTWPgEg9S8Ve0W8I4nFrSlF2mBQcbgaeA6ff91Oh504vg4e13ayoDN5CyZLEIJUsSFLsHktJy4XYk8Ov735uH8aEo4X03SMP6HQ8f0NYyiL40r8gSS4M-g1119K0VxWWQHDI0pDQNWweU_vxid0I5A2E0fY7KurG0bWckS20000)

上面的流程图写的时候还是挺直观的，但画出来的图片渲染效果不好，对逻辑的显示不清楚。由于这个原因 PlantUML 实现了另外版本的流程图脚本。

下面是 PlantUML 支持的新版本的流程图脚本，从使用角度来讲，更直观，画出来的图片也更漂亮，推荐使用。

```
@startuml

start
:"步骤1处理";
:"步骤2处理";
if ("条件1判断") then (true)
    :条件1成立时执行的动作;
    if ("分支条件2判断") then (no)
        :"条件2不成立时执行的动作";
    else
        if ("条件3判断") then (yes)
            :"条件3成立时的动作";
        else (no)
            :"条件3不成立时的动作";
        endif
    endif
    :"顺序步骤3处理";
endif

if ("条件4判断") then (yes)
:"条件4成立的动作";
else
    if ("条件5判断") then (yes)
        :"条件5成立时的动作";
    else (no)
        :"条件5不成立时的动作";
    endif
endif
stop
@enduml
```

![active diagram 2](http://plantuml.com/plantuml/png/Aov9B2hXib9wjdRforLB39ykQNa-eKt96YvY11V9J5FGK7esT-6JtTiCdtOiUJPjhPAcGab6Qfw2HabHQQecbm8GM44LFEkOy7nrzxFfsvvrBd-niEVvh9QdNIkUx9rZ3LO5DkffHzkpAUiXwetG3CpBXnW7DX9ggT6J7RsuZ5M2c9kQKvmAruVaNcCquojJYn7c8zjX3BS0tMYOyQXkGz6Bx3wislDICjEuK5bMIYyNxdgwgnyIsCRmm8QeG0vp4sn-WDbj0h4OsLPuM22POOel761ccUBq1AR_uNhm-HtY5mXPN99V0000)

TIPS：

* 使用 `start` 来表示流程开始，使用 `stop` 来表示流程结束
* 顺序流程使用冒号和分号 `:xxx;` 来表示
* 条件语句使用 `if ("condition 1") then (true/yes/false/no)` 来表示
* 条件语句可以嵌套

### 组件图

我们经常使用组件图来画部署视图，或者用来画系统的拓扑结构图。

```
@startuml

package "组件1" {
    ["组件1.1"] - ["组件1.2"]
    ["组件1.2"] -> ["组件2.1"]
}

node "组件2" {
    ["组件2.1"] - ["组件2.2"]
    ["组件2.2"] --> [负载均衡服务器]
}

cloud {
    [负载均衡服务器] -> [逻辑服务器1]
    [负载均衡服务器] -> [逻辑服务器2]
    [负载均衡服务器] -> [逻辑服务器3]
}

database "MySql" {
    folder "This is my folder" {
        [Folder 3]
    }

    frame "Foo" {
        [Frame 4]
    }
}

[逻辑服务器1] --> [Folder 3]
[逻辑服务器2] --> [Frame 4]
[逻辑服务器3] --> [Frame 4]

@enduml
```

![component diagram](http://plantuml.com/plantuml/png/uof8JCvEJ4zLK7g-k-N9xcs6IWhLN0f040qJq3DKYbNGHU8RASMYgJ02gR232nY1j73LSd7bvQV03JP2DzW8pM0Z38ED80Q3J7wnPVwBlNkVpcr_iN3XipczJxiMFfsv0cn7Sav-QGhCQEpAm6vxsR3xnRw9S473M59r696imnZim9J4aiIan69WGFXM1XVcm88XBJyd9RL8GIaa8xDO0OXoAw52C0LWozmWgemXTWDD0sijIim56kUMdu-g5Yni0bCAL8pfQKXe8ap5z2HK1SmiJ3-XAG00)

TIPS:

* 使用方括号 `[xxx]` 来表示组件
* 可以把几个组件合并成一个包，可以使用的关键字为 `package, node, folder, frame, cloud, database`。不同的关键字图形不一样。
* 可以在包内部用不同的箭头表达同一个包的组件之间的关系
* 可以在包内部直接表达到另外一个包内部的组件的交互关系
* 可以在流程图外部直接表达包之间或包的组件之间的交互关系

### 状态图

我们一般使用状态图来画状态机。

```
@startuml

scale 640 width

[*] --> NotShooting

state NotShooting {
    [*] --> Idle
    Idle --> Processing: SignalEvent
    Processing --> Idle: Finish
    Idle --> Configuring : EvConfig
    Configuring --> Idle : EvConfig
}

state Configuring {
    [*] --> NewValueSelection
    NewValueSelection --> NewValuePreview : EvNewValue
    NewValuePreview --> NewValueSelection : EvNewValueRejected
    NewValuePreview --> NewValueSelection : EvNewValueSaved
    state NewValuePreview {
        State1 -> State2
    }
}

@enduml
```

![State Diagram](http://plantuml.com/plantuml/png/SoWkIImgAStDuIfEJin9LJ0sDL0epqmfoU2ArefLqDMrK_3BBmdEoCyloSnBvm8gBab55b6eXglpJCb9vG8HO9vpVbvQPdff4KYDbO9h6OJFXImCquGiNmkr0baTmWg_rFAmn9pIrE3KdDJaaipyF2uC4HHr0KMfPPcfvM0BO69Sw99O3KRH4fIQ1HHDJI53Qt1Y6L0VDDZGT5Tp1OF43HM0fe1PHa3lrt8vfEQb0EC30000)

TIPS:

* 使用 `[*]` 来表示状态的起点
* 使用 state 来定义子状态图
* 状态图可以嵌套
* 使用 `scale` 命令来指定生成的图片的尺寸

## 总结

不需要去记这些标记，在需要的时候去使用它，通过不断地使用来熟悉不同的图的语法。可以下载 [PlanUML 官方文档][7] 作为参考，遇到问题的时候翻一翻，这样很快就可以学会使用 PlantUML 高效地画图。

[1]: http://plantuml.com/
[2]: http://www.sublimetext.com/
[3]: http://graphviz.org/
[4]: https://github.com/jvantuyl/sublime_diagram_plugin
[5]: https://github.com/jvantuyl/sublime_diagram_plugin/tarball/master
[6]: http://baike.baidu.com/view/1281729.htm
[7]: http://plantuml.com/PlantUML_Language_Reference_Guide.pdf