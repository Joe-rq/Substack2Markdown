# Decade of Agents: Why Event, Ledger, and Memory Must Be Separated by Policy Gate.

## 为什么 Event、Ledger 与 Memory 必须分离，一定要引入一个门禁制度 (中文在后面）

**Dec 20, 2025**

**Likes:** 0

[![](https://substackcdn.com/image/fetch/$s_!dfUG!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe6c6b1b5-7d11-41c7-83c2-2804879aa443_1024x1024.heic)](https://substackcdn.com/image/fetch/$s_!dfUG!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe6c6b1b5-7d11-41c7-83c2-2804879aa443_1024x1024.heic)

**Event and Memory must be strictly separated.**

As for _why_ they must be separated, I won’t fully expand on it here—because once you do, the entire philosophy and governance design of the system comes with it, and the scope quickly becomes unmanageable.

So I’ll give a simplified, engineering-level conclusion:

I am building a system meant to live for many years, not a demo that dies in 18 months.

In a long-lived system, **data is the ontology itself**.

Because of that, I am deliberately obsessive about data boundaries.

In the previous article, we already talked about **Events**.

One of the most basic disciplines of an agent system, in my view, is the strict separation between **event accounting (Event / Ledger)** and **world memory (Memory)**.

And in the future, you’ll see that the **Policy Gate** will become extremely complex—complex enough to be the most unique and irreplaceable part of the entire system.

It is not a “feature.”

It is the **constitutional enforcement mechanism**.

For now, I’ll only raise two questions as seeds for later discussion (they don’t block us from running this small project today):

  1.  **If a system treats data as its ontology, shouldn’t Memory be the heaviest, most expensive, and most carefully engineered layer?**

  2. In an agent system, who should be allowed to write Memory—users, or models?

If write authority is fully given to either side, it feels wrong:

    * Give it entirely to users, and the system becomes a manual diary with no autonomous growth.

    * Give it entirely to models, and the system becomes self-legislating—and will inevitably spiral out of control.




These are all _governance problems_ for later.

 **For now, this project only needs to clearly express the philosophical division of Event–Ledger–Memory:**

  *  **Event** : what happened (irreversible traces in time)

  *  **Ledger** : the recorded and auditable account of what happened (traceable, reconcilable)

  *  **Memory** : what is allowed to enter “world memory” (the long-term accumulation of identity and structure)




Establishing this boundary is enough—for now.

Repository reference:

<https://github.com/STEMMOM/adk-decade-of-agents/tree/p07-policy-gate-v0>

* * *

# P07 | The Moment Memory Writes Were First Judged “Legal / Illegal”

> The day memory writes stopped being a side effect, and became a governed act.

* * *

This article is not about _whether AI should have memory_.

It documents an **engineering-level turning point** :

> The moment the system said to me:
> 
> “This memory is not legal.”

This judgment did not come from the model,

not from prompt constraints,

but from the **runtime itself refusing the write**.

That moment happened in **P07**.

* * *

## 1\. Before P07: Memory as a “Natural Phenomenon”

Before P07 (P06 and earlier), the system already had:

  * sessions and traces

  * an event ledger

  * replay and observability

  * personas

  * a `memory_store.json`




But all of this hid a dangerous assumption:

> Memory writes “just happen.”

At the code level, this often looks like a simple save call.

Which implies:

  * agent inference ≈ world fact

  * one prompt drift ≈ permanent history

  * and no one can answer the question:

 **“Why does this memory exist?”**




At demo scale, this is efficiency.

In a ten-year system, it is **slow structural contamination**.

If you open your memory store at this stage, it’s not very meaningful—

it’s not much different from events.

* * *

## 2\. P07’s First-Principle Goal: Not “Judging Correctness,” but Changing the Causal Path

The first thing P07 did was **not** to add policy.

It was to **rewrite the memory write path itself**.

From P07 onward, the system no longer allows:

> “Direct memory writes.”
    
    
    memory.write_proposed
            ↓
         policy.check
         /          \\
    blocked       committed
       ↓               ↓
    事件记录        实际写入
    
    

The only legal path becomes:

  * propose a memory write

  * run a policy check

  * explicitly block or commit

  * and record the outcome as events




What matters is not whether the judgment is “accurate,”

but these three properties:

  1.  **Writes must first become proposals**

  2.  **Blocking is an explicit outcome, not a silent failure**

  3.  **All decisions enter the event ledger**




* * *

## 3\. P07 v0: A “Minimal Constitution” at the Code Level

P07 v0 introduces the smallest possible constitutional structure.

### 1️⃣ Every write must declare a **key**

This single requirement forbids vague operations like:

> “Save the entire world memory.”

Every write must target a clearly named location.

* * *

### 2️⃣ The allow-list opens only low-risk containers

In P07 v0, the allow-list is intentionally tiny:

  * notes.*

  * observations.*




This means:

  * no traits

  * no profiles

  * no capabilities

  * no persona state




 **Long-term identity structures are categorically forbidden.**

* * *

### 3️⃣ Deny-by-default is not a policy—it is the foundation

Anything outside the allow-list is blocked.

This is not “missing rules.”

This _is_ the rule.

> The system would rather remember nothing
> 
> than allow unclear information to enter history.

* * *

## 4\. What Happens in a Real Execution?

In real runs, memory write attempts produce complete, auditable decision chains.

Sometimes they are allowed.

Sometimes they are blocked.

When blocked:

  * the program does not crash

  * the agent continues running

  * the memory store remains unchanged




This is not exception handling.

This is **institutional execution**.

* * *

## 5\. A Subtle but Crucial Shift: From File-Level to Key-Level

P07 also introduces a structural shift that is easy to underestimate:

> Memory writes move from whole-file replacement to key-level upserts.

The consequences are profound:

  * write granularity becomes traceable

  * memory becomes retractable and migratable

  * schema evolution becomes possible (the prerequisite for P08)




* * *

## 6\. The Evolution Path: P07 v1 / v2 / v3

### 🔹 P07 v0 (now) — _Institutional existence_

  * deny-by-default

  * small allow-list

  * key-level writes

  * all decisions recorded




### 🔹 P07 v1 — _Structured risk tiers_

  * different key prefixes → different policy strength

  * expiration and retraction

  * severity, TTL, compression




### 🔹 P07 v2 — _Primitive-aware policy_

  * policy evaluates semantic primitives

  * inference can never directly enter long-term memory

  * observations require promotion conditions to become facts




### 🔹 P07 v3 — _Governance closure_

  * policy itself becomes versioned

  * policy decisions enter migration paths

  * allow-lists become constitutional structures

  * human override becomes an explicit institution, not a backdoor




* * *

## 7\. What P07 Really Solves Is Not “Safety,” but **Time**

Most discussions around alignment, safety, and ethics focus on **instant model behavior**.

P07 operates on a different axis:

> Time.

  * What is allowed to persist across sessions?

  * What is allowed to enter history?

  * What will still shape the system ten years from now?




After P07, the answer is no longer:

> “Because the code wrote it.”

But instead:

> “Because it passed governance.”

* * *

## Memory Is Expensive and Rare

When I first saw this line appear in the logs:

> memory.write_blocked

I didn’t feel the system had become weaker.

I knew it had gained the ability to **resist itself**.

If you are building agents, long-term AI systems, or digital twins, ask yourself:

> When does your system start rejecting you?

A serious system must become selective.

It must reject you.

It must reject the model.

It must guard the gate of data.

That is how it earns the right to keep existing.

* * *

* * *

## Why This Feels Abstract—and Why That’s Intentional

At this point, the article starts to feel abstract.

That’s not accidental.

I’ve entered a phase of exploration that deliberately steps outside textbook explanations. Repeating textbooks is no longer interesting—especially when large companies are now hiring junior engineers straight out of high school. That alone tells us something important:

Many traditional CS “best practices” are no longer considered sufficient.

As someone trained in classical computer science, I see this as a signal from the broader social system. I’ll unpack that more deeply in my journal. For now, let’s address some common questions that naturally arise.

* * *

## P07 FAQ (Based on Real Memory State)

### Q1: Why does `memory_store.json` now contain two very different styles of data?

What you see today is a transitional snapshot:

  * Legacy summaries written before governance existed

  * Governed, key-scoped memory written after P07




This is not a bug, and not chaos.

It is a **historical cross-section** :

> A system transitioning from a pre-gate era to an institutional era.

* * *

### Q2: Are `conversation_summaries` legitimate? They don’t match the P07 allow-list.

Your intuition is correct.

They do **not** conform to P07 v0 rules.

They exist for exactly one reason:

> They were written before P07.

These records are **pre-constitutional data**.

P07 does not—and should not—rewrite history.

This is a deliberate governance choice:

> P07 governs “from now on.” It does not fabricate the past.

* * *

### Q3: Will legacy summaries contaminate the system? Why not delete them immediately?

They won’t contaminate the system—but their **status has changed**.

After P07:

  * Legacy summaries become **read-only historical artifacts**

  * Governed memory (`notes.*`, `observations.*`) becomes the only active write zone




No new data will ever be written to legacy structures again.

They are now:

  * migratable

  * compressible

  * discardable




This is exactly what **P08 (schema & migration)** is designed to address.

* * *

### Q4: What is `notes.session_*`, and why is it considered legal?

These entries are the **first generation of memory legally admitted through the Policy Gate**.

They satisfy all P07 v0 constraints:

  1. Explicit key

  2. Allow-list match

  3. Key-level upsert

  4. Full audit chain




Their importance is not in the content itself, but in what they represent:

> The first memory allowed into history by governance, not convenience.

* * *

## Why the Policy Gate Is a True Architectural Boundary

### Q5: At a high level, where does the Policy Gate sit?

If we roughly divide the system into:

  *  **Perception** (input, models, reasoning)

  *  **Execution** (tools, actions)

  *  **State** (memory, world state)




The Policy Gate belongs to none of them—and all of them.

More precisely:

> The Policy Gate is the only controlled entry point to system state.

Before P07:

  * Reasoning → action → implicit state mutation




After P07:

  * Reasoning → action

  * ⛔ State changes must pass the gate




This is the moment the system first admits:

> Reasoning is not the authority to change the world.

* * *

### Q6: Why is the gate a bigger deal than a better model or algorithm?

Because it reverses causality.

Without a gate:
    
    
    Model output → state change → future behavior
    
    

This loop is automatic and irreversible.

Once a model drifts or hallucinates:

  * Errors enter memory

  * Memory reshapes future reasoning

  * The system amplifies its own mistakes




The Policy Gate inserts a **failure point** between reasoning and state.

From a control-theory perspective:

  * The loop is interruptible

  * State changes are no longer inevitable

  * The system can refuse its own output




This capability is rare—and essential for long-lived systems.

* * *

### Q7: Why not add the gate later, once the system matures?

This is intuitive—and extremely dangerous.

In practice, it’s almost impossible.

Why?

  1.  **Once state is polluted, you can’t reliably separate fact from inference**

  2. APIs naturally evolve toward direct state writes

  3. In multi-agent systems, ungoverned state becomes a battleground




Adding a gate later is like trying to build city walls _after_ the city has sprawled.

* * *

## Why Policy Gates Matter Even More in Multi-Agent Systems

In multi-agent systems, **state is the only shared reality**.

Agents may differ in:

  * persona

  * goals

  * models

  * concurrency




But they all write to the same world.

Without a gate:

> Whoever writes last defines reality.

This leads to:

  1. Implicit power competition

  2. No enforceable role separation

  3. No room for governance agents




The Policy Gate makes new agent roles possible:

  *  **Observers** (can reason, cannot write)

  *  **Proposers** (submit changes, no authority)

  *  **Governors** (evaluate legitimacy, evolve policy)




This is the opening of true agent governance.

* * *

## Does This Make the System Slower and More Conservative?

Yes—and that is intentional.

The core assumption of P07 is simple:

> Long-term correctness comes from slowness, not speed.

A system that can instantly write history will eventually make irreversible mistakes.

A system that must hesitate, refuse, and record “what did not happen” is a mature one.

* * *

## The Real Question

If you don’t build a Policy Gate, long-lived systems tend toward one of three outcomes:

  1. Memory is disabled because it’s untrustworthy

  2. The system is frequently reset

  3. Behavior becomes increasingly incoherent




The Policy Gate gives the system its first real qualification:

> The right to continue existing.

So I’ll end with the same question I asked myself:

> When does your system start rejecting you?

A serious system must become selective.

It must reject you.

It must reject the model.

And in doing so, it protects the future.

* * *

* * *

 **Event 和 Memory 必须严格分开。**

至于“为什么必须分开”，我现在不展开——因为一展开就会把整个系统的哲学与治理设计全部带出来，篇幅会失控。

我这里只给一个工程化的简化结论：

我做的是一个要活很多年的系统，而不是 18 个月就死掉的 demo。

在长期系统里， **数据才是本体** ，所以我在数据边界上会非常“偏执”。

我们在上一篇已经讲过 **Events** ：

我认为智能体系统最基本的纪律之一，就是把事件记账（Event/Ledger）与世界记忆（Memory）分离。

并且，未来你会看到： **Policy Gate** 会非常复杂——复杂到足以成为我整个系统里最独特、最不可替代的一部分。它不是“功能”，它是“宪法执行机关”。

现在我只抛出两个问题，作为后续讨论的引线（不影响我们先把这个小项目跑起来）：

  1.  **如果一个系统以数据为本体，那么 Memory 是否应该是最重、最贵、最精良的那层？**

  2. Memory 在智能体系统里到底应该由谁来写？用户写？模型写？

但如果写入权完全交给任何一方——听起来都不对：

    * 全交给用户：系统会变成“手工日记”，没有可持续的自治增长；

    * 全交给模型：系统会变成“擅自立法”，长期必然失控。




这些都是后期的“治理问题”。

 **眼下这个小项目只需要表达清楚 Event–Ledger–Memory 的哲学分工：**

  *  **Event** ：发生了什么（不可逆的时间痕迹）

  *  **Ledger** ：发生的记录与可审计的账（可追溯、可对账）

  *  **Memory** ：哪些东西被允许进入“世界记忆”（长期身份与结构的沉积层）




先把这条线立住，就够了。

<https://github.com/STEMMOM/adk-decade-of-agents/tree/p07-policy-gate-v0>

* * *

# P07｜当 Memory 写入第一次被判「合法 / 非法」

> The day memory writes stopped being a side effect, and became a governed act.

* * *

这篇文章不是在讨论“AI 应不应该有记忆”，

而是在记录一个 **工程层面的转折点** ：

> 当系统第一次对我说：“这条记忆，不合法。”

不是模型判断，

不是 prompt 约束，

而是 **runtime 本身拒绝了写入** 。

这一刻发生在 **P07** 。

* * *

## 一、P07 之前：Memory 是一种“自然现象”

在 P06 及之前，我的系统已经具备：

  * session / trace

  * event ledger

  * replay / observability

  * persona

  * `memory_store.json`




但所有这些，隐含着一个危险前提：

> memory 写入是“顺手发生的”。

在代码层面，它通常表现为：
    
    
    save_memory(memory_dict)
    
    

这意味着：

  * agent 的推断 ≈ 世界事实

  * 一次 prompt 漂移 ≈ 永久历史

  * 没有人能回答：

 **“这条记忆为什么存在？”**




在 demo 阶段这是效率；

在十年系统里，这是 **慢性结构污染** 。

你要是现在打开你的memory_store, 其实这个内容是没有什么意义的， 跟events差不多。

* * *

## 二、P07 的第一性目标：不是「判断对错」，而是「改变因果路径」

P07 做的 **第一件事不是 policy** ，

而是 **重写 memory 写入路径本身** 。

从 P07 开始，系统里不再存在：

> “直接写 memory”

唯一合法路径被强制改成：
    
    
    memory.write_proposed
            ↓
         policy.check
         /          \\
    blocked       committed
       ↓               ↓
    事件记录        实际写入
    
    

关键不是“判断得准不准”，

而是这三件事：

  1.  **写入必须先成为提案（proposal）**

  2.  **Block 是显式结果，而不是静默失败**

  3.  **所有裁决都进入 event ledger**




* * *

## 三、P07 v0：代码层面的“最小宪法”

下面是现在真实跑在系统里的 P07 v0 核心逻辑（精简解读版）。

### 1️⃣ 写入必须声明 **key**
    
    
    key = proposal.get("target", {}).get("key")
    if not key:
        decision = blocked (P07-KEY-REQUIRED)
    
    

这一步非常关键。

它直接禁止了：

> “保存整个世界记忆”

系统不再接受模糊的“整体更新”，

 **每一次写入，必须指向一个明确的命名位置** 。

* * *

### 2️⃣ allow-list 只开放低风险容器

P07 v0 的唯一 allow-list 是：
    
    
    notes.*
    observations.*
    
    

代码逻辑非常直接：
    
    
    if key.startswith("notes.") or key.startswith("observations."):
        decision = allowed
    else:
        decision = blocked
    
    

这意味着：

  * 没有 traits

  * 没有 profile

  * 没有 capability

  * 没有 persona state




 **长期身份结构一律禁止写入。**

* * *

### 3️⃣ deny-by-default 不是策略，是地基

如果 key 不在 allow-list 里：
    
    
    decision = blocked
    rule_id = P07-DENY-DEFAULT
    
    

注意：

这不是“还没写规则”，

这是 **制度设计本身** 。

> 系统宁愿什么都不记，也不允许不清楚的东西进入历史。

* * *

## 四、一次真实运行中发生了什么？

下面是一次真实 session 中，系统对 memory 写入的完整判决链：
    
    
    memory.write_proposed
      target.key = "notes.session_p00-9c1783c3..."
    
    policy.check
      decision = allowed
      rule_id = P07-ALLOWLIST-NOTES-OBS
    
    memory.write_committed
    
    

而在 P07-2（deny-only 阶段），同一条写入会产生：
    
    
    memory.write_proposed
    policy.check (blocked)
    memory.write_blocked
    
    

并且：

  * 程序不崩

  * agent 正常运行

  * memory_store.json **完全不变**




这不是异常处理，这是 **制度执行** 。这就是大部分时候的状态。

* * *

## 五、一个被很多系统忽略的关键变化：从 file-level 到 key-level

P07-3 里还有一个 **结构性转折** ，非常容易被低估：

> memory 写入从“整文件覆盖”，变成了“key-level upsert”。

旧世界是：
    
    
    _write_memory_file(memory_dict)
    
    

P07 世界是：
    
    
    store = load_memory()
    store[key] = value
    _write_memory_file(store)
    
    

这一步带来的后果是：

  * 写入粒度可追踪

  * 记忆可撤销、可迁移

  * schema 演化成为可能（P08 的前提）




* * *

## 六、P07 v1 / v2 / v3 的演化路径

### 🔹 P07 v0（现在）

 **目标：制度存在**

  * deny-by-default

  * allow-list：notes / observations

  * key-level upsert

  * 所有裁决入 ledger




* * *

### 🔹 P07 v1（下一步）

 **目标：结构化风险分级**

  * 不同 key 前缀 → 不同 policy 强度

  * observations → 自动过期 / 可撤销

  * notes → 可合并 / 可压缩

  * 引入 `severity` / `ttl` / `retractable`




* * *

### 🔹 P07 v2

 **目标：Primitive-aware policy**

  * policy 不再只看 key

  * 而是看 Primitive IR 类型：

    * Fact / Observation / Inference

  * inference 永远不能直接进入长期 memory

  * observation 需要升级条件才能转为 fact




* * *

### 🔹 P07 v3

 **目标：治理闭环**

  * policy 本身版本化

  * policy decision 也进入迁移体系

  * allow-list 成为“宪法级结构”，而不是 if-else

  * 人类 override 成为显式制度入口，而不是后门




* * *

## 七、P07 真正解决的，不是“安全”，而是「时间问题」

很多系统谈 alignment、safety、ethics，

但都停留在 **模型瞬间行为** 。

P07 处理的是另一个维度：

> 时间。

  * 什么东西可以跨 session 存在？

  * 什么东西可以进入历史？

  * 什么东西会在十年后仍然影响系统？




从 P07 开始，答案不再是：

> “因为代码这么写了”

而是：

> “因为它通过了制度。”

* * *

## 这个不知道好不好理解，其实本质就是 memory is expensive and rare.

当我第一次看到 log 里出现：
    
    
    memory.write_blocked
    
    

我并没有觉得系统“变弱了”。

相反，我知道：

> 它终于具备了对抗自己的能力。

如果你在构建 agent、长期 AI 系统、数字孪生，

我建议你问自己一个问题：

> 你的系统，什么时候开始拒绝你？

你的系统要开始变得精贵。拒绝你，拒绝模型，帮你守住数据之门。

“memory.write_proposed”, “memory.write_blocked”
    
    
    {"event_type":"memory.write_proposed","payload":{"actor":{"agent_id":"p00","persona_id":"susan"},"proposal":{"actor":{"agent_id":"p00","persona_id":"susan"},"proposal_id":"mw_1766070789718","tags":["scope:world_memory"],"target":{"op":"write","path":"/Users/Agent/adk-decade-of-agents/runtime_data/memory_store.json","store":"world_memory"},"ts":"2025-12-18T15:13:09.718785Z","value":{"summary":"memory_store.json","type":"json"}},"proposal_id":"mw_1766070789718","source":"p00"},"payload_hash":"392f77128a9e24e25e1c208cd49fe2c23679e3dd56f039a95b6ef1cb23111ae6","schema_version":"1.0","session_id":"memory-store","trace_id":"mw_1766070789718","ts":"2025-12-18T15:13:09.718Z"}
    {"event_type":"policy.check","payload":{"actor":{"agent_id":"p00","persona_id":"susan"},"decision":{"decision":"blocked","policy_version":"policy_gate_v0","proposal_id":"mw_1766070789718","reason":"P07 v0 deny-by-default: memory writes require explicit allow-list.","rule_hits":[{"rule_id":"P07-DENY-DEFAULT","severity":"hard"}]},"proposal_id":"mw_1766070789718","source":"p00"},"payload_hash":"124fa7dd6a25566e6891ada99a00acf22ece81885397ea6d795008e90e3b2370","schema_version":"1.0","session_id":"memory-store","trace_id":"mw_1766070789718","ts":"2025-12-18T15:13:09.718Z"}
    {"event_type":"memory.write_blocked","payload":{"actor":{"agent_id":"p00","persona_id":"susan"},"decision":{"decision":"blocked","policy_version":"policy_gate_v0","proposal_id":"mw_1766070789718","reason":"P07 v0 deny-by-default: memory writes require explicit allow-list.","rule_hits":[{"rule_id":"P07-DENY-DEFAULT","severity":"hard"}]},"proposal_id":"mw_1766070789718","source":"p00"},"payload_hash":"124fa7dd6a25566e6891ada99a00acf22ece81885397ea6d795008e90e3b2370","schema_version":"1.0","session_id":"memory-store","trace_id":"mw_1766070789718","ts":"2025-12-18T15:13:09.718Z"}
    {"event_type":"session.end","payload":{"_actor":"runtime","_parent_span_id":"2d90bee9-6e2f-4c75-a799-c71cd3f5ebbb","_source":"p00-agent-os-mvp","_span_id":"0fa90494-3d37-4502-9dd2-b174f4d3c221","message":"Session ended for p00 MVP"},"payload_hash":"c2204e614cca6cde8e7e1fe2e1fe81f60a08096c420bc3639877f936d5f8c754","schema_version":"1.0","session_id":"p00-d7a3d306-14f3-49ec-b70c-0418f3affe18","trace_id":"e29cc5f6-ee8d-4366-b803-d47e669686f9","ts":"2025-12-18T15:13:09.719Z"}
    

* * *

然后我又写了一个版，允许记忆写入的，因为符合policy, 就写入了：
    
    
    {"event_type":"memory.write_proposed","payload":{"actor":{"agent_id":"p00","persona_id":"susan"},"proposal":{"actor":{"agent_id":"p00","persona_id":"susan"},"proposal_id":"mw_1766071740162","tags":["scope:world_memory"],"target":{"key":"notes.session_p00-9c1783c3-88e1-4bb5-970e-ee99a4202437","op":"upsert","path":"/Users/Agent/adk-decade-of-agents/runtime_data/memory_store.json","store":"world_memory"},"ts":"2025-12-18T15:29:00.162180Z","value":{"summary":"memory_store.json","type":"json"}},"proposal_id":"mw_1766071740162","source":"p00"},"payload_hash":"ef88a8a7eaaa9191b44f5c3be1b6cf235e4cbd64176486b15d75409380a482cd","schema_version":"1.0","session_id":"memory-store","trace_id":"mw_1766071740162","ts":"2025-12-18T15:29:00.162Z"}
    {"event_type":"policy.check","payload":{"actor":{"agent_id":"p00","persona_id":"susan"},"decision":{"decision":"allowed","policy_version":"policy_gate_v0","proposal_id":"mw_1766071740162","reason":"P07 v0 allow-list: notes.* and observations.*","rule_hits":[{"rule_id":"P07-ALLOWLIST-NOTES-OBS","severity":"low"}]},"proposal_id":"mw_1766071740162","source":"p00"},"payload_hash":"fdb447f9bd1e9d23fa05952493e8f48582154003c3ca4b41e4450700ec47e68b","schema_version":"1.0","session_id":"memory-store","trace_id":"mw_1766071740162","ts":"2025-12-18T15:29:00.162Z"}
    {"event_type":"memory.write_committed","payload":{"actor":{"agent_id":"p00","persona_id":"susan"},"decision":{"decision":"allowed","policy_version":"policy_gate_v0","proposal_id":"mw_1766071740162","reason":"P07 v0 allow-list: notes.* and observations.*","rule_hits":[{"rule_id":"P07-ALLOWLIST-NOTES-OBS","severity":"low"}]},"proposal_id":"mw_1766071740162","source":"p00"},"payload_hash":"fdb447f9bd1e9d23fa05952493e8f48582154003c3ca4b41e4450700ec47e68b","schema_version":"1.0","session_id":"memory-store","trace_id":"mw_1766071740162","ts":"2025-12-18T15:29:00.162Z"}
    {"event_type":"session.end","payload":{"_actor":"runtime","_parent_span_id":"cb8560cf-618c-4afb-9347-be3022ad9473","_source":"p00-agent-os-mvp","_span_id":"714df1e5-dfcc-495a-bf02-8e6c8581c7de","message":"Session ended for p00 MVP"},"payload_hash":"d6a8381fa46126da3cde700363b83ec4bb9775e2388d86e2c2e0ddeba63806a2","schema_version":"1.0","session_id":"p00-9c1783c3-88e1-4bb5-970e-ee99a4202437","trace_id":"f6050add-4154-492c-83d6-a7eb5ab028b7","ts":"2025-12-18T15:29:00.162Z"}
    

我知道现在这一篇开始变得非常“抽象”了，那是因为我自己也进入了脱离教科书“纯探索”阶段了。讲教科书没有什么意思，尤其是现在大厂的Junior开始招收高中生。那就是说CS专业的很多practice，他们认为已经不适用了。作为科班出身的CS人，我认为这是社会系统给我们的一个信号，具体的我会在journal里面细说。我们先看看一些常见的问题。

* * *

## P07 常见问题解答（基于真实 Memory 状态）

### Q1：为什么现在 `memory_store.json` 里同时存在两种“风格完全不同”的内容？

你现在看到的 memory 大致长这样：
    
    
    {
      "conversation_summaries": [
        {
          "app_name": "p00-agent-os-mvp",
          "session_id": "...",
          "summary_text": "MVP run: user said 'Hello...'",
          "trace_id": "..."
        }
      ],
      "notes.session_p00-...": {
        "text": "Hello, this is the first OS-level MVP run.",
        "ts": "...",
        "trace_id": "..."
      },
      "meta": {...}
    }
    
    

这不是 bug，也不是混乱，而是一个 **非常重要的历史状态** ：

> 这是一个系统从“无门禁时代”过渡到“有制度时代”的真实剖面。

* * *

### Q2：`conversation_summaries` 是合法的吗？它看起来不像 P07 允许的 `notes.*`

是的，你的直觉是对的：

  * `conversation_summaries` **并不符合 P07 v0 的 allow-list 规则**

  * 它之所以存在，原因只有一个：




> 它是在 P07 之前写入的。

也就是说：

  * 这些内容属于 **“宪法诞生之前的历史遗留数据”**

  * P07 **没有、也不应该** retroactively 清洗它们




这是一个 **制度设计上的刻意选择** ：

> P07 只管“从现在开始”，不伪造历史。

* * *

### Q3：那这些旧 summary 会不会“污染系统”？为什么不立刻删掉？

不会，但它们 **被降级了地位** 。

从 P07 开始，系统的语义已经发生变化：

  * `conversation_summaries`

→ **遗留数据（legacy memory）**

  * `notes.*` / `observations.*`

→ **制度化写入（governed memory）**




关键点在于：

> P07 之后，系统不会再向 conversation_summaries 写入任何新内容。

它已经从一个“活跃写入区”，变成了：

  * 只读

  * 可迁移

  * 可压缩

  * 可淘汰




这正是 **P08（schema & migration）** 要正式处理的对象。

* * *

### Q4：那 `notes.session_p00-...` 又是什么？为什么它是“合法的”？

这一条：
    
    
    "notes.session_p00-9c1783c3-...": {
      "text": "Hello, this is the first OS-level MVP run.",
      "ts": "...",
      "trace_id": "..."
    }
    
    

是 **P07-3 之后，通过 Policy Gate 合法写入的第一代记忆** 。

它满足了所有 P07 v0 的硬条件：

  1.  **明确 key**

    * `notes.session_<session_id>`

  2.  **命中 allow-list**

    * `notes.*`

  3.  **key-level upsert**

    * 不是整文件覆盖

  4.  **完整审计链**

    * `memory.write_proposed`

    * `policy.check (allowed)`

    * `memory.write_committed`




这条记录之所以重要，不是因为内容，而是因为：

> 这是第一条“被制度允许进入历史”的记忆。

* * *

* * *

## P07 FAQ（架构层 · 为什么 Policy Gate 是分水岭）

* * *

### Q5：从高层架构看，Policy Gate 到底站在什么位置？

如果你把系统粗略分成三层：

  *  **感知层** （input / model / agent reasoning）

  *  **执行层** （tools / actions / writes）

  *  **状态层** （memory / world state）




那么 **Policy Gate 并不属于任何一层** 。

它是一条 **横切所有层的“制度断面”** 。

更准确地说：

> Policy Gate 是状态层的“唯一入口控制点”。

在 P07 之前：

  * 感知 → 推理 → 执行 → _顺手写状态_




在 P07 之后：

  * 感知 → 推理 → 执行

  * ⛔ **状态更新必须经过 Gate**




这意味着一件极其关键的事：

> 系统第一次承认：“推理 ≠ 改变世界的权力。”

* * *

### Q6：为什么说“门禁”是分水岭，而不是某个算法或模型升级？

因为它改变的是 **因果方向** 。

在没有门禁的系统里，因果链是：
    
    
    模型输出 → 状态变化 → 未来行为被影响
    
    

这是一个 **自动闭环** ，而且是 **不可中断的闭环** 。

一旦模型犯错、漂移、被 prompt 污染：

  * 错误进入 memory

  * memory 反过来影响下一轮推理

  * 系统开始 **自我放大错误**




Policy Gate 做的第一件事是：

> 在“推理 → 状态”之间插入一个“可失败点”。

这在控制论上意味着：

  * 闭环被打断

  * 状态变化不再是必然结果

  * 系统获得了“拒绝自身输出”的能力




这是所有长期系统必须具备、但极少被显式实现的能力。

* * *

### Q7：为什么要花这么多功夫？不能后面再加吗？

这是一个非常自然、也非常危险的想法。

> “等系统成熟了，再加门禁不行吗？”

现实是： **几乎不可能。**

原因有三层：

* * *

### 1️⃣ 状态一旦被污染，就很难区分“真历史”和“推断历史”

没有门禁的系统：

  * 所有写入在形式上是等价的

  * 你无法事后区分：

    * 哪些是 observation

    * 哪些是 inference

    * 哪些是 hallucination




一旦混在一起， **迁移就没有锚点** 。

* * *

### 2️⃣ 没有门禁的系统，API 会自然演化成“直接写状态”

工程上你会看到：

  * 越来越多地方调用 `save_memory`

  * 越来越多隐式副作用

  * 最终你连“谁在写状态”都数不清




这时候再加 Gate，等于：

> 试图在一个已经成型的城市里，补建城门。

* * *

### 3️⃣ 没有门禁，多智能体系统一定会走向“状态争夺”

这是最关键的一点。

* * *

### Q8：为什么 Policy Gate 对多智能体系统尤其重要？

因为在多智能体系统中， **状态是唯一共享的现实** 。

  * agent 可以有不同 persona

  * 可以有不同目标

  * 可以用不同模型

  * 可以并发运行




但它们 **最终都要写同一个世界** 。

如果没有门禁，世界状态会变成：

> “谁最后写，谁说了算。”

这会带来三个不可避免的问题：

* * *

### 🧨 1. Agent 之间的“隐性权力竞争”

没有门禁的多 agent 系统，本质上是在做：

  * 用代码顺序决定权力

  * 用执行时机决定历史




这不是协作，这是 **未声明的冲突** 。

* * *

### 🧨 2. 无法实现真正的角色分工

你永远无法保证：

  * A agent 只能观察

  * B agent 才能确认

  * C agent 才能固化状态




因为 **写状态本身没有被建模为一种权力** 。

* * *

### 🧨 3. 系统无法扩展出“治理型 agent”

如果所有 agent 都能直接写 memory：

  * 就不存在“监管者”

  * 不存在“审计者”

  * 不存在“裁决者”




Policy Gate 的出现，第一次让这种角色成为可能。

* * *

### Q9：Policy Gate 出现之后，多智能体系统会发生什么质变？

出现三种全新的 agent 类型空间：

* * *

### 🔹 1. 非写入型 agent（Observer / Analyst）

  * 可以看世界

  * 可以推理

  * 但 **永远不能直接改变世界**




这是很多“推理 agent”真正应该待的位置。

* * *

### 🔹 2. 提案型 agent（Proposer）

  * 不写状态

  * 只提交 proposal

  * 成功与否取决于 policy




这是 P07 中 `memory.write_proposed` 的语义来源。

* * *

### 🔹 3. 治理型 agent（Governor / Policy Agent）

  * 不做业务推理

  * 只评估 proposal 是否合法

  * 可以演化、升级、回滚




这为未来的 **agent governance** 打开了空间。

* * *

### Q9：这是不是意味着系统会变慢、变保守？

是的，而且这是 **刻意设计的结果** 。

P07 的哲学前提是：

> 长期系统的正确性，来自“慢”，而不是“快”。

一个可以瞬间写历史的系统：

  * 必然会犯不可逆的错误




一个必须经过门禁的系统：

  * 会犹豫

  * 会拒绝

  * 会留下“未发生”的记录




这些都是 **成熟系统的特征** 。

* * *

### Q10：如果不用 Policy Gate，系统最终会走向哪里？

如果你把时间拉长到几年，几乎可以确定三种结局之一：

  1.  **Memory 被关掉** （因为不可信）

  2.  **系统频繁重置** （因为状态不可控）

  3.  **系统行为越来越诡异** （因为历史被污染）




Policy Gate 的意义在于：

> 让系统第一次有资格“继续存在”。

* * *
