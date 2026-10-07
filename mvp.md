## 5. MVP — What is the smallest useful version?

The MVP should prove one core assumption:

> **If users can easily record their thoughts and later ask questions about their personal history, will they find the resulting insights useful?**

Therefore, the MVP should focus on **capturing thoughts, storing them, and turning them into searchable insights**. Features that do not help validate this core value should be postponed.

### Core MVP Features

- **User Authentication**
  - Users can securely create an account and sign in.
  - Journal data is private to each user.

- **Simple Journal Entry**
  - Users can create an entry using:
    - Text
    - Optional mood
    - Optional category
  - The entry should be quick and frictionless.

- **Journal History**
  - Users can view their previous entries.
  - Entries should be organized by date.
  - Users can search their history.

- **AI Entry Analysis**
  - When an entry is created, AI extracts useful information such as:
    - Emotions
    - Topics
    - Goals
    - Problems
    - Important events
    - Ideas
  - This information is stored alongside the original entry.

- **AI Personal Assistant**
  - Users can ask questions about their own journal history.
  - Example:
    - *“What have I been struggling with recently?”*
    - *“What goals have I mentioned?”*
    - *“What made me productive this week?”*
    - *“What patterns do you notice?”*

- **Basic Insights**
  - The system identifies simple recurring patterns across entries.
  - Example:
    > “You mentioned feeling overwhelmed several times when working on multiple tasks.”

- **Basic Reflection Prompts**
  - Provide optional prompts when the user doesn't know what to write.
  - Example:
    - *“What was the most important thing that happened today?”*
    - *“What did you learn today?”*
    - *“What would you do differently?”*

### What the MVP should NOT include

To keep the MVP small, postpone features such as:

- Complex dashboards and charts
- Social features
- Gamification and leaderboards
- Advanced habit tracking
- Voice transcription
- Wearable/device integrations
- Highly detailed personality analysis
- Complex recommendation systems
- Multiple AI agents
- Extensive customization
- Mobile applications

These can be added **after validating that users actually find the core experience valuable.**

### MVP User Journey

```text
Sign Up
   ↓
Write a thought
   ↓
Save Journal Entry
   ↓
AI analyzes the entry
   ↓
Personal information is stored
   ↓
User continues journaling
   ↓
User asks a question
   ↓
AI searches their personal history
   ↓
AI provides an insight
```

### MVP Success Criteria

The MVP is successful if users:

- **Actually return and record thoughts**
- **Find the AI's answers useful and personally relevant**
- **Discover something about themselves that they hadn't noticed**
- **Use the insights to reflect or make a decision**
- **Trust the application enough to record personal information**

### The MVP in one sentence

> **A private AI journal where users can quickly record their thoughts and later ask questions about their personal history to discover meaningful patterns and insights.**

This is the version I would build first. **Don't try to build the complete “AI life coach” yet.** First prove that the fundamental loop—**capture → remember → ask → discover**—actually creates value.