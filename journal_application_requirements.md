# 7. REQUIREMENTS --- What must the system do?

The MVP requirements should describe **what the system must be capable
of doing**, without deciding the implementation details yet.

## A. Authentication & User Management

-   The system must allow users to **sign up using email and password**.
-   The system must allow registered users to **sign in**.
-   The system must authenticate users using **JWT**.
-   The system must ensure that a user can access **only their own
    journal data**.
-   The system must allow users to **log out**.
-   Passwords must be **securely hashed** before being stored.
-   Each email address must belong to only one account.

> **MVP:** Keep authentication simple. Token rotation and blacklisting
> can be introduced later.

------------------------------------------------------------------------

## B. Journal Entry Management

The system must allow users to manage their personal journal entries.

-   Users must be able to **create** a journal entry.
-   An entry must contain:
    -   Text/content
    -   Category
    -   Creation date/time
-   The initial categories should be:
    -   **Personal**
    -   **Work**
    -   **Health**
-   Users must be able to **view** their entries.
-   Users must be able to **edit** their entries.
-   Users must be able to **delete** their entries.
-   Users must only be able to modify their own entries.

------------------------------------------------------------------------

## C. Journal History

The system must provide a clear way for users to explore their previous
entries.

-   Entries should be displayed in **chronological order**.
-   Users should be able to see when each entry was created.
-   Users should be able to open an entry to view its complete content.
-   Users should be able to navigate through their journal history.

### Later enhancement

-   Search
-   Category filtering
-   Date filtering
-   Sorting

These are useful, but they don't need to complicate the first version.

------------------------------------------------------------------------

## D. AI Entry Analysis

The system must be able to analyze an individual journal entry.

When a user creates an entry:

-   The system sends the entry for AI analysis.
-   AI identifies useful information from the entry, such as:
    -   Topics
    -   Emotions
    -   Activities
    -   Problems
    -   Goals
    -   Important events
    -   Ideas
-   The extracted information must be **stored with the journal entry**.
-   The original journal content must remain unchanged.
-   AI-generated information must be treated as **analysis**, not as the
    user's original words.

For example:

``` text
Journal Entry
    ↓
"I couldn't focus on my project today..."
    ↓
AI Analysis
    ├── Topic: Project
    ├── Emotion: Frustration
    ├── Activity: Programming
    └── Problem: Lack of focus
```

This structured information becomes useful later when the system
analyzes **multiple entries**.

------------------------------------------------------------------------

## E. Personal AI Chat

The system must allow users to ask questions about their own journal
history.

For example:

-   *"What have I been struggling with recently?"*
-   *"What problems keep appearing?"*
-   *"What have I been working on?"*
-   *"What patterns do you notice?"*
-   *"What have I improved at?"*

The system should:

1.  Receive the user's question.
2.  Find relevant information from their journal history.
3.  Analyze the relevant entries.
4.  Generate an answer based on the user's own data.
5.  Clearly distinguish between **information found in the journal** and
    AI interpretation.

------------------------------------------------------------------------

## F. Personal Insights

The system should eventually identify patterns across multiple entries.

For example:

> "You mentioned difficulty focusing four times in the past two weeks,
> usually when working on multiple tasks."

The system should be able to identify:

-   Recurring problems
-   Repeated emotions
-   Common topics
-   Recurring goals
-   Behavioral patterns
-   Changes over time

This is where the **main value of the product** begins to appear.

------------------------------------------------------------------------

## G. Privacy & Security

Because journal entries may contain extremely personal information:

-   Users must only access their own data.
-   Journal data must be protected from unauthorized access.
-   Authentication must be required for private data.
-   Sensitive data should not be unnecessarily exposed to other users or
    services.
-   AI processing should follow a clearly defined privacy policy.
-   The system should clearly communicate how user data is stored and
    processed.

**Privacy is not an optional enhancement for this product. It is a core
requirement.**

------------------------------------------------------------------------

# MVP Requirement Summary

  Area             MVP must support
  ---------------- -------------------------------------
  Authentication   Sign up, sign in, JWT, logout
  Journal          Create, view, edit, delete
  Categories       Personal, Work, Health
  History          Chronological journal timeline
  AI Analysis      Analyze individual entries
  AI Data          Store extracted information
  AI Chat          Ask questions about journal history
  Insights         Basic cross-entry patterns
  Security         User-level data isolation

## The Most Important Requirement

Everything ultimately needs to support this loop:

**Capture → Understand → Remember → Ask → Discover → Improve**

If a feature doesn't contribute to that loop, it probably **doesn't
belong in the MVP**.

> **Requirements define what the system must do.**\
> After this, translate the requirements into **technical requirements →
> architecture → database design → API design → stack choices**.
