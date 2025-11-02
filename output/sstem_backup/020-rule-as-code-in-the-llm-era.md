# Rule as Code in the LLM Era

## RaC showed us consensus could be compiled; LLMs show us it can also be debated, scaled, and alive.

**Oct 03, 2025**

**Likes:** 2

**Rule as Code (RaC)** was born in a very different technological landscape—a world where machines could not yet “understand” human language in any meaningful sense. Natural language processing was brittle, narrow, and far from robust enough to capture the complexity of real legal or policy texts. In that world, ambiguity was treated as the ultimate enemy. If a machine couldn’t handle it, then humans had to eliminate it by hand.

This led to the **deterministic tradition** of RaC. Every rule had to be modeled line by line, translated into formal logic, and encoded into decision tables or specialized languages. The ambition was to create a mirror of the law inside a computer, one where every possible input could produce a predictable output. This is why so much effort was invested in standards like **DMN (Decision Model and Notation)** for tabular decisions, **SBVR (Semantics of Business Vocabulary and Rules)** for precise terminology, or **LegalRuleML** for statutory obligations and permissions. These frameworks were valuable—they gave clarity, consistency, and rigor. They showed that law and policy could, in principle, be treated as executable logic.

But this tradition also hit hard limits. Translating complex rules into deterministic code required enormous expert labor. Every ambiguity had to be resolved upfront, every exception captured, every term defined. The process was **heavy, slow, and expensive.** Few projects moved beyond pilots. The dream of rules as code remained tantalizing, but fragile.

Now, the landscape has shifted dramatically. **Large language models (LLMs)** have introduced a new primitive: _predict the next token._ At first glance, it looks simplistic. But this primitive is astonishingly powerful because it mirrors the way humans—especially lawyers and judges—reason. Legal practitioners are, in essence, professional “token predictors”: given a statute, a precedent, or a case, they anticipate _what comes next_ —the next clause, the next interpretation, the likely ruling.

This parallel opens up a vast new horizon. In the LLM era, we no longer need to eliminate ambiguity at all costs. Instead, we can model, debate, and even **embrace ambiguity probabilistically.** LLMs can surface multiple plausible interpretations, simulate adversarial debates through multi-agent systems, and propose draft rules in ways that are legible to both machines and humans. The rigid deterministic RaC approach, once necessary, now becomes only one half of the equation.

What emerges is the possibility of **Consensus-as-Code** that is broader, fuzzier, and more powerful. Broader, because LLMs can ingest and synthesize enormous legal corpora. Fuzzier, because they can tolerate ambiguity instead of collapsing under it. More powerful, because they can scale interpretation and reasoning at speeds no manual modeling could match.

RaC gave us the first step: consensus compiled into deterministic logic. LLMs extend the vision: consensus explored through probabilistic reasoning. Together, they suggest that the future of governance technology lies not in erasing ambiguity, but in building systems that can handle both **precision and fuzziness** —a hybrid runtime where society’s agreements can be executed, debated, and evolved in real time.

* * *

 **The Rule Development Lifecycle (RDLC)**

To make this work more systematic, the RaC community borrowed from software engineering and articulated a **Rule Development Lifecycle (RDLC).** Much like the Software Development Lifecycle (SDLC), RDLC defined the stages through which rules would move:

  1.  **Discovery:** Identify relevant rules from legislation, regulations, or policy documents.

  2.  **Modeling:** Translate those rules into formal representations—decision tables, markup languages, or DSLs.

  3.  **Validation:** Ensure that the encoded rules faithfully represent the original text. This often involved test cases or side-by-side comparisons.

  4.  **Deployment:** Run the rules in an execution environment—such as a compliance system, eligibility checker, or decision engine.

  5.  **Monitoring:** Track performance, catch errors, and update rules as laws and policies evolve.




In the **pre-LLM world** , every stage of this lifecycle was painstaking manual labor. Discovery required teams of lawyers and analysts combing through documents. Modeling demanded experts fluent in specialized notations. Validation meant building test suites by hand. Deployment was often bespoke, and monitoring required constant human oversight.

This is where the **LLM era introduces a radical shift.** Large language models can now parse entire corpora of laws or regulations, surface relevant rules during discovery, and even generate draft representations in structured formats. What once took months of manual extraction and modeling can now be bootstrapped in hours.

Yet this does not mean the RDLC becomes obsolete. **Validation and legitimacy remain critical.** Just because an LLM can propose a machine-readable rule doesn’t mean it is correct, complete, or legally valid. Rule execution touches lives, rights, and obligations; errors can have catastrophic consequences. The LLM can accelerate the front end of the pipeline, but the back end—the human-led audit of fidelity, legitimacy, and accountability—becomes even more essential.

The **lesson** is that RDLC still matters, but the balance between humans and machines is shifting. Machines can now assist with discovery and modeling at scale, reducing costs and speeding up experimentation. But humans must remain in the loop for validation, interpretation, and governance. In fact, the most important role of humans may be not in writing the rules from scratch, but in **ensuring that “code = rule” in a way that society trusts.**

* * *

 **The Challenge of Interpretation and Consistency**

