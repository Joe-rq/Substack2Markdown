# Lesson 5: Build a Smart Shopping App with Just One Claude Skill

## Turning a single .json file into the 唯一真相源 (“sole source of truth”) for your AI-driven household assistant

**Oct 30, 2025**

**Likes:** 0

> “Build an App with Just One Claude Skill and One .json File — No Code, Just Structure.” —Susan STEM

In the old world, systems were built _for humans to use._

In the new world, systems must be built _for AI to understand._

The future standard of design is no longer “human-friendly,” but **“AI-friendly.”**

Because the real user of the future isn’t you.

It’s the AI that runs your system, reads your data, and executes your logic without ever touching a button.

And that shift changes everything:

  * Interface becomes secondary; **structure** becomes the truth.

  * Functionality fades; **semantic coherence** remains.

  * Efficiency matters less than **collaborative elasticity.**




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

* * *

###  **Step 1: Upload the Skill**

Start by uploading the **[SKILL.md](http://skill.md/)** file to Claude.

Then, create a dedicated project folder to hold both files — the **[SKILL.md](http://skill.md/)** and the `ledger.json` file.

You don’t have the `.json` file yet; you’ll generate it after uploading the Skill.

If you’re not familiar with uploading a Claude Skill, refer to the setup guide I shared earlier.

The complete code for the **[SKILL.md](http://skill.md/)** is provided at the bottom of this article.

Once the upload is complete, Claude’s interface should look like this:

[![](https://substackcdn.com/image/fetch/$s_!gZ6G!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3b3b2493-a3f4-4331-a6f3-c26c4d19d33a_748x183.heic)](https://substackcdn.com/image/fetch/$s_!gZ6G!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3b3b2493-a3f4-4331-a6f3-c26c4d19d33a_748x183.heic)

###  **Step 2: Create the**`.json` **File with one prompt**

Before we begin, it’s important to understand what this file truly represents—and why it’s called the **“single source of truth.”** A large language model like Claude doesn’t have memory of your current life. It doesn’t know what’s in your fridge, what you ordered last week, or even what you discussed yesterday. Every time you start a new session, the AI begins from zero—intelligent, yes, but forgetful. That’s why we need a file that acts as an external memory, a kind of structured notebook that records the evolving state of your life.

This file bridges the gap between the AI’s intelligence and your lived reality. Each entry, each update in the `.json` file becomes a way for the system to _remember_ —not through biological memory or cloud databases, but through structured truth. In this model, your data isn’t just information; it’s context. It gives the AI continuity, grounding it in the concrete details of your daily world.

So instead of teaching the AI to “remember,” we give it a place to look. The `ledger.json` becomes the reference point for everything the system knows about your household: what you’ve bought, what’s running low, what’s fresh, what’s expired. When Claude reads this file, it reconstructs your world; when it writes to it, your world updates.

In essence, this isn’t just a data file—it’s your **life’s state container** , the bridge between language and structure. Once you understand this, you’ll see why modern AI apps don’t need complicated databases or cloud infrastructures. All they need is one structured file that holds the truth, and one Skill smart enough to interpret and evolve it.

 **Create Ledger**

Now let’s start, with a new chat window in Claude and simply say

 _ **“create a new family shopping ledger”.**_

Boom! Easy.

[![](https://substackcdn.com/image/fetch/$s_!5ahK!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1c42a8d2-4685-4b81-aa90-a5e6a039f8de_1103x734.heic)](https://substackcdn.com/image/fetch/$s_!5ahK!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1c42a8d2-4685-4b81-aa90-a5e6a039f8de_1103x734.heic)

Now I want you do download this ledger.json file, just hit the download button:

[![](https://substackcdn.com/image/fetch/$s_!nUgU!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4dc5c76b-9314-4130-b7e9-b14e023139e4_676x283.heic)](https://substackcdn.com/image/fetch/$s_!nUgU!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4dc5c76b-9314-4130-b7e9-b14e023139e4_676x283.heic)

Move it to the file folder you just created for the this shopping app, with your SKILL file, make sure it looks like this:

[![](https://substackcdn.com/image/fetch/$s_!w90d!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4ff458de-8b76-42b8-a1f1-64cdbe1dca93_261x152.heic)](https://substackcdn.com/image/fetch/$s_!w90d!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4ff458de-8b76-42b8-a1f1-64cdbe1dca93_261x152.heic)

 **Add Items**

Ok, now let’s start by adding some routine groceries we need. For me, I have a very routine shopping items. Remember, you say everything in natural language, it can be in English, Chinese, Japanese, however you want. I would say:
    
    
    add the following items to my ledger: apples, bananas, chiken wings, pork shoulder and milk. 
    

and….Boom! Like magic.

[![](https://substackcdn.com/image/fetch/$s_!zLuD!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8cb6f64c-1076-4a93-9ae5-3e83b1410f56_1235x745.heic)](https://substackcdn.com/image/fetch/$s_!zLuD!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8cb6f64c-1076-4a93-9ae5-3e83b1410f56_1235x745.heic)

Ok, now I want to guide you through the .json file here, on the right. So you understand some basic of reading it. In this SKILL I have created, the SKILL has **built in** estimation of the expiry days of your grocery item. Look right here below. Just now I only said add Chicken Wings to my list, it fill up all the rest of input for me.
    
    
    {
    27      “name”: “Chicken Wings”,
    28      “unit”: “lb”,
    29      “par_level”: 2,
    30      “on_hand”: 0,
    31      “pending”: 0,
    32      “preferred_store”: “”,
    33      “category”: “Meat & Protein”,
    34      “expiry_days”: 2
    35    },
    

**Edit Item**

The par_level means how many chicken wings I wish to have in my stock. The default is 2 lbs. I am not happy with that, I want to change this setting about chicken wings. Just use one sentence, change everything.
    
    
    Change the chicken wing unit from “lb” into “bag”, par_level:1, preferred store: Costco
    

[![](https://substackcdn.com/image/fetch/$s_!j_V6!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F70228204-df6f-496c-a6a6-0de3cf5b8599_695x550.heic)](https://substackcdn.com/image/fetch/$s_!j_V6!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F70228204-df6f-496c-a6a6-0de3cf5b8599_695x550.heic)

And you would see within this context window, the ledger.json file has been changed.

[![](https://substackcdn.com/image/fetch/$s_!XJr2!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1cfb6465-a2db-4b92-b67f-74465eaa1821_254x197.heic)](https://substackcdn.com/image/fetch/$s_!XJr2!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1cfb6465-a2db-4b92-b67f-74465eaa1821_254x197.heic)

Here’s what each key means:

  * `name` — the name of the item.

  * `unit` — how the item is measured (by pound, bag, bottle, etc.).

  * `par_level` — how many you _want_ to keep in stock. For chicken wings, the default is `2 lbs`, but I prefer more. I can simply say, _“Change par level for chicken wings to 5 lbs,”_ and the file will update automatically.

  * `on_hand` — how much you currently have at home.

  * `preferred_store` — where you usually buy this item, so your shopping trips are more efficient.

  * `category` — automatically classified, but you can adjust it if needed.

  * `expiry_days` — estimated shelf life in days, also auto-calculated but editable.




Remember: **you don’t need to write code.** Every command can be expressed in plain natural language. For example:

> “Change expiry days for milk to 7.”
> 
> “Add a note that chicken wings are on sale this week.”

The Skill will interpret your sentence, update the JSON, and return both a friendly summary and the full updated file. My language is also very messy, unstructured when it comes to this, and it is totally OK, that’s the beauty of natural language. Use it this way, combine your instructions, hint your intentions even. Expiry date, and category is built-in. 

[![](https://substackcdn.com/image/fetch/$s_!lHXd!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F06f39c0f-b316-4aaf-9fce-411b7df2551f_1223x692.heic)](https://substackcdn.com/image/fetch/$s_!lHXd!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F06f39c0f-b316-4aaf-9fce-411b7df2551f_1223x692.heic)

### **Step 3: Understanding and Updating Your**`ledger.json`

Before closing this session, **make sure you download the most recent version of your**`ledger.json` **.**

If you don’t, any new data created in this chat window will be lost.

Always keep **one—and only one—**`ledger.json` in your shopping app folder, replacing the old one each time. This is what we mean by the **唯一真相源** , or _the single source of truth_ : there is only one file that defines your system’s current state. Every Skill you build later will read and write from this **same** file. We just have to manual do it for now. Constantly download from Claude and **REPLACE** the old one!

[![](https://substackcdn.com/image/fetch/$s_!40fV!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fea91d11b-97d6-44b0-b4bc-22fe5219083a_261x152.heic)](https://substackcdn.com/image/fetch/$s_!40fV!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fea91d11b-97d6-44b0-b4bc-22fe5219083a_261x152.heic)

our folder should always look like this, just ONE ledger.json file! Throw the OLD one into trash and REPLACE it with the most updated version— what you just downloaded from Claude.

* * *

###  **Step 4: Open a New Window and Upload Your Local File**

Now it’s time to start shopping.

Open a new chat window and upload the `ledger.json` file you saved on your local computer. This step reconnects your current conversation with your latest data.

Remember—Claude doesn’t retain full memory of what was discussed in your previous session. Each new window is a fresh start, so uploading your most recent `ledger.json` ensures the AI knows the current state of your household.

It’s also a good practice to include a date in your ledger file name, such as `ledger20251030.json`. This helps you keep track of updates over time while always maintaining **one active file** as your single source of truth. 

[![](https://substackcdn.com/image/fetch/$s_!3gco!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F351d69f2-9a8e-4463-b3bf-d7dfa8deda20_638x702.heic)](https://substackcdn.com/image/fetch/$s_!3gco!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F351d69f2-9a8e-4463-b3bf-d7dfa8deda20_638x702.heic)

Just say, going to Costco, give me a shopping list. 

[![](https://substackcdn.com/image/fetch/$s_!KNFK!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe00ce8f9-bb62-4570-b977-4b5b92bd683b_690x663.heic)](https://substackcdn.com/image/fetch/$s_!KNFK!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe00ce8f9-bb62-4570-b977-4b5b92bd683b_690x663.heic)

You can continue adding, creating, and editing items in this new window just as we discussed earlier. Once your 

ledger.json

file is uploaded, Claude will automatically route your requests to the **family.shopping.review** Skill, handling all updates and summaries seamlessly in the background. And he would write to the new uploaded file (like this one, the new file I just added ledger20251030.json).

SKILL.md
    
    
    ---
    name: family-shopping-review
    description: >
      Create, review, and edit a family shopping ledger.json file.
      This Skill automatically summarizes purchases and consumables,
      classifies household items, estimates expiry dates for perishables,
      and supports natural-language multi-turn edits.
      It outputs a friendly human summary and, when requested,
      a complete updated ledger.json to copy and replace.
    ---
    # ───────────────────────────────
    # Inputs
    # ───────────────────────────────
    inputs:
      - id: intent
        type: string
        required: true
        description: One of: create | review | edit
      - id: ledger_json
        type: json
        required: false
        description: Paste the current full ledger.json (omit for intent=create)
      - id: instructions
        type: string
        required: false
        description: Natural-language edit instructions
                     (e.g. “add 6 bananas from Costco price 0.25 par=6”,
                     “remove paper plates”, “set oat milk par to 3”)
      - id: apply_fixes
        type: boolean
        required: false
        description: If true, automatically apply fixes found during review (default false)
    
    # ───────────────────────────────
    # Outputs
    # ───────────────────────────────
    outputs:
      - id: review_summary
        type: markdown
        description: User-friendly summary of household shopping and inventory
      - id: suggestions
        type: json
        description: Structured improvement suggestions: [{type, item, reason, proposed_change}]
      - id: new_ledger_json
        type: json
        description: Full updated ledger.json (returned for intent=create/edit or when apply_fixes=true)
    
    # ───────────────────────────────
    # Built-in classification & expiry knowledge
    # ───────────────────────────────
    notes: |
      • Trigger language:
          “create a new family shopping ledger” → intent=create (auto-initialize with expiry dates)
    
      • Auto-category taxonomy (detected by name keywords):
          Produce: bananas, apples, berries, lettuce, spinach, tomato, onion, garlic, potato
          Dairy & Alternatives: milk, oat milk, yogurt, cheese, butter
          Pantry: rice, pasta, flour, sugar, oil, salt, canned
          Meat & Protein: chicken, beef, pork, tofu, eggs
          Bakery: bread, bagel, tortilla
          Beverages: coffee, tea, juice, soda, water
          Household & Cleaning: paper towel, toilet paper, detergent, trash bag, sponge
          Personal Care: toothpaste, shampoo, soap, tissue
          Pet: dog food, cat litter, treats
          School & Office: notebook, pen, tape, batteries
    
      • Default expiry presets (days):
          # --- Fresh produce ---
          bananas: 7, berries: 5, lettuce: 5, spinach: 4, tomato: 7,
          onion: 21, potato: 21, garlic: 30,
          # --- Dairy & refrigerated goods ---
          milk: 7, oat milk: 14, yogurt: 10, cheese: 14, butter: 30,
          # --- Protein & frozen foods ---
          chicken: 2, beef: 4, pork: 4, fish: 2,
          tofu: 7, eggs: 21, frozen berries: 90, frozen meat: 120,
          # --- Bakery & pantry items ---
          bread: 5, bagel: 7, rice: 180, pasta: 180, flour: 120, sugar: 365, oil: 180, salt: 365, canned: 540,
          # --- Household & cleaning supplies ---
          paper towel: 365, toilet paper: 365, detergent: 180, trash bag: 365, sponge: 30,
          # --- Personal care ---
          toothpaste: 180, shampoo: 180, soap: 90, tissue: 180,
          # --- Pet & miscellaneous ---
          dog food: 60, cat litter: 30, notebook: 730, batteries: 730
    
          # --- Smart defaults for unknown items ---
          # If the item is not found in this table:
          #   - If it’s a refrigerated food → assume 7 days
          #   - If it’s a frozen food → assume 30 days
          #   - If it’s a dry pantry item (non-perishable) → assume 180 days
          #   - If it’s a household consumable (soap, toothpaste, etc.) → assume 180 days
          #   - Otherwise (tools, durable goods, or unknown category) → assume 365 days
    
          (Items without a specific match will receive the most reasonable household estimate
           based on category: fresh = 1 week, refrigerated = 1 week, frozen = 1 month,
           pantry = 6 months, cleaning/personal = 6 months, durable goods = 1 year.)
    
    
      • Expiry logic:
          If last_purchased exists and expiry_days known →
          next_expiry = last_purchased + expiry_days.
          Items expiring ≤3 days → “expiring_soon”.
          Items past expiry → “expired”.
    
      • Par-gap calculation:
          need_qty = max(0, par_level - on_hand - pending)
    
      • Example edit grammar:
          “add 6 bananas @Costco price 0.25 par=6”
          “remove paper plates”
          “set oat milk par=3 store=’Trader Joe’s’”
          “rename ‘Milk’ to ‘Milk (Oat)’”
    
      • Always preserve unknown fields in the ledger_json when editing;
        only modify relevant items or metadata.
    
    # ───────────────────────────────
    # Behavior
    # ───────────────────────────────
    behavior: |
      • intent=create:
          - Can be triggered by the phrase “create a new family shopping ledger”.
          - Generate a new ledger.json structure with:
              version, household (”Family” default),
              last_cycle=TODAY, items=[], events[]
          - If starter items appear in instructions, add them with
            auto-classification and expiry presets.
          - Output new_ledger_json and review_summary of what was created.
    
      • intent=review:
          - Read ledger_json but do not mutate unless apply_fixes=true.
          - Compute:
              1) Purchase summary for last 7/14/30 days
              2) Top consuming items (by purchase frequency)
              3) Shortages to reach par (by store)
              4) Expiring soon / expired items
              5) Duplicate or near-duplicate names
              6) Inactive items (no purchases in 60 days → suggest lower par)
          - Return a readable review_summary and structured suggestions.
            If apply_fixes=true, also include new_ledger_json with fixes.
    
      • intent=edit:
          - Parse natural-language instructions; for each command:
              • add / remove / modify items
              • update par_level, preferred_store, on_hand/pending
              • set last_price / last_purchased if applicable
          - Auto-classify category and assign expiry_days if missing.
          - Append event logs (type “edit” or “purchase” as needed).
          - Recompute next_expiry; return full new_ledger_json + summary.
    
    # ───────────────────────────────
    # Examples
    # ───────────────────────────────
    examples:
      - inputs:
          intent: “create”
          instructions: “starter: oat milk par=2 @Trader Joe’s; eggs par=2 @Costco; bananas par=6 @Costco”
        outputs:
          review_summary: |
            ✅ Initialized ledger with 3 items (auto-categories and expiry set)
            • Oat Milk → Dairy & Alternatives, expiry 14d, par=2 @Trader Joe’s
            • Eggs → Meat & Protein, expiry 21d, par=2 @Costco
            • Bananas → Produce, expiry 7d, par=6 @Costco
          new_ledger_json:
            version: “1.0”
            household: “Family”
            last_cycle: “AUTO-TODAY”
            items:
              - { name: “Oat Milk”, unit: “carton”, par_level: 2, on_hand: 0, pending: 0,
                  preferred_store: “Trader Joe’s”, category: “Dairy & Alternatives”, expiry_days: 14 }
              - { name: “Eggs”, unit: “dozen”, par_level: 2, on_hand: 0, pending: 0,
                  preferred_store: “Costco”, category: “Meat & Protein”, expiry_days: 21 }
              - { name: “Bananas”, unit: “pcs”, par_level: 6, on_hand: 0, pending: 0,
                  preferred_store: “Costco”, category: “Produce”, expiry_days: 7 }
            events: []
    
      - inputs:
          intent: “review”
          ledger_json:
            version: “1.0”
            household: “Feltner”
            last_cycle: “2025-10-23”
            items:
              - { name: “Oat Milk”, unit: “carton”, par_level: 2, on_hand: 0, pending: 0,
                  preferred_store: “Trader Joe’s”, last_purchased: “2025-10-20” }
              - { name: “Eggs”, unit: “dozen”, par_level: 2, on_hand: 1, pending: 0,
                  preferred_store: “Costco”, last_purchased: “2025-10-22” }
              - { name: “Bananas”, unit: “pcs”, par_level: 6, on_hand: 2, pending: 0,
                  preferred_store: “Costco”, last_purchased: “2025-10-25” }
            events:
              - { ts: “2025-10-22T15:30:00Z”, type: “purchase”, store: “Costco”,
                  lines: [{ name: “Eggs”, qty: 1, unit: “dozen”, price: 3.49 }] }
              - { ts: “2025-10-25T10:00:00Z”, type: “purchase”, store: “Costco”,
                  lines: [{ name: “Bananas”, qty: 6, unit: “pcs”, price: 0.25 }] }
        outputs:
          review_summary: |
            🧾 Family Shopping Review
            • Last 7 days: 2 purchases (Eggs, Bananas)
            • To reach par: Trader Joe’s → Oat Milk × 2 cartons; Costco → Eggs × 1 dozen
            • Expiring soon (≤3 days): Bananas (7 d preset) — check ripeness; Oat Milk near 14 d window
            • Suggestions: unify “Milk”/”Oat Milk” naming; set expiry_days where missing
          suggestions:
            - { type: “naming”, item: “Oat Milk”, reason: “consistent naming”, proposed_change: “keep ‘Oat Milk’” }
            - { type: “expiry”, item: “Oat Milk”, reason: “apply preset 14 d”, proposed_change: { expiry_days: 14 } }
            - { type: “par_tune”, item: “Bananas”, reason: “frequent waste”, proposed_change: { par_level: 4 } }
    
      - inputs:
          intent: “edit”
          instructions: “add 6 bananas @Costco price 0.25 par=6; remove paper plates; set oat milk par=3; add tofu 2 packs @Trader Joe’s price 2.49”
          ledger_json:
            version: “1.0”
            household: “Feltner”
            last_cycle: “2025-10-30”
            items:
              - { name: “Oat Milk”, unit: “carton”, par_level: 2, on_hand: 2, pending: 0, preferred_store: “Trader Joe’s” }
              - { name: “Bananas”, unit: “pcs”, par_level: 6, on_hand: 0, pending: 0, preferred_store: “Costco” }
            events: []
        outputs:
          review_summary: |
            ✍️ Edits applied
            • Bananas +6 pcs @Costco ($0.25) → on_hand +6, expiry 7 d
            • Removed: paper plates
            • Oat Milk par → 3
            • Added: Tofu × 2 packs @Trader Joe’s ($2.49), expiry 7 d
            ✅ Copy new_ledger_json to overwrite your file
          new_ledger_json:
            version: “1.0”
            household: “Feltner”
            last_cycle: “AUTO-TODAY”
            items:
              - { name: “Oat Milk”, unit: “carton”, par_level: 3, on_hand: 2, pending: 0,
                  preferred_store: “Trader Joe’s”, category: “Dairy & Alternatives”, expiry_days: 14 }
              - { name: “Bananas”, unit: “pcs”, par_level: 6, on_hand: 6, pending: 0,
                  preferred_store: “Costco”, category: “Produce”, expiry_days: 7,
                  last_price: 0.25, last_purchased: “AUTO-TODAY” }
              - { name: “Tofu”, unit: “pack”, par_level: 2, on_hand: 2, pending: 0,
                  preferred_store: “Trader Joe’s”, category: “Meat & Protein”, expiry_days: 7,
                  last_price: 2.49, last_purchased: “AUTO-TODAY” }
            events:
              - { ts: “AUTO-NOW”, type: “purchase”, store: “Costco”,
                  lines: [{ name: “Bananas”, qty: 6, unit: “pcs”, price: 0.25 }] }
              - { ts: “AUTO-NOW”, type: “purchase”, store: “Trader Joe’s”,
                  lines: [{ name: “Tofu”, qty: 2, unit: “pack”, price: 2.49 }] }
    

* * *
