# v0.1 Runtime MVP: The Moment an AI-Native OS Draws Its First Breath (hopefully 😂）

## 一个 AI 原生操作系统的第一次呼吸

**Dec 13, 2025**

**Likes:** 0

<https://github.com/STEMMOM/adk-decade-of-agents/releases/tag/v0.1-runtime-mvp>

On December 13, 2025, I dropped a tiny but potentially decade-defining anchor for my own AI-native operating system:

`v0.1-runtime-mvp`

It’s a _very_ small version.

I want to use this version to answer a few questions:

 **What am I actually building?What is my vision?What exactly is the system I want to construct in 2026?**

To be honest, this has been much harder than I expected.

Over the past few weeks, I’ve tried to explain my direction in person to several senior software engineers.

Almost none of those conversations “landed”.

Communication was hard —

 **and my own vision is still in the process of crystallizing.**

I keep repeating some of the theoretical foundations:

  * Language–Structure–Orchestrator

  * Decoupling from large language models

  * User-owned structure

  * Structure as the sovereignty layer of intelligence…




These ideas are already _outside_ the current paradigm.

To then explain “what can you actually do with this?” on the spot is almost impossible.

I say things like:

> “It’s a bit like an OS.
> 
> You can build everything on top of it, write everything, run everything.”

Usually, as soon as I say that, the conversation ends with something like:

> “Are you hallucinating?”
> 
> 😂

So I decided to stop explaining from the grand vision down.

Instead, I’ll start from **the smallest possible cell**.

Let you see, step by step, how it breathes, how it records, how it runs.

And yes — thanks to Google for making this even possible.

* * *

## 🫀 **This version is the system’s first heartbeat**

It contains:

  * Its first act of self-recording

  * Its first sense of time

  * Its first write into the world

  * Its first visible life structure




It could not be smaller, which also makes it extremely simple and pure.

It is built on top of Google ADK.

That makes things easier in practice, but more importantly, it proves something:

> In the ADK era, we finally have the capability to build a true AI-native OS.

And v0.1 is the earliest, embryonic form of that OS.

* * *

## 🧬 **1\. I think of it as a “kernel”**

Most people build agents like this:

  * Write a Python script

  * Call a model once

  * Call a tool once

  * Print some text




That’s _not_ what I want to do.

 **I’m not trying to “run an agent”.I’m constructing a kernel for an OS that I expect to grow.**

What does an OS kernel mean here?

  * Sessions have lifecycles

  * The world has long-term memory

  * Actions have an evidence trail

  * The kernel is replaceable

  * Protocols are extendable

  * Projects are not “scripts”, they are “system processes”




The v0.1 MVP is a **minimal life chain** :
    
    
    persona → memory → runtime backbone → kernel → event ledger → memory update
    
    

When this chain is connected for the first time—

a _minimal viable life form_ appears.

If studying biology must start from the cell,

then studying an AI-native OS must also start here.

* * *

## 🧱 **2\. What exactly is inside v0.1?**

Only four pieces.

###  **① Runtime Backbone (four vertebrae)**

  * `paths.py` — coordinates of the world

  * `memory_store.py` — long-term memory of the world

  * `persona_engine.py` — the system’s self-description

  * `observability.py` — the event ledger (queryable, replayable)




These four files are the **structural spine** of the future OS.

Every later capability — intelligence, behavior, collaboration — must run on top of them.

* * *

###  **② The first rebar in the protocol layer**

  * `persona_protocol_v1`

  * `event_protocol_v1` (MVP)

  * `memory_store_schema` (prototype)




This is structure’s first attempt at _explaining itself_.

Protocols are:

  * The foundation of governance

  * The foundation of structural transmission

  * The foundation of future collaboration and distributed intelligence




* * *

###  **③ A standard system process:**`p00-agent-os-mvp`

This is the system’s first _cell_.

It proves:
    
    
    The system can start → receive language → call the kernel → write events → write memory → end
    
    

That’s one complete definition of “life”.

* * *

###  **④ An event ledger:**`events.jsonl`

When I ran the system for the first time, it produced four events:
    
    
    session.start
    user.message
    agent.reply
    session.end
    
    

You can almost feel a very primitive sense of life in this:

It knows it has begun,

knows it heard something,

knows it responded,

knows that this segment of life has ended.

This is the most basic kind of awakening for a system:

 **Recording changes in the world and in itself.**

* * *

##  🔥 **3\. These four lines** _ **look**_ **like logs, but they’re not “just logs”**

