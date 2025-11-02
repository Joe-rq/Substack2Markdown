# 🚀 Free Lesson: Build a Fully Functional Calendar App with Just One Claude Skill and a JSON File

## Learn how to turn plain natural language into a smart, self-updating calendar system — no coding, no setup, just pure structure and intelligence.

**Oct 31, 2025**

**Likes:** 3

Just as I mentioned in the previous lesson — all you need to do is upload the **SKILL.md** file I’ve provided, and learn how to download the **calendar.json** file each time you start a new chat window in Claude.

[![](https://substackcdn.com/image/fetch/$s_!BWhz!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7fc4bc4b-8026-408f-8e70-5540617ae4ba_693x187.heic)](https://substackcdn.com/image/fetch/$s_!BWhz!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7fc4bc4b-8026-408f-8e70-5540617ae4ba_693x187.heic)

[ Lessons & Prompts](https://www.entropycontroltheory.com/p/lesson-5-build-a-smart-shopping-app)[

## Lesson 5: Build a Smart Shopping App with Just One Claude Skill

](https://www.entropycontroltheory.com/p/lesson-5-build-a-smart-shopping-app)

[Susan STEM](https://substack.com/profile/268169855-susan-stem)

·

Oct 30

[![Lesson 5: Build a Smart Shopping App with Just One Claude Skill](https://substackcdn.com/image/fetch/$s_!5ahK!,w_1300,h_650,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1c42a8d2-4685-4b81-aa90-a5e6a039f8de_1103x734.heic)](https://www.entropycontroltheory.com/p/lesson-5-build-a-smart-shopping-app)

“Build an App with Just One Claude Skill and One .json File — No Code, Just Structure.” —Susan STEM

[Read full story](https://www.entropycontroltheory.com/p/lesson-5-build-a-smart-shopping-app)

You start first by saying “create a new calendar”.

[![](https://substackcdn.com/image/fetch/$s_!AB3S!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fac816fe0-8291-419d-8b70-a43ed9123132_1232x733.heic)](https://substackcdn.com/image/fetch/$s_!AB3S!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fac816fe0-8291-419d-8b70-a43ed9123132_1232x733.heic)

And it would initiate a new calendar.json file. 

[![](https://substackcdn.com/image/fetch/$s_!7OHv!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7fea68c4-1b82-4a33-98f2-dd492b141cad_1248x702.heic)](https://substackcdn.com/image/fetch/$s_!7OHv!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7fea68c4-1b82-4a33-98f2-dd492b141cad_1248x702.heic)

I added all the public school holidays, early release dates for 2 years in one sentence. 

[![](https://substackcdn.com/image/fetch/$s_!TsfE!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff31fdfbb-508b-44fd-9f5b-cdad823b556e_681x280.heic)](https://substackcdn.com/image/fetch/$s_!TsfE!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff31fdfbb-508b-44fd-9f5b-cdad823b556e_681x280.heic)

It works instantly — no more missed school days or forgotten early pick-up times for my kids!

You can even add your yoga classes, school schedules, favorite restaurants, or every restaurant in a given ZIP code — including their lunch specials — all using simple natural language, as long as the information is public.

Give it a try!

SKILL.md
    
    
    ---
    
    name: personal-schedule-manager
    description: >
      Create, review, and edit a `calendar.json` file for schedules and routines.
      Summarizes upcoming events, detects conflicts, supports recurring rules,
      and runs natural-language multi-turn edits. Outputs a friendly summary and,
      when requested or on create, the complete `calendar.json` to copy/replace.
      Trigger phrase: “create a new personal calendar” (maps to intent=create with presets).
    
    ---
    # ───────────────────────────────
    # Inputs
    # ───────────────────────────────
    inputs:
      - id: intent
        type: string
        required: true
        description: One of: create | review | edit | export
    
      - id: calendar_json
        type: json
        required: false
        description: Paste full current `calendar.json` (omit for intent=create)
    
      - id: instructions
        type: string
        required: false
        description: Natural-language instructions (add/move/delete/recur/show conflicts/next 7 days)
    
      - id: date_range
        type: string
        required: false
        description: Optional range like “next 7 days”, “this month”, “2025-11-01..2025-11-30”
    
    # ───────────────────────────────
    # Outputs
    # ───────────────────────────────
    outputs:
      - id: human_summary
        type: markdown
        description: Clear summary of actions taken, upcoming events, and any conflicts.
    
      - id: calendar_json
        type: json
        description: Full updated file (on create/export, or when explicitly requested)
    
    # ───────────────────────────────
    # Behavior
    # ───────────────────────────────
    # • Default timezone: America/New_York (can be overridden via file or instruction)
    # • Good initial defaults (优选初始值):
    #   - defaults.event_duration_minutes = 60
    #   - defaults.reminder_minutes_before = 30
    #   - defaults.work_hours = 09:00–17:00, MO–FR
    #   - defaults.priority = “normal”
    #   - defaults.category = “personal”
    # • Recurrence: iCalendar RRULE (e.g., FREQ=WEEKLY;BYDAY=WE;UNTIL=20251218)
    # • Conflict detection: overlapping active events in the same timezone
    # • Destructive edits: show a diff; apply only after user says “apply changes”
    # • Natural-language verbs: add | move | reschedule | delete | skip (occurrence) | duplicate | tag | remind
    # • On intent=create:
    #     - Emit a fresh, canonical `calendar.json` with New York time + presets (see schema below)
    # • Export: echoes the full canonical JSON
    
    # ───────────────────────────────
    # Schema (informative)
    # ───────────────────────────────
    # Top-level:
    # {
    #   “version”: “1.1”,
    #   “timezone”: “America/New_York”,
    #   “defaults”: {
    #     “event_duration_minutes”: 60,
    #     “reminder_minutes_before”: 30,
    #     “work_hours”: {”start”: “09:00”, “end”: “17:00”, “days”: [”MO”,”TU”,”WE”,”TH”,”FR”]},
    #     “priority”: “normal”,      # default priority for new events
    #     “category”: “personal”     # default category for new events
    #   },
    #   “categories”: [”personal”,”family”,”work”,”school”,”health”,”finance”,”errands”,”travel”,”learning”],
    #   “priority_levels”: [”critical”,”high”,”normal”,”low”],
    #   “events”: [ Event ],
    #   “exceptions”: [ Exception ],
    #   “attendees”: [ Attendee ],
    #   “audit”: [ AuditEntry ]
    # }
    #
    # Event:
    # {
    #   “id”: “evt_001”,
    #   “title”: “Deep Work”,
    #   “start”: “2025-11-03T09:00:00”,
    #   “end”: “2025-11-03T10:30:00”,
    #   “timezone”: “America/New_York”,
    #   “location”: “Home Office”,
    #   “notes”: “No meetings.”,
    #   “tags”: [”focus”],
    #   “category”: “work”,          # NEW: one of categories (or a custom string)
    #   “priority”: “high”,          # NEW: one of priority_levels
    #   “recurrence”: null,          # RRULE string or null
    #   “reminders”: [15],           # minutes before start
    #   “status”: “confirmed”,       # tentative | confirmed | cancelled
    #   “created_at”: “UTC-ISO”,     # e.g., 2025-10-30T20:00:00Z
    #   “updated_at”: “UTC-ISO”
    # }
    
    
