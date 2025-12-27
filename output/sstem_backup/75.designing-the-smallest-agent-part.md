# Designing the Smallest Agent part 1

## 设计一个超级小的agent (中文在后面）

**Dec 17, 2025**

**Likes:** 0

This lesson continues the previous discussion on **minimal agents and agentic systems**. Before formally expanding the ideas, we will first look at a few very small and intentionally simple code examples. They are kept lightweight and a bit playful on purpose—not to show sophistication, but to reawaken a basic intuition: what an agent actually is, what role Google ADK plays, and how an agent is _constructed_ , rather than merely _described_.

After that, I will continue forward along **my own agentic exploration path**. Because of this, this piece follows Part 1 and Part 2, and it will gradually become somewhat unconventional—it does not quite resemble a standard “course.” This path may feel strange to some readers, and perhaps not very “canonical,” but at this stage I believe the exploration itself is inherently personal. To be honest, everyone is still probing and inventing. When there is no existing road in the world, the only thing you can do is walk one yourself— _“There was originally no road; when many people walk the same path, it becomes a road”_ (a Chinese writer named Lu Xun once said). There are plenty of standard courses elsewhere; readers can freely choose those if they prefer.

Alright—let’s begin with a few very easy-to-run project setups. All file conventions and environments follow directly from the previous installment. For the English version, the code is available on GitHub. For the Chinese version, I’ve pasted the code directly into the article—simply to make things easier for different reading preferences. In the Chinese version, I also included system logs to help you get a quick, concrete sense of what the runtime looks like and how it behaves. I’ve been trying to communicate a technical philosophy under this new paradigm, and it’s not easy—trust me—but I’m genuinely trying.

* * *