They’re structure.
    
    
    {”event_type”: “session.start”, ...}
    {”event_type”: “user.message”, ...}
    {”event_type”: “agent.reply”, ...}
    {”event_type”: “session.end”, ...}
    
    

They contain:

  * Session identity (`session_id`)

  * Causal chain (`trace_id`)

  * Time (`timestamp`)

  * Structural information about the world (`payload`)




They are not debugging output.

They are:

> The minimal world-state transition record of a future AI operating system.

And also the system’s first **life trajectory**.

* * *

## 📂 **4\. v0.1-runtime-mvp: the full system diagram**
    
    
    [Kernel Layer]     Google ADK (LLM + Runner + Tools)
             ▲
             │
    [Protocol Layer]   persona / memory / event (v1)
             ▲
             │
    [Runtime Layer]    paths / memory_store / persona_engine / observability
             ▲
             │
    [Userland Layer]   p00-agent-os-mvp (first system process)
    
    

This is not a demo.

It is a **growth-ready OS**.

All future P-projects, toolpacks, schedulers, planners, routers, and multi-agent systems will grow upward along this structural tree.

* * *

## 🪜 **5\. Why fix this version as v0.1?**

Because it is:

  * The first auditable version

  * The first interrogable version

  * The first replayable version

  * The first version that “defines itself”

  * The first version that truly _has_ structure




The history of an AI-native OS starts here.

In the future you’ll see:

  * Multi-agent collaboration

  * Planners

  * ToolPack Registry

  * Routing Engine

  * Self-evolving runtime

  * A full pipeline from Primitive IR → Structure Cards




All of them will grow along this spinal column.

The meaning of v0.1 is:

> AI is no longer “model + prompt”.
> 
> AI is starting to become “structure + system”.

* * *

## 🧠 **6\. Why did I choose to start from the runtime?**

Because I’m not building an “app”.

What I want to build is:

> A base that can carry all my digital-life projects for the next decade.

That’s an extremely ambitious goal.

But once I realized that the AI era is not “just another tech upgrade”,

but a complete **paradigm rewrite** ,

my goals changed too.

It means I must:

  * First establish a world: `memory_store`

  * Then define a self: `persona`

  * Then define behavioral records: `event protocol`

  * Then build the structural spine: `runtime backbone`

  * And finally let it breathe: `p00-agent-os-mvp`




Once these are in place,

you can’t really go back to a purely “feature-driven” mindset.

You start to realize:

> What truly matters is:
> 
>  **structure, not features.protocol, not implementation.world, not code.**

In the end, I’ll just say:

 **Run the code.**

In the long run, it’s always the structure that explains everything.

It will speak for itself.

