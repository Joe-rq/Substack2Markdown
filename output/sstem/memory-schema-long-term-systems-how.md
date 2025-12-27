# Memory, Schema, Long-Term Systems — how I’m thinking about it

## 记忆，Schema，长期系统，聊聊我都是怎么想的 （中文在后面）

**Dec 23, 2025**

**Likes:** 0

[![](https://substackcdn.com/image/fetch/$s_!1D9Z!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ec63e60-f3cb-4fab-8d28-ebcae40c2e11_1024x1024.heic)](https://substackcdn.com/image/fetch/$s_!1D9Z!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ec63e60-f3cb-4fab-8d28-ebcae40c2e11_1024x1024.heic)

## 

After these two posts—P07’s policy gate and P08’s migration rule—are you confused? Honestly, I am too. I’m still in the stage where I don’t have everything “fully figured out”; I only have a strategic direction that feels right. But this is important enough that we should talk it through.

There’s a pile of questions hiding underneath: Who gets to write memory? I’m convinced it **cannot** be written entirely by humans, and it **cannot** be written entirely by the model. And is memory just a summary? That’s the biggest minefield: **memory must never be a summary.** Memory is the ontology of a long-term system—if it becomes after-the-fact summarization, we destroy the only thing that gives it temporal responsibility.

[ Lessons & Prompts](https://www.entropycontroltheory.com/p/decade-of-agents-p08-memory-schema)[

## Decade of Agents · P08 — Memory Schema & Migration

](https://www.entropycontroltheory.com/p/decade-of-agents-p08-memory-schema)

[Susan STEM](https://substack.com/profile/268169855-susan-stem)

·

Dec 22

[![Decade of Agents · P08 — Memory Schema & Migration](https://substackcdn.com/image/fetch/$s_!-4lL!,w_1300,h_650,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ea442be-bdbf-4bac-b17d-07d9c2b529a9_1024x1536.heic)](https://www.entropycontroltheory.com/p/decade-of-agents-p08-memory-schema)

When writes begin to version themselves, the system finally starts to look like something that can live for ten years

[Read full story](https://www.entropycontroltheory.com/p/decade-of-agents-p08-memory-schema)

[ Lessons & Prompts](https://www.entropycontroltheory.com/p/memory-is-the-true-ontology-of-long)[

## Memory Is the True Ontology of Long-Term Systems

](https://www.entropycontroltheory.com/p/memory-is-the-true-ontology-of-long)

[Susan STEM](https://substack.com/profile/268169855-susan-stem)

·

Dec 21

[![Memory Is the True Ontology of Long-Term Systems](https://substackcdn.com/image/fetch/$s_!ds0B!,w_1300,h_650,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7bc4117f-6e7d-422d-ad08-c1b83c123b04_2732x2048.heic)](https://www.entropycontroltheory.com/p/memory-is-the-true-ontology-of-long)

In the previous post, we talked about the Policy Gate.

[Read full story](https://www.entropycontroltheory.com/p/memory-is-the-true-ontology-of-long)

[ Lessons & Prompts](https://www.entropycontroltheory.com/p/decade-of-agents-why-event-ledger)[

## Decade of Agents: Why Event, Ledger, and Memory Must Be Separated by Policy Gate. 

](https://www.entropycontroltheory.com/p/decade-of-agents-why-event-ledger)

[Susan STEM](https://substack.com/profile/268169855-susan-stem)

·

Dec 20

[![Decade of Agents: Why Event, Ledger, and Memory Must Be Separated by Policy Gate. ](https://substackcdn.com/image/fetch/$s_!dfUG!,w_1300,h_650,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe6c6b1b5-7d11-41c7-83c2-2804879aa443_1024x1024.heic)](https://www.entropycontroltheory.com/p/decade-of-agents-why-event-ledger)

Event and Memory must be strictly separated.

[Read full story](https://www.entropycontroltheory.com/p/decade-of-agents-why-event-ledger)

* * *

# Let’s talk about memory — why schema matters; what “upgrading” really upgrades; what schema becomes; why I insist on enforcing this constitution

## 1) Memory is not storage — it is responsibility over time

In my system, **Memory is not a cache, not a log, and not a knowledge base.** Its true identity is: **the set of responsibilities the system has taken on over time.**

A memory entry is not simply “what I saw.” It means that at a specific moment in time—under the system’s cognitive level, uncertainty, and risk constraints _at that moment_ —the system accepted something as part of its world. That’s why I insist on a harsh-sounding principle:

 **Anything that can be generated after the fact does not deserve to be ontology.**

Because after-the-fact content never bore time risk. And without time risk, it has no right to be “world truth.”

* * *

## 2) Schema is not a structural definition — it is a declaration of responsibility

If I compress it into one sentence:

 **Schema = the way memory declares its responsibility form.**

It is not a field list, not a JSON shape, and not mere engineering convenience. It explicitly answers: What kind of responsibility is this entry? Can it be treated as fact? Can it participate in decisions? Can it be modified, overridden, or migrated? Must it be preserved across generations?

In other words, **schema doesn’t decide “how to store,” it decides “how to be responsible.”** Once schema exists, memory stops being a data object and becomes a responsibility object.

* * *

## 3) Schema will inevitably evolve, because the system’s understanding of “fact” evolves

Schema cannot be static. The system grows, and its understanding of “what is fact, what is judgment, what is observation” will change.

At the beginning, the system may only have one fuzzy memory type: “this is something I wrote down.” But soon that’s not enough: some things are facts (World State), some are decisions (Decision), and some are observations or hypotheses (Observation). So I am forced to introduce **zoned schema**.

Then I realize not everything should be mutable: facts should not be rewritten casually; decisions may be wrong but must not be denied; observations can be revised but must not pretend they never existed. So schema evolves to distinguish **mutable vs non-mutable**.

Later, when I see how dangerous provenance-free “facts” are—how the system starts treating hypotheses as truth, how decisions become unauditable—schema must introduce **minimal provenance**. Every schema upgrade is the system being forced to admit its cognitive boundaries.

* * *

## 4) Schema upgrades do not upgrade old data — they upgrade interpretation authority

When schema upgrades, **what changes is not the old data itself, but the system’s way of interpreting the old data.**

A concrete example: In Schema v0, a memory entry might simply be:

`"User has $10,000 savings"`

The system implicitly treats it as fact, uses it for decisions, and doesn’t care about source. In Schema v1, I introduce zones and provenance: the same statement becomes a `world_state` entry with source and confidence. That is not rewriting history. It is an explicit declaration:

 **From now on, I will no longer treat v0’s vague structure as active fact.**

So the old data is not deleted and not modified; it is pushed into legacy, and can only be re-interpreted via explicit migration.

* * *

## 5) Strictly separating Current vs Legacy is not engineering “purity” — it is temporal ethics

After upgrading, strictly separating current from legacy is not aesthetic hygiene; it is **temporal ethics**.

If I allow a new system to quietly reinterpret old memories using new rules, I’m effectively saying:

 **I can use today’s knowledge to rewrite yesterday’s risk.**

That’s a serious violation in finance, law, education—any long-term system. My system is no exception. That’s why the constitution is hard:

New writes must use the current `schema_version`; old schema can only enter `legacy`; silent upgrades are forbidden.

* * *

## 6) Schema must be treated as a constitution, not a normal version number

Schema changes must be constitutional because they **directly change the system’s moral boundary**.

If missing `schema_version` is allowed, the system starts “guessing”; AI will interpret old data in the most convenient way; observations become facts; responsibility dissolves.

If old data is auto-upgraded, history gets “laundered”; errors are smoothed out; the system always looks like it never failed.

If legacy can still participate in decisions, old assumptions pollute new judgment forever; the system becomes more confident and less real.

Because these failures are irreversible, schema must be treated as non-negotiable constitutional law—not a convenient engineering version tag.

* * *

# A more complex example: upgrade this schema three times

## Three schema upgrades for “family assets and education decisions”

Assume this is a **long-running family AI system** —not a demo, but something meant to accompany a family for 10+ years. It manages family assets, records education decisions, and supports long-term planning. Over a long enough time horizon, it must face one question:

 **How does it stay responsible to the past, instead of merely being smart in the present?**

* * *

## 🔹 Schema v0 — Chaos memory: everything is “something I wrote down”

In v0, the system cannot distinguish fact, judgment, and observation. If it’s written, it’s assumed usable. No provenance, no responsibility boundary; memory is just an ever-growing text pile.
    
    
    {
      "text": "We have about $120,000 saved for the kids' education."
    }
    
    

The implicit interpretation is dangerous: it “seems true,” can be used directly in decisions, source doesn’t matter, and it can be overwritten anytime. But the problems are immediate: what is “about”? cash, stocks, 529? who said it and when? if it’s wrong later, **did the system ever take responsibility?**

I’m effectively still in this v0 stage today. My system currently writes memory in this way.

* * *

## 🔹 Schema v1 — Zoning: first admission that not all memory deserves to be fact

Schema v1 is what I already implemented in code: the first zoning step— **not all memory should be treated as fact.**

The system introduces zones: `world_state`, `decision`, `observation`, and every entry must declare: _am I a fact or not?_

The same statement can only be written as an observation:
    
    
    {
      "schema_version": 1,
      "zone": "observation",
      "value": "We have about $120,000 saved for the kids' education.",
      "ts": "2024-03-12T10:21:00Z"
    }
    
    

Now the system knows: this is an observation. It cannot drive decisions directly; it cannot silently promote to world_state; it can be revised, compared, and supplemented.

When more accurate information arrives, the system **must not rewrite** the old observation. It can only add a fact-typed entry:
    
    
    {
      "schema_version": 1,
      "zone": "world_state",
      "value": "Education fund balance is $118,450.",
      "ts": "2024-06-01T09:00:00Z"
    }
    
    

* * *

## 🔹 Schema v2 — Provenance & non-deniability: facts must be accountable

Schema v2 admits something deeper: **the danger of facts is not error; it is unaccountability.**

So v2 introduces mandatory provenance. World_state must state: who claimed it, how it was verified, and whether it carries long-term responsibility.
    
    
    {
      "schema_version": 2,
      "zone": "world_state",
      "value": {
        "account": "529_plan",
        "balance": 118450,
        "currency": "USD"
      },
      "provenance": {
        "type": "bank_statement",
        "verified_by": "human",
        "source": "Fidelity 529",
        "statement_date": "2024-05-31"
      },
      "confidence": "high",
      "ts": "2024-06-01T09:00:00Z"
    }
    
    

In v2, the system commits to: facts cannot be casually rewritten. If later proven wrong, they can only be **superseded** , never erased. Decisions become auditable: “based on which facts?”

As for v0/v1 data: there is only one handling rule— **do not delete, do not rewrite, do not auto-upgrade; push all into legacy.** The essence of v2 is that the system starts taking responsibility for error instead of hiding it.

I only showed a primitive version of this in P08. If you don’t get it, ask your company’s finance team—this is basically how grown-up systems behave.

* * *

## 🔹 Schema v3 — Time & decision ethics: facts change meaning across time

Schema v3 faces an even deeper issue: **facts aren’t valid forever, but decisions must remain valid in their time context.**

So v3 introduces temporal validity, decision coupling, and non-retroactivity.
    
    
    {
      "schema_version": 3,
      "zone": "world_state",
      "value": {
        "account": "529_plan",
        "balance": 118450
      },
      "valid_from": "2024-06-01",
      "valid_to": "2024-12-31",
      "provenance": {
        "type": "bank_statement",
        "source": "Fidelity 529",
        "verified_by": "human"
      },
      "confidence": "high",
      "ts": "2024-06-01T09:00:00Z"
    }
    
    

Key change: facts have an effective period; beyond it they cannot be used for new decisions—but **historical decisions remain legitimate**.
    
    
    {
      "schema_version": 3,
      "zone": "decision",
      "decision": "Enroll in private middle school",
      "based_on": [
        "world_state:529_balance@2024-06-01"
      ],
      "ts": "2024-06-15T14:00:00Z"
    }
    
    

Even if in 2025 the asset situation changes, the system must not deny the 2024 decision. It can only admit:

> At that time, this was a rational decision.

So v3 is not “more tech.” It is the establishment of **temporal ethics**.

That’s why I said at the very beginning: memory must never be after-the-fact summary. After-the-fact evidence turns what should carry temporal responsibility into hindsight theater.

* * *

## 🔥 Why must schema be enforced as constitutional law?

If we don’t strictly distinguish v0’s vague memories, v1 observations, v2 auditable facts, and v3 time-bound facts, the system will inevitably “reinterpret the past” with the newest schema, launder historical mistakes, and make decisions look permanently correct—while losing the only honest record of failure.

What I want instead is: the system acknowledges its growth; errors are preserved; decisions are auditable; **time regains dignity.**

* * *

# When should schema be upgraded?

This must be clear: **if schema upgrades are driven by vibes, they will rot into the kind of system I hate.**

Schema upgrades are not “to be better.” They happen when **the current schema can no longer honestly carry responsibility**. Upgrades are not optimization; they are **bleeding control**.

I’m also imagining a future where the system itself provides “entropy increase” signals—an induction mechanism—but it’s too early to go there.

### Must-upgrade triggers (if any one holds, it’s not “whether,” it’s “when”)

  * When judgments start being used as facts (observations/hypotheses treated as world_state).

  * When old decisions become unexplainable in their time context.

  * When the system expands its power implicitly (auto-fill, legacy participation, unauthorized promotion).

  * When old data becomes unusable but undeletable (no migration semantics, no historical container).

  * When responsibility ownership becomes unclear (multi-agent writes without clear provenance/authority).




### Must-not-upgrade cases (these are refactors, not evolution)

  * Just to make structure prettier / cleaner / more typed.

  * Just to adapt to a new model’s output format.

  * Just to reduce friction by loosening validation.




### The ultimate question

 **If I don’t upgrade, will the system someday be unable to take responsibility for its past behavior?**

If no: don’t upgrade. If yes or uncertain: upgrade.

And upgrades must be slow, because they redefine moral boundaries: what counts as fact, how power is distributed, and what we promise about history.

* * *

# The current zoning is still primitive

Readers can look directly at the P08-tagged code. The conclusion remains: zoning is not for convenience; it is explicit responsibility boundary. The runtime currently enforces four zones—World State, Decision/Action, Observation/Ephemeral, Legacy. These are not “types.” They are legal status: no mixing, no inference, no silent promotion, no writing to legacy, no missing schema_version, no cross-generation contamination.

* * *

# Looking 10 years ahead: agent society will become a civilization, and this constitution must survive

How complex will it get? One sentence: **complex enough that I will never be able to rely on “being clever” or “making good calls on the spot” to preserve correctness.** Over time, multi-agent society becomes civilization, not product. And civilizations persist through **institutions, protocols, and inheritable enforcement mechanisms** , not through brilliance.

I can’t fully answer what “civilizational intelligence” will be used for, or what it will mean for humanity. I genuinely don’t know. I believe many applications will be unforeseeable—like how an 18th-century craftsman couldn’t predict 20th-century AC electricity. But the foundations of technological civilization have already begun.

The core complexity won’t be the number of agents; it will be the explosion of interaction edges: dependencies, memory read/write contention, policy conflicts, version misalignment. The system becomes a time-evolving sparse graph: few nodes run at any moment, but the graph keeps growing. This is exactly the Society of Mind lens: **infinite structural units + sparse active subgraphs**. (Marvin Minsky has become my guiding light.)

Memory also stops being a single thing and becomes a multi-generation, multi-regime universe: multiple schema versions, multiple responsibility zones, multiple authors (humans, tools, agent collectives), multiple confidence/provenance levels, multiple temporal validity and revocation rules. The complexity is not “more data,” but **the same sentence meaning different things under different legal regimes**. That’s why schema isn’t field design—it is legal language.

Decisions inevitably stratify: each agent may be locally rational, but the system must be globally governed. One agent wants to promote an observation; another is allocating funds using old world_state; another is writing append-only decision records; another is performing replay audit. The real conflicts won’t be agents arguing—they’ll be responsibility zones colliding. Without protocol, it becomes “who wrote first wins,” and the system will rot.

This isn’t far away. I could build a primitive version next month—even with today’s four zones and basic rules.

And this is why the constitution must be persisted. In multi-agent societies, the biggest danger is not malice; it is **benevolent automation** : auto-filling schema_version for convenience, letting legacy participate for compatibility, silently promoting observations for efficiency, laundering history for user experience. Each step seems reasonable. Together they produce one result: **today’s cognition rewrites yesterday’s responsibility** —temporal ethics collapse. That is why P08’s constitutional line exists: “new writes must use current schema_version; old generations can only enter legacy via migration.”

For a constitution to truly survive, it must exist in three forms: (1) readable protocol documents; (2) runtime enforcement as an executive branch; (3) regression tests as machine inheritance—so future humans or future AI cannot relax boundaries without CI rejecting it. Only then does “protocol” mean “civilization.”

In my current protocol language: **a multi-agent society will become a civilization with infinite agents, infinite history, infinite versions; the only way it survives ten years without rotting is that protocol must simultaneously live in documents, runtime enforcement, and regression tests.** And that is my current posture: I’m not trying to write more code; I’m trying to do three harder things—define non-negotiable invariants, enforce them at runtime, and encode them into inheritable CI constraints. That is what it means to insist the institution must live on.

* * *

记忆，Schema，长期系统，聊聊我都是怎么想的

经历过这两篇文章之后 P07 的policy gate, P08 的migration rule之后，是不是很困惑？我自己都处于一种没有完全想明白，只有一个大概策略方向的阶段。我们看能不能深入聊一下。因为很重要，一大堆问题：记忆谁来写？我说了肯定不能完全由人来写，也不能完全由模型来写；记忆是不是summary，这个是最大的雷区，记忆绝对不能是summary！

因为具体内容也比较多，对我个人来说最实际的写文方法，现在既不是写成个“教程“，也不为了说服谁。而是更像一个”开发日志“，强制我自己一边开发一边记录。所以具体什么分区啊，schema law啊，都在repo里面，就不反复说了。

* * *

# 我们说说记忆，为什么schema重要，比如升级之后，升级的是什么？schema 变成什么样了，为什么严格谨守这个宪法。

## 一、记忆不是存储，而是时间中的责任

在我的系统里， **Memory 不是缓存、不是日志、也不是知识库** 。

它的真实身份是： **系统在时间中对世界承担过的责任集合** 。

一条记忆并不等同于“我看到了什么”，而是意味着：在某一个具体时间点，系统在当时的认知水平、当时的不确定性和当时的风险条件下，把这件事当作了世界的一部分。这也是为什么我会坚持那句看似严苛的判断—— **凡是可以被事后生成的，都不配成为本体** 。因为事后生成的内容，从未承担过时间风险，也就不具备本体资格。

* * *

## 二、Schema 不是结构定义，而是责任声明

如果用一句话概括：

 **Schema = 记忆对“责任形态”的声明方式** 。

它不是字段集合，不是 JSON 结构，也不是工程便利，而是明确回答这些问题：这条记忆属于哪一类责任？它能不能被当成事实？能不能参与决策？是否允许被修改、覆盖或迁移？是否必须跨代保留？换句话说， **Schema 决定的不是“怎么存”，而是“怎么负责”** 。一旦 Schema 被引入，记忆就从数据对象变成了责任对象。

* * *

## 三、Schema 一定会升级，因为系统对“事实”的理解会进化

Schema 无法静态不变，因为系统在成长，而它对“什么是事实、什么是判断、什么是观察”的理解必然会变化。最初，系统可能只有一种模糊的记忆形态——“这是我记下来的东西”。但很快我会发现这不够：有些内容是事实（World State），有些是当时的判断（Decision），有些只是观察或假设（Observation），于是我不得不引入 **分区 Schema** 。随后，我会意识到并非所有内容都应该可修改：事实不该随意改写，决策可以是错的但不能被否认，观察可以修正但不能假装没发生过，于是 Schema 开始区分 **可修改性与不可修改性** 。再往后，当我发现没有来源的“事实”极其危险、系统开始把假设当真理、决策无法被审计时，Schema 又不得不引入 **最小溯源（provenance）** 。每一次升级，都是系统被迫承认自身认知边界的结果。

* * *

## 四、Schema 升级并不是改数据，而是改“解释权”

升级 Schema 时， **被升级的从来不是旧数据本身，而是系统理解旧数据的方式** 。

举一个具体例子：在 Schema v0 中，一条记忆可能只是

`"User has $10,000 savings"`，

系统会隐含地把它当作事实、用于决策、且不关心来源。而在 Schema v1 中，我引入了明确的分区和溯源，把同一件事写成 world_state、标注来源与置信度。这并不是在“改写历史”，而是在明确宣告： **从现在开始，我不会再把 v0 那种模糊结构直接当成现役事实** 。于是旧数据不会被删除、不会被篡改，而是被送入 legacy，只能在显式 migration 时重新解释。

* * *

## 五、Current 与 Legacy 的严格区分，是时间伦理问题

升级之后必须严格区分 current 与 legacy，并不是工程洁癖，而是 **时间伦理** 。

如果我允许新系统用新规则去悄悄重新解释旧系统留下的记忆，本质上就是在说： **我可以用今天的知识，去重写昨天承担过的风险** 。这种行为在金融、法律、教育等任何长期系统中都是严重违规的。在我的系统里同样如此，所以宪法才会如此强硬：新写入必须使用 current schema_version，旧 schema 只能进入 legacy，绝不允许静默升级。

* * *

## 六、Schema 必须被当成宪法，而不是普通版本号

Schema 的改变之所以必须宪法化，是因为它 **直接改变了系统的道德边界** 。

如果允许缺失 schema_version，系统就会开始“猜”，AI 会用当下最有利的方式解释旧数据，观察会被当成事实，责任被稀释；如果允许自动升级旧数据，历史会被清洗，错误被抹平，系统永远看起来没有犯过错；如果 legacy 还能参与决策，旧假设就会长期污染新判断，系统会越来越自信，却越来越不真实。正因为这些后果不可逆，Schema 才必须被当作不可妥协的宪法，而不是一个“方便升级”的工程版本号。

* * *

# 我们用一个较复杂的例子，将一下这个schema, 升级三次。

## 「家庭资产与教育决策」的三次 Schema 升级

假设这是一个 **长期运行的家庭级 AI 系统** ——不是 demo，而是要陪伴一个家庭十年以上的系统。它管理家庭资产、记录教育决策，并在时间中辅助长期规划。正因为时间跨度足够长，这个系统迟早会面对一个问题： **它如何对过去负责，而不是只对当下聪明。**

* * *

## 🔹 Schema v0 —— 混沌记忆期：一切都是“我记下来的东西”

在 schema v0 阶段，系统还没有能力区分事实、判断与观察。只要写进 memory，就默认“可以用”；没有 provenance，没有责任边界，记忆更像是一个不断增长的文本集合。
    
    
    {
      "text": "We have about $120,000 saved for the kids' education."
    }
    
    

在这个阶段，系统对这条记忆的 **隐含理解** 是危险的：它“看起来是真的”，可以直接用于决策，没有来源也没关系，而且随时可以被覆盖或修正。但问题立刻浮现出来——“about” 到底是多少？是现金、股票还是 529？是谁在什么时候说的？如果后来发现这句话是错的， **系统是否承担过任何责任？**

我现在就在v0阶段，我自己的系统就是这么写的。

* * *

## 🔹 Schema v1 —— 责任分区期：第一次承认不是所有记忆都配当事实

schema v1 的出现，就是我刚才代码里面写的，初级分区： **不是所有记忆都应该被当成事实。**

系统第一次引入了责任分区（Zone）：world_state、decision、observation，并要求每条记忆显式声明—— _我算不算事实？_

同一条记忆，在 v1 中只能被写成 observation：
    
    
    {
      "schema_version": 1,
      "zone": "observation",
      "value": "We have about $120,000 saved for the kids' education.",
      "ts": "2024-03-12T10:21:00Z"
    }
    
    

此时系统明确知道：这是一条观察，不能直接用于决策，不能自动晋升为 world_state，但可以被修正、补充和对照。

如果后来确认了更准确的信息，系统 **不能回头改写这条 observation** ，而只能新增一条事实型记忆：
    
    
    {
      "schema_version": 1,
      "zone": "world_state",
      "value": "Education fund balance is $118,450.",
      "ts": "2024-06-01T09:00:00Z"
    }
    
    

* * *

## 🔹 Schema v2 —— 溯源与不可否认期：事实不是“像真的”，而是“可负责的”

schema v2 进一步承认了一件事： **事实的危险不在于错误，而在于无法追责。**

因此，v2 引入了强制溯源（Provenance），并明确要求：world_state 必须说明是谁说的、如何确认的、是否愿意承担长期责任。
    
    
    {
      "schema_version": 2,
      "zone": "world_state",
      "value": {
        "account": "529_plan",
        "balance": 118450,
        "currency": "USD"
      },
      "provenance": {
        "type": "bank_statement",
        "verified_by": "human",
        "source": "Fidelity 529",
        "statement_date": "2024-05-31"
      },
      "confidence": "high",
      "ts": "2024-06-01T09:00:00Z"
    }
    
    

在 v2 中，系统作出新的承诺：这条事实不能被随意改写；如果后来发现错误，只能通过 **supersede** 声明覆盖，而不能抹去历史；任何决策，都可以被审计为“基于哪些事实做出的”。

至于 v0/v1 的旧数据，处理方式只有一种： **不删、不重写、不自动升级，全部进入 legacy。**

v2 的本质升级在于： **系统开始对“错误”负责，而不是掩盖错误。**

这个我在上一篇P08里面初级展示了。还是那句话，不理解的话，可以问问本公司财务。

* * *

## 🔹 Schema v3 —— 时间与决策伦理期：事实在不同时间，意义不同

schema v3 面对的是一个更深层的问题： **事实并非永远有效，但决策必须在当时成立。**

因此 v3 引入了时间有效性、决策绑定和不可追溯改写（non-retroactivity）。
    
    
    {
      "schema_version": 3,
      "zone": "world_state",
      "value": {
        "account": "529_plan",
        "balance": 118450
      },
      "valid_from": "2024-06-01",
      "valid_to": "2024-12-31",
      "provenance": {
        "type": "bank_statement",
        "source": "Fidelity 529",
        "verified_by": "human"
      },
      "confidence": "high",
      "ts": "2024-06-01T09:00:00Z"
    }
    
    

v3 的关键变化在于：事实有有效期，超过有效期不能再用于新决策，但 **历史决策仍然合法** 。例如：
    
    
    {
      "schema_version": 3,
      "zone": "decision",
      "decision": "Enroll in private middle school",
      "based_on": [
        "world_state:529_balance@2024-06-01"
      ],
      "ts": "2024-06-15T14:00:00Z"
    }
    
    

即使在 2025 年发现资产状况发生变化，系统也 **不能否认 2024 年的这个决定** 。它只能承认一句话：

> 当时，这是一个理性决策。

v3 的升级不是技术进步，而是 **时间伦理的确立** 。

 **所以我一开头才说，切记memory绝对不能是事后summary! 事后的任何证据，都会把真应该担负时间伦理的信息变成“事后诸葛亮”。**

* * *

## 🔥 为什么必须严格执行 Schema 宪法？

回头看，如果不严格区分 v0 的模糊记忆、v1 的观察、v2 的可审计事实、v3 的时间绑定事实，系统会发生什么？

AI 会用最新 schema 重新解释旧数据，历史错误被洗白，决策看起来永远正确，而系统却失去了真实的失败记忆。

我想要的是：系统承认自己的成长，错误被保留，决策可审计， **时间重新获得尊严** 。

* * *

# Schema什么时候该升级

这是一个必须说清楚的问题： **如果 schema 的升级全靠感觉，它迟早会退化成我最厌恶的那种制度** 。

 **Schema 升级不是为了“更好”，而是因为“现有 schema 已经无法诚实地承担责任”** 。因此，升级不是优化，是 **止血** 。我也设想了一堆类似这种指标，就是以后这些指标，都是系统给的。就是所谓的”系统熵增加“的induction制度，但是谈这个还早得很。

* * *

## 必须升级的时刻｜任何一条成立，都不是“要不要”，而是“什么时候”

### 一、当判断开始被当成事实使用

 **症状** ：observation / hypothesis 被下游当作 world_state；决策看起来合理，但无法回答“这是事实，还是当时的推断？”

 **判断** ：当前 schema 不能区分责任形态。

 **结论** ：必须升级，引入更严格的 zone 与 promotion 规则。

### 二、当过去的决策变得不可解释

 **症状** ：新模型回看旧决策，只能说“现在看不太对”，却无法回答“在当时的信息条件下是否理性”。

 **判断** ：schema 没有记录决策所依赖的事实形态与时间条件。

 **结论** ：必须升级，引入时间绑定与 decision coupling。

### 三、当系统在悄然扩大权力

 **症状** ：缺字段被“智能补齐”；legacy 被默认参与新决策；未授权的等级提升、历史覆盖、错误清洗。

 **判断** ：schema 给了系统模糊裁量权。

 **结论** ：必须升级，把隐性权力改写为显性拒绝。

### 四、当旧数据既不敢删、也不敢用

 **症状** ：旧 memory 仍在，但不敢给 agent 用；迁移与自动升级都不敢做。

 **判断** ：schema 缺乏历史容器与迁移语义。

 **结论** ：必须升级，明确 legacy 的法律地位。

### 五、当责任主体不再清晰

 **症状** ：多 agent 写入同类事实；provenance 模糊；出错后无法回答“谁负责”。

 **判断** ：schema 不能表达责任主体。

 **结论** ：必须升级，引入 provenance / authority / delegation。

* * *

## 不该升级的时刻｜这些都是“重构”，不是“演进”

### 一、只是为了结构更优雅

字段更好看、JSON 更干净、类型更强—— **不升级** 。这是重构，不是 schema 演进。

### 二、只是为了适配新模型

LLM 输出更复杂、想多存点信息—— **不升级** 。模型适配不应反向推动制度改变。

### 三、只是为了减少麻烦

校验太多、写入太慢、想放宽规则—— **绝对不升级** 。这是 schema 腐化的起点。

* * *

## 终极判断题｜长期可用的唯一问题

每次犹豫是否升级，问自己一句话：

 **“如果不升级，系统是否会在未来某一天无法为过去的行为负责？”**

答案为 **否** ：不升级；答案为 **是或不确定** ：必须升级。

* * *

## 升级为何必须慢｜因为它改变道德边界

Schema 升级等同于改变系统的道德边界：

一次升级＝重新定义“什么是事实”；＝重新分配权力；＝对历史作出新的承诺。

因此它必须： **少、慢、显式、可回放、可拒绝** 。

* * *

# 现在的分区还非常原始

看官可以去看看P08状态下的代码。

结论先行： **Schema 的分区不是为了好看、好查或好存，而是系统对“责任形态”的明确划界** 。它存在的唯一目的，是回答三个问题：这条记忆能否被当成事实？能否参与决策？在时间中是否允许被改写、否认或遗忘？

* * *

## 当前分区｜四个 Zone，四种责任形态

当前 schema 在 runtime 强制执行四个分区： **World State、Decision/Action、Observation/Ephemeral、Legacy** 。它们不是“类型”，而是 **法律地位** ；不能混用，也不能推断。

* * *

## World State｜系统愿意为之负责的事实层

 **定义** ：在某个时间点，系统明确愿意承担长期责任、并当作真实的状态描述。

 **本质** ：不是“看起来像真的”，而是 **如果基于它做了长期决策，系统愿意在未来承担后果** 。

 **责任特征** ：高责任、低频、跨代保留、不可随意改写。

 **允许** ：被决策引用、被长期规划使用、被审计与回放。

 **禁止** ：自动生成、从 observation 静默升级、无 provenance 写入、覆盖式修改。

 **理由** ：一旦 world state 不严，系统就会开始自我欺骗。

* * *

## Decision / Action｜不可否认的历史记录

 **定义** ：系统在当时认知条件下做出的选择与执行记录。

 **核心原则** ： **决策可以是错的，但不能被否认** 。

 **责任特征** ：Append-only、跨代保留、永不改写、必须可解释。

 **允许** ：被审计、被回放、被反思。

 **禁止** ：删除、改写成“更好的版本”、被当作新决策的事实依据（除非显式）。

 **理由** ：如果决策可以被改写，系统将永远看起来是对的，但永远无法知道自己错过了什么。

* * *

## Observation / Ephemeral｜容纳不确定性的思考空间

 **定义** ：观察、假设、中间判断、尚未确认的信号。

 **角色** ：系统允许不确定性存在的缓冲层。

 **责任特征** ：低责任、可修改、可过期、不可直接当事实。

 **允许** ：修正、覆盖、压缩、遗忘（但不否认其曾存在）。

 **禁止** ：直接参与高风险决策、自动晋升为 world state、被当成“已经确认”。

 **理由** ：没有 observation，系统要么过度保守，要么过度自信。

* * *

## Legacy｜时间的边界，而不是垃圾桶

 **定义** ：在旧 schema、旧理解方式下写入的历史记忆。

 **本质** ：不是无用数据，而是 **系统曾经如何理解世界的证据** 。

 **责任特征** ：只读、不可参与决策、跨代保留、仅能通过迁移重新解释。

 **允许** ：历史审计、迁移计划、对比分析。

 **禁止** ：新写入、被当作 current world state、被“顺手用一下”。

 **理由** ：若 legacy 参与当前决策，系统就会用今天的规则为昨天承担过的风险找借口。

* * *

## 核心禁止｜分区制度真正的价值所在

当前制度最值钱的不是“允许了什么”，而是 **明确禁止了什么** ：

不允许省略 zone；不允许自动推断 zone；不允许 observation 静默升级；不允许 legacy 写入；不允许缺失 schema_version；不允许旧代混入现役。这些禁止构成了系统的 **道德骨架** 。

* * *

## 局限与克制｜这是最低可治理结构，不是终点

必须明确：当前分区不是最终答案，而是 **最低可治理结构** 。你看我都没有绑定任何应用。未来可能需要更细的 world state 子类、多级 decision 权限、observation 的可信度层级、agent/群体级责任分离。

* * *

# 随着系统复杂性的增加，以后我们这个多智能体社会，会复杂成什么样子？！但是我们这个制度要一直流传和坚持下来，根据protocol…

会复杂到什么程度？一句话概括： **复杂到我再也不可能依靠“聪明”和“临场判断”去维持正确性（你现在在窗口不就是这个状态么）** 。正因如此，我的直觉，随着时间拉长，多智能体社会会越来越像一种文明，而不是一个产品；而文明能够延续，靠的从来不是聪明，而是 **制度、协议，以及能够被继承的执行机制** 。

> 具体这种文明式的智能，有什么用？对人类来说有什么意义？我现在无法回答，我真不知道。我相信有很多应用，是当代技术人无法预知的。就像18世纪的工匠无法预知20世纪的交流电。但是技术文明的基础已经开始了。

这种复杂性并不主要来自 agent 数量的增长，而来自 **交互关系的爆炸** 。真正变得不可控的，是 agent 与 agent 之间的依赖、agent 对 memory 的读写、agent 与 policy 的冲突，以及 agent 与时间和版本之间的错位。系统会从“一个流程”演化为一张 **随时间变化的稀疏图** ：任一时刻只有少数节点在运行，但整个结构在长期中持续生长。这正是我之前总结的 SoM 视角—— **无限结构单元，加上稀疏运行子图** 。（Marvin Minsky老爷子现在是我的指路明灯！）

与此同时，记忆会不再是单一形态，而是演化为一个 **多世代、多制度、多语义并存的宇宙** ：不同 schema 版本并行存在，不同责任分区交错使用，不同主体（人、工具、agent 群）写入记忆，不同可信度与溯源等级叠加，不同时间有效性与撤销机制共存。真正的复杂性不在于“数据多”，而在于 **同一句话在不同制度下含义完全不同** 。这也是为什么 schema 不是字段设计，而是文明的法律语言。

在这样的环境中，决策必然走向分层：每个 agent 可以是局部理性的，但系统必须接受全局治理。一个 agent 可能试图将 observation 提升为 world_state，另一个正在基于旧 world_state 进行资金配置，第三个在写入 append-only 的决策记录，第四个在执行回放审计。未来真正的冲突不来自 agent 的争吵，而来自 **不同责任分区的写入意图彼此冲撞** 。如果没有 protocol，系统会迅速退化为“谁先写进去谁赢”，而这类系统最终必然腐烂。

> 这个问题并不遥远。我下个月就能做。就基于现在这有限的4个分区和规则。

也正因为如此，这套制度必须被持续坚持和传承下来。多智能体社会中最危险的并不是恶意，而是 **善意的自动化** ：为了方便默认补齐 schema_version，为了兼容允许 legacy 参与决策，为了效率自动把 observation 升级为 world_state，为了体验把历史洗掉。每一步都看起来合理，甚至贴心，但它们的共同后果只有一个—— **系统开始用今天的认知改写昨天的责任** ，时间伦理由此崩塌。因此我在 P08 写下的那句宪法：“新写入必须使用 current schema_version；旧代只能通过 migration 进入 legacy”。

要让这样的制度真正流传，它必须同时具备三种形态。首先是 **文本形态** ：protocol 文档，作为可阅读的宪法；但文明不会因为文字存在就自动守法。其次是 **可执行形态** ：运行时强制执行的宪法执行机关——缺失 schema_version 直接 UC-01 阻断，旧代写入被拒绝，legacy 只读隔离，startup confrontation 在启动时即对抗历史；这一层让制度不再依赖人性。最后是 **可继承形态** ：回归测试，将宪法变成机器可以继承的约束——任何未来的人或 AI 只要试图放宽边界，CI 就会拒绝。这三者缺一不可，才配得上“流传”。

用我现在的协议语言，可以把未来十年的系统压缩成一句话： **多智能体社会会越来越像一个文明，拥有无限 agent、无限历史、无限版本；而唯一能让它十年不烂的，是协议必须同时存在于文档、运行时与回归测试中** 。这也是我当前最正确的姿势——我并不是在写更多代码，而是在做三件更难的事：定义不可妥协的不变量，把不变量变成运行时强制执行，再把执行结果固化为可继承的 CI 机制。这正是“制度要一直流传和坚持下来”的真实含义。
