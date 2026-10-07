# 10. DATA --- What information do we store?

The system stores two kinds of information:

1.  **User-generated data** --- information directly created by the
    user.
2.  **System-generated data** --- information derived or created by the
    application and AI.

The user's original journal content must always remain the **source of
truth**. AI-generated information is derived data and can be regenerated
or updated later.

------------------------------------------------------------------------

## 1. User

Stores the information required to identify and authenticate a user.

### Fields

-   `id`
    -   Unique identifier for the user.
    -   Primary key.
-   `email`
    -   User's email address.
    -   Must be unique.
-   `username`
    -   User's display/identity name.
-   `passwordHash`
    -   Hashed password.
    -   Never store the plain-text password.
-   `createdAt`
    -   Account creation timestamp.
-   `updatedAt`
    -   Last account update timestamp.

### Relationships

``` text
User
 ├── has many Journal Entries
 ├── has many Conversations
 └── has many Insights
```

### Important

Do **not** store JWT access tokens in the `User` table for the MVP.

Token rotation and token blacklisting can be introduced later if
required.

------------------------------------------------------------------------

# 2. Journal Entry

The journal entry is the **primary user-generated data** and the source
of truth for the user's experiences.

### Fields

-   `id`
    -   Unique identifier.
    -   Primary key.
-   `userId`
    -   Identifies the owner of the journal entry.
    -   Foreign key → `User.id`.
-   `content`
    -   The original text written by the user.
-   `category`
    -   The user's selected category.
    -   MVP categories:
        -   `PERSONAL`
        -   `WORK`
        -   `HEALTH`
-   `createdAt`
    -   When the entry was created.
-   `updatedAt`
    -   When the entry was last modified.

### Example

``` text
JournalEntry
────────────────────────
id:        101
userId:    25
content:   "I worked on my project..."
category:  WORK
createdAt: 2026-10-07 15:30
updatedAt: 2026-10-07 15:30
```

### Important principle

> **Never replace or modify the original journal content with
> AI-generated information.**

The original entry represents what the user actually said.

------------------------------------------------------------------------

# 3. Journal Analysis

Journal Analysis contains information extracted by AI from an individual
journal entry.

It is **derived data**, not the original user data.

### Fields

-   `id`
    -   Unique identifier.
    -   Primary key.
-   `journalId`
    -   Identifies the journal entry being analyzed.
    -   Foreign key → `JournalEntry.id`.
-   `topics`
    -   Topics identified in the entry.
-   `emotions`
    -   Possible emotions expressed in the entry.
-   `activities`
    -   Activities mentioned in the entry.
-   `problems`
    -   Problems or difficulties identified.
-   `goals`
    -   Goals mentioned by the user.
-   `events`
    -   Important events mentioned.
-   `ideas`
    -   Ideas or thoughts that may be useful later.
-   `createdAt`
    -   When the analysis was generated.
-   `updatedAt`
    -   When the analysis was last updated.

### Example

``` text
Journal Entry
      ↓
"I couldn't focus on my project today.
I kept checking social media."

      ↓ AI Analysis

Journal Analysis
────────────────────────
topics:     ["project", "productivity"]
emotions:   ["frustration"]
activities: ["programming", "social media"]
problems:   ["lack of focus"]
goals:      []
events:     []
ideas:      []
```

### Relationship

``` text
User
  │
  └── Journal Entry
          │
          └── Journal Analysis
```

One journal entry has **one analysis**.

The analysis does not need its own `userId` because ownership can be
determined through the journal entry.

------------------------------------------------------------------------

# 4. Conversation

A Conversation represents one chat session between the user and the AI.

### Fields

-   `id`
    -   Unique identifier.
    -   Primary key.
-   `userId`
    -   Identifies the owner of the conversation.
    -   Foreign key → `User.id`.
-   `title`
    -   Optional title for the conversation.
    -   Can be generated later from the first messages.
-   `createdAt`
    -   When the conversation was created.
-   `updatedAt`
    -   When the conversation was last updated.

### Relationship

``` text
User
  │
  └── has many Conversations
             │
             └── has many Messages
```

------------------------------------------------------------------------

# 5. Message

A Message represents an individual message inside a conversation.

### Fields

-   `id`
    -   Unique identifier.
    -   Primary key.
-   `conversationId`
    -   Identifies the conversation.
    -   Foreign key → `Conversation.id`.