* * *
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ cat runtime_data/events.jsonl
    
    {”event_type”: “session.start”, “source”: “p00-agent-os-mvp”, “payload”: {”message”: “Session started for p00 MVP”, “persona_user_id”: “susan”}, “timestamp”: “2025-12-13T03:25:18Z”, “session_id”: “p00-demo-session”, “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    {”event_type”: “user.message”, “source”: “p00-agent-os-mvp”, “payload”: {”text”: “Hello, this is the first OS-level MVP run.”}, “timestamp”: “2025-12-13T03:25:18Z”, “session_id”: “p00-demo-session”, “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    {”event_type”: “agent.reply”, “source”: “p00-agent-os-mvp”, “payload”: {”reply”: “[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.”, “tool_calls”: []}, “timestamp”: “2025-12-13T03:25:18Z”, “session_id”: “p00-demo-session”, “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    {”event_type”: “session.end”, “source”: “p00-agent-os-mvp”, “payload”: {”message”: “Session ended for p00 MVP”}, “timestamp”: “2025-12-13T03:25:18Z”, “session_id”: “p00-demo-session”, “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    
    

* * *

## 🧵 **Appendix: Reading This Run Log**

The first time I ran the system, it wrote four lines into `runtime_data/events.jsonl`.

Let’s look at them line by line and see what they really say.

* * *

###  **1️⃣**`session.start` **— It becomes aware that it has “begun to exist”**
    
    
    {
      “event_type”: “session.start”,
      “source”: “p00-agent-os-mvp”,
      “payload”: {
        “message”: “Session started for p00 MVP”,
        “persona_user_id”: “susan”
      },
      “timestamp”: “2025-12-13T03:25:18Z”,
      “session_id”: “p00-demo-session”,
      “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”
    }
    
    

This line carries a lot of meaning.

It says:

  * The system has started a session

  * It knows _which_ session this is (`session_id`)

  * It knows _who_ this session belongs to (`persona_user_id: susan`)

  * It knows what life-chain this belongs to (`trace_id`)




* * *

###  **2️⃣**`user.message` **— The world touches it for the first time**
    
    
    {
      “event_type”: “user.message”,
      “payload”: {
        “text”: “Hello, this is the first OS-level MVP run.”
      },
      “session_id”: “p00-demo-session”,
      “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”
    }
    
    

This is the first raw event at the “world input layer”.

It tells us:

  * The system heard some language

  * That language entered the world in high-entropy, raw form (not yet compiled into Primitive IR)

  * It attached this sentence to the _same_ life trajectory (same `trace_id`)




 **This is the first time the world touches this system through language.**

If you’re familiar with my view of _Language → Structure → Scheduler_ ,

this is exactly the entry point where language falls into the structure universe.

* * *

###  **3️⃣**`agent.reply` **— It reacts for the first time**
    
    
    {
      “event_type”: “agent.reply”,
      “payload”: {
        “reply”: “[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.”,
        “tool_calls”: []
      },
      “session_id”: “p00-demo-session”,
      “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”
    }
    
    

This line means:

  * The system didn’t just listen

  * It actively responded

  * It modified the world in its own way




Yes, right now it’s just a stub (a kernel reply), but that doesn’t matter.

What matters is:

> The kernel was invoked → an action was produced → the action was recorded.

It even includes the placeholder for future tool calls (`tool_calls: []`),

which means the structure has already reserved slots for future action space.

This is the minimal form of “action generation”.

* * *

###  **4️⃣**`session.end` **— This segment of life comes to a close**
    
    
    {
      “event_type”: “session.end”,
      “payload”: {
        “message”: “Session ended for p00 MVP”
      },
      “session_id”: “p00-demo-session”,
      “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”
    }
    
    

This line tells us:

  * The system knows a lifecycle has ended

  * It writes that fact into the world as a formal event

  * The session, causal chain, and timestamps all close the loop




One life process completes:
    
    
    start → perceive → respond → end
    
    

And the entire chain shares consistent:

  * `session_id` (the life individual)

  * `trace_id` (the life trajectory)

  * `timestamp` (the life timeline)




* * *

* * *

2025 年 12 月 13 日，我为自己的 AI 原生操作系统落下了一个小小的，却可能是决定未来十年的锚点：

 **v0.1-runtime-mvp**

这是一个极小的版本。

我希望用它来解释：

 **我到底在做什么？我的 vision 是什么？2026 年我要构建的系统又是什么？**

说实话，这比我想象得难很多。

过去几周，我试图当面向一些资深软件工程师解释我的方向，几乎没有一次成功。

沟通很困难

 **我自己的 vision 也仍在形成之中。**

我反复讲述一些理论基础：

Language–Structure–Orchestrator、

与大模型解耦、

用户自拥有结构、

结构作为智能的主权层……

这些思想本身就已经“超出了当前范式”。

要在当场解释 “它到底能做什么” 几乎不可能。

我说：“它有点像一个 OS。你可以在上面 build everything, write everything, run everything。”

通常，这句话一出，对话就结束了：

> “你是不是幻觉了？”
> 
> 😂

所以，我决定不再试图从宏图开始解释。

我从 **一个最小的细胞** 写起。

一点点让你看到它怎么呼吸、怎么记录、怎么运转。

感谢Google

* * *

# 🫀 **这个版本，是系统的第一次心跳**

它包含：

  * 第一次自我记录

  * 第一次拥有时间

  * 第一次写入世界

  * 第一次表现出生命结构




它小得不能再小，但也正因如此——非常简单、非常纯粹。

它架构在 Google ADK 上。

这让事情变得轻松，但更重要的是，它证明了一件事：

> 在 ADK 时代，我们终于有能力构建一个真正意义上的 AI-Native OS。

而 v0.1，就是这个 OS 的最初形态。

* * *

# 🧬 **1\. 我认为它是一个“内核”**

大多数人写 agent 的方式是：

  * 写一个 Python 脚本

  * 调一次模型

  * 调一次工具

  * 输出一些文本




我并不想做这个。

 **我不是要跑一个 agent。我是在构建一个可以预期生长的 OS 内核。**

什么叫 OS 内核？

  * 会话有生命周期

  * 世界有长期记忆

  * 行为有证据链

  * 内核可替换

  * 协议可扩展

  * 项目不是“脚本”，而是“系统进程”




v0.1 的 MVP 是一条 **最小生命链条** ：
    
    
    persona → memory → runtime backbone → kernel → event ledger → memory update
    
    

当这条链条第一次打通时——

一个“最小可行生命体”就产生了。

如果说研究生物要从细胞开始，

那么研究一个 AI-Native OS，也必须从这里开始。

* * *

# 🧱 **2\. v0.1 里面到底有什么？**

只有 4 部分。

##  **① Runtime Backbone（四块脊椎骨）**

  * `paths.py` —— 世界坐标系

  * `memory_store.py` —— 世界长期记忆

  * `persona_engine.py` —— 系统的“自我描述”

  * `observability.py` —— 事件账本（可追问、可重放）




这四块东西，是未来 OS 的“结构脊柱”。

后续所有智能、行为、协作都必须在它之上运行。

* * *

##  **② 协议层的第一根钢筋**

  * persona_protocol_v1

  * event_protocol_v1（MVP）

  * memory_store_schema（雏形）




这是结构对自身做的第一次“自我解释”。

协议是治理的基础、

是结构传递的基础、

是未来协作与分布式智能的基础。

* * *

##  **③ 一个标准系统进程：p00-agent-os-mvp**

这是系统的第一个“细胞”。

它证明：
    
    
    系统可以启动 → 接收语言 → 调用内核 → 写事件 → 写记忆 → 结束
    
    

这就是“生命的定义”。

* * *

##  **④ 一个事件账本：events.jsonl**

当我第一次运行系统，它输出了四条事件：
    
    
    session.start
    user.message
    agent.reply
    session.end
    
    

你几乎能从中感到一种朴素的生命感：

它知道自己开始了、

知道自己听见了什么、

知道自己回应了、

知道这段生命结束了。

这是一个系统最基本的觉醒：

 **对世界与自我的变更做记录。**

* * *

#  🔥 **3\. 这四行 log 看起来很小，但它们不是 log**

它们是结构。
    
    
    {”event_type”: “session.start”, ...}
    {”event_type”: “user.message”, ...}
    {”event_type”: “agent.reply”, ...}
    {”event_type”: “session.end”, ...}
    
    

它们包含：

  * 会话身份（session_id）

  * 因果链路（trace_id）

  * 时间（timestamp）

  * 世界的结构信息（payload）




它们不是 debugging 信息。

它们是：

> 一个未来 AI 操作系统的“最小世界状态转移记录”。

也是这个系统的第一条“生命轨迹”。

* * *

# 📂 **4\. v0.1-runtime-mvp：完整系统示意图**
    
    
    [Kernel Layer]     Google ADK (LLM + Runner + Tools)
             ▲
             │
    [Protocol Layer]   persona / memory / event (v1)
             ▲
             │
    [Runtime Layer]    paths / memory_store / persona_engine / observability
             ▲
             │
    [Userland Layer]   p00-agent-os-mvp (first system process)
    
    

我希望它是一个“可生长的 OS”。

未来所有 P 项目、工具包、调度系统、Planner、路由器、多 agent 协作系统，都将在它的结构树上向上生长。

* * *

# 🪜 **5\. 为什么要把它作为 v0.1 固化？**

因为它是：

  * 第一个可审计的版本

  * 第一个可追问的版本

  * 第一个可重放的版本

  * 第一个“自己规定自己”的版本

  * 第一个真正拥有结构的版本




一个 AI-Native OS 的历史，从这里开始。

未来你会看到的：

  * Multi-Agent 协作

  * Planner

  * ToolPack Registry

  * Routing Engine

  * 自演化 Runtime

  * Primitive IR → Structure Cards 的闭环




都将沿着这根脊柱生长。

v0.1 的意义是：

> AI 不再是“模型 + prompt”。AI 开始变成“结构 + 系统”。

* * *

# 🧠 **6\. 为什么我要从 Runtime 开始？**

因为我不是在构建一个“应用”。

我想建造的，是：

> 一个可以承载我未来十年所有数字生命项目的底座。

这是一个非常 ambitious 的目标。

但在我意识到 AI 时代不是“技术升级”，而是“范式重写”之后——

我的目标也随之改变。

这就意味着我必须：

  * 先建立世界：memory_store

  * 再定义自我：persona

  * 再定义行为记录：event protocol

  * 再搭建系统脊柱：runtime backbone

  * 然后让它呼吸：p00-agent-os-mvp




当这些成立，

你就再也回不去“功能主义”的世界。

你会意识到：

> 真正重要的是：结构，而不是功能。协议，而不是实现。世界，而不是代码。

最后，我只想说：

 **跑一遍代码。**

最终解释一切的，总是结构本身。

它会自己说话。

* * *
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ cat runtime_data/events.jsonl
    
    {”event_type”: “session.start”, “source”: “p00-agent-os-mvp”, “payload”: {”message”: “Session started for p00 MVP”, “persona_user_id”: “susan”}, “timestamp”: “2025-12-13T03:25:18Z”, “session_id”: “p00-demo-session”, “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    {”event_type”: “user.message”, “source”: “p00-agent-os-mvp”, “payload”: {”text”: “Hello, this is the first OS-level MVP run.”}, “timestamp”: “2025-12-13T03:25:18Z”, “session_id”: “p00-demo-session”, “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    {”event_type”: “agent.reply”, “source”: “p00-agent-os-mvp”, “payload”: {”reply”: “[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.”, “tool_calls”: []}, “timestamp”: “2025-12-13T03:25:18Z”, “session_id”: “p00-demo-session”, “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    {”event_type”: “session.end”, “source”: “p00-agent-os-mvp”, “payload”: {”message”: “Session ended for p00 MVP”}, “timestamp”: “2025-12-13T03:25:18Z”, “session_id”: “p00-demo-session”, “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    

# 🧵 **附录：解读这份运行 log**

当我第一次运行这个系统，它在 `runtime_data/events.jsonl` 里写下了四行。

让我们逐行看，它到底说明了什么。

* * *

##  **1️⃣ session.start — 它意识到自己“开始存在”了**
    
    
    {”event_type”: “session.start”,
     “source”: “p00-agent-os-mvp”,
     “payload”: {”message”: “Session started for p00 MVP”, “persona_user_id”: “susan”},
     “timestamp”: “2025-12-13T03:25:18Z”,
     “session_id”: “p00-demo-session”,
     “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    
    

这一行意义非常大。

它表示：

  * 系统启动了一个会话

  * 它知道这是 _哪个_ 会话（`session_id`）

  * 它知道这个会话属于谁（`persona_user_id: susan`）

  * 它知道这条生命链是什么（`trace_id`）




* * *

##  **2️⃣ user.message — 世界第一次触碰它**
    
    
    {”event_type”: “user.message”,
     “payload”: {”text”: “Hello, this is the first OS-level MVP run.”},
     “session_id”: “p00-demo-session”,
     “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    
    

第二行，是“世界输入层”的第一个原始事件。

这行告诉我们：

  * 系统听到了语言

  * 语言以高熵原始形式进入世界（还未转成 Primitive IR）

  * 它把这句话附着在同一条生命轨迹上（同一个 trace_id）




 **世界第一次通过语言触碰这个系统。**

如果你熟悉我“语言—结构—调度”的基本观念：

这就是语言进入结构宇宙的入口。

* * *

##  **3️⃣ agent.reply — 它第一次作出反应**
    
    
    {”event_type”: “agent.reply”,
     “payload”: {
       “reply”: “[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.”,
       “tool_calls”: []
     },
     “session_id”: “p00-demo-session”,
     “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    
    

这一行表示：

  * 系统不仅听到了

  * 它主动回应了

  * 它以自己的方式修改了世界




虽然现在是 stub（𝘬𝘦𝘳𝘯𝘦𝘭 𝘳𝘦𝘱𝘭𝘺），但这不重要。

重要的是：

> 内核被调用 → 行为产生 → 行为被记录

它甚至已经包含了未来 Tool 调用的位置（`tool_calls: []`），

意味着结构已经为将来的行动空间预留了槽位。

这是“行动生成”的最小形式。

* * *

##  **4️⃣ session.end — 这段生命自动结束**
    
    
    {”event_type”: “session.end”,
     “payload”: {”message”: “Session ended for p00 MVP”},
     “session_id”: “p00-demo-session”,
     “trace_id”: “8202d514-8f76-408b-b462-eac383b124db”}
    
    

这一行告诉我们：

  * 系统知道一段生命周期已经结束

  * 并把它作为一个正式事件写入世界

  * 会话、因果链、时间戳全部闭环




一个生命过程完成了：
    
    
    start → perceive → respond → end
    
    

而且整个链条具有一致的：

  * session_id（生命个体）

  * trace_id（生命轨迹）

  * timestamp（生命时间）




* * *