At the heart of Rule as Code lies a deceptively simple but existential question: **how do we prove that “code = rule”?**

When a law, regulation, or policy is transformed into executable logic, how can citizens, regulators, and courts be sure that the machine’s output reflects the legal intent? If the logic diverges, even slightly, from the authoritative text, the result is not just a bug—it is a potential breach of rights, a misallocation of benefits, or an unlawful penalty.

 **Pre-LLM RaC: the search for certainty**

In the pre-LLM era, RaC approached this challenge with a **deterministic toolkit**. Ambiguity was treated as a flaw to be eliminated. Three core methods dominated:

  1.  **Formal verification:** Borrowed from computer science, this meant mathematically proving that the rule logic conformed to a given specification. If the law said “benefit applies if income < $50,000,” the code could be formally proven to uphold that condition under all cases.

  2.  **Rule-based unit tests:** Much like in software engineering, RaC projects created test suites with representative cases—“golden scenarios” agreed on by legal experts. If the code produced the same outcome as the legal text in these cases, confidence increased.

  3.  **Dual representation:** Many initiatives maintained two linked artifacts—human-readable text and machine-executable code—kept in parallel. Tools like **DMN decision tables** or **LegalRuleML** were designed to straddle this gap, providing a bridge where both humans and machines could validate alignment.




These methods provided a measure of assurance. But they were also brittle. Laws evolve, exceptions proliferate, and edge cases defy exhaustive testing. And above all, the process was slow, expensive, and expert-driven.

* * *

 **The LLM Era: probabilistic interpretation**

Large language models disrupt this equation. Suddenly, machines can _interpret_ rules expressed in natural language without requiring exhaustive hand-coding. Given a statute, an LLM can extract conditions, identify obligations, and even draft executable versions in a DSL or markup language.

This is powerful—but it reopens the consistency problem in a new form. LLMs are **probabilistic interpreters.** Their answers are shaped by training data and context, not by guaranteed logical conformance. They can propose plausible translations of rules—but “plausible” is not the same as “legally valid.”

The risk is obvious: if an LLM-generated rule deviates subtly from legislative intent, who is accountable? How do we trace why the model produced that logic? Can courts accept machine interpretation as authoritative, or does legitimacy always require a deterministic backbone?

 **Toward a hybrid solution**

The likely outcome is a **hybrid model** where RaC and LLMs complement one another:

  *  **RaC provides the formal backbone.** Deterministic standards like DMN, SBVR, or LegalRuleML remain essential for legitimacy, auditability, and legal certainty. They ensure that at the core of any system, “code = rule” is formally testable.

  *  **LLMs provide the interpretive interface.** Instead of replacing RaC, LLMs accelerate discovery, assist with drafting, simulate adversarial debate (multiple agents exploring different readings), and surface ambiguities humans must resolve. They make rule modeling faster and more usable, but the ultimate validation must still rest on formal methods.




In this vision, RaC is the **constitution** —clear, auditable, and stable—while LLMs act as the **commentary and courtroom debate** , agile, adaptive, and human-facing.

* * *

 **The enduring importance of legitimacy**

Ultimately, the consistency problem is not just technical but political. Societies will only accept “rules as code” if they can **trust** that execution matches intent. That trust is earned through transparency, provenance, and validation—principles that RaC pioneered and that remain non-negotiable, even in the age of LLMs.

The challenge of interpretation and consistency, then, is not a flaw but the central design question of consensus-as-code. The task ahead is to **fuse deterministic formality with probabilistic flexibility** —to create systems where machines can help us interpret at scale, but where legitimacy is never outsourced to probability alone.

* * *

 **Looking forward**

RaC was born in a world before LLMs. It proved that consensus could be compiled into code, but only by eliminating ambiguity and encoding every rule deterministically. It gave us the first glimpse of what executable consensus might look like, but it was also brittle, slow, and expert-driven.

Today, with LLMs, we see the other half of the picture. Consensus is not always crisp; it is often **fuzzy, emergent, and probabilistic.** “Predict the next token” turns out to be a surprisingly human primitive — echoing how lawyers, judges, and regulators anticipate what comes next. And as LLM applications advance, we might discover entirely new tools to make consensus executable.

Imagine a **specialized runtime** : a universal machine designed not to run just software, but a certain type of rules — legal, ethical, organizational. Or an **agent society** , where multiple personas argue, negotiate, and debate rules until fuzziness collapses into clarity, and truth emerges from structured disagreement. In these futures, RaC provides the hard spine of legitimacy, while LLMs and agent systems supply the flexible muscle of interpretation, exploration, and adaptation.

Together, they point toward something far more ambitious than “legal automation.” They gesture at a new paradigm: **a runtime not just for code, but for civilization itself** — a platform where rules can be written, debated, executed, and evolved in real time, across human and machine actors alike.

[![](https://substackcdn.com/image/fetch/$s_!_lOx!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F21b46b5d-5f61-41d6-9118-1eeb7a533fec_1536x1024.heic)](https://substackcdn.com/image/fetch/$s_!_lOx!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F21b46b5d-5f61-41d6-9118-1eeb7a533fec_1536x1024.heic)