-   `role`
    -   Identifies who produced the message.
    -   Possible values:
        -   `USER`
        -   `ASSISTANT`
-   `content`
    -   Message text.
-   `createdAt`
    -   When the message was created.

### Example

``` text
Conversation
      │
      ├── Message
      │     role: USER
      │     content: "What has been affecting my productivity?"
      │
      └── Message
            role: ASSISTANT
            content: "Your journal suggests..."
```

Messages generally do not need `updatedAt` because chat messages should
normally be immutable after creation.

------------------------------------------------------------------------

# 6. Insight

An Insight represents a **pattern, observation, or change discovered
across multiple journal entries**.

It is not a journal entry and it is not a fact directly written by the
user.

It is **derived information** created by the system.

### Fields

-   `id`
    -   Unique identifier.
    -   Primary key.
-   `userId`
    -   Identifies the owner.
    -   Foreign key → `User.id`.
-   `type`
    -   Type of insight.
    -   Examples:
        -   `RECURRING_PROBLEM`
        -   `PATTERN`
        -   `PROGRESS`
        -   `EMOTION_TREND`
        -   `GOAL`
-   `title`
    -   Short description of the insight.
-   `description`
    -   Detailed explanation of the pattern.
-   `status`
    -   Current state of the insight.
    -   Examples:
        -   `ACTIVE`
        -   `IMPROVING`
        -   `RESOLVED`
-   `createdAt`
    -   When the insight was first generated.
-   `updatedAt`
    -   When the insight was last evaluated or updated.

### Example

``` text
Insight
────────────────────────────────────
type:        RECURRING_PROBLEM
title:       Difficulty focusing
description: You frequently mentioned
             difficulty focusing when
             handling multiple tasks.
status:      IMPROVING
```

### Important principle

An insight should **not claim certainty about the user's life**.

Instead of:

> "Your focus problem is solved."

Prefer:

> "Your journal shows fewer mentions of focus problems over the past
> month."

The insight is an interpretation based on available journal data.

------------------------------------------------------------------------

# 7. How the Data Connects

The overall relationship looks like this:

``` text
                         USER
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
         JOURNALS     CONVERSATIONS    INSIGHTS
             │             │
             ▼             ▼
        AI ANALYSIS     MESSAGES
```

More specifically:

``` text
User
 │
 ├── 1 ──── N ──► JournalEntry
 │                    │
 │                    └── 1 ──── 1 ──► JournalAnalysis
 │
 ├── 1 ──── N ──► Conversation
 │                    │
 │                    └── 1 ──── N ──► Message
 │
 └── 1 ──── N ──► Insight
```

------------------------------------------------------------------------

# 8. Source Data vs Derived Data

This distinction is extremely important for the architecture.

## Source Data

Data directly provided by the user:

``` text
User
JournalEntry
Message
```

This data should be treated as authoritative.

## Derived Data

Data generated by the system or AI:

``` text
JournalAnalysis
Insight
```

Derived data can be:

-   Re-generated
-   Updated
-   Corrected
-   Re-analyzed with a better AI model

without modifying the original journal entry.

------------------------------------------------------------------------

# 9. MVP Data Model

The initial database can therefore contain these six tables:

  Table               Purpose
  ------------------- ------------------------------------------------
  `User`              User account and authentication
  `JournalEntry`      Original user journal content
  `JournalAnalysis`   AI analysis of an individual entry
  `Conversation`      Chat session
  `Message`           Individual chat messages
  `Insight`           Patterns and observations discovered over time

### Relationship Summary

``` text
User
 │
 ├──< JournalEntry ──1:1── JournalAnalysis
 │
 ├──< Conversation ──1:N── Message
 │
 └──< Insight
```

------------------------------------------------------------------------

# 10. Data Flow

The data flows through the system like this:

``` text
User writes something
        ↓
JournalEntry
        ↓
AI analyzes the entry
        ↓
JournalAnalysis
        ↓
More entries accumulate
        ↓
System analyzes patterns
        ↓
Insight
        ↓
User views Insights
```

For Chat:

``` text
User asks a question
        ↓
Message
        ↓
Backend retrieves relevant
journal data / analysis
        ↓
AI generates answer
        ↓
Assistant Message
```

------------------------------------------------------------------------

# Core Data Principle

> **Store what the user said, derive what the system understands, and
> never confuse the two.**

This gives the application a reliable foundation:

**User Data → AI Analysis → Long-Term Insights → Personal Reflection**
