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


------------------------------------------------------------------------

# 11. VISUAL DESIGN SYSTEM — Color Palette

The journal application should use a **Midnight + Warm Amber** visual
identity.

The overall personality should feel:

- Calm
- Intelligent
- Personal
- Cinematic
- Premium
- Private

The interface should feel like a quiet space for reflection rather than
a generic productivity dashboard or a neon "AI SaaS" application.

## Core Color Palette

| Color | Hex | Primary Usage | Purpose |
|---|---|---|---|
| Midnight | `#0F1115` | Main app/page background | Deep, calm, private foundation |
| Charcoal | `#171A21` | Sidebar, navbar, secondary sections, inputs | Creates visual separation |
| Card | `#1D2129` | Journal cards, chat cards, insight cards, modals | Content containers |
| Border | `#2A2E37` | Inputs, cards, dividers, separators | Subtle structure |
| Warm White | `#F4F1EA` | Headings, primary text, journal content | Comfortable readable text |
| Muted Gray | `#9A9DA5` | Descriptions, timestamps, placeholders | Secondary information |
| Amber | `#D9A441` | Primary buttons, active states, selected items | Main brand/action color |
| Light Amber | `#F0C674` | Hover states, highlights, important insight text | Secondary amber emphasis |
| Success Green | `#7FAF8A` | Improving/success states | Positive progress |
| Warning | `#C98B5B` | Warnings and attention states | Caution |
| Error | `#C96B6B` | Errors and destructive actions | Danger |

## UI Color Usage

| UI Element | Color |
|---|---|
| App background | `#0F1115` |
| Sidebar / Navbar | `#171A21` |
| Journal card | `#1D2129` |
| Chat message card | `#1D2129` |
| Input background | `#171A21` |
| Input border | `#2A2E37` |
| Input focus border | `#D9A441` |
| Heading | `#F4F1EA` |
| Normal text | `#F4F1EA` |
| Description text | `#9A9DA5` |
| Timestamp | `#9A9DA5` |
| Primary button | `#D9A441` |
| Primary button text | `#0F1115` |
| Primary button hover | `#F0C674` |
| Selected navigation item | `#D9A441` |
| Selected navigation background | `rgba(217, 164, 65, 0.10)` |
| Links | `#F0C674` |
| AI indicator | `#D9A441` |
| Insight icon/highlight | `#F0C674` |
| Improving insight | `#7FAF8A` |
| Warning state | `#C98B5B` |
| Error/Delete | `#C96B6B` |
| Dividers | `#2A2E37` |

## Color Proportion

The palette should remain restrained:

```text
#0F1115  → ~60% → Main environment
#171A21  → ~20% → Sections / inputs
#1D2129  → ~15% → Content cards
#F4F1EA  → Text
#D9A441  → ~5%  → Actions / attention
```

The **amber color should not dominate the interface**.

It should behave like a warm light inside a dark room: users notice it
when something is actionable, selected, important, or insightful.

## Screen-Specific Usage

### Journal — Capture

Use:

- `#0F1115` for the page background
- `#171A21` for the writing/input area
- `#1D2129` for journal entry cards
- `#F4F1EA` for journal text
- `#9A9DA5` for timestamps and secondary information
- `#D9A441` only for save, selection, focus, and active states

The Journal screen should feel **quiet and distraction-free**.

### Chat — Explore

Use:

- `#0F1115` as the main background
- `#1D2129` for conversation/message containers
- `#F4F1EA` for readable conversation text
- `#9A9DA5` for metadata and secondary text
- `#D9A441` for the AI indicator and important interactive states

The Chat screen should feel **focused and conversational**, not like a
generic AI chatbot.

### Insights — Discover

Use:

- `#0F1115` as the background
- `#1D2129` for insight cards
- `#F4F1EA` for insight titles and descriptions
- `#F0C674` for discovery/highlight elements
- `#7FAF8A` for improving/progress states
- `#C98B5B` for attention/warning states

The Insights screen can use **slightly more amber** than the Journal and
Chat screens because this is where the product's "discovery" value is
most visible.

## Design Rule

Do not use amber on every button, card, icon, or heading.

The visual hierarchy should communicate:

**Darkness → Reflection → Warm highlight → Insight**

The design identity should ultimately feel like:

> **A quiet, cinematic space for understanding yourself.**
