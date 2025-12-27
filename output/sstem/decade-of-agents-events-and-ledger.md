# Decade of Agents: Events and Ledger: The Rulebook of Agents

## 事件和账本，智能体的规则。中文在后面

**Dec 19, 2025**

**Likes:** 0

[![](https://substackcdn.com/image/fetch/$s_!1PgM!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa060be12-4379-4610-94d6-85e5e85355c3_1536x1024.heic)](https://substackcdn.com/image/fetch/$s_!1PgM!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa060be12-4379-4610-94d6-85e5e85355c3_1536x1024.heic)

<https://github.com/STEMMOM/adk-decade-of-agents/tree/P06-pre-policy-gate>

* * *

There are a few baseline assumptions I want to make explicit first.

This repo is called **Decade of Agents**.

Before I fully unfold the long-term system I’m building, there are really only two things I want to convey:

 **First,** over the next decade, the work I believe in most will revolve around **agents**.

 **Second,** no matter how the application layer changes—no matter how many concrete projects I’ve imagined, derived, and abandoned over the past two years—they all converge to the same question in the end: **agent infrastructure**. Applications can change, scenarios can change, but the principles of the base layer are stable.

 **Lessons and Prompts** is simply where I show _how this base layer gets built_.

My worldview will gradually reveal itself throughout this series, but I don’t recommend treating it as a “course.” The name “Lessons” isn’t perfect; I just couldn’t find a better one.

If you’ve ever played Chinese Go (Weiqi), you can think of every “P” in this series as a single move— _one stone placed on the board_.

What I’m choosing is this: **to play while explaining** , rather than first burying myself in rehearsed patterns and only explaining afterward.

If this were the old me, I wouldn’t explain anything. I’d just grind in silence.

But now I need constraints. I need to communicate in sync with people who genuinely understand my technical philosophy _while I’m building it for real_ —especially now that I’ve realized that, as a solo builder, I might actually be able to shoulder a system of this scale. An engineering project of this size used to be unthinkable for an individual developer.

That is the real reason this repo exists—and why the series that follows, full of agent “infrastructure” that looks boring, exists. The further I go, the harder it becomes to write these things like “lessons,” because the system gets more complex and my cognitive load keeps rising. Meanwhile, people selling courses for traffic will always put “you can build this” at the front. But for frontier exploration, I don’t think that framing matters much—at least, I can’t do it anymore. So these so-called “lessons” will become jumpy and pointillistic, because I simply cannot, alone, under heavy development, perfectly demonstrate every step end-to-end. Once again: freeCodeCamp is incredible.

 **Infrastructure = the things that, once clarified and locked in, you basically don’t dare to casually change for the next ten years.**

It’s not a question of “is it convenient,” but rather:

> once the measurement standard drifts, the system will die a slow death.

Logs can be messy.

 **Events cannot.**

* * *

## So what exactly is “infrastructure” in an AI-Native / Agent OS?

Not servers.

Not cloud resources.

Not models.

I believe it’s **four categories of irreversible constraints**.

* * *

## 1) Time Infrastructure

 **How does the system perceive time, record ordering, and replay history?**

In this repo, that’s:

  * `events.jsonl`

  * `session.start / session.end`

  * `trace_id`

  * causal ordering




👉 **Once time gets confused, the system becomes neither auditable nor governable.**

Logs can be messy.

 **Events cannot.**

* * *

## 2) Identity Infrastructure

 **Who is speaking? Who is acting?**

In this repo, that’s:

  * `persona.json`

  * session bound to a persona

  * every call anchored to the same “you”




👉 Without an identity anchor, memory has no subject.

And then history has no meaning.

* * *

## 3) World-State Infrastructure

 **What does the “world the system remembers” look like?**

In this repo, that’s:

  * `memory_store.json`

  * schema + version

  * migration




👉 Without a stable world-state, every upgrade is basically amnesia.

* * *

Code itself is not the point.

I assume anyone reading this already has powerful AI-assisted programming tools.

And I’m not saying this from the position of someone who “can’t code.” On the contrary: I used to be a heavy **freeCodeCamp** learner, and I know that path extremely well. I just haven’t paid attention to it for a year—not because code stopped mattering, but because **the center of gravity moved**.

What you truly need to see is not a specific implementation, but **the path itself** , and the **system philosophy** behind it.

Once that is solid, code stops being the bottleneck.

Implementation should be done in the context of _your_ project, unfolding naturally with AI assistance. You can use different languages, different frameworks, and different styles to land the same structural principles.

So don’t get stuck on whether a function is written “the best way,” or whether a class is elegant. Those are replaceable, evolvable layers.

If you understand the direction and the constraints here,

code is simply the branches and leaves that grow from the trunk.

* * *

# P04 | Deterministic Envelope: when the system first gains “history that cannot drift”

I’ve been doing something that looks “boring”: making a minimal AI system run in the terminal, write a few files, and print a line.

But P04 is a watershed—because from this moment on, the system gains something for the first time: **history that cannot drift**.

Not logs.

Not “what I feel happened today.”

But **an event trace that machines can parse consistently—and that can still be understood ten years from now**.

* * *

## 1) Why do P04? Isn’t the chat window enough?

The problem with the chat window isn’t “unstable answers.” It’s that it has no laws of history.

  * It’s hard to reproduce what actually happened in a conversation

  * It’s hard to ask “what exactly happened?”

  * It’s even harder to guarantee that after upgrades, old history remains usable




You think you’re building an agent, but you’re actually just using a model as a temporary talking machine.

What I’m building is an OS. It must know:

> what truly counts as having happened.

In this OS:

 **If it didn’t enter the event ledger, then from the system’s perspective it did not happen. (This sentence matters.)**

* * *

## 2) What did P04 do? One sentence.

We unify every line of `runtime_data/events.jsonl` into a fixed Envelope:

> schema_version / event_type / session_id / trace_id / ts / payload / payload_hash

And we lock the standards:

  * `ts` unified to UTC (prevent timezone drift)

  * `payload_hash` computed by the system: `sha256(canonical_json(payload))`

  * all events go through a single write entry (prevent multiple competing formats)




This sounds like engineering detail, but it’s actually an **OS constitution**.

* * *

## 3) What does “Deterministic” really mean?

It means:

> for the same payload, no matter how key ordering changes, it must produce the same hash.

This is critical, because in the future you will:

  * replay

  * run regression tests

  * audit

  * enforce a policy gate

  * migrate




All of that depends on one fact:

> events must be verifiable structural facts, not narrative text.

This looks like extra work, but you have to imagine this system could become something people absolutely must not be able to alter—for institutions, money, authorization, and other sensitive domains. Having this is better than not having it. What is infrastructure? Infrastructure is anticipating the future and removing landmines, not planting a thousand landmines for future you. If anything, I only worry this still isn’t enough.

* * *

## 4) What does the actual output look like?

After one OS-level MVP run, I `tail -n 4 runtime_data/events.jsonl` and see (one JSON per line):
    
    
    {"event_type":"session.start","payload":{"_source":"p00-agent-os-mvp","message":"Session started for p00 MVP","persona_user_id":"susan"},"payload_hash":"...","schema_version":"1.0","session_id":"p00-4c31...","trace_id":"633d...","ts":"2025-12-18T01:55:18.998Z"}
    {"event_type":"user.message","payload":{"_source":"p00-agent-os-mvp","text":"Hello, this is the first OS-level MVP run."},"payload_hash":"...","schema_version":"1.0","session_id":"p00-4c31...","trace_id":"633d...","ts":"2025-12-18T01:55:18.999Z"}
    {"event_type":"agent.reply","payload":{"_source":"p00-agent-os-mvp","reply":"[MVP Kernel Stub] You said: ...","tool_calls":[]},"payload_hash":"...","schema_version":"1.0","session_id":"p00-4c31...","trace_id":"633d...","ts":"2025-12-18T01:55:18.999Z"}
    {"event_type":"session.end","payload":{"_source":"p00-agent-os-mvp","message":"Session ended for p00 MVP"},"payload_hash":"...","schema_version":"1.0","session_id":"p00-4c31...","trace_id":"633d...","ts":"2025-12-18T01:55:18.999Z"}
    
    

Notice a few things:

  * `session_id` is unique per run → runs don’t get blended into one “life”

  * `trace_id` binds the causal chain → preparation for P05

  * `payload_hash` is recomputable → preparation for audit/regression

  * `_source` is constrained inside payload → the top-level protocol stays minimal and stable




This is not “logging.” It’s **a structural fingerprint of system behavior**.

And yes, causality matters. If you’ve used LLMs long enough, you already know their behavior patterns. In the agent era, how could causality _not_ matter?

* * *

## 5) The real value of P04: it becomes the foundation for everything that follows

Without a unified event envelope, everything later will drift:

  * P05 Trace & Causality: you can’t stably track “who caused what”

  * P06 Replay Runner: you can’t reliably replay history

  * P07 Policy Gate: you can’t audit “why this memory was written”

  * P08 Migration: you can’t migrate across versions without breaking continuity

  * P09 Observability: metrics won’t reconcile

  * P10 System Process: different processes will write different formats and the system will immediately split




That’s why I say: P04 looks small, but it’s irreversible.

* * *

## 6) The ending of this lesson: one OS-level conclusion

Many people treat agents as “model + tools.”

I treat agents as “a living process.”

And a living process must leave history.

History must be verifiable.

To be verifiable, you need an envelope.

 **P04 is the moment this system first gained “history that cannot drift.”**

Next I’ll do P05: define how trace truly propagates and branches, so the system moves from a “timeline” into a “causal tree.”

* * *

# P05 | Trace & Causality: when the system first knows “who caused what”

In P04, we turned `events.jsonl` into deterministic history: every event has a stable envelope (schema_version, ts, payload_hash), and the system gained a “timeline that cannot drift.” But a timeline answers only one question: **what happened, in what order**. P05 pushes the system from “recording” to “attribution”: not just what happened, but **who caused what** , and how an action chain grows inside the system. In other words, P05 evolves the system from logs/流水账 into **causal structure** —the shared foundation for Replay (P06), Policy Gate (P07), governance and risk control (the MCP series).

* * *

## 1) What does P05 do? One sentence.

Assign a “causal node” to every action that can influence downstream outcomes (causality matters, causality matters, causality matters!!!), and use a parent pointer to connect nodes into a tree.

Engineering-wise, it compresses into two fields:

  * `span_id`: who I am (the causal node ID)

  * `parent_span_id`: where I came from (points to the parent)




We first place them inside `payload` (so we don’t break the P04 top-level protocol):

  * `payload._span_id`

  * `payload._parent_span_id`




And we add one governance-required field:

  * `payload._actor`: who triggered this event (runtime/user/agent/tool/policy)




From this point on, causality is not inferred—it is **explicitly written by the system**.

* * *

## 2) Why is this an OS-level watershed?

Because without causality, your system can only “happen,” not be “governed.”

  *  **Errors can’t be attributed** : you see an error, but don’t know which chain it belongs to

  *  **Tool risk can’t be localized** : tool calls may be temporally adjacent but causally unrelated

  *  **Policy gates have nowhere to attach** : policy intercepts “action nodes,” not fuzzy semantics

  *  **Replay can’t be real** : replay is not “ask the model again,” it’s re-playing a structured path




P05’s goal is clear: give the system a capability— **answer “why” with structure**. I can’t imagine any agent system not needing this.

* * *

## 3) What does the reconstructed causal tree look like?

I wrote a debug script `scripts/render_trace_tree.py`. It reads `runtime_data/events.jsonl` and rebuilds the causal tree using `_span_id/_parent_span_id`. After one minimal MVP run, it prints:

(session.start root → user.message → agent.reply; session.end alongside.)

And it reports:

  * ROOTS: 1 (only one root)

  * ORPHANS: 0 (no orphan nodes)




These two numbers matter a lot: they mean the causal structure is **reconstructable** , not merely “looks like it.”
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ python scripts/render_trace_tree.py
    
    ========================================================================================
    SESSION: p00-7f28677d-aae4-4a00-91cd-273a68d5b0a1
    TRACE:   2cf60704-99e5-497a-9eda-ddfe8ef420d5
    EVENTS:  4  | ROOTS: 1  | ORPHANS: 0
    
    --- ROOT 1 ---
    session.start  actor=runtime  span=fd41dfd3-124c-4c2f-94c7-6cc5eb196557  ts=2025-12-18T02:41:11.417Z
        ↳ Session started for p00 MVP
        payload={"message": "Session started for p00 MVP", "persona_user_id": "susan"}
       ├─ user.message  actor=user  span=733a11c0-25a8-4de3-a1cc-ba3e70fb216c  parent=fd41dfd3-124c-4c2f-94c7-6cc5eb196557  ts=2025-12-18T02:41:11.417Z
       │      ↳ Hello, this is the first OS-level MVP run.
       │      payload={"text": "Hello, this is the first OS-level MVP run."}
       │  └─ agent.reply  actor=agent  span=3d20e599-7312-466e-9cca-c3b65f807f07  parent=733a11c0-25a8-4de3-a1cc-ba3e70fb216c  ts=2025-12-18T02:41:11.417Z
       │         ↳ [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
       │         payload={"reply": "[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.", "tool_calls": []}
       └─ session.end  actor=runtime  span=70736632-74bb-4982-b153-e0cbea19972b  parent=fd41dfd3-124c-4c2f-94c7-6cc5eb196557  ts=2025-12-18T02:41:11.418Z
              ↳ Session ended for p00 MVP
              payload={"message": "Session ended for p00 MVP"}
    
    Done.
    
    

* * *

## 4) A critical standard: lifecycle vs business chain (the core of P05 v1)

There’s an easy mistake: attaching `session.end` under the last business action (e.g. under `agent.reply`). In v0 it seems fine, but semantically it’s a future landmine. Once you add tool calls, policy, and memory writes, you’ll find the session boundary becomes harder and harder to define.

So in P05 v1 I lock the standard:

  * `session.start` is the lifecycle root (root span)

  * `session.end`’s parent **must point to the root span**

  * business chains (user → agent → tool → policy → memory) grow freely under the root




This cleanly orthogonalizes two structures:

  *  **Lifecycle Tree** : start/end defines the boundary of “life”

  *  **Business Chain** : action chain defines causal propagation




Anyone reading events can immediately tell: which is life structure, which is behavior structure.

* * *

## 5) The philosophy of P05 implementation: don’t “guess causality,” _write causality_

I deliberately made causality generation independent of the model, prompts, or “semantic reasoning”:

  * `span_id` is generated by runtime (uuid)

  * `parent_span_id` is determined by runtime rules

  * `actor` is labeled by runtime




Meaning: **causality is a legal fact of the system, not the model’s opinion.**

* * *

## 6) After P05, what did the system truly gain?

One sentence: you gain a governable agent system.

  * you can replay a span (P06)

  * you can limit certain actors (P07 / MCP)

  * you can introduce tool_calls as branch nodes (real complexity starts here)

  * you can make “memory writes” auditable causal events (otherwise a ten-year system will be polluted)




P04 gives you history.

P05 gives you the **structure** of history.

And once history has structure, it becomes the skeleton of the system, not just text records.

* * *

## Next: P06 / P07 becomes natural

P06 Replay Runner reads the tree and replays a session by nodes (you can even validate structure consistency without calling a model). P07 Policy Gate inserts adjudication nodes on `memory.write_*` spans—explicit allow/deny/human override causal chains.

But they only stand because P05 already achieved:

> causality can be structurally written, and can be reconstructed.

That is P05’s meaning.

* * *

# P05 More | Tool Calls & Branching: when the causal tree enters the “real battlefield” for the first time

The core of P05 is not adding a few IDs—it’s giving the system a capability for the first time: **write execution as a reconstructable causal structure**. In the initial P05, `span_id / parent_span_id / actor` upgrades a session from a timeline into a causal tree, answering “who caused what.” But the real battlefield begins here—when you add `tool.call / tool.result`, you introduce the first **branching**. An `agent.reply` is no longer just text output; it starts triggering external capabilities, creating side effects, introducing risk, and therefore requiring governance.

* * *

## 1) Why is tool branching a watershed for P05?

Because tools push the agent into a high-privilege world.

  * without tools, the agent only speaks

  * with tools, the agent starts changing the world: search, write files, send requests, modify data, move money…




Once tools are allowed, the problem is no longer “response quality,” but:

  *  **risk chain** : which tool call caused which consequence?

  *  **governance insertion point** : where should policy gates attach?

  *  **audit responsibility** : who triggered the high-privilege action?

  *  **replay & reproduction**: how do you prove the system actually took that step?




All of these share one prerequisite: **tool calls must be causally structured**.

* * *

You note your philosophy:

> Policy Gate comes later. My philosophy is that Events, Ledger, and Memory are layered in a strict progression. You cannot treat Events as Memory—if you do, the system will blow up.

* * *

## 2) P05 More: what standards did we lock?

We define tool calls as a subtree under the triggering `agent.reply`, and we lock the parent-child relations:

  * `tool.call`’s parent **must be** the `agent.reply` that triggered it

  * `tool.result`’s parent **must be** the corresponding `tool.call`




So a tool chain becomes a governable unit:

agent.reply → tool.call → tool.result

When a reply triggers multiple tools, the tree naturally branches into sibling subtrees.

This is the “real battlefield”: you stop guessing causality from timestamps—you write an explicit execution graph via parent pointers.

* * *

## 3) What does the structure look like in practice?

Using the same `render_trace_tree.py`, after introducing tool branching, it prints:

session.start

└ user.message

└ agent.reply

└ tool.call

└ tool.result

session.end

And it satisfies three hard indicators:

  *  **ROOTS = 1**

  *  **ORPHANS = 0**

  *  **tool.result is always under tool.call**




Not “looks like it,” but “machines can reliably reconstruct it.”
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗  rm -f runtime_data/events.jsonl
    python -m projects.p00-agent-os-mvp.src.main
    python scripts/render_trace_tree.py
    
    [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
    
    ========================================================================================
    SESSION: p00-efa4acca-6968-49e1-a941-9761cf687648
    TRACE:   77b306b1-0e0e-4c8b-98ea-9607acecd2b3
    EVENTS:  6  | ROOTS: 1  | ORPHANS: 0
    
    --- ROOT 1 ---
    session.start  actor=runtime  span=2c5f4095-d505-45bd-88ff-034c292c71cf  ts=2025-12-18T04:02:39.761Z
        ↳ Session started for p00 MVP
        payload={"message": "Session started for p00 MVP", "persona_user_id": "susan"}
       ├─ user.message  actor=user  span=229a141d-b8ec-4a47-89ac-6f173938bd43  parent=2c5f4095-d505-45bd-88ff-034c292c71cf  ts=2025-12-18T04:02:39.761Z
       │      ↳ Hello, this is the first OS-level MVP run.
       │      payload={"text": "Hello, this is the first OS-level MVP run."}
       │  └─ agent.reply  actor=agent  span=21125454-8ecd-4f29-ad1d-9a29fded0e7f  parent=229a141d-b8ec-4a47-89ac-6f173938bd43  ts=2025-12-18T04:02:39.761Z
       │         ↳ [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
       │         payload={"reply": "[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.", "tool_calls": [{"args": {"q": "AI news this week"}, "to…
       │     └─ tool.call  actor=tool  span=eea2350d-1595-4824-a835-48be34ef30c3  parent=21125454-8ecd-4f29-ad1d-9a29fded0e7f  ts=2025-12-18T04:02:39.762Z
       │            payload={"args": {"q": "AI news this week"}, "tool_name": "fake_search"}
       │        └─ tool.result  actor=tool  span=abfaee15-9f85-4227-9879-090c77842dee  parent=eea2350d-1595-4824-a835-48be34ef30c3  ts=2025-12-18T04:02:39.762Z
       │               payload={"result": {"data": "stub tool result", "ok": true}, "tool_name": "fake_search"}
       └─ session.end  actor=runtime  span=a170df23-f9ce-4054-aed4-ef56f53ddd73  parent=2c5f4095-d505-45bd-88ff-034c292c71cf  ts=2025-12-18T04:02:39.762Z
              ↳ Session ended for p00 MVP
              payload={"message": "Session ended for p00 MVP"}
    
    Done.
    
    

* * *

## 4) A key correction: lifecycle must not be hijacked by the business chain

After adding tool branching, you must lock a subtle standard:

`session.end` should point back to the lifecycle root (`session.start`), not to the last business action.

Because `session.end` is a life event. It closes the life boundary; it should not become the tail of the business chain. Otherwise, as the business chain grows deep and complex (and concurrent), session boundaries will be hijacked and replay/statistics become harder.

So the stable structure is:

  * lifecycle: start/end closes at the root

  * business: user → agent → tool → … grows under the root




Clean OS-level semantics.

* * *

## 5) Why does this structure directly determine future governance capability?

Because all higher-order capabilities need a concrete “mount point”:

  *  **Policy Gate (P07)** attaches before `tool.call` as `policy.check → allow/deny`

  *  **Replay (P06)** replays nodes by causal order (not “ask the model again”)

  *  **Observability & cost (P09)** can record latency/token/cost/error across tool boundaries

  *  **MCP / security architecture** : tool.call is the capability exposure point; tool.result is the side-effect evidence point—between them is the minimal safety loop




Once tool calls are structured as causal subtrees, they stop being “a tool call” and become **a governed capability execution unit**.

* * *

## 6) Ending: one sentence

P04 gave the system history.

P05 gave history causal structure.

And **P05 More (tool branching)** means:

> for the first time, the system wrote “action” into its auditable causal tree.
> 
> from here on, intelligence is no longer “sounds good,” but “acts correctly—and is accountable.”

* * *

# P06 | Replay Runner: when “reproducibility” becomes a fact for the first time

P04 gave deterministic history: stable envelopes, UTC timestamps, `payload_hash`. P05 gave causal structure: a reconstructable tree via `span_id / parent_span_id / actor`, and with `tool.call / tool.result` it entered the real battlefield—branching execution, emerging risk, and therefore governance footholds. P06 pushes it one level deeper: **make the system capable of replaying a run purely from**`events.jsonl`, without depending on the model, without depending on context windows, without depending on subjective narration—reproducibility becomes engineering reality, not a slogan.

* * *

## 1) What does P06 do? One sentence.

 **Replay Runner reads the event ledger, rebuilds the session’s causal execution graph, and automatically validates key invariants.**

It’s not “ask the model again.” It’s:

  * recover structure from the ledger

  * recover paths from structure

  * recover an auditable execution narrative from paths




You can think of it as:

 **a “decompiler” for the event ledger.**

* * *

## 2) Why is Replay so important in agent systems?

Because models are inherently unstable, but systems must be stable.

  * model outputs drift (temperature, versions, context)

  * tools create side effects

  * memory writes can pollute long-term world state




If you can’t replay a run, you can’t:

  * do regression tests

  * audit

  * attribute responsibility

  * enforce policy gates

  * migrate long-term systems




So P06 is OS-level engineering: it lets the system say:

> “I can prove what I did.”

* * *

## 3) A minimal replay_runner

You wrote `scripts/replay_runner.py`, which does something simple but hard:

  1. read `runtime_data/events.jsonl`

  2. group by `session_id`

  3. rebuild the causal tree from `_span_id/_parent_span_id`

  4. traverse the tree and print replay output

  5. validate red lines:

    * `payload_hash` matches payload

    * `tool.result` is under `tool.call`

    * `session.end` points to the lifecycle root

    * detect orphan / cycle




* * *

## 4) What does replay output look like?

You run replay on a session and get a structured transcript that is ledger-reconstructed—not model-summarized.

In other words: **history itself is speaking**.
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ python scripts/replay_runner.py --session p00-efa4acca-6968-49e1-a941-9761cf687648
    
    ========================================================================================
    REPLAY SESSION: p00-efa4acca-6968-49e1-a941-9761cf687648
    TRACE_IDS: ['77b306b1-0e0e-4c8b-98ea-9607acecd2b3']
    EVENTS: 6
    
    REPLAY OUTPUT:
    - session.start actor=runtime ts=2025-12-18T04:02:39.761Z
      - user.message actor=user ts=2025-12-18T04:02:39.761Z
          user: Hello, this is the first OS-level MVP run.
        - agent.reply actor=agent ts=2025-12-18T04:02:39.761Z
            agent: [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
            tool_calls: 1
          - tool.call actor=tool ts=2025-12-18T04:02:39.762Z
              tool.call: fake_search args={'q': 'AI news this week'}
            - tool.result actor=tool ts=2025-12-18T04:02:39.762Z
                tool.result: fake_search result={'data': 'stub tool result', 'ok': True}
      - session.end actor=runtime ts=2025-12-18T04:02:39.762Z
    
    Done.
    
    

* * *

## 5) The core value: integrity checks

You did something sneaky: manually tamper with a `user.message` payload to “HACKED” without changing `payload_hash`, and replay immediately flags a mismatch.

That matters because it proves:

  * the ledger is not a “trusted file,” it’s a _verifiable_ file

  * post-hoc tampering is detectable (at least at the payload level)

  * replay has credibility, not just “seems plausible”




In default mode it can keep replaying (useful for debugging); in `--strict` mode it becomes a CI-grade hard gate.

* * *

## 6) Where does P06 take the system?

You now have a critical closed loop:

  * P04: history is deterministic

  * P05: history is causal

  * P06: history is replayable and verifiable




Meaning the system moves from “it happens” to “it can prove.”

And “can prove” is the prerequisite for governance, risk control, and sovereignty layers (Policy / MCP / Sovereignty).

* * *

## 7) Next: stronger anti-tamper (optional upgrade)

Your tamper experiment also reveals a deeper truth:

> if an attacker tampers with payload and recomputes payload_hash, replay still “passes.”

So the natural upgrade is:

  * `envelope_hash` for the entire envelope

  * `prev_envelope_hash` to create a hash chain within a session

  * signatures for non-repudiation




That pushes tamper detection into real security & sovereignty engineering.

> This must be added when safety requirements rise. Infrastructure isn’t always one-and-done. But for now, we’ll stop here.

Now you see why I said you need to hash it.
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ python scripts/replay_runner.py --session p00-efa4acca-6968-49e1-a941-9761cf687648
    
    ========================================================================================
    REPLAY SESSION: p00-efa4acca-6968-49e1-a941-9761cf687648
    TRACE_IDS: ['77b306b1-0e0e-4c8b-98ea-9607acecd2b3']
    EVENTS: 6
    
    WARNINGS:
     - [WARN] payload_hash mismatch: expected=1671f8263d2185809fc1ec9e34096bb7fee8c34aadfa06dfe017d41b25d4043b calc=a2f071924d5454d72f61d947cce28d579f285e711051b3a29732bd0c431a8cd6 event_type=user.message
    
    REPLAY OUTPUT:
    - session.start actor=runtime ts=2025-12-18T04:02:39.761Z
      - user.message actor=user ts=2025-12-18T04:02:39.761Z
          user: HACKED
        - agent.reply actor=agent ts=2025-12-18T04:02:39.761Z
            agent: [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
            tool_calls: 1
          - tool.call actor=tool ts=2025-12-18T04:02:39.762Z
              tool.call: fake_search args={'q': 'AI news this week'}
            - tool.result actor=tool ts=2025-12-18T04:02:39.762Z
                tool.result: fake_search result={'data': 'stub tool result', 'ok': True}
      - session.end actor=runtime ts=2025-12-18T04:02:39.762Z
    
    Done.
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ 
    

* * *

## One-sentence summary

P06’s value is not “printing a tree.” It’s:

> the system’s first ability to reproduce itself purely from its own history.

From here, an agent stops being a disposable chat phenomenon and becomes a long-lived runtime organism that can be verified, governed, and evolved.

* * *

## Pre-P07 world statement + link

> Before P07, it’s an agent world where capability comes first, structure is ungovened, and good faith is assumed by default.

Concretely:

  * agents **can do a lot**

  * memory **can be written**

  * events **can be recorded**

  * personas **can evolve**

  * but:

    * no “who allowed you to do this”

    * no “what must never enter world memory”

    * no “is this overreach / irreversible”




It’s a phase that is **technically feasible, but civilizationally dangerous**.

Next, we introduce the gate.

Pre-policy world link:

<https://github.com/STEMMOM/adk-decade-of-agents/tree/P06-pre-policy-gate>

* * *

有一些基础预设，我想先说清楚。

这个 repo 叫 **Decade of Agents** 。

在不向你完整展开我正在构建的长期系统之前，其实我只想传达两件事：

 **第一，** 在接下来的十年里，我所看好的工作重心，几乎都会围绕「智能体（agents）」展开。

 **第二，** 不论应用层如何变化——无论是我过去两年里反复构思、推演、又放弃的那些具体项目——最终都会收敛到同一个问题： **智能体的基础设施** 。应用可以变，场景可以换，但底座的原理是稳定的。

 **Lessons and Prompts** ，只是我用来展示“这个底座是如何被搭出来”的地方。

我的系统观会随着这个系列逐步展开，但我并不建议把它当成一套教程。“Lessons”这个名字本身并不完美，只是因为我暂时想不到一个更合适的称呼。

如果你下过中国围棋，可以把这个系列里面的每一个“P”，理解为我落下的一枚「一子」。

我选择的是： **一边对弈，一边讲棋** ，而不是先埋头把所有定式摆完，再回头解释。

要是以前，我才不会讲任何事情，自己一个人埋头苦干。

现在我需要约束，需要在真实的开发过程中，与真正能理解我技术哲学的人同步沟通。尤其是我发现我一个人，有可能扛起如此巨大的一个系统的时候。这种体量的工程，以前个人开发者根本不敢想。

这也是这个 repo、以及后面一系列智能体基建，看上去都很无聊的内容存在的真正原因。我越到后面，越是难把这些内容写得像个“课”，因为系统越来越复杂，我的认知负担越来越重。相反那些为了流量在卖课的，会将“你能实现”摆在最前面。但是我认为这个对于前沿探索者来说，是意义不大的。至少我做不到了，所以所谓的lessons，会变得非常跳跃和点到为止。主要是因为我实在没有办法一个人，在重度开发的前提下，还能把步骤一步一步的完美展示。再次感叹一下free code camp的伟大。

 **基建 = 那些一旦立住，未来十年你几乎不敢随便改的东西。**

它们不是“好不好用”的问题，而是：

> 一旦口径漂移，系统就会慢性死亡的部分。

* * *

## 在 AI-Native / Agent OS 里的“基建”到底是什么？

不是服务器

不是云资源

不是模型

我认为是 **四类不可逆约束** 。

* * *

## 一、时间基建（Time Infrastructure）

 **系统如何感知时间、记录发生顺序、回放历史？**

在你这里就是：

  * `events.jsonl`

  * `session.start / session.end`

  * `trace_id`

  * 因果顺序




👉 **时间一旦混乱，系统就不再可审计，也不可治理。**

日志可以乱，

 **事件不可以。**

* * *

## 二、身份基建（Identity Infrastructure）

 **“谁”在说话、谁在行动？**

在你这里是：

  * `persona.json`

  * session 绑定 persona

  * 每次调用都锚定同一个“你”




👉 没有身份锚，memory 就没有主体，

历史也就没有意义。

* * *

## 三、世界状态基建（World-State Infrastructure）

 **系统“记住的世界”长什么样？**

在你这里是：

  * `memory_store.json`

  * schema + version

  * migration




👉 没有稳定世界状态，

系统每次升级都等于失忆。

## 四、权力与约束基建（Authority Infrastructure）

 **谁允许什么发生？谁能否决？**

在你这里逐渐形成的是：

  * Policy Gate

  * MCP

  * deny-by-default

  * 写入门禁




👉 没有约束的智能，叫风险源，不叫系统。

* * *

* * *

代码本身并不重要。

我默认读到这里的人，都已经拥有强大的 AI 辅助编程能力。

我并不是站在“不会写代码”的位置说这句话。相反，我曾经是 **freeCodeCamp** 的重度学习者，对那套路径非常熟悉。但我已经有一年没有再关注它了——不是因为代码不重要，而是因为 **重要性发生了迁移** 。

你真正需要看清的，不是某一段具体实现，而是这条 **路径本身** ，以及它背后的 **系统哲学** 。

一旦这一点成立，代码就不再是瓶颈。

具体的实现方式，应该结合你自己的项目，在 AI 的辅助下自然展开。你完全可以用不同语言、不同框架、不同风格去落地同一套结构原理。

因此，不必纠结某个函数怎么写、某个类是否优雅，那些都属于可替换、可演化的层。

如果你理解了这里的方向和约束，

代码，只是随之生长出来的枝叶。

* * *

# P04｜Deterministic Envelope：当系统第一次拥有“不可漂移的历史”

我一直在做一件看起来很“无聊”的事：让一个最小的 AI 系统在终端里跑起来、写一点文件、打印一句话。

但 P04 是一个分水岭——因为从这一刻起，这个系统第一次拥有了 **不可漂移的历史** 。

不是 log。

不是“今天我觉得发生了什么”。

而是 **机器能稳定解析、未来十年还能读懂的事件轨迹** 。

* * *

## 1) 为什么要做 P04？Chat 窗口不够吗？

Chat 窗口的问题不是“回答不稳定”，而是：它没有历史法则。

  * 你很难复现一次对话的真实过程

  * 你很难追问“到底发生了什么”

  * 你更无法保证系统升级后，旧历史仍然可用




你以为你在做 agent，实际上你只是把模型当成一个临时对话机。

而我做的是 OS：它必须知道——

> 什么才算真的发生过。

在这个 OS 里：

 **没进入事件账本的事，从系统角度等于没发生。（这句话很重要）**

* * *

## 2) P04 做了什么？一句话

把 `runtime_data/events.jsonl` 的每一条事件统一成固定信封（Envelope）：

> schema_version / event_type / session_id / trace_id / ts / payload / payload_hash

并锁死口径：

  * `ts` 统一 UTC（避免时区漂移）

  * `payload_hash` 由系统计算：`sha256(canonical_json(payload))`

  * 所有事件必须走单一写入口（避免分裂成多套格式）




这听起来像工程细节，但它实际上是 **OS 宪法** 。

* * *

## 3) “Deterministic”到底是什么意思？

它的意思是：

> 同样的 payload，无论 key 顺序如何变化，都必须产生同样的 hash。

这件事非常关键，因为未来你会：

  * 回放（Replay）

  * 做回归测试（Regression）

  * 审计（Audit）

  * 做策略门禁（Policy Gate）

  * 做迁移（Migration）




而这些都依赖一个事实：

> 事件必须是可验证的结构事实，而不是叙事文本。

这个看上去很浪费功夫，但是你要设想你这个应用，有可能是绝对不能让人改的东西。比如一些机构，一些涉及到钱，授权，等很敏感的领域。有总比没有好。基建是什么？基建是想办法设想未来，而且尽可能的排掉未来所有的雷，而不是去给未来埋无数雷。我只会嫌这个还不够。

* * *

## 4) 实际输出长什么样？

这是我跑完一次 OS-level MVP 后，`tail -n 4 runtime_data/events.jsonl` 的结果（每行一条 JSON）：
    
    
    {"event_type":"session.start","payload":{"_source":"p00-agent-os-mvp","message":"Session started for p00 MVP","persona_user_id":"susan"},"payload_hash":"...","schema_version":"1.0","session_id":"p00-4c31...","trace_id":"633d...","ts":"2025-12-18T01:55:18.998Z"}
    {"event_type":"user.message","payload":{"_source":"p00-agent-os-mvp","text":"Hello, this is the first OS-level MVP run."},"payload_hash":"...","schema_version":"1.0","session_id":"p00-4c31...","trace_id":"633d...","ts":"2025-12-18T01:55:18.999Z"}
    {"event_type":"agent.reply","payload":{"_source":"p00-agent-os-mvp","reply":"[MVP Kernel Stub] You said: ...","tool_calls":[]},"payload_hash":"...","schema_version":"1.0","session_id":"p00-4c31...","trace_id":"633d...","ts":"2025-12-18T01:55:18.999Z"}
    {"event_type":"session.end","payload":{"_source":"p00-agent-os-mvp","message":"Session ended for p00 MVP"},"payload_hash":"...","schema_version":"1.0","session_id":"p00-4c31...","trace_id":"633d...","ts":"2025-12-18T01:55:18.999Z"}
    
    

注意几个点：

  * `session_id` 每次运行唯一 → 不会把多次运行混成一条生命

  * `trace_id` 把因果链绑定在一起 → 为 P05 做准备

  * `payload_hash` 可重算 → 为审计/回归做准备

  * `_source` 收敛在 payload 里 → 顶层协议保持最小稳定




这不是“日志”，而是 **系统行为的结构指纹** 。

这里要讲一下，因果很重要，你使用大语言模型那么久了，已经知道他的行为模式。在智能体时代，因果怎么会不重要。

* * *

## 5) P04 的真正价值：它是后续所有项目的地基

没有统一事件信封，后面所有东西都会漂移：

  * P05 Trace & Causality：你无法稳定追踪“谁导致了谁”

  * P06 Replay Runner：你无法可靠回放历史

  * P07 Policy Gate：你无法审计“为什么这条记忆被写入”

  * P08 Migration：你无法跨版本迁移而不断代

  * P09 Observability：指标无法对账

  * P10 System Process：不同进程写出不同格式，系统立刻分裂




所以我才说：P04 看起来小，但它是不可逆的。

* * *

## 6) 这一课的结尾：一句 OS 级结论

很多人把 agent 当成“模型+工具”。

我把 agent 当成“生命过程”。

而生命过程必须留下历史。

历史必须可验证。

可验证必须先有信封。

 **P04 就是这个系统第一次拥有“不可漂移的历史”。**

下一篇我会做 P05：给 trace 定义真正的传播与分叉规则，让系统从“时间线”进入“因果树”。

* * *

P04的主要实现，就是在runtime 加入：

[events.py](http://events.py/)
    
    
    from __future__ import annotations
    
    import json
    import hashlib
    from dataclasses import dataclass
    from datetime import datetime, timezone
    from pathlib import Path
    from typing import Any, Dict, Optional
    
    SCHEMA_VERSION = "1.0"
    
    def utc_ts_iso() -> str:
        # UTC, RFC3339-ish with milliseconds, always ends with Z
        dt = datetime.now(timezone.utc)
        return dt.isoformat(timespec="milliseconds").replace("+00:00", "Z")
    
    def canonical_json(obj: Any) -> str:
        """
        Deterministic JSON string:
        - sort keys
        - no whitespace
        - ensure_ascii=False (stable for unicode)
        """
        return json.dumps(obj, sort_keys=True, separators=(",", ":"), ensure_ascii=False)
    
    def sha256_hex(s: str) -> str:
        return hashlib.sha256(s.encode("utf-8")).hexdigest()
    
    @dataclass(frozen=True)
    class EventEnvelopeV1:
        schema_version: str
        event_type: str
        session_id: str
        trace_id: str
        ts: str
        payload: Dict[str, Any]
        payload_hash: str
    
        def to_dict(self) -> Dict[str, Any]:
            return {
                "schema_version": self.schema_version,
                "event_type": self.event_type,
                "session_id": self.session_id,
                "trace_id": self.trace_id,
                "ts": self.ts,
                "payload": self.payload,
                "payload_hash": self.payload_hash,
            }
    
    class EventWriter:
        """
        Single write入口：所有事件都从这里 append 到 events.jsonl
        """
        def __init__(self, events_file: Path):
            self.events_file = events_file
            self.events_file.parent.mkdir(parents=True, exist_ok=True)
    
        def emit(
            self,
            *,
            event_type: str,
            session_id: str,
            trace_id: str,
            payload: Optional[Dict[str, Any]] = None,
            ts: Optional[str] = None,
        ) -> EventEnvelopeV1:
            payload = payload or {}
            ts = ts or utc_ts_iso()
    
            payload_canon = canonical_json(payload)
            payload_hash = sha256_hex(payload_canon)
    
            env = EventEnvelopeV1(
                schema_version=SCHEMA_VERSION,
                event_type=event_type,
                session_id=session_id,
                trace_id=trace_id,
                ts=ts,
                payload=payload,
                payload_hash=payload_hash,
            )
    
            line = canonical_json(env.to_dict())
            with self.events_file.open("a", encoding="utf-8") as f:
                f.write(line + "\\n")
    
            return env
    
    

# P05｜Trace & Causality：当系统第一次知道“是谁导致了谁”

P04 我们把 `events.jsonl` 变成了确定性的历史：每一条事件都有稳定的信封（schema_version、ts、payload_hash），系统第一次拥有了“不可漂移的时间线”。但时间线只回答一个问题： **发生了什么、按什么顺序发生** 。P05 要把系统从“会记录”推进到“会归因”：不仅知道发生了什么，还要知道 **是谁导致了谁** ，以及一条行为链是如何在系统里生长出来的。换句话说，P05 让系统从日志/流水账进化为 **因果结构** ——这一步是后续 Replay（P06）、Policy Gate（P07）、治理与风控（MCP 系列）的共同地基。

* * *

## 1) P05 在做什么？一句话

给每一个会影响后续结果的动作分配一个“ **因果** 节点”（因果因果因果！！！），并用父指针把节点连成树。

在工程上，这被压缩成两个字段：

  * `span_id`：我是谁（一个因果节点的 ID）

  * `parent_span_id`：我从哪里来（指向父节点）




我们先把它们放进 `payload`（不破坏 P04 顶层协议）：

  * `payload._span_id`

  * `payload._parent_span_id`




并补一个治理必需字段：

  * `payload._actor`：是谁触发了这个事件（runtime/user/agent/tool/policy）




从此以后，“因果链”不是推断出来的，而是 **系统显式写出来的** 。

* * *

## 2) 为什么这一步是 OS 级分水岭？

因为没有因果，你的系统永远只能“发生”，不能“治理”。

  *  **错误无法归因** ：你只能看到 error 出现，不知道它挂在哪条链上

  *  **工具风险无法定位** ：tool_call 只是时间上靠近，不等于因果相关

  *  **策略门禁无从下手** ：policy 想拦截什么？拦截的是“动作节点”，不是模糊语义

  *  **回放无法成立** ：Replay 不是“再问一遍模型”，而是按因果树重放结构路径




P05 的目标非常明确：让系统拥有一种能力—— **用结构回答“为什么”** 。这个问题非常重要，我想不到有任何智能体系统，不需要做这个。

* * *

## 3) 我们最终跑出来的因果树长什么样？

我写了一个调试脚本 `scripts/render_trace_tree.py`，它会读取 `runtime_data/events.jsonl`，按 `_span_id/_parent_span_id` 还原因果树。跑完一次最小 MVP 之后，它打印出这棵树：
    
    
    session.start (root)
    ├─ user.message
    │   └─ agent.reply
    └─ session.end
    
    

并且它显示：

  * ROOTS: 1（只有一个根）

  * ORPHANS: 0（没有孤儿节点）




这两个数字非常重要：它意味着系统的因果结构是 **可重建的** ，而不是“看起来像”。

* * *

## 4) 一个关键口径：生命周期 vs 业务链（P05 v1 的核心）

在实现过程中有一个非常容易犯的错：把 `session.end` 挂在“最后一个业务动作”后面（比如挂在 `agent.reply`）。这在 v0 看起来也能工作，但从 OS 语义上是隐患：生命周期会被业务链挟持，未来加入 tool_call、policy、memory 写入之后，你会发现 session 的边界越来越难定义。

所以 P05 v1 我把口径钉死为：

  * `session.start` 是生命周期根节点（root span）

  * `session.end` 的 parent **必须指向 root span**

  * 业务链（user → agent → tool → policy → memory）挂在 root 下面自由生长




这让系统清晰地分成两条正交结构：

  *  **Lifecycle Tree** ：start/end 管生命边界

  *  **Business Chain** ：动作链管因果传播




读事件的人一眼就知道：哪个是生命结构，哪个是行为结构。

* * *

## 5) P05 的实现哲学：不是“猜因果”，而是“写因果”

这里我刻意做了一件事：因果结构的生成不依赖模型，不依赖 prompt，不依赖“语义推理”。

  * `span_id` 由 runtime 生成（uuid）

  * `parent_span_id` 由 runtime 规则确定

  * `actor` 由 runtime 标注




这意味着： **因果是系统的法律事实，不是模型的意见。**

* * *

## 6) P05 完成后，系统真正获得了什么？

一句话：你获得了一个可以被治理的 agent 系统。

  * 你可以对某个 span 做回放（P06）

  * 你可以对某类 actor 做限制（P07 / MCP）

  * 你可以把 tool_call 作为一个分叉节点引入（真正的复杂性从这里开始）

  * 你可以把“记忆写入”变成可审计的因果事件（否则十年系统必被污染）




P04 给了你“历史”。

P05 给了你“历史的结构”。

而历史一旦有结构，它就开始变成系统的骨架，而不再是文本记录。

* * *

## 下一步：P06 / P07 会变得非常自然

P06 Replay Runner 的本质，就是读取这棵树，按节点顺序重放一个 session（甚至不需要调用模型就能验证结构一致性）。P07 Policy Gate 的本质，就是在 `memory.write_*` 这种 span 上插入裁决节点，明确写入允许/禁止/人工 override 的因果链。

但它们能成立的前提，就是你已经在 P05 做到了：

> 因果可以被结构化写入，并且能被还原。

这就是 P05 的意义。

在runtime 加入：
    
    
    # adk_runtime/trace_context.py
    import uuid
    
    class TraceContext:
        def __init__(self, trace_id: str | None = None):
            self.trace_id = trace_id or str(uuid.uuid4())
            self._stack = []
    
        def new_span(self) -> str:
            span_id = str(uuid.uuid4())
            parent = self._stack[-1] if self._stack else None
            self._stack.append(span_id)
            return span_id, parent
    
        def end_span(self):
            if self._stack:
                self._stack.pop()
    
    

render_trace_tree.py
    
    
    #!/usr/bin/env python3
    from __future__ import annotations
    
    import argparse
    import json
    from dataclasses import dataclass
    from pathlib import Path
    from typing import Any, Dict, List, Optional, Tuple, Set
    
    @dataclass
    class Node:
        span_id: str
        parent_span_id: Optional[str]
        event_type: str
        actor: str
        ts: str
        session_id: str
        trace_id: str
        payload: Dict[str, Any]
    
    def _shorten(s: str, n: int = 80) -> str:
        s = s.replace("\\n", " ").strip()
        return s if len(s) <= n else s[: n - 1] + "…"
    
    def _read_jsonl(path: Path) -> List[Dict[str, Any]]:
        rows: List[Dict[str, Any]] = []
        with path.open("r", encoding="utf-8") as f:
            for i, line in enumerate(f, start=1):
                line = line.strip()
                if not line:
                    continue
                try:
                    rows.append(json.loads(line))
                except json.JSONDecodeError as e:
                    raise SystemExit(f"[ERROR] Invalid JSON on line {i}: {e}") from e
        return rows
    
    def _extract_node(row: Dict[str, Any]) -> Optional[Node]:
        """
        Expects P04 envelope with P05 fields stored in payload:
          payload._span_id
          payload._parent_span_id
          payload._actor
        Returns None for rows that don't have a span_id.
        """
        payload = row.get("payload") or {}
        span_id = payload.get("_span_id")
        if not span_id:
            return None
    
        return Node(
            span_id=str(span_id),
            parent_span_id=(str(payload.get("_parent_span_id")) if payload.get("_parent_span_id") else None),
            event_type=str(row.get("event_type", "")),
            actor=str(payload.get("_actor", "unknown")),
            ts=str(row.get("ts", "")),
            session_id=str(row.get("session_id", "")),
            trace_id=str(row.get("trace_id", "")),
            payload=payload,
        )
    
    def _group_key(n: Node) -> Tuple[str, str]:
        return (n.session_id, n.trace_id)
    
    def _build_tree(nodes: List[Node]) -> Tuple[Dict[str, Node], Dict[str, List[str]], List[str], List[str]]:
        """
        Returns:
          - id2node
          - children_map: parent_span_id -> [child_span_id...]
          - roots: span_ids whose parent is None or missing
          - orphans: span_ids whose parent_span_id references a missing node
        """
        id2node: Dict[str, Node] = {n.span_id: n for n in nodes}
    
        children: Dict[str, List[str]] = {}
        orphans: List[str] = []
        roots: List[str] = []
    
        for n in nodes:
            pid = n.parent_span_id
            if pid is None:
                roots.append(n.span_id)
                continue
            if pid not in id2node:
                orphans.append(n.span_id)
                roots.append(n.span_id)  # treat orphan as root for display
                continue
            children.setdefault(pid, []).append(n.span_id)
    
        # stable ordering: by timestamp then event_type
        for pid, kids in children.items():
            kids.sort(key=lambda sid: (id2node[sid].ts, id2node[sid].event_type))
    
        roots.sort(key=lambda sid: (id2node[sid].ts, id2node[sid].event_type))
        return id2node, children, roots, orphans
    
    def _fmt_node(n: Node, show_payload: bool = True) -> str:
        # pick a human-friendly summary from payload
        summary = ""
        if n.event_type == "user.message":
            summary = _shorten(str(n.payload.get("text", "")))
        elif n.event_type == "agent.reply":
            summary = _shorten(str(n.payload.get("reply", "")))
        elif "message" in n.payload:
            summary = _shorten(str(n.payload.get("message", "")))
    
        base = f"{n.event_type}  actor={n.actor}  span={n.span_id}"
        if n.parent_span_id:
            base += f"  parent={n.parent_span_id}"
        if n.ts:
            base += f"  ts={n.ts}"
        if summary:
            base += f"\\n    ↳ {summary}"
    
        if show_payload:
            # show a trimmed payload without noisy keys
            p = dict(n.payload)
            p.pop("_source", None)
            p.pop("_actor", None)
            p.pop("_span_id", None)
            p.pop("_parent_span_id", None)
            if p:
                base += f"\\n    payload={_shorten(json.dumps(p, ensure_ascii=False), 140)}"
        return base
    
    def _detect_cycle(id2node: Dict[str, Node], children: Dict[str, List[str]], roots: List[str]) -> bool:
        visited: Set[str] = set()
        stack: Set[str] = set()
    
        def dfs(sid: str) -> bool:
            if sid in stack:
                return True
            if sid in visited:
                return False
            visited.add(sid)
            stack.add(sid)
            for c in children.get(sid, []):
                if dfs(c):
                    return True
            stack.remove(sid)
            return False
    
        for r in roots:
            if dfs(r):
                return True
        return False
    
    def _print_tree(id2node: Dict[str, Node], children: Dict[str, List[str]], root: str, indent: str = "", last: bool = True,
                    show_payload: bool = True, max_depth: Optional[int] = None, _depth: int = 0) -> None:
        prefix = "└─ " if last else "├─ "
        if indent == "":
            # root line
            print(_fmt_node(id2node[root], show_payload=show_payload))
        else:
            print(indent + prefix + _fmt_node(id2node[root], show_payload=show_payload).replace("\\n", "\\n" + indent + ("   " if last else "│  ")))
    
        if max_depth is not None and _depth >= max_depth:
            if children.get(root):
                print(indent + ("   " if last else "│  ") + "└─ … (max depth reached)")
            return
    
        kids = children.get(root, [])
        for i, c in enumerate(kids):
            is_last = i == len(kids) - 1
            next_indent = indent + ("   " if last else "│  ")
            _print_tree(id2node, children, c, indent=next_indent, last=is_last, show_payload=show_payload, max_depth=max_depth, _depth=_depth + 1)
    
    def main() -> None:
        ap = argparse.ArgumentParser(description="Render causal trace tree from runtime_data/events.jsonl")
        ap.add_argument("--file", default="runtime_data/events.jsonl", help="Path to events.jsonl")
        ap.add_argument("--session", default=None, help="Filter by session_id (exact match)")
        ap.add_argument("--trace", default=None, help="Filter by trace_id (exact match)")
        ap.add_argument("--no-payload", action="store_true", help="Hide payload details")
        ap.add_argument("--max-depth", type=int, default=None, help="Max depth to render")
        args = ap.parse_args()
    
        path = Path(args.file)
        if not path.exists():
            raise SystemExit(f"[ERROR] File not found: {path}")
    
        rows = _read_jsonl(path)
        nodes_all: List[Node] = []
        for r in rows:
            n = _extract_node(r)
            if n:
                nodes_all.append(n)
    
        if not nodes_all:
            raise SystemExit("[ERROR] No span-based events found. (Missing payload._span_id?)")
    
        # group by (session_id, trace_id)
        groups: Dict[Tuple[str, str], List[Node]] = {}
        for n in nodes_all:
            if args.session and n.session_id != args.session:
                continue
            if args.trace and n.trace_id != args.trace:
                continue
            groups.setdefault(_group_key(n), []).append(n)
    
        if not groups:
            raise SystemExit("[ERROR] No events match the given filters.")
    
        for (session_id, trace_id), nodes in sorted(groups.items(), key=lambda kv: (kv[0][0], kv[0][1])):
            nodes.sort(key=lambda x: (x.ts, x.event_type))
            id2node, children, roots, orphans = _build_tree(nodes)
    
            print("\\n" + "=" * 88)
            print(f"SESSION: {session_id}")
            print(f"TRACE:   {trace_id}")
            print(f"EVENTS:  {len(nodes)}  | ROOTS: {len(roots)}  | ORPHANS: {len(orphans)}")
            if orphans:
                print("WARN: orphan spans (parent missing):")
                for sid in orphans:
                    print(f"  - {sid} (parent={id2node[sid].parent_span_id})")
    
            if _detect_cycle(id2node, children, roots):
                print("ERROR: cycle detected in span graph (this should never happen).")
                # still print what we can
    
            for i, r in enumerate(roots):
                print("\\n--- ROOT", i + 1, "---")
                _print_tree(
                    id2node,
                    children,
                    r,
                    indent="",
                    last=True,
                    show_payload=not args.no_payload,
                    max_depth=args.max_depth,
                )
    
        print("\\nDone.")
    
    if __name__ == "__main__":
        main()
    
    

events.jsonl 长这样：
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ rm -f runtime_data/events.jsonl
    python -m projects.p00-agent-os-mvp.src.main
    tail -n 4 runtime_data/events.jsonl
    
    [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
    {"event_type":"session.start","payload":{"_actor":"runtime","_source":"p00-agent-os-mvp","_span_id":"faea18e8-c7de-458e-8028-d35bcce017a4","message":"Session started for p00 MVP","persona_user_id":"susan"},"payload_hash":"87387fbbb44b9f9df3e55d550fd099eb6678902dc45abdbc313e36db384ab432","schema_version":"1.0","session_id":"p00-9832c7c9-3c8b-4f6c-8959-9fac37dd6d21","trace_id":"1243cc3e-43f8-4453-b0ba-7bdb00cde028","ts":"2025-12-18T02:28:10.544Z"}
    {"event_type":"user.message","payload":{"_actor":"user","_parent_span_id":"faea18e8-c7de-458e-8028-d35bcce017a4","_source":"p00-agent-os-mvp","_span_id":"4e9dd8cd-6ba3-4d91-b68c-94c3fd2f4026","text":"Hello, this is the first OS-level MVP run."},"payload_hash":"6bb29564c19bf0d4e5892e6e17caf1e550b3371137f6b0fc8619d00adc5f49c8","schema_version":"1.0","session_id":"p00-9832c7c9-3c8b-4f6c-8959-9fac37dd6d21","trace_id":"1243cc3e-43f8-4453-b0ba-7bdb00cde028","ts":"2025-12-18T02:28:10.545Z"}
    {"event_type":"agent.reply","payload":{"_actor":"agent","_parent_span_id":"4e9dd8cd-6ba3-4d91-b68c-94c3fd2f4026","_source":"p00-agent-os-mvp","_span_id":"d0e5d961-9edf-47da-a99e-810ac858c909","reply":"[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.","tool_calls":[]},"payload_hash":"4500eb08a8fc54be8d10e927e08be4489ebd57af7fced09e024153fcc93954f2","schema_version":"1.0","session_id":"p00-9832c7c9-3c8b-4f6c-8959-9fac37dd6d21","trace_id":"1243cc3e-43f8-4453-b0ba-7bdb00cde028","ts":"2025-12-18T02:28:10.545Z"}
    {"event_type":"session.end","payload":{"_actor":"runtime","_parent_span_id":"d0e5d961-9edf-47da-a99e-810ac858c909","_source":"p00-agent-os-mvp","_span_id":"8baa9be9-0903-4663-b44c-6845ce007d24","message":"Session ended for p00 MVP"},"payload_hash":"695bdc0883dbc4ddd9543cdc98c6c604fcf4c909e5ce7b1b6de8d1379458716d","schema_version":"1.0","session_id":"p00-9832c7c9-3c8b-4f6c-8959-9fac37dd6d21","trace_id":"1243cc3e-43f8-4453-b0ba-7bdb00cde028","ts":"2025-12-18T02:28:10.545Z"}
    

你写个trace tree, 可以更容易看，让他长这样：

再次重申，代码不重要，出来的东西长这样就行。
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ python scripts/render_trace_tree.py
    
    ========================================================================================
    SESSION: p00-7f28677d-aae4-4a00-91cd-273a68d5b0a1
    TRACE:   2cf60704-99e5-497a-9eda-ddfe8ef420d5
    EVENTS:  4  | ROOTS: 1  | ORPHANS: 0
    
    --- ROOT 1 ---
    session.start  actor=runtime  span=fd41dfd3-124c-4c2f-94c7-6cc5eb196557  ts=2025-12-18T02:41:11.417Z
        ↳ Session started for p00 MVP
        payload={"message": "Session started for p00 MVP", "persona_user_id": "susan"}
       ├─ user.message  actor=user  span=733a11c0-25a8-4de3-a1cc-ba3e70fb216c  parent=fd41dfd3-124c-4c2f-94c7-6cc5eb196557  ts=2025-12-18T02:41:11.417Z
       │      ↳ Hello, this is the first OS-level MVP run.
       │      payload={"text": "Hello, this is the first OS-level MVP run."}
       │  └─ agent.reply  actor=agent  span=3d20e599-7312-466e-9cca-c3b65f807f07  parent=733a11c0-25a8-4de3-a1cc-ba3e70fb216c  ts=2025-12-18T02:41:11.417Z
       │         ↳ [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
       │         payload={"reply": "[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.", "tool_calls": []}
       └─ session.end  actor=runtime  span=70736632-74bb-4982-b153-e0cbea19972b  parent=fd41dfd3-124c-4c2f-94c7-6cc5eb196557  ts=2025-12-18T02:41:11.418Z
              ↳ Session ended for p00 MVP
              payload={"message": "Session ended for p00 MVP"}
    
    Done.
    
    

# P05 More｜Tool Calls & Branching：因果树第一次进入“真正战场”

P05 的核心不是给事件加几个 ID，而是让系统第一次具备一种能力： **把执行过程写成可还原的因果结构** 。在最初的 P05 里，我们用 `span_id / parent_span_id / actor` 把一次 session 从时间线升级为因果树，解决了“是谁导致了谁”。但真正的战场从这里才开始——当你加入 `tool.call / tool.result`，系统第一次出现 **分叉** ：一条 `agent.reply` 不再只是输出文本，它开始触发外部能力、产生副作用、引入风险，也因此第一次需要治理。

* * *

## 1) 为什么 Tool 分叉是 P05 的分水岭？

因为 tool 让 agent 进入“高权限世界”。

  * 没有 tool，agent 只是说话

  * 有了 tool，agent 开始改变世界：搜索、写文件、发请求、改数据、动资金……




一旦允许 tool，你面对的就不再是“对话质量”，而是：

  *  **风险链条** ：哪个 tool call 导致了什么后果？

  *  **治理插口** ：policy gate 应该插在哪？

  *  **审计责任** ：谁触发了高权限动作？

  *  **回放与复现** ：怎么证明系统当时确实做了这一步？




这些问题只有一个共同前提： **工具调用必须被因果结构化** 。

* * *

> Policy gate的事情我们后面再说。我的哲学是Events, Ledger, Memory， 是一个层层递进的关系。你不能把Events当成memory, 这样系统肯定爆。

## 2) P05 More：我们钉死了什么口径？

我们把工具调用定义为 `agent.reply` 的子树，并且钉死了父子关系：

  * `tool.call` 的 parent **必须是** 触发它的 `agent.reply`

  * `tool.result` 的 parent **必须是** 对应的 `tool.call`




这让工具链变成一个可治理的单元：
    
    
    agent.reply
    └─ tool.call
       └─ tool.result
    
    

更重要的是：当一个 reply 触发多个工具时，树自然分叉，变成并列兄弟节点：
    
    
    agent.reply
    ├─ tool.call(A) -> tool.result(A)
    └─ tool.call(B) -> tool.result(B)
    
    

这就是 P05 的“真实战场”：你不再靠时间顺序猜因果，而是靠 parent 指针显式写出执行图。

* * *

## 3) 我们跑出来的结构长什么样？

我写了一个调试脚本 `scripts/render_trace_tree.py`，读取 `runtime_data/events.jsonl`，按 `_span_id/_parent_span_id` 还原因果树。加入 tool 分叉后，打印结果像这样：
    
    
    session.start (root)
    ├─ user.message
    │  └─ agent.reply
    │     └─ tool.call
    │        └─ tool.result
    └─ session.end
    
    

这棵树同时满足三个硬指标：

  *  **ROOTS = 1** ：只有一个根（生命周期根）

  *  **ORPHANS = 0** ：没有孤儿 span（结构可回放）

  *  **tool.result 挂在 tool.call 下** ：结果归因不会混乱




这不是“看起来像”，而是“机器可以稳定重建”。

* * *

## 4) 一个关键修正：生命周期不被业务链挟持

在加入 tool 分叉后，我们还必须钉死一个容易忽视的口径：

`session.end` 的 parent 应该指向 `session.start`（生命周期根），而不是指向最后一个业务动作。

理由很简单：session.end 是“生命事件”，它应该闭合生命边界，而不是成为业务链的尾巴。否则当业务链变深、变复杂、变并发，session 的边界会被挟持，Replay 与统计会越来越难做。

所以最终的稳定结构是：

  * 生命周期：`start → end` 回指根闭合

  * 业务链：`user → agent → tool → …` 在根下面自由生长




这是 OS 语义的清洁分层。

* * *

## 5) 为什么这一结构会直接决定未来的治理能力？

因为后面所有高阶能力，都需要一个明确的“挂载点”。

  *  **Policy Gate（P07）** 应该插在哪？

插在 `tool.call` 之前，做 `policy.check → allow/deny`。

  *  **回放（P06）** 如何成立？

Replay 不是“再问一次模型”，而是按因果树重放节点：先重放 tool.call，再验证 tool.result。

  *  **观测与成本（P09）** 怎么统计？

tool.call/tool.result 自带天然区间：你可以在 result 里记录 latency、token、cost、error。

  *  **MCP / 安全架构** 怎么落地？

tool.call 是“能力暴露点”，tool.result 是“副作用证据点”，两者之间就是安全治理的最小闭环。




一旦 tool 被结构化为因果子树，它就不再是“工具调用”，而是 **受治理的能力执行单元** 。

* * *

## 6) 这一课的结尾：一句话总结

P04 让系统拥有了历史。

P05 让历史有了因果结构。

而 **P05 More（tool 分叉）**意味着：

> 系统第一次把“行动”写进了自己的可审计因果树。
> 
> 从此以后，智能不再是“说得好”，而是“做得对、做得可追责”。

做出来长这样，你可以看到分叉，因果，和继承。
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗  rm -f runtime_data/events.jsonl
    python -m projects.p00-agent-os-mvp.src.main
    python scripts/render_trace_tree.py
    
    [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
    
    ========================================================================================
    SESSION: p00-efa4acca-6968-49e1-a941-9761cf687648
    TRACE:   77b306b1-0e0e-4c8b-98ea-9607acecd2b3
    EVENTS:  6  | ROOTS: 1  | ORPHANS: 0
    
    --- ROOT 1 ---
    session.start  actor=runtime  span=2c5f4095-d505-45bd-88ff-034c292c71cf  ts=2025-12-18T04:02:39.761Z
        ↳ Session started for p00 MVP
        payload={"message": "Session started for p00 MVP", "persona_user_id": "susan"}
       ├─ user.message  actor=user  span=229a141d-b8ec-4a47-89ac-6f173938bd43  parent=2c5f4095-d505-45bd-88ff-034c292c71cf  ts=2025-12-18T04:02:39.761Z
       │      ↳ Hello, this is the first OS-level MVP run.
       │      payload={"text": "Hello, this is the first OS-level MVP run."}
       │  └─ agent.reply  actor=agent  span=21125454-8ecd-4f29-ad1d-9a29fded0e7f  parent=229a141d-b8ec-4a47-89ac-6f173938bd43  ts=2025-12-18T04:02:39.761Z
       │         ↳ [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
       │         payload={"reply": "[MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.", "tool_calls": [{"args": {"q": "AI news this week"}, "to…
       │     └─ tool.call  actor=tool  span=eea2350d-1595-4824-a835-48be34ef30c3  parent=21125454-8ecd-4f29-ad1d-9a29fded0e7f  ts=2025-12-18T04:02:39.762Z
       │            payload={"args": {"q": "AI news this week"}, "tool_name": "fake_search"}
       │        └─ tool.result  actor=tool  span=abfaee15-9f85-4227-9879-090c77842dee  parent=eea2350d-1595-4824-a835-48be34ef30c3  ts=2025-12-18T04:02:39.762Z
       │               payload={"result": {"data": "stub tool result", "ok": true}, "tool_name": "fake_search"}
       └─ session.end  actor=runtime  span=a170df23-f9ce-4054-aed4-ef56f53ddd73  parent=2c5f4095-d505-45bd-88ff-034c292c71cf  ts=2025-12-18T04:02:39.762Z
              ↳ Session ended for p00 MVP
              payload={"message": "Session ended for p00 MVP"}
    
    Done.
    
    

# P06｜Replay Runner：当“可复现”第一次变成事实

P04 我们把事件写成了确定性的历史：每条事件都有稳定信封、UTC 时间戳、以及 `payload_hash = sha256(canonical_json(payload))`。P05 我们让历史有了因果：用 `span_id / parent_span_id / actor` 把一次 session 写成一棵可还原的树，并在加入 `tool.call / tool.result` 后进入真正战场——执行开始分叉，风险开始出现，治理才有落点。P06 的目标是把这一切再往下压一层： **让系统只靠**`events.jsonl` **就能“回放”一次运行** ，不依赖模型、不依赖上下文窗口、不依赖主观解释——可复现从口号变成工程事实。

* * *

## 1) P06 到底在做什么？一句话

 **Replay Runner 读取事件账本，重建 session 的因果执行图，并对关键不变量做自动校验。**

它不是“再问一次模型”，而是：

  * 从账本恢复结构

  * 从结构恢复路径

  * 从路径恢复可审计的执行叙事




你可以把它理解为：

 **事件账本的“反编译器”** 。

* * *

## 2) 为什么 Replay 在 Agent 系统里如此重要？

因为模型天然不稳定，但系统必须稳定。

  * 模型输出会漂移（温度、版本、上下文）

  * 工具调用会产生副作用

  * 记忆写入可能污染长期世界状态




如果你无法回放一次运行，你就无法：

  * 做回归测试（Regression）

  * 做安全审计（Audit）

  * 做责任归因（Attribution）

  * 做治理门禁（Policy Gate）

  * 做长期迁移（Migration）




所以 P06 是 OS 级工程：它保证系统能对自己说一句话——

> “我能证明我当时做过什么。”

* * *

## 3) 我们做了一个最小 replay_runner

我写了一个脚本：`scripts/replay_runner.py`。它做的事情很朴素，但非常硬：

  1. 读取 `runtime_data/events.jsonl`

  2. 按 `session_id` 分组

  3. 用 `_span_id/_parent_span_id` 重建因果树

  4. 按树遍历打印 replay 输出

  5. 校验关键红线：

    * `payload_hash` 必须匹配当前 payload

    * `tool.result` 必须挂在 `tool.call` 下

    * `session.end` 必须回指生命周期 root（P05 v1 口径）

    * 检测 orphan / cycle




* * *

## 4) 回放输出长什么样？

对某个 session 执行：
    
    
    python scripts/replay_runner.py --session <session_id>
    
    

我得到的 replay 输出是：
    
    
    - session.start actor=runtime
      - user.message actor=user
          user: Hello, this is the first OS-level MVP run.
        - agent.reply actor=agent
            agent: [MVP Kernel Stub] You said: ...
            tool_calls: 1
          - tool.call actor=tool
              tool.call: fake_search args={'q': 'AI news this week'}
            - tool.result actor=tool
                tool.result: fake_search result={'data': 'stub tool result', 'ok': True}
      - session.end actor=runtime
    
    

注意：这段输出不是“模型生成的总结”，而是账本结构的重建结果。

换句话说： **这是系统历史本身在说话** 。

* * *

## 5) P06 的核心价值：完整性校验（Integrity Check）

P06 不只是打印树，它还验证历史是否可信。

我们做了一件“sneaky”的测试：手动篡改 `events.jsonl` 里 `user.message` 的内容，把文本改成 `HACKED`，但不改 `payload_hash`。结果 replay_runner 立刻给出警告：
    
    
    payload_hash mismatch: expected=... calc=... event_type=user.message
    
    

并且 replay 输出确实显示用户内容变成了 `HACKED`。

这件事非常重要，因为它证明：

  * 账本不是“信任文件”，而是“可验证文件”

  * 任何事后篡改都会被检测出来（至少在 payload 层面）

  * replay 输出在工程上有可信度，而不是“看起来合理”




在默认模式下，它会继续回放（便于调试）；在 `--strict` 模式下，你可以让它直接 fail，把它变成 CI 里的回归硬门槛。

* * *

## 6) P06 把系统推进到哪里了？

到这里，我们已经形成了一条非常关键的闭环：

  * P04：历史可确定（deterministic）

  * P05：历史可归因（causal）

  * P06：历史可回放（replayable）且可校验（verifiable）




这意味着：系统从“会发生”进入了“能证明”。

 **能证明** 是一切治理、风控、主权层（Policy / MCP / Sovereignty）开始的前提。

* * *

## 7) 下一步：更强的防篡改（可选升级）

刚才的篡改实验也同时暴露了下一层事实：

> 如果攻击者同时篡改 payload 并重算 payload_hash，replay 仍然会“通过”。

所以 P06 的自然升级是加入：

  * `envelope_hash`：对整个信封做 hash

  * `prev_envelope_hash`：在 session 内做 hash 链

  * 甚至签名（不可抵赖）




这会把“可检测篡改”推进到更高层级，进入真正的安全与主权工程。

> 这个在我们系统的安全性能需要提升的时候，必须加。所以所谓的基建，也不是一次性的。但是我们现在先点到为止。

* * *

## 一句话总结

P06 的意义不在于“打印了一棵树”，而在于：

> 系统第一次获得了“只靠自己的历史，就能复现自己”的能力。

从这里开始，Agent 不再是一次性的对话现象，而是一个可以被验证、被治理、可长期演化的运行时生命体。
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ python scripts/replay_runner.py --session p00-efa4acca-6968-49e1-a941-9761cf687648
    
    ========================================================================================
    REPLAY SESSION: p00-efa4acca-6968-49e1-a941-9761cf687648
    TRACE_IDS: ['77b306b1-0e0e-4c8b-98ea-9607acecd2b3']
    EVENTS: 6
    
    REPLAY OUTPUT:
    - session.start actor=runtime ts=2025-12-18T04:02:39.761Z
      - user.message actor=user ts=2025-12-18T04:02:39.761Z
          user: Hello, this is the first OS-level MVP run.
        - agent.reply actor=agent ts=2025-12-18T04:02:39.761Z
            agent: [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
            tool_calls: 1
          - tool.call actor=tool ts=2025-12-18T04:02:39.762Z
              tool.call: fake_search args={'q': 'AI news this week'}
            - tool.result actor=tool ts=2025-12-18T04:02:39.762Z
                tool.result: fake_search result={'data': 'stub tool result', 'ok': True}
      - session.end actor=runtime ts=2025-12-18T04:02:39.762Z
    
    Done.
    
    

# 还在P06, 我们现在做点Sneaky的事情，手动篡改数据

所以你就看到哈希的重要性了。
    
    
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ python scripts/replay_runner.py --session p00-efa4acca-6968-49e1-a941-9761cf687648
    
    ========================================================================================
    REPLAY SESSION: p00-efa4acca-6968-49e1-a941-9761cf687648
    TRACE_IDS: ['77b306b1-0e0e-4c8b-98ea-9607acecd2b3']
    EVENTS: 6
    
    WARNINGS:
     - [WARN] payload_hash mismatch: expected=1671f8263d2185809fc1ec9e34096bb7fee8c34aadfa06dfe017d41b25d4043b calc=a2f071924d5454d72f61d947cce28d579f285e711051b3a29732bd0c431a8cd6 event_type=user.message
    
    REPLAY OUTPUT:
    - session.start actor=runtime ts=2025-12-18T04:02:39.761Z
      - user.message actor=user ts=2025-12-18T04:02:39.761Z
          user: HACKED
        - agent.reply actor=agent ts=2025-12-18T04:02:39.761Z
            agent: [MVP Kernel Stub] You said: Hello, this is the first OS-level MVP run.
            tool_calls: 1
          - tool.call actor=tool ts=2025-12-18T04:02:39.762Z
              tool.call: fake_search args={'q': 'AI news this week'}
            - tool.result actor=tool ts=2025-12-18T04:02:39.762Z
                tool.result: fake_search result={'data': 'stub tool result', 'ok': True}
      - session.end actor=runtime ts=2025-12-18T04:02:39.762Z
    
    Done.
    (.venv) ➜  adk-decade-of-agents git:(main) ✗ 
    

replay_runner.py
    
    
    #!/usr/bin/env python3
    from __future__ import annotations
    
    import argparse
    import json
    import hashlib
    from dataclasses import dataclass
    from pathlib import Path
    from typing import Any, Dict, List, Optional, Tuple, Set
    
    def canonical_json(obj: Any) -> str:
        return json.dumps(obj, sort_keys=True, separators=(",", ":"), ensure_ascii=False)
    
    def sha256_hex(s: str) -> str:
        return hashlib.sha256(s.encode("utf-8")).hexdigest()
    
    @dataclass
    class Event:
        event_type: str
        ts: str
        session_id: str
        trace_id: str
        payload: Dict[str, Any]
        payload_hash: str
    
        span_id: Optional[str]
        parent_span_id: Optional[str]
        actor: Optional[str]
    
    def read_jsonl(path: Path) -> List[Dict[str, Any]]:
        rows: List[Dict[str, Any]] = []
        with path.open("r", encoding="utf-8") as f:
            for i, line in enumerate(f, start=1):
                line = line.strip()
                if not line:
                    continue
                try:
                    rows.append(json.loads(line))
                except json.JSONDecodeError as e:
                    raise SystemExit(f"[ERROR] Invalid JSON on line {i}: {e}") from e
        return rows
    
    def parse_event(row: Dict[str, Any]) -> Event:
        payload = row.get("payload") or {}
        return Event(
            event_type=str(row.get("event_type", "")),
            ts=str(row.get("ts", "")),
            session_id=str(row.get("session_id", "")),
            trace_id=str(row.get("trace_id", "")),
            payload=payload,
            payload_hash=str(row.get("payload_hash", "")),
            span_id=(str(payload.get("_span_id")) if payload.get("_span_id") else None),
            parent_span_id=(str(payload.get("_parent_span_id")) if payload.get("_parent_span_id") else None),
            actor=(str(payload.get("_actor")) if payload.get("_actor") else None),
        )
    
    def verify_payload_hash(e: Event) -> Optional[str]:
        calc = sha256_hex(canonical_json(e.payload))
        if calc != e.payload_hash:
            return f"payload_hash mismatch: expected={e.payload_hash} calc={calc} event_type={e.event_type}"
        return None
    
    def build_span_index(events: List[Event]) -> Tuple[Dict[str, Event], Dict[str, List[str]], List[str], List[str]]:
        """
        Returns:
          span2event: span_id -> representative event (one per span in our MVP)
          children: parent_span_id -> [child_span_id...]
          roots: span_ids with parent None (or missing parent treated as root)
          orphans: span_ids with missing parent span
        """
        span2event: Dict[str, Event] = {}
        for e in events:
            if e.span_id and e.span_id not in span2event:
                span2event[e.span_id] = e
    
        children: Dict[str, List[str]] = {}
        roots: List[str] = []
        orphans: List[str] = []
    
        for sid, ev in span2event.items():
            pid = ev.parent_span_id
            if pid is None:
                roots.append(sid)
            else:
                if pid not in span2event:
                    orphans.append(sid)
                    roots.append(sid)
                else:
                    children.setdefault(pid, []).append(sid)
    
        # stable order: by ts then event_type
        def key(sid: str) -> Tuple[str, str]:
            ev = span2event[sid]
            return (ev.ts, ev.event_type)
    
        for pid, kids in children.items():
            kids.sort(key=key)
        roots.sort(key=key)
    
        return span2event, children, roots, orphans
    
    def detect_cycle(children: Dict[str, List[str]], roots: List[str]) -> bool:
        visited: Set[str] = set()
        stack: Set[str] = set()
    
        def dfs(sid: str) -> bool:
            if sid in stack:
                return True
            if sid in visited:
                return False
            visited.add(sid)
            stack.add(sid)
            for c in children.get(sid, []):
                if dfs(c):
                    return True
            stack.remove(sid)
            return False
    
        for r in roots:
            if dfs(r):
                return True
        return False
    
    def replay_session(events: List[Event], strict: bool = True) -> Tuple[List[str], List[str]]:
        """
        Replay is event-driven:
          - Reconstruct transcript + tool executions from the ledger
          - Validate key invariants (P04 hash, P05 causality)
        Returns: (replay_lines, warnings)
        """
        warnings: List[str] = []
        lines: List[str] = []
    
        # 1) P04 hash verification
        for e in events:
            err = verify_payload_hash(e)
            if err:
                if strict:
                    raise SystemExit(f"[ERROR] {err}")
                warnings.append(f"[WARN] {err}")
    
        # 2) Span graph build & sanity
        span2event, children, roots, orphans = build_span_index(events)
    
        if detect_cycle(children, roots):
            msg = "cycle detected in span graph"
            if strict:
                raise SystemExit(f"[ERROR] {msg}")
            warnings.append(f"[WARN] {msg}")
    
        if orphans:
            msg = f"orphan spans detected: {len(orphans)}"
            if strict:
                raise SystemExit(f"[ERROR] {msg}")
            warnings.append(f"[WARN] {msg}")
    
        # 3) Find lifecycle root: prefer session.start
        root_sid: Optional[str] = None
        for sid in roots:
            if span2event[sid].event_type == "session.start":
                root_sid = sid
                break
        if root_sid is None and roots:
            root_sid = roots[0]
    
        if root_sid is None:
            msg = "no roots found"
            if strict:
                raise SystemExit(f"[ERROR] {msg}")
            warnings.append(f"[WARN] {msg}")
            return lines, warnings
    
        # 4) Validate lifecycle end points to root (P05 v1)
        # find session.end event
        end_sid = None
        for sid, ev in span2event.items():
            if ev.event_type == "session.end":
                end_sid = sid
                # must parent=root
                if ev.parent_span_id != root_sid:
                    msg = f"session.end parent mismatch: end.parent={ev.parent_span_id} root={root_sid}"
                    if strict:
                        raise SystemExit(f"[ERROR] {msg}")
                    warnings.append(f"[WARN] {msg}")
                break
    
        # 5) Replay: walk tree from root, produce a readable trace
        def walk(sid: str, depth: int = 0):
            ev = span2event[sid]
            indent = "  " * depth
            actor = ev.actor or "unknown"
            lines.append(f"{indent}- {ev.event_type} actor={actor} ts={ev.ts}")
    
            # Attach human-friendly content
            p = ev.payload
            if ev.event_type == "user.message":
                lines.append(f"{indent}    user: {p.get('text','')}")
            elif ev.event_type == "agent.reply":
                lines.append(f"{indent}    agent: {p.get('reply','')}")
                # show tool_calls summary if present
                tc = p.get("tool_calls")
                if isinstance(tc, list) and tc:
                    lines.append(f"{indent}    tool_calls: {len(tc)}")
            elif ev.event_type == "tool.call":
                lines.append(f"{indent}    tool.call: {p.get('tool_name')} args={p.get('args')}")
            elif ev.event_type == "tool.result":
                lines.append(f"{indent}    tool.result: {p.get('tool_name')} result={p.get('result')}")
    
            # Validate tool.result parent rule locally (if tool.result -> parent must be tool.call)
            if ev.event_type == "tool.result":
                pid = ev.parent_span_id
                if pid and pid in span2event and span2event[pid].event_type != "tool.call":
                    msg = f"tool.result parent must be tool.call, got parent_type={span2event[pid].event_type}"
                    if strict:
                        raise SystemExit(f"[ERROR] {msg}")
                    warnings.append(f"[WARN] {msg}")
    
            for child in children.get(sid, []):
                walk(child, depth + 1)
    
        walk(root_sid, 0)
    
        # Also: ensure session.end exists
        if end_sid is None:
            msg = "missing session.end"
            if strict:
                raise SystemExit(f"[ERROR] {msg}")
            warnings.append(f"[WARN] {msg}")
    
        return lines, warnings
    
    def main() -> None:
        ap = argparse.ArgumentParser(description="P06 Replay Runner (event-driven replay from events.jsonl)")
        ap.add_argument("--file", default="runtime_data/events.jsonl", help="Path to events.jsonl")
        ap.add_argument("--session", default=None, help="Replay only a specific session_id")
        ap.add_argument("--strict", action="store_true", help="Fail fast on any validation error")
        args = ap.parse_args()
    
        path = Path(args.file)
        if not path.exists():
            raise SystemExit(f"[ERROR] File not found: {path}")
    
        rows = read_jsonl(path)
        events = [parse_event(r) for r in rows]
    
        # group by session_id
        sessions: Dict[str, List[Event]] = {}
        for e in events:
            if args.session and e.session_id != args.session:
                continue
            sessions.setdefault(e.session_id, []).append(e)
    
        if not sessions:
            raise SystemExit("[ERROR] No sessions found (check --session filter or file).")
    
        for sid, evs in sorted(sessions.items(), key=lambda kv: kv[0]):
            evs.sort(key=lambda e: (e.ts, e.event_type))  # stable-ish
    
            print("\\n" + "=" * 88)
            print(f"REPLAY SESSION: {sid}")
            trace_ids = sorted({e.trace_id for e in evs})
            print(f"TRACE_IDS: {trace_ids}")
            print(f"EVENTS: {len(evs)}")
    
            lines, warnings = replay_session(evs, strict=args.strict)
    
            if warnings:
                print("\\nWARNINGS:")
                for w in warnings:
                    print(" -", w)
    
            print("\\nREPLAY OUTPUT:")
            for line in lines:
                print(line)
    
        print("\\nDone.")
    
    if __name__ == "__main__":
        main()
    
    

> p07 之前，是一个“能力优先、结构未治理、默认善意”的智能体世界。

具体来说：

  * agent **能做很多事**

  * memory **能被写**

  * event **能被记录**

  * persona **能演化**

  * 但：

    * 没有“谁允许你这么做”

    * 没有“哪些东西不该进世界记忆”

    * 没有“这是不是越权、是不是未来不可逆”




这是一个 **技术上可行，但文明上危险** 的阶段。

下一步，我们要引入门禁。

<https://github.com/STEMMOM/adk-decade-of-agents/tree/P06-pre-policy-gate>
