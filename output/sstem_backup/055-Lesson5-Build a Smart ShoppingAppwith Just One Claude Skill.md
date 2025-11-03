> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.entropycontroltheory.com](https://www.entropycontroltheory.com/p/lesson-5-build-a-smart-shopping-app)

> Turning a single .json file into the 唯一真相源 (“sole source of truth”) for your AI-driven household assi......

> “Build an App with Just One Claude Skill and One .json File — No Code, Just Structure.” —Susan STEM

In the old world, systems were built _for humans to use._

In the new world, systems must be built _for AI to understand._

The future standard of design is no longer “human-friendly,” but **“AI-friendly.”**

Because the real user of the future isn’t you.

It’s the AI that runs your system, reads your data, and executes your logic without ever touching a button.

And that shift changes everything:

*   Interface becomes secondary; **structure** becomes the truth.
    
*   Functionality fades; **semantic coherence** remains.
    
*   Efficiency matters less than **collaborative elasticity.**
    

In this lesson, we’ll prove that philosophy in practice—by building a fully functional **shopping app** powered by just **one Claude Skill** and **one JSON file as its 唯一真相源 (the One Source of Truth).**

You don’t need to know code.

You only need to think in structures.

Stay with me.

We’ll start simple—one stone at a time.

Each week, we’ll add a new function, test it in real life, and let it grow through real use.

You’ll live with it, not just build it.

And when we look back a few months from now,

we won’t just have a prototype—

we’ll have created something that a traditional software engineer might spend months developing,

packaging, and selling on the App Store.

But we’ll have built it differently—

not through code,

but through **structure, iteration, and living intelligence.**

Start by uploading the **[SKILL.md](http://skill.md/)** file to Claude.

Then, create a dedicated project folder to hold both files — the **[SKILL.md](http://skill.md/)** and the `ledger.json` file.

You don’t have the `.json` file yet; you’ll generate it after uploading the Skill.

If you’re not familiar with uploading a Claude Skill, refer to the setup guide I shared earlier.

The complete code for the **[SKILL.md](http://skill.md/)** is provided at the bottom of this article.

Once the upload is complete, Claude’s interface should look like this:

[![](https://substackcdn.com/image/fetch/$s_!gZ6G!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3b3b2493-a3f4-4331-a6f3-c26c4d19d33a_748x183.heic)](https://substackcdn.com/image/fetch/$s_!gZ6G!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3b3b2493-a3f4-4331-a6f3-c26c4d19d33a_748x183.heic)

Before we begin, it’s important to understand what this file truly represents—and why it’s called the **“single source of truth.”** A large language model like Claude doesn’t have memory of your current life. It doesn’t know what’s in your fridge, what you ordered last week, or even what you discussed yesterday. Every time you start a new session, the AI begins from zero—intelligent, yes, but forgetful. That’s why we need a file that acts as an external memory, a kind of structured notebook that records the evolving state of your life.

This file bridges the gap between the AI’s intelligence and your lived reality. Each entry, each update in the `.json` file becomes a way for the system to _remember_—not through biological memory or cloud databases, but through structured truth. In this model, your data isn’t just information; it’s context. It gives the AI continuity, grounding it in the concrete details of your daily world.

So instead of teaching the AI to “remember,” we give it a place to look. The `ledger.json` becomes the reference point for everything the system knows about your household: what you’ve bought, what’s running low, what’s fresh, what’s expired. When Claude reads this file, it reconstructs your world; when it writes to it, your world updates.

In essence, this isn’t just a data file—it’s your **life’s state container**, the bridge between language and structure. Once you understand this, you’ll see why modern AI apps don’t need complicated databases or cloud infrastructures. All they need is one structured file that holds the truth, and one Skill smart enough to interpret and evolve it.

**Create Ledger**

Now let’s start, with a new chat window in Claude and simply say

_**“create a new family shopping ledger”.**_

Boom! Easy.

[![](https://substackcdn.com/image/fetch/$s_!5ahK!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1c42a8d2-4685-4b81-aa90-a5e6a039f8de_1103x734.heic)](https://substackcdn.com/image/fetch/$s_!5ahK!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1c42a8d2-4685-4b81-aa90-a5e6a039f8de_1103x734.heic)

Now I want you do download this ledger.json file, just hit the download button:

[![](https://substackcdn.com/image/fetch/$s_!nUgU!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4dc5c76b-9314-4130-b7e9-b14e023139e4_676x283.heic)](https://substackcdn.com/image/fetch/$s_!nUgU!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4dc5c76b-9314-4130-b7e9-b14e023139e4_676x283.heic)

Move it to the file folder you just created for the this shopping app, with your SKILL file, make sure it looks like this:

[![](https://substackcdn.com/image/fetch/$s_!w90d!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4ff458de-8b76-42b8-a1f1-64cdbe1dca93_261x152.heic)](https://substackcdn.com/image/fetch/$s_!w90d!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4ff458de-8b76-42b8-a1f1-64cdbe1dca93_261x152.heic)

**Add Items**
