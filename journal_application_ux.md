# 8. UX --- What should the user see?

The MVP should have **three main screens**. Each screen should have one
clear purpose.

> **Journal = Capture**\
> **Chat = Explore**\
> **Insights = Discover**

The UX should be simple, private, and low-friction. The user should be
able to record a thought quickly without feeling like they are filling
out a complicated form.

------------------------------------------------------------------------

## 1. Journal

**Purpose:** Capture and manage the user's thoughts and experiences.

### What the user sees

-   A **Create Journal Entry** area at the top.
-   A large text input for writing their thoughts.
-   Category selection:
    -   Personal
    -   Work
    -   Health
-   A **Save** button.
-   A chronological list/timeline of previous entries.

### Journal Entry Card

Each entry can display:

-   Short preview of the content
-   Category
-   Date and time
-   Optional AI-generated tags
-   Edit action
-   Delete action

### Example

``` text
┌─────────────────────────────────────┐
│ What happened today?                │
│                                     │
│ I worked on my project today...     │
│                                     │
│ [Personal] [Work] [Health]          │
│                         [Save]      │
└─────────────────────────────────────┘

              JOURNAL

October 7
─────────────────────────────────────
Worked on my project for several hours...
Work · 4:30 PM

October 6
─────────────────────────────────────
Had a difficult conversation with...
Personal · 8:15 PM
```

### Important UX principle

The user should **not** have to manually enter:

-   Emotions
-   Topics
-   Problems
-   Goals
-   Activities
-   Patterns

The AI should extract these automatically after the entry is saved.

------------------------------------------------------------------------

## 2. Chat --- Ask About Yourself

**Purpose:** Allow the user to interact with their personal history.

This is where the user asks questions about their journal entries.

### What the user sees

A familiar chat interface:

``` text
┌─────────────────────────────────────┐
│          Ask About Yourself          │
├─────────────────────────────────────┤
│                                     │
│ You:                                │
│ Why have I been struggling lately?  │
│                                     │
│ AI:                                 │
│ I've noticed that you've mentioned  │
│ difficulty focusing several times   │
│ recently, particularly when you     │
│ have multiple tasks at once.        │
│                                     │
│ You:                                │
│ What should I change?               │
│                                     │
├─────────────────────────────────────┤
│ Ask something about yourself...     │
│                              [Send]  │
└─────────────────────────────────────┘
```

### Example questions

Users can ask:

-   "What have I been struggling with recently?"
-   "What problems keep repeating?"
-   "What have I improved at?"
-   "What have I been working on?"
-   "What makes me productive?"
-   "What patterns do you notice?"
-   "What goals have I mentioned?"

### Important UX principle

The chat should answer based on the user's **own journal data**, rather
than giving generic self-help advice.

------------------------------------------------------------------------

## 3. Insights

**Purpose:** Show patterns the system has already discovered.

Unlike Chat, the user does not need to ask a question.

The system proactively presents meaningful observations from their
journal history.

### What the user sees

A collection of simple insight cards.

``` text
                 INSIGHTS

┌─────────────────────────────────────┐
│ Focus Pattern                       │
│                                     │
│ You've mentioned difficulty         │
│ focusing 5 times this month.        │
│                                     │
│ This usually happened when you      │
│ were working on multiple tasks.     │
│                                     │
│              [View Entries]         │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│ Progress                            │
│                                     │
│ You've recently mentioned finishing │
│ tasks more consistently.            │
│                                     │
│              [Explore]              │
└─────────────────────────────────────┘
```

### Types of insights

The MVP can focus on:

-   Recurring problems
-   Repeated emotions
-   Common topics
-   Recurring goals
-   Behavioral patterns
-   Changes over time
-   Signs of improvement

------------------------------------------------------------------------

# Navigation

The MVP only needs three primary navigation items:

``` text
┌──────────────────────────────────────┐
│                                      │
│              Application             │
│                                      │
│   Journal    Chat    Insights        │
│                                      │
└──────────────────────────────────────┘
```

The user can move between the three areas at any time.

------------------------------------------------------------------------

# Overall User Experience

The three screens form a simple loop:

``` text
          ┌─────────────┐
          │   JOURNAL   │
          │   Capture   │
          └──────┬──────┘
                 │
                 ▼
          ┌─────────────┐
          │     AI      │
          │ Understand  │
          └──────┬──────┘
                 │
          ┌──────┴──────┐
          ▼             ▼
   ┌────────────┐  ┌────────────┐
   │    CHAT    │  │  INSIGHTS  │
   │   Explore  │  │  Discover  │
   └─────┬──────┘  └──────┬─────┘
         │                │
         └───────┬────────┘
                 ▼
             REFLECTION
                 │
                 ▼
              IMPROVE
```

## UX Principle

> **The user should spend their effort expressing themselves and
> reflecting---not organizing their data.**

The application handles the complexity of:

**Organizing → Analyzing → Searching → Connecting → Finding patterns**

while the user simply:

**Writes → Asks → Reflects → Improves.**
