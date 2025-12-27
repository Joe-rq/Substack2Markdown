# Decade of Agents · P08 — Memory Schema & Migration

## 记忆的schema和migration才是数据本体系统能活十年的基建（中文在后面）

**Dec 22, 2025**

**Likes:** 0

## When writes begin to version themselves, the system finally starts to look like something that can live for ten years

Continuing from the previous post, I want to start with a very short log.

This _Lessons & Prompts_ series is less a tutorial and more a **development log**. I almost treat it as a rule: _if I touched code today, I must write a piece today_. It serves as a **forced pause point** in my solo development process.

That’s why these posts are naturally connected. If you actually want to reproduce or truly understand what’s happening, going back through the history will help far more than reading a single post in isolation.

The log below looks like an ordinary warning, but in reality, it marks the first time this system truly **grounds a “ten-year mindset” into runtime enforcement** :
    
    
    (.venv) ➜  adk-decade-of-agents git:(p07-policy-gate-v0) ✗ \\
    python -m projects.p00-agent-os-mvp.src.main
    
    WARNING: Memory write blocked by policy: write must use current schema_version;
    older versions belong in legacy via migration
    
    [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
    
    

You can read this as a **constitutional clause** :

> New writes must use the current generation (current schema_version).
> 
> Older generations must not be mixed directly into active memory; they may only enter the system via migration into legacy.

Only when a system is willing to choose **“writing correctly”** over **“writing at all”** does it begin to show the character of a **long-term system**.

 **That single choice contains the entire meaning of P08.**

https://github.com/STEMMOM/adk-decade-of-agents/tree/p08-schema-governance-v0

[![](https://substackcdn.com/image/fetch/$s_!-4lL!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ea442be-bdbf-4bac-b17d-07d9c2b529a9_1024x1536.heic)](https://substackcdn.com/image/fetch/$s_!-4lL!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ea442be-bdbf-4bac-b17d-07d9c2b529a9_1024x1536.heic)

* * *

## 1\. What P08 does: turning “memory versioning” into a runtime fact

Before P07, “writing memory” was essentially just a function call:

You write it, it gets written—at most with some field validation.

P07 marked the real boundary:

 **Writes were elevated into explicit governance actions** :
    
    
    write_proposed
    → policy.check
    → write_committed / blocked
    
    

P08 then adds a **harder law** on top of that gate:

> The Schema Version Law

The goal of P08 is not to make memory richer, but to make memory resemble the **ontology of a long-lived world** :

  * The same memory store will survive multiple structural upgrades

  * Old data must be allowed to exist (history cannot be erased)

  * But old data must be prevented from continuing to grow as _active world facts_

  * Therefore, the system must have:

 **schemas, versions, migration, partitioning, and confrontation**




As I write this log, the time is **2025-12-21 (US East Coast)**.

I’ve just completed a write using a new schema and finished a smoke test.

The memory structure now looks roughly like this (legacy first, then new writes):
    
    
    {
      "legacy": {
        "notes.session_p00-0f5c6f7a-2b38-4132-b844-900fb9278c7a": {
          "text": "Hello, this is the first OS-level MVP run.",
          "ts": "2025-12-21T22:32:48.552157+00:00",
          "trace_id": "a29e1ac2-8c1d-411c-9d7a-5e76c8646ba8"
        }
      },
      "notes.session_p00-0f5c6f7a-2b38-4132-b844-900fb9278c7a": {
        "text": "Hello, this is the first OS-level MVP run.",
        "ts": "2025-12-21T22:32:48.552157+00:00",
        "trace_id": "a29e1ac2-8c1d-411c-9d7a-5e76c8646ba8"
      },
      "observations.smoke_test": {
        "ts": "2025-12-21T22:53:20.134662Z",
        "note": "smoke test"
      }
    }
    
    

* * *

## 2\. The foundations of P08: three pillars, none optional

P08 is not “just writing a migration script.”

It stands on three foundations.

* * *

### 2.1 Data ontology: Memory is ontology

I previously stated a rather uncompromising principle:

> Anything that can be generated after the fact does not qualify as ontology.
> 
> What barely qualifies must satisfy three conditions:
> 
>  _written at the time, without knowing the outcome, while bearing real risk._

This principle transforms memory from “summaries / knowledge caches” into **auditable facts of the system’s world**.

Once memory becomes ontology, a hard engineering consequence follows:

> Ontological structure cannot change freely,
> 
> but the world inevitably changes—
> 
> therefore it must version forward, not fracture.

This is the **philosophical necessity** of P08.

* * *

### 2.2 Gate constitution: Policy Gate as constitutional enforcement

P07 already upgraded writes from “usability engineering” to “governance engineering.”

P08 clarifies one more thing:

> The gate does not only filter content—it filters generational legitimacy.

In other words:

  * The OS never trusts the _semantics_ of the payload

  * The OS only trusts the _legal properties_ of the envelope

  * `schema_version` is one of those core legal properties




So in P08, validating `schema_version` is **not field validation**.

It is **constitutional enforcement**.

* * *

### 2.3 Partitioning and migration: Active vs Legacy + migration-only

The core P08 design is intentionally simple:

  *  **Active** : current-generation memory that continues to grow and be scheduled

  *  **Legacy** : historical data that may only be reviewed, audited, or migrated

  * The **only legal path** from old to new: migration




If old generations are allowed to write directly into active memory,

then `schema_version` is merely a comment.

 **Only when old generations are forcibly confined to legacy does**`schema_version` **become law.**

* * *

## 3\. A key principle: why Startup Confrontation must happen in p00

One **design red line** in P08 is this:

> Schema confrontation must not wait until the first memory write.

The reason is simple—and fatal if ignored:

  * History would already have been implicitly used

  * Legacy data may already have participated in decisions

  * Temporal ethics would already be broken




The only legal order is:
    
    
    system startup
    → confront history
    → then allow sessions
    
    

This is why **Startup Confrontation must occur explicitly in p00**.

p00 is the only correct location.

* * *

## 4\. What happened after that log: how P08 was made to pass

Making P08 truly work boiled down to one thing:

> Pin down “what is the current generation” as a single source of truth,
> 
> and force every write path to obey it.

The final smoke output looked like this:
    
    
    observation write: {'status': 'committed', ...}
    missing schema_version: {'status': 'blocked', 'reason': 'UC-01: missing schema_version'}
    
    

This is not “tests passing.”

It is proof that two laws are now enforced:

  1.  **Legal writes must be committed**

  2.  **Missing schema_version must be blocked with a precise UC-01 reason**




The full smoke run:
    
    
    python -m projects.p08_memory_schema_migration_smoke
    
    
    
    
    observation write: { status: committed, decision: allowed, ... }
    missing schema_version: { status: blocked, reason: UC-01 }
    
    

**Here, a smoke test is not testing functionality—it is testing whether the system dares to reject itself.**

* * *

## 5\. What comes after P08

Passing P08 only means one thing:

 **The system has earned the right to become long-lived.**

It does not mean the work is finished.

At minimum, the following directions remain (to be expanded in P09/P10):

  * Freeze P08 outcomes as **constitutional CI regression tests**

  * Enforce canonical schema_version writes everywhere

  * Make migration itself auditable via a migration ledger

  * In P09, turn governance execution into observable metrics

  * In P10, fully process-ify the system




* * *

## 6\. Conclusion: P08 is not about versions—it is about refusing yourself

The most important thing in P08 is not the `schema_version` field.

It is the choice made in front of that log:

  * Allowing the system to reject writes for long-term consistency

  * Confining old generations to legacy and migration paths

  * Proving enforcement through smoke tests

  * Freezing governance semantics via CI




This is a rare engineering posture:

> Slow if necessary.
> 
> Hard if required.
> 
> Write less if that’s what it takes.
> 
>  **But never mix generations.**

True long-term reliability is born precisely from this kind of refusal.

* * *

After AI began to truly write code, a friend I met on Twitter—his name should be **Junzi Zhongyong** —said something that stayed with me:

> Documentation should outweigh code.

For a long time, I didn’t fully agree.

I was more fluent in another engineering culture:

> Talk is cheap. Give me the code.

But my judgment has fundamentally changed.

I’ve gradually realized that in an era where **AI can fill in implementation details at any time** , code itself is shifting from a _scarce asset_ to a _renewable resource_.

So my position has become this:

> I need to talk, but not too much.
> 
>  **I need to write code, but the code itself is not essential.**
> 
>  **What I truly need is a large body of documents—because AI can finish the job whenever I want.**

These documents are not comments, not READMEs, and not “to be filled in later.”

They are **protocols, boundaries, constitutions, constraints, and non-negotiable judgments**.

Code can be regenerated, rewritten, and migrated endlessly by AI.

But **without these documents, a system will slowly deform through one “reasonable” refactor after another**.

That is why I have attached **all protocols written during P08** at the end.

* * *

## 当写入开始“不断代”，系统才第一次像一个能活十年的东西

紧接上文，我想从一条非常短的 log 开始。

这个 _Lessons & Prompts_ 系列，与其说是教程，不如说是我的 **开发日志** 。我几乎是“只要今天动了代码，就一定顺手写一篇”，把它当成一个 **个人开发的强制暂停点** 。

所以它们天然是连在一起的——如果你真的想复现或理解，翻回去看历史反而更有帮助。

下面这条 log，看起来像个普通警告，但实际上，它标志着这个系统第一次 **把“十年主义”真正落到了运行时执法路径上** ：
    
    
    (.venv) ➜  adk-decade-of-agents git:(p07-policy-gate-v0) ✗ \\
    python -m projects.p00-agent-os-mvp.src.main
    
    WARNING: Memory write blocked by policy: write must use current schema_version;
    older versions belong in legacy via migration
    
    [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
    
    

你可以把它读成一句 **宪法条文** ：

> 新写入必须使用当前代（current schema_version）。旧代内容不得直接混入现役记忆（active memory），只能经由迁移进入历史区（legacy）。

如果一个系统愿意在

 **“能不能写进去”** 和 **“写得是否正确”** 之间选择后者，

它才第一次具备了 **长期系统** 的气质。

 **P08 的全部意义，就在这一句选择里。**

* * *

## 1\. P08 在做什么：把“记忆不断代”变成运行时事实

在 P07 之前，“写 memory”本质上还是一个函数调用：

写就写了，最多做一些字段校验。

P07 的分水岭在于：

 **写入被提升为一个显式治理动作** ：
    
    
    write_proposed
    → policy.check
    → write_committed / blocked
    
    

P08 则是在这套门禁之上，再加了一条 **更硬的法律** ：

> 代际法（Schema Version Law）

P08 的目标不是让 memory 更丰富，而是让 memory 更像一个 **长期世界的本体** ：

  * 同一份 memory store 会跨越多次结构升级

  * 系统必须允许旧数据存在（历史不可抹去）

  * 但系统必须禁止旧数据以“现役世界事实”的身份继续增长

  * 于是就必须有：

 **schema、版本、迁移、分区、对抗（confrontation）**




在我写这篇日志的时候，时间是 **2025-12-21（美国东岸）** 。

我刚跑完一个新 schema 的写入，并完成了一次冒烟测试。

现在 memory 的结构大致长这样（前面是 legacy，后面是新写入）：
    
    
    {
      "legacy": {
        "notes.session_p00-0f5c6f7a-2b38-4132-b844-900fb9278c7a": {
          "text": "Hello, this is the first OS-level MVP run.",
          "ts": "2025-12-21T22:32:48.552157+00:00",
          "trace_id": "a29e1ac2-8c1d-411c-9d7a-5e76c8646ba8"
        }
      },
      "notes.session_p00-0f5c6f7a-2b38-4132-b844-900fb9278c7a": {
        "text": "Hello, this is the first OS-level MVP run.",
        "ts": "2025-12-21T22:32:48.552157+00:00",
        "trace_id": "a29e1ac2-8c1d-411c-9d7a-5e76c8646ba8"
      },
      "observations.smoke_test": {
        "ts": "2025-12-21T22:53:20.134662Z",
        "note": "smoke test"
      }
    }
    
    

* * *

## 2\. P08 的基础是什么：三个底座，缺一不可

P08 并不是“写个 migration 脚本”这么简单。

它之所以成立，是因为它立在三个基础之上。

* * *

### 2.1 数据本体论：Memory is Ontology

我之前给过一句很硬的原则：

> 凡是可以被事后生成的，都不配成为本体。
> 
> 勉强配得上本体的内容，必须满足：
> 
>  _当时写下、当时不知道结果、当时承担风险。_

这条原则把 memory 从“总结文本 / 知识缓存”，

直接推成了： **系统世界的可审计事实** 。

一旦 memory 成为 ontology，就必须接受一个工程后果：

> Ontology 的结构不能随意变，但世界一定会变，所以必须不断代，而不能断裂。

这就是 **P08 必须存在的哲学理由** 。

* * *

### 2.2 门禁宪法：Policy Gate as Constitutional Enforcement

P07 已经把写入从“可用性工程”升级成了“治理工程”。

P08 进一步明确了一点：

> 门禁不仅筛内容，还筛代际合法性。

换句话说：

  * OS 永远不信任 payload 的“语义”

  * OS 只信任 envelope 的“法律属性”

  * `schema_version` 正是 envelope 的核心法律字段之一




所以在 P08 中，

`schema_version` 的校验 **不是字段校验** ，

而是一次 **宪法执行** 。

* * *

### 2.3 分区与迁移：Active vs Legacy + Migration-Only

P08 最关键的设计其实非常朴素：

  *  **Active** ：当前代增长的世界记忆（未来会被调度器反复调用）

  *  **Legacy** ：旧代历史（只能被回看、审计、迁移参考）

  * 旧代 → 新代的 **唯一合法路径** ：Migration




如果你允许旧代直接写入 active，

那么 `schema_version` 只是注释；

 **只有当旧代被强制进入 legacy，**`schema_version` **才真正成为法律。**

* * *

## 3\. 原理关键点：为什么 Startup Confrontation 必须在 p00

P08 的一个 **设计红线** 是：

> Schema 对抗不能等到第一次写 memory 才发生。

原因很简单，但很致命：

  * 那样历史已经被 implicit 使用

  * legacy 可能已经参与 decision

  * 时间伦理已经被破坏




所以唯一合法的顺序是：
    
    
    系统启动
    → confront history
    → 再允许进入 session
    
    

这也是为什么 **Startup Confrontation 必须显式发生在 p00** 。

p00 是唯一正确的位置。
    
    
    {"ts": 1766109038.557258, "event_type": "memory.version_check", "session_id": "p00-startup", "payload": {"ok": true, "store_version": null, "supported": 0}}
    {"ts": 1766109222.4727821, "event_type": "memory.version_check", "session_id": "p00-startup", "payload": {"ok": true, "store_version": null, "supported": 0}}
    {"ts": 1766109222.473336, "event_type": "memory.legacy_detected", "session_id": "p00-startup", "payload": {"reason": "missing_or_invalid_schema_version", "action": "quarantine_and_refuse_writes"}}
    {"ts": 1766109222.474973, "event_type": "memory.zone_validation", "session_id": null, "payload": {"ok": false, "decision": {"decision": "blocked", "reason": "store quarantined; requires migration", "rule_hits": [{"rule_id": "P08-QUARANTINED", "severity": "hard"}]}}}
    {"ts": 1766110013.8439198, "event_type": "memory.version_check", "session_id": "p00-startup", "payload": {"ok": true, "store_version": null, "supported": 0}}
    {"ts": 1766110013.845823, "event_type": "memory.zone_validation", "session_id": null, "payload": {"ok": false, "decision": {"decision": "blocked", "reason": "UC-04: older schema_version — requires migration", "rule_hits": [{"rule_id": "P08-VALIDATION", "severity": "hard"}]}}}
    {"ts": 1766110145.0845098, "event_type": "memory.version_check", "session_id": "p00-startup", "payload": {"ok": true, "store_version": null, "supported": 0}}
    {"ts": 1766110145.086048, "event_type": "memory.zone_validation", "session_id": null, "payload": {"ok": false, "decision": {"decision": "blocked", "reason": "write must use current schema_version; older versions belong in legacy via migration", "rule_hits": [{"rule_id": "P08-VALIDATION", "severity": "hard"}]}}}
    {"ts": 1766356368.551223, "event_type": "memory.version_check", "session_id": "p00-startup", "payload": {"ok": true, "store_version": null, "supported": 0}}
    {"ts": 1766356368.55217, "event_type": "memory.zone_validation", "session_id": null, "payload": {"ok": true, "zone": "observation", "schema_version": 1}}
    
    

* * *

## 4\. 那条 log 之后发生了什么：我们如何把 P08 跑通

P08 真正跑通的过程，本质只有一件事：

> 把“谁是当前代”钉成单一真源，并让所有写入路径只能服从这个真源。

最终跑通的冒烟输出是这样的：
    
    
    observation write: {'status': 'committed', ...}
    missing schema_version: {'status': 'blocked', 'reason': 'UC-01: missing schema_version'}
    
    

这不是“测试通过”，

而是两条制度被证明已经生效：

  1.  **合法写入必须进入 committed**

  2.  **缺失 schema_version 必须被 UC-01 精确阻断**




完整的 smoke 运行如下：
    
    
    python -m projects.p08_memory_schema_migration_smoke
    
    
    
    
    observation write: { status: committed, decision: allowed, ... }
    missing schema_version: { status: blocked, reason: UC-01 }
    
    

**Smoke test 在这里不是测功能，而是在验证：制度是否真的敢拒绝自己。**

自己写个冒烟测试：
    
    
    {"ts": 1766357080.444414, "event_type": "memory.version_check", "session_id": "smoke-startup", "payload": {"ok": true, "store_version": null, "supported": 0}}
    {"ts": 1766357080.445394, "event_type": "memory.legacy_detected", "session_id": "smoke-startup", "payload": {"reason": "future_schema_version", "action": "quarantine_and_refuse_writes"}}
    {"ts": 1766357080.4456818, "event_type": "memory.zone_validation", "session_id": null, "payload": {"ok": false, "decision": {"decision": "blocked", "reason": "future_schema_version", "rule_hits": [{"rule_id": "P08-QUARANTINED", "severity": "hard"}]}}}
    {"ts": 1766357080.445778, "event_type": "memory.zone_validation", "session_id": null, "payload": {"ok": false, "decision": {"decision": "blocked", "reason": "future_schema_version", "rule_hits": [{"rule_id": "P08-QUARANTINED", "severity": "hard"}]}}}
    {"ts": 1766357600.134471, "event_type": "memory.version_check", "session_id": "smoke-startup", "payload": {"ok": true, "store_version": null, "supported": 0}}
    {"ts": 1766357600.134778, "event_type": "memory.zone_validation", "session_id": null, "payload": {"ok": true, "zone": "observation", "schema_version": 1}}
    {"ts": 1766357600.136105, "event_type": "memory.zone_validation", "session_id": null, "payload": {"ok": false, "decision": {"decision": "blocked", "reason": "UC-01: missing schema_version", "rule_hits": [{"rule_id": "P08-VALIDATION", "severity": "hard"}]}}}
    
    

* * *

## 5\. P08 之后我们还需要做什么

P08 通过冒烟，只意味着：

 **系统第一次具备了长期化的资格** ，而不是结束。

接下来至少还有这些方向（我会在后续 P09/P10 再展开）：

  * 将 P08 的结果冻结为 **CI 宪法回归测试**

  * 统一 schema_version 的 canonical 写入形式

  * 为 migration 本身建立可审计的 ledger

  * 在 P09 把制度执行变成可观测指标

  * 在 P10 把系统彻底进程化




* * *

## 6\. 小结：P08 的意义不是版本，而是“拒绝自己”

P08 最重要的不是 schema_version 这个字段，

而是在那条 log 面前做出的选择：

  * 允许系统为了长期一致性而拒绝写入

  * 把旧代限制在 legacy 与 migration 通道

  * 用 smoke 证明制度真的执行

  * 用 CI 冻结制度语义




这是一种非常稀缺的工程风格：

> 宁可慢、宁可硬、宁可少写，也不混代。

长期系统真正的可靠性。

* * *

AI 开始真正写代码之后，我在推特上认识的一位朋友——名字应该叫 **君子中庸** ——说过一句话，一直留在我心里：

> 文档应该比代码多。

在很长一段时间里，我并不完全认同这句话。

我更熟悉、也更习惯另一套工程文化：

> Talk is cheap. Give me the code.

但现在，我的判断发生了根本性的变化。

我慢慢意识到，在一个 **AI 已经可以随时补全实现细节的时代** ，

代码本身，正在从“稀缺资产”，变成“可再生资源”。

于是我的立场变成了这样：

> I need to talk, but not too much.
> 
>  **I need to write code, but the code itself is not essential.**
> 
>  **What I really need is a lot of documents — because AI can finish the job anytime I want.**

这些文档不是注释，不是 README，也不是“以后再补”的说明。

它们是 **协议、边界、宪法、约束条件、不可妥协的判断** 。

代码可以被 AI 反复生成、重写、迁移；

但 **如果没有这些文档，系统就会在一次又一次“看似合理的重构”中慢慢变形** 。

所以我把 **P08 阶段写下的所有 protocol 都附在后面** 。
    
    
    # Memory Schema v0 — World Memory Responsibility Zones  
    记忆架构 v0 —— 世界记忆责任分区
    
    ## 1. Purpose 目的
    Defines the minimum responsibility structure for long-running world memory. Any memory without a declared zone and schema version is invalid.  
    定义长生命周期世界记忆的最小责任结构。未声明分区和版本的记忆视为无效。
    
    ## 2. Core Principle 核心原则
    - Memory is a time responsibility contract, not just storage.  
    - Each entry must belong to exactly one zone.  
    - Zones cannot be mixed, inferred, or auto-upgraded.  
    记忆是时间责任契约，而非存储；每条记忆必须且只能属于一个分区；分区不可混用、推断或自动升级。
    
    ## 3. Four Memory Zones 四个记忆分区
    
    ### I. World State Memory（世界状态记忆）
    - Definition 定义: States treated as true at a given time. 系统确认的真实世界状态。  
    - Temporal Responsibility 时间责任: Cross-generation required; not modifiable except migration/supersession. 跨代保留；仅迁移/替换可改。  
    - Constraints 约束: Low-frequency, high-confidence; minimal provenance; no speculation. 低频高可信，最小溯源，无推测。  
    - Responsibility 责任: Writing here accepts long-term accountability. 写入即承担长期责任。
    
    ### II. Decision & Action Record（决策与行动记录）
    - Definition 定义: Decisions and resulting actions. 系统决策及执行记录。  
    - Temporal Responsibility 时间责任: Cross-generation required; append-only; not reused for new decisions. 跨代保留、仅追加，不用于新决策。  
    - Constraints 约束: May be wrong but never denied or rewritten. 可错但不可否认或改写。
    
    ### III. Observational / Ephemeral Memory（观察 / 短期记忆）
    - Definition 定义: Observations, hypotheses, intermediate judgments. 观察、假设、中间判断。  
    - Temporal Responsibility 时间责任: Cross-generation optional; modifiable. 跨代可选，可修改。  
    - Constraints 约束: Not treated as fact; cannot auto-promote to World State; may expire/compress. 不作事实，不可自动晋升，可过期/压缩。  
    - Integrity 完整性: Can be forgotten but not pretended nonexistent. 可遗忘但不可假装未曾存在。
    
    ### IV. Legacy / Historical Memory（遗留 / 历史记忆）
    - Definition 定义: Data from older schemas or deprecated semantics. 旧版本或废弃语义下的记忆。  
    - Temporal Responsibility 时间责任: Preserved; read-only; no decision participation. 保留、只读，不参与决策。  
    - Constraints 约束: Access only via explicit migration or historical inspection. 仅迁移或历史审查可用。
    
    ## 4. Zone Integrity Rules 分区完整性规则
    - Every entry must declare its zone. 每条记忆必须声明分区。  
    - Cross-zone promotion is explicit only. 分区间提升必须显式进行。  
    - Schema evolution must not reduce historical responsibility. 架构演进不得降低历史责任。  
    - Legacy memory is preserved by default. 遗留记忆默认保留。
    
    ## 5. Minimal Validity Requirement 最小有效性要求
    Schema v0 is active when:  
    - All entries are zoned. 所有记忆已分区。  
    - Legacy memory is separated. 遗留记忆独立。  
    - World State is treated as high-responsibility data. 世界状态视为高责任数据。  
    - Observations cannot silently become facts. 观察不得悄然变成事实。
    
    
    
    
    # Canonical World Memory Store (v0)  
    # 世界记忆存储规范（v0）
    
    ## 1. Purpose 目的
    - Define the minimal canonical shape of world memory: containers and responsibility boundaries, not content fields.  
    - 界定世界记忆的最小规范形状：关注容器与责任边界，而非具体字段。
    
    ## 2. Mandatory Top-Level Concepts 顶层必备概念
    - Store Version 存储版本：识别存储结构本身的版本。  
    - Current Schema Version 当前架构版本：标识运行时的理解世代。  
    - Memory Zones 记忆分区：四个责任分区的容器。  
    - Legacy Container 遗留容器：显式隔离、只读的历史记忆。  
    - Minimal Provenance Indicator 最低来源标识：可接受的最小溯源等级。
    
    ## 3. Canonical Responsibility Shape (Conceptual) 责任结构（概念）
    - Distinguish World State / Decision / Observation. 区分世界状态/决策/观察。  
    - Distinguish current generation vs legacy generation. 区分当前世代与遗留世代。  
    - Distinguish active memory vs historical memory. 区分活跃记忆与历史记忆。  
    Exact serialization is implementation-defined, but zone boundaries and version visibility are mandatory.  
    具体序列化由实现决定，但分区边界与版本可见性不可缺省。
    
    ## 4. Provenance (Minimal Requirement) 最低溯源要求
    - World State must indicate at least one: user-declared, tool-verified, or human-approved.  
    - 世界状态至少注明：用户声明、工具验证或人工确认之一。  
    - Absence of provenance disqualifies World State writes. 无溯源则不得写入世界状态。
    
    ## 5. Forbidden Practices 禁止事项
    - Mixing zones in the same container. 不得在同一容器混合分区。  
    - Writing to legacy memory. 不得写入遗留记忆。  
    - Omitting `schema_version`. 不得省略 `schema_version`。  
    - Inferring zone from content. 不得根据内容推断分区。  
    - Auto-upgrading old memory without audit. 不得无审计自动升级旧记忆。
    
    ## 6. Canonical Principle 根本原则
    - If memory cannot be migrated, it must at least be preserved.  
    - 若无法迁移，至少应被保留。
    
    
    
    
    # Schema Version — Temporal Generation Contract  
    # 架构版本 —— 跨时代的契约
    
    ## 1. Definition 定义
    - `schema_version` identifies the generation of world understanding under which a memory entry was created.  
    - It is a temporal contract, not just a technical label.  
    `schema_version` 表示记忆条目创建时所属的世界理解“世代”。这是时间上的契约，而不仅是技术标签。
    
    ## 2. Core Commitments 核心承诺
    - Every memory entry must declare `schema_version`.  
    - Writes are allowed only under the current `schema_version`.  
    - The system prefers refusal over temporal inconsistency.  
    每条记忆必须声明 `schema_version`；仅允许在当前版本下写入；系统宁可拒绝也不接受时间上的不一致。
    
    ## 3. Runtime Obligations 运行时义务
    - At startup, the runtime must confront memory versioning before any session.  
    - The system must be able to state:  
      - Which schema version it supports  
      - Which version stored memory belongs to  
      - Whether legacy memory exists  
    - Silent compatibility is forbidden.  
    启动时先处理版本；系统必须声明支持的版本、存储的版本、是否存在遗留记忆；禁止静默兼容。
    
    ## 4. Evolution Rule 演进规则
    - Upgrades may expand understanding and reinterpret future behavior.  
    - They must not deny past understanding.  
    - A system may grow wiser, but must never pretend it was always so.  
    升级可以拓展理解、影响未来行为，但不得否认历史理解。系统可以变得更聪明，但不能假装一直如此。
    
    
    
    
    # Memory Schema Migration (p08) — Plan & Checklist  
    # 记忆架构迁移（p08）—— 计划与检查清单
    
    ## Purpose 目的
    - Migrate world memory to newer schema versions without losing responsibility guarantees.  
    - 在迁移到新版架构时，保持责任约束与可审计性。
    
    ## Scope 范围
    - Applies to `runtime_data/memory_store.json` and zoned memory containers.  
    - 适用于 `runtime_data/memory_store.json` 及分区记忆。
    
    ## Principles 原则
    - Audit-first: every migration step is logged. 审计优先，迁移步骤必须记录。  
    - No silent upgrades: version changes are explicit. 禁止静默升级，版本变更需显式执行。  
    - Preserve legacy: on failure, keep legacy data read-only. 失败时保留只读遗留数据。
    
    ## Migration Steps 迁移步骤
    1. Inventory: detect current `schema_version` and legacy zones.  
       清点：检测当前 `schema_version` 与遗留分区。  
    2. Plan: map source zones/keys to target schema fields.  
       规划：映射源分区/键到目标架构字段。  
    3. Execute: transform with checksums and backups.  
       执行：携带校验和与备份进行转换。  
    4. Validate: verify zone separation, provenance, and version tags.  
       验证：确认分区隔离、溯源与版本标记。  
    5. Commit: write new store; retain legacy snapshot for audit.  
       提交：写入新存储，并保留遗留快照以供审计。
    
    ## Validation Checklist 验证清单
    - `schema_version` updated and declared. `schema_version` 已更新并声明。  
    - Zones intact: World / Decision / Observation / Legacy separated. 分区完好：世界/决策/观察/遗留清晰分隔。  
    - Provenance preserved or upgraded; none lost. 溯源保留或升级，无丢失。  
    - Events emitted for proposal / check / commit (P07 path). 已记录事件：提案/检查/提交（P07 流程）。  
    - Legacy snapshot stored read-only. 遗留快照已只读存档。
    
    