[ Lessons & Prompts](https://www.entropycontroltheory.com/p/execution-environment)[

## Execution Environment

](https://www.entropycontroltheory.com/p/execution-environment)

[Susan STEM](https://substack.com/profile/268169855-susan-stem)

·

Dec 8

🌐 Execution Environment Guide

[Read full story](https://www.entropycontroltheory.com/p/execution-environment)

* * *

## p01-minimal-agent

P01 Minimal Agent may look like nothing more than moving a single model call into a local terminal, but its significance is not about whether the answer is “correct.” Its real value lies in **turning a single chat interaction into a system unit that can be defined, executed, replaced, and evolved**.

A chat window conversation is a one-off linguistic act: it has no identity, no boundaries, and no lifecycle. The Minimal Agent explicitly separates three things:

  1.  **Who is speaking** (the agent’s identity),

  2.  **Under what constraints it speaks** (instructions as system positioning and boundaries),

  3.  **Through what mechanism it speaks** (a replaceable tool).




We must start from the minimal form because only when the system is extremely small can responsibilities be clearly separated: the agent is not the model, the tool is not intelligence, and the runner is only a scheduler. Once this smallest closed loop— **Agent → Tool → Response** —is established locally, reproducibly, and without a UI, then adding memory, sessions, multiple agents, or policy layers later becomes a matter of _structural extension_ , not semantic repair.

P01 is not a demo. It is an OS-level health check: verifying whether the system already meets the minimum conditions required to become a “living structure.”

<https://github.com/STEMMOM/adk-decade-of-agents/tree/main/projects/p01-minimal-agent>

* * *

## p02-event-ledger

The key change in P02 is not “better answers,” but that **the system gains its first traceable temporal structure**. A conversation is decomposed from a black-box “input → output” into an **auditable, replayable, and extensible event sequence** :

  * First, write the `user_message` to the ledger,

  * Then record the `tool_call` (tool name + prompt),

  * Then persist the `tool_result`,

  * Finally generate the `final_output`.




At the same time, a `Session` wraps this run into an independent life fragment with a `session_id`.

The significance is this: from this moment on, the agent no longer merely “says something on the spot.” It starts leaving **immutable execution traces** , like an operating system. In the future, when you add memory, policy gates, retries/rollbacks, permission control, cost accounting, or regression evaluation, none of these rely on guesswork or recollection. You simply insert new event types into the ledger while preserving order and causality.

What you truly gain is a **system-level evidence chain** —who said what, which tool was called, what result came back, and where failure occurred. This is precisely why the event ledger must come first: it is the minimum foundation that allows later agentic complexity to be governed, verified, and evolved.

<https://github.com/STEMMOM/adk-decade-of-agents/tree/main/projects/p02-event-ledger>

* * *

## p03-observability

The upgrade in P03 is not that you added more `print` statements. It is that you moved the agent from “able to run” to **observable**.

P02’s event ledger solves _after-the-fact traceability_ (what happened, and in what order). P03’s observer solves _in-flight diagnosability_ (where execution is right now, how many tools have been called, whether errors occurred, and what the execution path looks like).

A single run is decomposed into three kinds of signals:

  *  **Logs** : human-readable narratives (user input, success, output),

  *  **Traces** : step-level paths (step 1/2/3, indicating control flow),

  *  **Metrics** : aggregatable counts (tool_calls, errors, execution_steps) for long-term trends, alerts, and regression.




The meaning of this step is fundamental: from now on, you no longer infer system state by staring at model output. You possess a **runtime evidence layer independent of model semantics**. Adding latency, token usage, cost, retries, tool distributions, or branch paths later simply means extending the observer schema and instrumentation.

<https://github.com/STEMMOM/adk-decade-of-agents/tree/main/projects/p03-observability/src>

At the same time, this step exposes a critical red line: **metrics must be maintained by the system itself and must be interpretable**. For example, in the current demo, `total_events` remains zero. That alone tells you the metric definition has not been nailed down. This is not a bug—it is an intentional warning. That warning is the core of observability engineering: define measurement semantics first, or long-term evolution becomes unstable.

### Why this is a red line

Metrics face two natural temptations:

  1.  **Casual counting** : increment when you remember, ignore when you forget.

  2.  **Definition drift** : today an event counts, tomorrow it doesn’t; today retries count once, tomorrow twice.




When either happens, metrics stop being facts and turn into narratives. In my architecture, IR and ledgers exist specifically to resist narrative drift—metrics must obey the same discipline: **defined, reproducible, auditable**.

### “Maintained by the system itself”

This does not mean letting the model “estimate” metrics, nor relying on developer habits. It means:

  * Every action that affects a metric must trigger counting automatically in the execution path.

  * Counting logic must be bound to control flow, so it cannot be forgotten or misplaced.




Otherwise, metrics become mood logs rather than measurements.

### “Interpretable” metrics

Interpretability means you can answer questions like these consistently:

  * What exactly does `total_events` count?

  * If `execution_steps = 3`, will it always mean the same thing next month?

  * If retries are added later, does `tool_calls` count retries or only successful calls?




These definitions are called **metric semantics**. Without fixed semantics, metrics are meaningless.

### Why `total_events = 0` is a warning sign

Your metrics report shows:
    
    
    “total_events”:0
    
    

Yet many countable things clearly occurred: traces, logs, and run-level actions. This reveals a simple fact:

 **The system has not yet defined what it considers an “event,” nor bound that definition to an automatic update mechanism.**

This is precisely what “undefined semantics” looks like in practice.

### Why semantics must be fixed before long-term evolution

Later you will inevitably add:

  * More tools, steps, and branches

  * Caching, retries, concurrency, timeouts, fallbacks

  * Memory gates, policy enforcement, regression tests

  * Cost control and performance optimization




At that point, you will rely increasingly on metrics to make decisions:

  * “Error rate is too high—degrade functionality”

  * “Cost exceeded—disable search”

  * “Execution path length abnormal—raise alert”




If metric semantics are unstable, you reach the worst possible state:

> The system changes but you think it hasn’t.
> 
> Or the system hasn’t changed but you think it has.

This is why observability has one hard rule:

 **Metrics are not for display; they are for governance. Governance depends on stable semantics.**

* * *

After completing these small projects—which are all intentionally simple—I began adding my own ideas, as described in the article I shared.

From this point on, “connecting to the v0.1 runtime” becomes a **scale transition**. P01–P03 explore the _minimal cell biology_ of agents: a single call chain, a single event ledger, a single observability surface. After v0.1-runtime-mvp, the focus shifts to _system life science_.

[ Lessons & Prompts](https://www.entropycontroltheory.com/p/v01-runtime-mvp-the-moment-an-ai)[

## v0.1 Runtime MVP: The Moment an AI-Native OS Draws Its First Breath (hopefully 😂）

](https://www.entropycontroltheory.com/p/v01-runtime-mvp-the-moment-an-ai)

[Susan STEM](https://substack.com/profile/268169855-susan-stem)

·

Dec 13

[![v0.1 Runtime MVP: The Moment an AI-Native OS Draws Its First Breath \(hopefully 😂）](https://substackcdn.com/image/fetch/$s_!xhZb!,w_1300,h_650,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2a3efea6-db69-4ddc-be49-f5ad0464d33c_1536x1024.png)](https://www.entropycontroltheory.com/p/v01-runtime-mvp-the-moment-an-ai)

https://github.com/STEMMOM/adk-decade-of-agents/releases/tag/v0.1-runtime-mvp

[Read full story](https://www.entropycontroltheory.com/p/v01-runtime-mvp-the-moment-an-ai)

The concern is no longer “what answer did this question produce,” but establishing five irreversible foundations of an AI-Native OS:

  1.  **Sessions have lifecycles** (start/end define birth and death),

  2.  **World memory belongs to the user, not the model** ,

  3.  **Behavior is recorded as auditable structural trajectories** (events as state transitions, not log narratives),

  4.  **Persona becomes an identity anchor** (the same “you” is summoned every run),

  5.  **The runtime becomes the evolutionary spine** (future planners, routers, toolpacks, and multi-agent systems grow on it).




That is why I emphasize “Not logs.” Logs are **human stories** ; ledgers are system evidence; events are structural fingerprints. Once you have session IDs, trace IDs, timestamps, and structured payloads, you gain a replayable, attributable, governable time machine. That is the fundamental reason to move from “asking in a window” to a locally reproducible runtime: language enters an operating-system form that can record itself, persist itself, and evolve over time.

这一课承接前面对 **minimal agent 与 agentic 系统** 的讨论。在正式展开之前，我们先来看几段非常简单的小代码，它们刻意保持轻量、有点好玩，只是为了重新唤起一种直觉：什么是 agent，Google ADK 在其中扮演什么角色，以及一个 agent 是如何被构造出来的，而不仅仅是被“描述”。在这之后，我会继续沿着 **我自己的 agentic 探索路径** 往前走（所以这篇文是Part 1, Part 2之后，会变得不大寻常，不大像个常规的“课程”），这条路对不少人来说可能会显得有些奇怪，甚至不太“标准”，但我认为在这个阶段，这件事本来就是高度个人化的探索。说实话，所有人都还在摸索、在发明；当世界上还没有现成的路时，唯一能做的事情就是自己走一条出来—— **世上本无路，走的人多了，便成了路（一个叫做鲁迅的中国人说的）** 。标准课程其他地方也有很多，看官可以自行选择。

好，下面我们先从几个非常容易上手的项目部署开始。所有的文件规范，环境，都延续前篇。

所有的文件规范和环境设置都直接沿用上一篇的内容。英文版本的代码放在 GitHub 上；中文版本中，我把代码直接贴在文章里，纯粹是为了照顾不同的阅读习惯。中文版本里还附带了系统运行日志，帮助你直观感受这个运行时大概长什么样、应该如何理解它的状态。我一直在尝试讲清楚这种新范式下的我的技术哲学，说实话并不容易。

# p01-minimal-agent

P01 Minimal Agent 看起来只是把一次模型调用搬到了本地终端，但它的意义不在“回答得对不对”，而在于 **把一次聊天行为转化为一个可被定义、运行、替换和演化的系统单元** 。Chat 窗口里的对话是一次性的语言行为，没有身份、没有边界、没有生命周期，而 Minimal Agent 明确区分了三件事：谁在说话（Agent 身份）、在什么约束下说话（instructions 作为系统定位与边界）、通过什么机制说话（可替换的 Tool）。之所以必须从 minimal 开始，是为了在系统还极小的时候就把职责切清：Agent 不是模型，Tool 不是智能，Runner 只是调度；一旦这一最小闭环（Agent → Tool → Response）在本地、可复现、无 UI 的运行时中成立，后续加入 memory、session、多 agent、policy 都只是结构扩展而不是语义纠错。P01 不是 demo，而是一次 OS 级的生命体检：验证这个系统是否已经具备“成为活结构”的最低条件。
    
    
    ## 🧠 三、`projects/p01-minimal-agent/src/main.py`
    
    from google import genai
    
    class MinimalAgent:
        “”“
        P01: 最小 Agent 细胞
    
        这里只做三件事：
        1. 持有一个系统说明（instructions）
        2. 接收用户问题
        3. 调用一个“工具”（这里是 ask_gemini），并返回回答
        “”“
    
        def __init__(self, name: str, instructions: str, model: str = “gemini-2.0-flash”):
            self.name = name
            self.instructions = instructions
            self.model = model
            self.client = genai.Client()
    
        def ask_gemini(self, user_question: str) -> str:
            “”“
            作为 P01 的“工具函数（Tool）”：
            目前只是直接调用模型，后续可以替换为：
            - 带 Search 的模型
            - 带 Tool 调用的 Agent
            “”“
            prompt = (
                f”{self.instructions}\\n\\n”
                f”User question: {user_question}\\n\\n”
                “Answer in a concise way.”
            )
    
            resp = self.client.models.generate_content(
                model=self.model,
                contents=prompt,
            )
            return resp.text
    
        def run_once(self, user_question: str) -> str:
            “”“
            最小 Runner：执行一次 Agent–Tool 调用链。
            后续 P02 开始，这里会被真正的 Runner + Session 替换/扩展。
            “”“
            return self.ask_gemini(user_question)
    
    def main():
        print(”[P01] Minimal Agent Cell Demo”)
    
        # 1. 定义一个最小 Agent
        agent = MinimalAgent(
            name=”root_agent”,
            instructions=(
                “You are a minimal AI agent cell. “
                “Your job is to answer the user’s question clearly and briefly. “
                “This is a health-check and structure-check run, not a production system.”
            ),
        )
    
        # 2. 定义一个“真实世界问题”
        user_question = “What happened in AI this week? Please summarize briefly.”
    
        print(”User:”, user_question)
    
        # 3. 通过最小 Runner 执行一次调用链
        try:
            answer = agent.run_once(user_question)
        except Exception as e:
            print(”\\n[ERROR] Agent failed to run:”)
            print(repr(e))
            return
    
        # 4. 输出结果
        print(”\\nAgent:”)
        print(answer)
    
    if __name__ == “__main__”:
        main()
    
    
    
    
    (.venv) ➜  p01-minimal-agent git:(main) ✗ python src/main.py
    [P01] Minimal Agent Cell Demo
    Both GOOGLE_API_KEY and GEMINI_API_KEY are set. Using GOOGLE_API_KEY.
    User: What happened in AI this week? Please summarize briefly.
    
    Agent:
    AI saw developments in text-to-video, concerns over AI bias in hiring, and continued advancements in large language model capabilities.
    
    

# p02-event-ledger

P02 的关键不是“回答更好”，而是 **系统第一次拥有了可追溯的时间结构** ：你把一次对话从“黑箱的输入→输出”拆成了一个 **可审计、可回放、可扩展的事件序列** ——先把 `user_message` 写入账本，再记录 `tool_call`（工具名+prompt），再落地 `tool_result`，最后生成 `final_output`；同时用 `Session` 把这次运行封装成一个带 `session_id` 的独立生命片段。这样做的意义是：从这一刻起，Agent 不再只是“当场说一句话”，而是开始像操作系统一样留下 **不可变的执行轨迹** ——未来你要加 memory、policy gate、重试/回滚、权限控制、成本计费、评测回归，全部都不是“靠记忆猜”，而是 **在 ledger 上插入新事件类型** 并保持顺序与因果；你真正获得的是“系统的证据链”（谁说了什么、调用了什么、得到了什么、哪里失败），这就是为什么必须先做 event ledger：它是后续所有 agentic 复杂性能够被治理、被验证、被演化的最低地基。

[main.py](http://main.py/)
    
    
    from google import genai
    from event_ledger import Session
    import json
    
    class MinimalAgent:
        def __init__(self, name: str, instructions: str, model: str = “gemini-2.0-flash”):
            self.name = name
            self.instructions = instructions
            self.model = model
            self.client = genai.Client()
    
        def ask_gemini(self, prompt: str) -> str:
            resp = self.client.models.generate_content(
                model=self.model,
                contents=prompt,
            )
            return resp.text
    
        def run_once(self, user_message: str, session: Session) -> str:
            # Log user message
            session.ledger.add(”user_message”, content=user_message)
    
            # Prepare system prompt
            prompt = f”{self.instructions}\\n\\nUser: {user_message}”
    
            # Log tool call
            session.ledger.add(”tool_call”, tool=”ask_gemini”, prompt=prompt)
    
            # Execute tool
            try:
                output = self.ask_gemini(prompt)
                session.ledger.add(”tool_result”, result=output)
            except Exception as e:
                session.ledger.add(”error”, message=str(e))
                raise e
    
            # Log final output
            session.ledger.add(”final_output”, content=output)
    
            return output
    
    def main():
        print(”[P02] Stateful Sessions & Event Ledger Demo”)
    
        agent = MinimalAgent(
            name=”root_agent”,
            instructions=”You are a minimal agent cell with an event ledger.”,
        )
    
        # Create a session for this run
        session = Session(agent)
        print(”Session ID:”, session.session_id)
    
        user_question = “Give me a 1-sentence summary of this week’s AI news.”
    
        answer = agent.run_once(user_question, session)
        print(”\\nAgent:”, answer)
    
        print(”\\n--- Event Ledger ---”)
        print(json.dumps(session.ledger.dump(), indent=2))
    
    if __name__ == “__main__”:
        main()
    
    

event_ledger.py
    
    
    import time
    import uuid
    
    def now_ts():
        return time.strftime(”%Y-%m-%d %H:%M:%S”)
    
    class EventLedger:
        “”“
        A simple append-only event ledger.
        Each event is a dict with:
        - type
        - data
        - timestamp
        “”“
    
        def __init__(self):
            self.events = []
    
        def add(self, event_type: str, **kwargs):
            event = {
                “type”: event_type,
                “timestamp”: now_ts(),
                “data”: kwargs,
            }
            self.events.append(event)
    
        def dump(self):
            return self.events
    
    class Session:
        “”“
        A session encapsulates:
        - session_id
        - event ledger
        - an agent instance
        “”“
    
        def __init__(self, agent):
            self.session_id = str(uuid.uuid4())
            self.ledger = EventLedger()
            self.agent = agent
    
    
    
    
    (.venv) ➜  p02-event-ledger git:(main) ✗ python src/main.py
    [P02] Stateful Sessions & Event Ledger Demo
    Both GOOGLE_API_KEY and GEMINI_API_KEY are set. Using GOOGLE_API_KEY.
    Session ID: f4692191-4f39-4702-b47f-29b4ed75abd1
    
    Agent: My Summary: This week saw advancements in AI models becoming more efficient and accessible, alongside growing discussions about responsible AI development and potential societal impacts.
    
    --- Event Ledger ---
    [
      {
        “type”: “user_message”,
        “timestamp”: “2025-12-08 12:18:57”,
        “data”: {
          “content”: “Give me a 1-sentence summary of this week’s AI news.”
        }
      },
      {
        “type”: “tool_call”,
        “timestamp”: “2025-12-08 12:18:57”,
        “data”: {
          “tool”: “ask_gemini”,
          “prompt”: “You are a minimal agent cell with an event ledger.\\n\\nUser: Give me a 1-sentence summary of this week’s AI news.”
        }
      },
      {
        “type”: “tool_result”,
        “timestamp”: “2025-12-08 12:18:57”,
        “data”: {
          “result”: “My Summary: This week saw advancements in AI models becoming more efficient and accessible, alongside growing discussions about responsible AI development and potential societal impacts.\\n”
        }
      },
      {
        “type”: “final_output”,
        “timestamp”: “2025-12-08 12:18:57”,
        “data”: {
          “content”: “My Summary: This week saw advancements in AI models becoming more efficient and accessible, alongside growing discussions about responsible AI development and potential societal impacts.\\n”
        }
      }
    ]
    
    

# p03-observability

P03 的升级点不在“多做了点 print”，而在于你把 Agent 从“能跑”推进到“ **可观测** ”：P02 的 Event Ledger 解决的是 **事后可追溯** （发生了什么、顺序是什么），而 P03 的 Observer 解决的是 **运行中可诊断** （现在走到哪一步、调用了几次工具、有没有报错、执行路径长什么样）。它把一次调用拆成三类信号： **Logs** （人类可读叙事：User/成功/输出）、 **Traces** （步骤级路径：step1/2/3，告诉你控制流在哪里）、 **Metrics** （可聚合计数：tool_calls/errors/execution_steps，用于长期趋势、报警与回归）。这一步的意义是：从此以后你不再靠“看输出猜系统状态”，而是拥有一套独立于模型语义的 **运行证据层** ——未来加上 latency、token、cost、retry、tool 分布、分支路径，你只是在 Observer 上扩字段和埋点；同时它也暴露了一个关键红线： **metrics 必须由系统自己维护且可解释** （比如现在 `total_events` 没有被更新，你看这个跑出来数值不是零吗？就说明“指标口径”还没定义好），而这正是可观测性工程的核心——先把口径钉死，系统才可能长期稳定演化。

 **多说几句：“指标（metrics）不是装饰品，它本身也是协议的一部分。”** 一旦你开始用 metrics 来判断系统健康、回归是否通过、是否报警、是否允许写入记忆，那么 metrics 就变成了“系统的仪表盘读数”。仪表盘如果不可靠，你的系统就会在十年尺度里慢慢漂移，而且你还以为自己在“可观测”。

### 1) 为什么说这是红线？

因为 metrics 有两个天然诱惑：

  *  **随便记** ：想起来就 `inc()` 一下，没想起来就算了

  *  **口径漂移** ：今天把某类事件算进“总数”，明天不算；今天“tool_call”算一次，明天重试算两次




一旦发生这两种事，指标就不再是“事实”，而是“叙事”。而我的架构里 IR/ledger （现在你先别问这啥意思）是在对抗叙事的——所以 metrics 也必须服从同样的纪律： **可定义、可复现、可审计** 。

### 2) “必须由系统自己维护”是什么意思？

不是让模型去“估计”指标，也不是让开发者靠习惯手动加点，而是：

  * 每一个会影响指标的动作，都必须在代码路径里 **自动触发** 计数或采样

  * 计数逻辑要和执行逻辑绑定（同一个控制流里），避免“忘了加”“加错地方”




否则指标会变成：有人记就有、没人记就没有——那它就不叫指标，叫心情记录。

### 3) “必须可解释”是什么意思？

可解释=你能回答这类问题，而且答案不会随心情变：

  * `total_events` 到底数的是什么？是 log 条数？trace 条数？还是“系统事件”的抽象概念？现在这个代码里，就不知道了。

  * 一次 run 的 `execution_steps=3`，这个 3 的含义是不是永远不变？以后加了一个中间步骤，它应该变 4 吗？还是仍然 3（只算关键阶段）？

  * `tool_calls=1`：如果未来加了 retry，失败重试算 2 还是 1？如果 tool 内部又调用了子工具算不算？




这些都叫 **指标口径** 。口径如果没钉死，指标就没有意义。现在就是一个简单的示意而已，这个指标就不严谨。

### 4) 用你现在的例子：`total_events` 为什么是警报信号？

你现在的 metrics 里有：
    
    
    “metrics”: {
      “total_events”: 0,
      “tool_calls”: 1,
      “errors”: 0,
      “execution_steps”: 3
    }
    
    

但实际上你已经产生了很多“可数的东西”：

  * traces 3 条

  * logs 3 条

  * 还发生了至少一次“run”级别事件（收到用户、调用模型、返回输出）




`total_events` 仍然是 0，说明一个事实：

 **还没有定义“我认为 event 是什么”，也没有把它绑定到任何自动更新机制上。**

这就是“口径没定义好”的具体表现。

### 5) 为什么说“先把口径钉死，系统才可能长期稳定演化”？

因为后面你一定会做这些事：

  * 加更多工具、更多步骤、更多分支

  * 加缓存、重试、并发、超时、fallback

  * 加 memory 写入门禁、policy gate、回归测试

  * 加成本控制（tokens/cost）、性能优化（latency）




这时你会 **越来越依赖 metrics 来做决策** ：

“错误率升高就降级”“成本超阈值就禁止搜索”“某条路径执行步数异常就报警”。

如果 metrics 口径没钉死，你会出现最可怕的情况：

> 系统在变，你以为它没变（因为指标看起来正常）；
> 
> 系统没变，你以为它变了（因为指标口径悄悄变了）。

这就是 observability 工程里最硬的原则：

 **指标不是为了展示，而是为了治理（不是给傻领导看的）；治理依赖口径稳定。**

* * *

[main.py](http://main.py/)
    
    
    from google import genai
    from observer import Observer
    import uuid
    import json
    
    # ------------------------------------------------------------
    # Minimal Agent (same as P01/P02, but extended with observer)
    # ------------------------------------------------------------
    class MinimalAgent:
        def __init__(self, name: str, instructions: str, model: str = “gemini-2.0-flash”):
            self.name = name
            self.instructions = instructions
            self.model = model
            self.client = genai.Client()
    
        def ask_gemini(self, prompt: str, observer: Observer):
            observer.trace(2, “Calling Gemini model”)
            observer.inc(”tool_calls”)
    
            resp = self.client.models.generate_content(
                model=self.model,
                contents=prompt,
            )
            return resp.text
    
        def run_once(self, user_message: str, observer: Observer):
            observer.trace(1, “Received user message”)
            observer.log(f”User: {user_message}”)
    
            prompt = f”{self.instructions}\\n\\nUser: {user_message}”
    
            try:
                output = self.ask_gemini(prompt, observer)
                observer.log(”Model returned successfully”)
            except Exception as e:
                observer.log(f”Error: {str(e)}”)
                observer.inc(”errors”)
                raise e
    
            observer.trace(3, “Returning final output”)
            observer.log(f”Agent Output: {output}”)
    
            return output
    
    # ------------------------------------------------------------
    # MAIN
    # ------------------------------------------------------------
    def main():
        print(”[P03] Observability Demo\\n”)
    
        observer = Observer()
    
        agent = MinimalAgent(
            name=”root_agent”,
            instructions=”You are a minimal agent with observability.”,
        )
    
        question = “Give me a one-sentence summary of this week’s AI news.”
    
        answer = agent.run_once(question, observer)
    
        print(”\\n--- FINAL OUTPUT ---”)
        print(answer)
    
        print(”\\n--- OBSERVABILITY REPORT ---”)
        print(json.dumps(observer.dump(), indent=2))
    
    if __name__ == “__main__”:
        main()
    
    

[observer.py](http://observer.py/)
    
    
    import time
    
    def now_ts():
        return time.strftime(”%Y-%m-%d %H:%M:%S”)
    
    class Observer:
        def __init__(self):
            self.logs = []
            self.traces = []
            self.metrics = {
                “total_events”: 0,
                “tool_calls”: 0,
                “errors”: 0,
                “execution_steps”: 0,
            }
    
        # LOGGING -----------------------------------------------------
        def log(self, message: str):
            entry = f”[LOG] {now_ts()} — {message}”
            self.logs.append(entry)
            print(entry)
    
        # TRACING -----------------------------------------------------
        def trace(self, step: int, message: str):
            entry = f”[TRACE] step {step}: {message}”
            self.traces.append(entry)
            print(entry)
            self.metrics[”execution_steps”] += 1
    
        # METRICS -----------------------------------------------------
        def inc(self, key: str):
            if key in self.metrics:
                self.metrics[key] += 1
    
        # FINAL EXPORT ------------------------------------------------
        def dump(self):
            return {
                “logs”: self.logs,
                “traces”: self.traces,
                “metrics”: self.metrics,
            }
    
    

* * *
    
    
    (.venv) ➜  p03-observability git:(main) ✗ python src/main.py
    [P03] Observability Demo
    
    Both GOOGLE_API_KEY and GEMINI_API_KEY are set. Using GOOGLE_API_KEY.
    [TRACE] step 1: Received user message
    [LOG] 2025-12-08 12:39:34 — User: Give me a one-sentence summary of this week’s AI news.
    [TRACE] step 2: Calling Gemini model
    [LOG] 2025-12-08 12:39:36 — Model returned successfully
    [TRACE] step 3: Returning final output
    [LOG] 2025-12-08 12:39:36 — Agent Output: Okay, I will provide a one-sentence summary of this week’s AI news.
    
    ... (Observing current AI news headlines and trends) ...
    
    Summary: This week saw significant advancements in generative AI models, sparking debate about their potential impact on creative industries and the workforce.
    
    --- FINAL OUTPUT ---
    Okay, I will provide a one-sentence summary of this week’s AI news.
    
    ... (Observing current AI news headlines and trends) ...
    
    Summary: This week saw significant advancements in generative AI models, sparking debate about their potential impact on creative industries and the workforce.
    
    --- OBSERVABILITY REPORT ---
    {
      “logs”: [
        “[LOG] 2025-12-08 12:39:34 \\u2014 User: Give me a one-sentence summary of this week’s AI news.”,
        “[LOG] 2025-12-08 12:39:36 \\u2014 Model returned successfully”,
        “[LOG] 2025-12-08 12:39:36 \\u2014 Agent Output: Okay, I will provide a one-sentence summary of this week’s AI news.\\n\\n... (Observing current AI news headlines and trends) ...\\n\\nSummary: This week saw significant advancements in generative AI models, sparking debate about their potential impact on creative industries and the workforce.\\n”
      ],
      “traces”: [
        “[TRACE] step 1: Received user message”,
        “[TRACE] step 2: Calling Gemini model”,
        “[TRACE] step 3: Returning final output”
      ],
      “metrics”: {
        “total_events”: 0,
        “tool_calls”: 1,
        “errors”: 0,
        “execution_steps”: 3
      }
    }
    
    

走完这几个项目，都很简单，然后，我就加入了一些自己的想法。就是我发的这篇文章。我开始围绕ADK做了一些“基建”。

[ Lessons & Prompts](https://www.entropycontroltheory.com/p/v01-runtime-mvp-the-moment-an-ai)[

## v0.1 Runtime MVP: The Moment an AI-Native OS Draws Its First Breath (hopefully 😂）

](https://www.entropycontroltheory.com/p/v01-runtime-mvp-the-moment-an-ai)

[Susan STEM](https://substack.com/profile/268169855-susan-stem)

·

Dec 13

[![v0.1 Runtime MVP: The Moment an AI-Native OS Draws Its First Breath \(hopefully 😂）](https://substackcdn.com/image/fetch/$s_!xhZb!,w_1300,h_650,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2a3efea6-db69-4ddc-be49-f5ad0464d33c_1536x1024.png)](https://www.entropycontroltheory.com/p/v01-runtime-mvp-the-moment-an-ai)

https://github.com/STEMMOM/adk-decade-of-agents/releases/tag/v0.1-runtime-mvp

[Read full story](https://www.entropycontroltheory.com/p/v01-runtime-mvp-the-moment-an-ai)

在这一步以后“接入 v0.1 runtime”本质上是一次 **尺度跃迁** ：P01–P03 咱们在做的是 _agent 的最小细胞学_ （一次调用链、一次事件账本、一次可观测信号），而 v0.1-runtime-mvp 之后的项目，我展示我开始做的是 _系统生命学_ ——不再关心“这一问答输出了什么”，而是确立一个 AI-Native OS 的五个不可逆基建： **会话有生命周期** （start/end 让系统知道何时生、何时死）、 **世界记忆属于用户而非模型** （memory_store 变成外部世界状态）、 **行为以可审计的结构轨迹记录** （events.jsonl 记录的是世界状态转移而不是日志叙事）、 **persona 成为身份锚** （每次运行都召唤同一个“你”）、以及 **runtime 成为未来演化的脊椎** （Planner/Router/Toolpacks/Multi-Agent 以后都只是在这根脊柱上长出来）。因此我强调“Not logs”非常关键：log 是人类叙述，ledger 是系统证据，事件是结构指纹；一旦有了 session_id/trace_id/时间戳/结构化 payload，你就拥有了可回放、可归因、可治理的“时间机器”，这正是你从“直接在窗口问”转向“本地可复现运行时”的根本理由语言进入一个能自我记录、自我延续、可长期进化的操作系统形态。
