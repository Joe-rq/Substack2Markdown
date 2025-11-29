# My Core Position on AI-Native Development： Part 2 (for developers)

## 我对 AI 原生开发的核心立场(面向开发者） （中文在最后）

**Nov 18, 2025**

**Likes:** 0

# 🧬 The Fixed-Point Logic of AI-Native System Design —

And Why It Can Resist Entropy in the World of Language

What is the biggest problem in the world of language?

It’s not that we don’t have enough ways to express ourselves.

It’s that **language is inherently a high-entropy system** :

  * vague

  * random

  * polysemous

  * easy to misinterpret

  * drifting over time

  * shifting across contexts

  * the same word can mean completely different things in different minds




This means:

> The default trend of the language world = entropy increase.

If an AI-Native system runs directly on raw natural language,

its world model will inevitably move toward **chaos and non-schedulability**.

So anyone who is serious about building a **long-term stable system inside a language world**

will eventually run into the same foundational question:

> How do we find a non-moving anchor inside an ever-entropy-increasing world of language?

That is the role of a pre-determined **fixed point(不动点）**.

Original protocol reference: 

<https://github.com/STEMMOM/structure-protocols/blob/main/protocols/structure-dna/v1.0/spec.md>

* * *

# Ⅰ. What Is a Fixed Point?

 _(Fixed Point = Structural Anchor)_

A “fixed point” is not a feature, not a code snippet, not a module.

It is a **structural rule that does not change**

with time, environment, application, or implementation style.

It is the philosophical base of the system,

and the shared reference frame for all behavioral logic.

In my system, it takes four concrete forms:

  * field invariants

  * state-machine invariants

  * temporal semantics invariants

  * ledger container invariants




Together, these form the **physical layer of Structure DNA**.

They share three properties:

  1.  **Stable across time**

(you cannot call it `due` today and rename it `deadline` tomorrow)

  2.  **Stable across space**

(every Skill must recognize it)

  3.  **Stable across agents**

(no matter who expresses the language, it collapses into the same structure)




When a structure satisfies these three conditions,

it becomes a **fixed point**.

* * *

# Ⅱ. Why Are Fixed Points Important?

## Because they are the only mechanism that can resist entropy in language.

The nature of natural language is to **keep expanding** :

  * meanings expand

  * meanings drift

  * meanings get distorted

  * meanings get misunderstood

  * meanings decay




If your structure is unstable,

the system will gradually fall into the following pattern:

  1. Fields become polysemous.

  2. Semantics become blurry.

  3. Behavior becomes unpredictable.

  4. The scheduler can no longer infer state.

  5. Feedback can no longer write back reliably into structure.

  6. The lifecycle of the system breaks.




The final outcome is:

> Language entropy ↑ → Structure collapses → System fails.

This is not a theoretical edge case.

This is reality in the natural language world every single day.

The purpose of fixed points is precisely to **break this chain**.

* * *

# Ⅲ. How Do Fixed Points Suppress Entropy?

 _(Examples + Principles)_

#  **Mechanism 1: Structure Compression**

Natural language is a textbook **high-entropy system**. It has:

  * high dimensionality (countless ways to say the same thing)

  * high redundancy (synonyms, analogies, metaphors)

  * non-determinism (context drift)

  * ambiguity (multiple meanings, fuzzy intentions)




If AI relies directly on raw language, it falls into **unbounded entropy** :

  * the more you talk, the more meanings diverge

  * the more you write, the more structure fragments

  * the longer it runs, the less stable the system becomes




Fixed points (Structure DNA) provide the first anti-entropy mechanism:

 **structure compression**.

* * *

## ✅ Example: How Is a Single Sentence Compressed?

User input:

> “Next week please help me organize my paper-writing plan. The earlier the better. I’m feeling a bit anxious, and I probably need to make some progress every day.”

This is a high-entropy utterance, containing:

  * a task (organize a paper-writing plan)

  * an emotion (anxiety)

  * time (next week, as early as possible, every day)

  * vague intention (make some progress)

  * personal state (probably need to)




If you don’t compress it,

the AI may “understand a different version of you” every time it runs.

* * *

## → After Fixed-Point Compression, It Becomes Three Layers:

###  **1\. Language → Primitive IR (Semantic Primitives)**
    
    
    Entity: 论文 (paper)
    Action: 整理 (organize)
    Time: 下周 (next week)
    Frequency: 每天 (every day)
    Constraint: 越早越好 (as early as possible)
    Emotion: 焦虑 (anxious) – can be dropped or stored separately
    
    

Dimensionality is dramatically reduced.

* * *

###  **2\. IR → Structure DNA (Field Layer)**

Compressed into a minimal structural unit:
    
    
    {
      “id”: “G-001”,
      “title”: “Organize Paper”,
      “start”: “2025-02-03T09:00:00”,
      “due”: “2025-02-09T23:59:00”,
      “tags”: [”daily”],
      “status”: “open”,
      “created_at”: “...”,
      “updated_at”: “...”
    }
    
    

Notice:

  * The emotion does not enter the core structure (entropy-filtered).

  * Vague terms are collapsed into `start / due / tags`.

  * “As early as possible” becomes a time range (earlier `start`).

  * “Every day” becomes a behavioral tag (`tags: [”daily”]`).




This is entropy control:

> The divergence of language is compressed into a finite set of fields.

* * *

###  **3\. Structure → Schedulable State**

Now the system can schedule it:
    
    
    open → scheduled → in_progress → done
    
    

High-entropy natural language has been compressed into a

 **schedulable unit of life**.

* * *

## 🧩 Principle Summary

> Structure compression = dimensionality reduction
> 
>  **Dimensionality reduction = entropy reduction**
> 
>  **Entropy reduction = system sustainability**

This is the **first anti-entropy mechanism** in the AI-Native framework.

* * *

# Ⅳ. Mechanism 2: State-Machine Closure

Natural language has **no inherent lifecycle**.

You say “write”, but that could mean:

  * write today

  * write tomorrow

  * write a bit now

  * write a lot later

  * write until… who knows when




No lifecycle = non-schedulable.

Non-schedulable = entropy increase.

Fixed points force language into a **finite state space** :
    
    
    open → scheduled → in_progress → done
    ↑                        ↙
    deferred ← canceled
    
    

* * *

## ✅ Example: How Does a Single “write” Become a Closed Loop?

User says:

> “Let’s start writing the paper tomorrow.”

Natural language is still unstructured.

* * *

### After Transformation:
    
    
    {
      “id”: “S-010”,
      “title”: “Write paper”,
      “start”: “2025-02-02T09:00:00”,
      “status”: “scheduled”
    }
    
    

**From this point onward:**

  * At `start` → automatically enters `in_progress`.

  * When completed → moves to `done`.

  * If postponed → goes to `deferred`.

  * If canceled → goes to `canceled`.




From infinite possibilities → to 6 states.

That is **closure**. That is an anti-entropy structure.

* * *

## 🧩 Principle Summary

  * Natural language state space = infinite.

  * Fixed-point state space = finite (6 states).

  * Finite state machine = schedulable = closable.




> Lifecycle is the temporal skeleton of a structured world.Once you have a state machine, language drift is constrained.

* * *

# Ⅴ. Mechanism 3: Unified Temporal Semantics

Time in natural language is messy:

  * “Send it to me later.”

  * “Do it sometime.”

  * “Let’s find time this week.”

  * “Please handle it ASAP.”




There is no unified reference frame for “time” in language.

You can’t reliably sort, compare, infer, or schedule from it.

Fixed points allow only three temporal keys:
    
    
    start / due / duration
    
    

This is equivalent to constructing:

> a unified coordinate system → a unified time axis → a unified rhythm.

* * *

## ✅ Example: How Does Natural Language Become Unified Time?

User says:

> “Let’s have a meeting next week, about two hours, not too late in the day.”

This is a highly ambiguous temporal expression.

After structuring:
    
    
    {
      “start”: “2025-02-05T09:00:00”,
      “due”: “2025-02-05T11:00:00”,
      “duration”: “2h”
    }
    
    

Now the system can:

  * check for conflicts

  * rank priorities

  * build dependency graphs

  * plan the schedule

  * perform reflection and analytics




A **unified clock** allows the system to run

 **for a long time without collapsing**.

* * *

## 🧩 Principle Summary

  * Many forms of time in language → one form of structured time.

  * Structured time → computable time.

  * Computable → schedulable.

  * Schedulable → feedback-able.

  * Feedback-able → evolvable.




This is the **third anti-entropy mechanism**.

* * *

# Ⅵ. Mechanism 4: Ledger Container Stability

Natural language has infinite extensibility.

Everyone can invent their own format, fields, and structures.

Fixed points (Structure DNA) **force the ledger container** to be:
    
    
    {
      “module”: “...”,
      “schema”: “StructureDNA-v1.0”,
      “last_updated”: “...”,
      “data”: [],
      “metadata”: {}
    }
    
    

This is the **stability layer of the world’s outer shell**.

* * *

## ✅ Example: Why Must the Container Stay Fixed?

Without a fixed container, you will see:

  * someone renaming `data` → `entries`

  * someone removing `metadata`

  * someone replacing `data` with `list`

  * someone writing natural-language strings into `module`




The result:

> AI can no longer read its “old world”,nor maintain a continuous world model.

That is “entropy in the language world.”

By locking the container structure, the system always knows:

  * where the world begins

  * what the world consists of

  * how the world is scheduled

  * how the world can be replayed




Container stability = world stability.

* * *

## 🧩 Principle Summary

  * The container is the “world coordinate system.”

  * Once the coordinate system drifts → all behavior drifts.

  * If the coordinate system is locked → behavior becomes sustainable.




This is the **fourth anti-entropy mechanism**.

* * *

# 🧬 **Summary: Why Do Fixed Points Resist Entropy?**

All four mechanisms share the same essence:

> Infinite language → finite structureInfinite expression → finite statesInfinite time → finite keysInfinite worlds → finite containers

From “infinite” compressed into “finite”,

from “divergent” compressed into “schedulable”,

from “semantic drift” compressed into “structural sequences”—

That is what we call **anti-entropy**.

This is the foundation of a structural civilization,

and the root of AI-Native design.

* * *

# 🧬 **Must / Must Not Checklist for AI-Native Development**

* * *

## 1️⃣ Structure as Fixed Point

### ✅ Must

  *  **Must** treat Structure DNA fields, the state machine, time keys, and the ledger container as **fixed points** , not “suggestions”.

  *  **Must** explicitly declare, in each Skill / protocol, the structural assumptions you depend on:

    * `schema` (e.g. `StructureDNA-v1.0`)

    * `module`

    * state machine (`open / scheduled / in_progress / done / deferred / canceled`)

    * time keys (`start / due / duration`)




### ❌ Must Not

  *  **Must Not** rename, delete, or reinterpret any core fields (e.g. `id / status / created_at / updated_at`).

  *  **Must Not** invent new state names (e.g. `“doing”`, `“processing”`) or new time fields (e.g. `“deadline”`, `“finish_at”`) to replace existing fixed points.




* * *

## 2️⃣ Append-Only Evolution

### ✅ Must

  *  **Must** use an **append-only** strategy when extending structure:

    * add new fields (with defaults or nullable)

    * add new sections

    * add new interpretive layers _without_ changing old meanings

  *  **Must** update `version` / `schema` explicitly during evolution, not “silently”.




### ❌ Must Not

  *  **Must Not** delete fields, change field types (e.g. string → object), or repurpose field meanings (e.g. treat `due` as priority).

  *  **Must Not** “reformat” old structures into a completely different JSON layout just because it looks cleaner.




* * *

## 3️⃣ User Ledger as Single Source of Truth

### ✅ Must

  *  **Must** treat the user’s JSON ledger as the **only authoritative state** :

    * Read: only from the file provided by the user.

    * Write: all changes must be written back to `new_ledger_json`.

  *  **Must** ensure any internal cache or index can always be reconstructed from the ledger, and can be discarded at any time.




### ❌ Must Not

  *  **Must Not** maintain a shadow ledger that only the Skill knows about.

  *  **Must Not** hide critical state in platform DBs, sessions, or configuration without writing it back into the user ledger.




* * *

## 4️⃣ Stateless Skill, Structural State

### ✅ Must

  *  **Must** make Skill behavior as close to a pure function as possible:

    * Input: `ledger + instructions`

    * Output: `new_ledger_json + suggestions + summary`

  *  **Must** write all state that affects future behavior into the ledger, not into code branches or hidden state.




### ❌ Must Not

  *  **Must Not** let a Skill’s behavior depend on “what happened last time” in internal memory.

  *  **Must Not** change system behavior via hidden variables, caches, or temp files without leaving a trace in the ledger.




* * *

## 5️⃣ Preserve Unknown Fields

 _(Respect Other People’s Structure—Don’t Touch What You Don’t Own)_

### ✅ Must

  *  **Must** preserve, when editing an entry:

    * all unknown fields

    * all extension fields written by other Skills

    * any `metadata` subfields you don’t recognize

  *  **Must** assume that **the ledger is a shared public space for multiple developers and agents**.




### ❌ Must Not

  *  **Must Not** “clean up” fields you don’t understand.

  *  **Must Not** assume that fields you didn’t create are “garbage” or safe to delete.

  *  **Must Not** overwrite an entry wholesale with `new_entry = { …your fields… }`.




* * *

## 6️⃣ Honor Time & State Machine Fixed Points

### ✅ Must

  *  **Must** strictly use:

    * time keys: `start / due / duration`

    * state machine: `open / scheduled / in_progress / done / deferred / canceled`

  *  **Must** make state transitions explicit in Skill logic:

    * When does `open → scheduled` happen?

    * Under what conditions does `in_progress → done` happen?




### ❌ Must Not

  *  **Must Not** use tags or notes to imitate state (e.g. `status: “open”` \+ `tag: “finished”`).

  *  **Must Not** jump directly from `open → done` “for simplicity,” leaving the Scheduler and LLC unable to reason about the lifecycle.




* * *

## 7️⃣ Explainable & Auditable

### ✅ Must

  *  **Must** make it possible for humans to see “what happened” in your output:

    * Which entries were changed?

    * Which fields were changed?

    * Why were they changed?

  *  **Must** make it possible for your future self / other developers / other agents to reconstruct the logic from the ledger diff.




### ❌ Must Not

  *  **Must Not** perform “black-box refactors”:

    * massively changing many entries without explanation

    * leaving the user only with “things look different now,” but no idea **why**.




* * *

## 8️⃣ Respect the Fixed Point, Change Everything Else

### ✅ Must

  *  **Must** treat “fixed points” as truly **inviolable base laws** :

    * field invariants

    * state machine invariants

    * temporal semantics invariants

    * ledger container invariants

  *  **Must** innovate freely _on top of_ those:

    * new modules

    * new Skills

    * new protocols

    * new collaboration patterns




### ❌ Must Not

  *  **Must Not** modify fixed points just to make a local use case easier.

  *  **Must Not** put “local convenience” above “global structural order”.




* * *

# 🧬 AI 原生系统设计 **不动点的基本逻辑，以及它为什么能在语言世界中对抗熵增**

语言世界的最大问题是什么？

不是表达不够丰富，

而是 **语言天然是高熵系统** ：

  * 模糊

  * 随机

  * 多义

  * 可被误解

  * 随时间漂移

  * 随场景变化

  * 同一词在不同人脑中完全不同




这意味着：

 **语言世界的默认趋势 = 熵增。**

而 AI-Native 系统如果直接基于自然语言运转，

它的世界模型会不可避免地走向混乱与不可调度。

因此，任何试图在语言世界中构建“长期稳定系统”的人，

都会遇到同一个根本问题：

> 如何在熵增的语言世界里找到一个不会变化的锚点？

这就是“不动点（fixed point）”存在的意义。

协议原文：

<https://github.com/STEMMOM/structure-protocols/blob/main/protocols/structure-dna/v1.0/spec.md>

* * *

# Ⅰ. 什么是不动点？（Fixed Point = Structural Anchor）

“不动点”不是一个功能、不是一个代码片段、不是一个模块。

它是一种 **不会随时间、环境、应用、实现方式而变化的结构性规则** 。

它是系统的哲学基底，也是所有行为逻辑的共同参照帧。

我现在给它的形式就是：

  * 字段不动点

  * 状态机不动点

  * 时间语义不动点

  * Ledger 容器不动点




这些共同构成了 Structure DNA 的物理层。

它们有三个特征：

  1.  **跨时间稳定** （不能今天叫 “due”，明天叫 “deadline”）

  2.  **跨空间稳定** （任何 Skill 都必须识别）

  3.  **跨主体稳定** （无论是谁表达语言，结果都能落入同一结构）




当一个结构具备这三点时，它就成为“不动点”。

* * *

# Ⅱ. 不动点为什么重要？

## 因为它是唯一能对抗语言熵增的机制

自然语言的天性是： **不断发散** 。

意义会扩张、漂移、扭曲、误解、衰减。

如果结构不稳定，系统就会一步步进入以下状态：

  1. 字段变多义

  2. 语义变模糊

  3. 行为变不可预测

  4. 调度器无法判断状态

  5. 反馈无法回写结构

  6. 系统生命周期断裂




最后的终点是：

> 语言熵增 → 结构失效 → 系统崩溃

这不是理论，这是自然语言世界每天的现实。

不动点的作用正是破坏这个链条。

* * *

# Ⅲ. 不动点如何压制熵增？（举例 + 原理）

#  **机制一：结构压缩（Structure Compression）**

自然语言是典型的高熵系统。

它具有：

  * 高维度（无数表达方式）

  * 高冗余（同义、类比、隐喻）

  * 不定性（上下文漂移）

  * 歧义性（多义词、模糊意向）




AI 如果直接依赖自然语言，将陷入无限熵增：

意思越讲越乱、结构越写越散、系统越跑越不稳定。

不动点（Structure DNA）提供的第一层反熵机制就是 **结构压缩** 。

* * *

## ✅ **举例：一句话如何被压缩？**

用户输入：

> “下周帮我整理一下论文的计划，越早越好，我现在有点焦虑，可能需要每天推进一点。”

这是一个高熵语言，里面包含：

  * 任务（整理论文计划）

  * 情绪（焦虑）

  * 时间（下周、越早越好、每天）

  * 模糊意图（推进一点）

  * 个人状态（可能需要）




如果不压缩，AI 每次执行都可能“理解不同版本的你”。

* * *

## → 不动点压缩后的三层结构：

###  **1\. 语言 → Primitive IR（语义原语）**
    
    
    Entity: 论文
    Action: 整理
    Time: 下周
    Frequency: 每天
    Constraint: 越早越好
    Emotion: 焦虑（可丢弃或记录）
    
    

维度高度降低。

* * *

###  **2\. IR → Structure DNA（字段层）**

压缩成最小结构单元：
    
    
    {
      “id”: “G-001”,
      “title”: “整理论文计划”,
      “start”: “2025-02-03T09:00:00”,
      “due”: “2025-02-09T23:59:00”,
      “tags”: [”daily”],
      “status”: “open”,
      “created_at”: “...”,
      “updated_at”: “...”
    }
    
    

看到没有？

  * 情绪没有进入结构（反熵过滤）

  * 模糊词全部结构化到 start/due/tags

  * “越早越好”变成一个时间域（start 最早）

  * “每天”变成一个行为标签（tags: daily）




这就是熵控：

 **语言的发散被压缩成有限字段。**

* * *

###  **3\. Structure → Schedulable State（可调度状态）**

系统现在可以调度它：
    
    
    open → scheduled → in_progress → done
    
    

自然语言被压缩为 **可执行的生命单元** 。

* * *

## 🧩 原理总结：

> 结构压缩 = 降维
> 
>  **降维 = 降熵**
> 
>  **降熵 = 系统可持续**

这是 AI-Native 体系中的第一重反熵机制。

* * *

# Ⅳ. 机制二：状态机闭环（State Machine Closure）

自然语言没有生命周期。

你说“写作”，可能是今天写、明天写、写一点、写很多、写到什么时候都不清楚。

没有生命周期 = 不可调度。

不可调度 = 熵增。

不动点将语言封闭到一个 **有限状态空间** ：
    
    
    open → scheduled → in_progress → done
    ↑                        ↙
    deferred ← canceled
    
    

* * *

## ✅ **举例：一句“写作”如何闭环？**

用户说：

> “明天开始写论文吧。”

自然语言仍然是无结构的。

* * *

### 转化后：
    
    
    {
      “id”: “S-010”,
      “title”: “写论文”,
      “start”: “2025-02-02T09:00:00”,
      “status”: “scheduled”
    }
    
    

**从此开始：**

  * 到了 start → 自动进入 `in_progress`

  * 完成 → 进入 `done`

  * 推迟 → 进入 `deferred`

  * 被取消 → 进入 `canceled`




从无限可能 → 转成 6 个状态。

这就是“封闭性”，就是反熵结构。

* * *

## 🧩 原理总结：

  * 自然语言状态空间 = 无限

  * 不动点状态空间 = 有限（6 个）

  * 有限状态机 = 可调度 = 可闭环




> 生命周期是结构化世界的时间骨架。只要有状态机，语言的漂移就会被限制。

* * *

# Ⅴ. 机制三：时间语义统一（Unified Temporal Semantics）

自然语言中的时间是混乱的：

  * “之后发我”

  * “改天做”

  * “这周找时间”

  * “尽快处理一下”




语言中的“时间”没有统一基准，

无法排序、对比、推断、调度。

而不动点只允许三个时间键：
    
    
    start / due / duration
    
    

这就等同于建立了：

 **统一坐标系 → 统一时间轴 → 统一节奏**

* * *

##  ✅ **举例：自然语言如何变成统一时间？**

用户说：

> “下周开一个会，大概两个小时，不要太晚。”

这是高度模糊的时间表达。

转结构后：
    
    
    {
      “start”: “2025-02-05T09:00:00”,
      “due”: “2025-02-05T11:00:00”,
      “duration”: “2h”
    }
    
    

系统现在可以：

  * 做冲突检测

  * 排优先级

  * 做依赖关系图

  * 做日程规划

  * 做反思与统计




“统一时钟”让系统可以 **长期运行不崩** 。

* * *

## 🧩 原理总结：

  * 多种时间语言 → 一种时间结构

  * 结构化时间 → 可计算时间

  * 可计算 → 可调度

  * 可调度 → 可反馈

  * 可反馈 → 可演化




这是第三重反熵结构。

* * *

# Ⅵ. 机制四：容器强制稳定（Ledger Container Stability）

自然语言具有无限扩展性。

每个人都可能写出不同的格式、不同字段、不同结构。

而不动点（Structure DNA）强制 Ledger 容器必须是：
    
    
    {
      “module”: “...”,
      “schema”: “StructureDNA-v1.0”,
      “last_updated”: “...”,
      “data”: [],
      “metadata”: {}
    }
    
    

这是 **世界的外壳稳定层** 。

* * *

## ✅ **举例：为什么容器必须不变？**

如果没有固定容器，你会看到：

  * 有人把 `data` 改成 `entries`

  * 有人把 `metadata`删掉

  * 有人用 `list` 代替 `data`

  * 有人把 `module`写成自然语言




结果就是：

> AI 无法再读旧世界，
> 
> 也无法维护一个连续的世界模型。

这就是“语言世界的熵增”。

不动点锁定容器结构，让系统永远知道：

  * 世界从哪里开始

  * 世界由哪些部分组成

  * 世界如何被调度

  * 世界如何被回放




容器稳定 = 世界稳定。

* * *

## 🧩 原理总结：

  * 容器是“世界坐标系”

  * 坐标系一旦漂移 → 所有行为都会漂移

  * 坐标系锁定 → 行为变得可持续




这是第四重反熵机制。

* * *

# 🧬 **总结：为什么不动点能反熵？**

四大机制本质上都是：

> 无限语言 → 有限结构无限表达 → 有限状态无限时间 → 有限键无限世界 → 有限容器

从“无限”压缩为“有限”，

从“发散”压缩为“可调度”，

从“语义漂移”压缩为“结构序列”，

这就是反熵。

这是结构文明的基础，也是 AI-Native 的根。

* * *

# 🧬 AI-Native 开发的 **Must / Must Not 清单**

* * *

## 1️⃣ Structure as Fixed Point

### ✅ Must

  *  **Must** treat Structure DNA fields, state machine, time keys, and ledger container as **fixed points** , not “建议值”。

  *  **Must** 在 Skill / 协议中，显式声明自己依赖的：

    * `schema`（如 `StructureDNA-v1.0`）

    * `module`

    * 状态机（`open / scheduled / in_progress / done / deferred / canceled`）

    * 时间键（`start / due / duration`）




### ❌ Must Not

  *  **Must Not** 重命名、删除、重新解释任何核心字段（如 `id/status/created_at/updated_at`）。

  *  **Must Not** 自创状态名（如 `“doing”`, `“processing”`）或时间字段（如 `“deadline”`, `“finish_at”`）来替代既有不动点。




* * *

## 2️⃣ Append-Only Evolution（只追加，不重写）

### ✅ Must

  *  **Must** 在需要扩展结构时，采用 **append-only** ：

    * 增加新字段（有默认值或可为空）

    * 增加新 section

    * 增加新解释层，但不改变旧含义

  *  **Must** 在版本演进时显式更新 `version` / `schema`，而不是“偷偷改”。




### ❌ Must Not

  *  **Must Not** 删除字段、改变字段类型（string → object）、挪用字段含义（把 `due` 当成优先级）。

  *  **Must Not** 将旧结构“重排、重构”为另一个完全不同的 JSON，只因为“看起来更整洁”。




* * *

## 3️⃣ User Ledger as Single Source of Truth（用户 Ledger 是唯一真相源）

### ✅ Must

  *  **Must** 把用户的 JSON ledger 视为 **唯一权威状态** ：

    * 读：只读用户给出的文件

    * 写：所有变更都写回 `new_ledger_json`

  *  **Must** 确保任何内部缓存、索引，都可从 ledger 重建，且随时可丢弃。




### ❌ Must Not

  *  **Must Not** 维护一个“只有 Skill 自己知道”的影子 ledger。

  *  **Must Not** 把重要状态藏在平台 DB、Session、隐藏配置中，而不回写到用户 ledger。




* * *

## 4️⃣ Stateless Skill, Structural State（Skill 无状态，结构有状态）

### ✅ Must

  *  **Must** 让 Skill 行为尽量接近“纯函数”：

    * 输入：`ledger + instructions`

    * 输出：`new_ledger_json + suggestions + summary`

  *  **Must** 把所有会影响后续行为的“状态”，写进 ledger，而不是写进代码分支。




### ❌ Must Not

  *  **Must Not** 让 Skill 的行为依赖“上一次调用时的内部记忆”。

  *  **Must Not** 通过隐藏变量、缓存、临时文件，改变系统行为，却不在 ledger 中留下痕迹。




* * *

## 5️⃣ Preserve Unknown Fields（尊重他人结构，不乱动）

### ✅ Must

  *  **Must** 在修改 entry 时：

    * 保留所有未知字段

    * 保留其他 Skill 写入的扩展字段

    * 保留 `metadata` 中你不认识的子字段

  *  **Must** 假定： **这个 ledger 是一个多开发者、多智能体共享的公共空间** 。




### ❌ Must Not

  *  **Must Not** “清洗”你看不懂的字段；

  *  **Must Not** 认为非自己写的字段就是“脏数据”或“可以删”；

  *  **Must Not** 为了图方便，直接 `new_entry = { …你自己的字段… }` 覆盖原 entry。




* * *

## 6️⃣ Honor Time & State Machine（尊重时间与状态机的不动点）

### ✅ Must

  *  **Must** 严格使用：

    * 时间键：`start / due / duration`

    * 状态机：`open / scheduled / in_progress / done / deferred / canceled`

  *  **Must** 在 Skill 逻辑里，把状态流转写清楚：

    * `open → scheduled` 何时发生？

    * `in_progress → done` 的条件是什么？




### ❌ Must Not

  *  **Must Not** 用 tag 或备注字段代替状态机（例如：`status: “open”` \+ `tag: “finished”`）。

  *  **Must Not** 为了“简单”，直接 `open → done` 跳过中间阶段，让调度器和 LLC 无法推理过程。




* * *

## 7️⃣ Explainable & Auditable（所有改变都要可解释、可追踪）

### ✅ Must

  *  **Must** 在输出里，让人类看得懂“发生了什么”：

    * 哪些 entry 被改？

    * 改了哪些字段？

    * 为什么这样改？

  *  **Must** 让未来的你/别的开发者/别的代理，可以从 ledger 差分中重建这次执行的逻辑。




### ❌ Must Not

  *  **Must Not** 做“黑箱式大改”：

    * 一次性改动大量 entry，却不给任何解释

    * 让用户只能看到“结果变了”，看不到“为什么这样变”




* * *

## 8️⃣ Respect the Fixed Point, Change Everything Else

### ✅ Must

  *  **Must** 把“不动点”真正当作“不可侵犯的底层定律”：

    * 字段不动点

    * 状态机不动点

    * 时间语义不动点

    * Ledger 容器不动点

  *  **Must** 在这个基础上自由创新：

    * 新模块

    * 新 Skill

    * 新协议

    * 新协作模式




### ❌ Must Not

  *  **Must Not** 为了一时方便，直接改动不动点，去适配某个特定场景。

  *  **Must Not** 把“局部方便”放在“全局秩序”之上。




* * *
