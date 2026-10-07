# 9. ARCHITECTURE --- How should the system work?

The MVP should use a **simple modular architecture** that separates the
frontend, backend, database, and AI processing.

The goal is to keep the system easy to understand and extend without
overengineering it.

------------------------------------------------------------------------

## 1. High-Level Architecture

``` text
┌──────────────────────┐
│       Angular        │
│      Frontend        │
│                      │
│ Journal │ Chat │     │
│ Insights│ Auth       │
└──────────┬───────────┘
           │ HTTPS / REST API
           ▼
┌──────────────────────┐
│      NestJS API      │
│       Backend        │
│                      │
│ Auth Module          │
│ Journal Module       │
│ AI Module            │
│ Chat Module          │
│ Insights Module      │
└───────┬─────────┬────┘
        │         │
        ▼         ▼
┌────────────┐  ┌─────────────┐
│  MongoDB   │  │  AI Service │
│            │  │             │
│ Users      │  │ LLM / API   │
│ Journals   │  │             │
│ Analysis   │  └─────────────┘
└────────────┘
```

------------------------------------------------------------------------

# 2. Frontend --- Angular

The frontend is responsible for the **user experience**.

### Main areas

-   **Authentication**
    -   Sign up
    -   Sign in
    -   Logout
-   **Journal**
    -   Create entry
    -   View entries
    -   Edit entry
    -   Delete entry
    -   Select category
-   **Chat**
    -   Ask questions about personal history
    -   Display AI responses
    -   Maintain the current conversation
-   **Insights**
    -   Display discovered patterns
    -   Show recurring problems
    -   Show trends and improvements

### Frontend principle

> The frontend should primarily handle **interaction and presentation**.
> Business logic and AI processing should remain on the backend.

------------------------------------------------------------------------

# 3. Backend --- NestJS

NestJS acts as the **main application server**.

It is responsible for:

-   Authentication
-   Authorization
-   Journal CRUD
-   User data isolation
-   AI orchestration
-   Chat processing
-   Insights
-   Validation
-   Error handling
-   Security

The backend should be divided into modules rather than putting
everything into one large service.

### Suggested modules

``` text
src/
├── auth/
├── users/
├── journal/
├── ai/
├── chat/
├── insights/
└── common/
```

------------------------------------------------------------------------

# 4. Authentication Flow

For the MVP:

``` text
User
 ↓
Angular
 ↓
POST /auth/login
 ↓
NestJS
 ↓
Validate credentials
 ↓
Generate JWT
 ↓
Angular stores token
 ↓
Token sent with protected requests
```

Protected requests should look conceptually like:

``` text
Authorization: Bearer <JWT>
```

The backend validates the token before allowing access to private
resources.

### Important rule

Every journal-related request must be associated with the authenticated
user.

For example:

``` text
GET /journal
```

must return:

> **Only the authenticated user's entries.**

Never trust a `userId` sent from the frontend to determine ownership.

------------------------------------------------------------------------

# 5. Journal Architecture

The journal is the foundation of the entire application.

### Create flow

``` text
User writes entry
       ↓
Angular
       ↓
POST /journal
       ↓
NestJS validates request
       ↓
Save original entry
       ↓
MongoDB
       ↓
Return success to user
```

The original journal entry should be treated as the **source of truth**.

------------------------------------------------------------------------

# 6. AI Entry Analysis

AI analysis should be a **separate process from saving the journal
entry**.

Do not make the user wait for the AI before the journal is saved.

Instead:

``` text
User creates entry
       ↓
NestJS
       ↓
Save journal entry
       ↓
Return response
       │
       └──────────────► AI Analysis
                              ↓
                         Analyze entry
                              ↓
                         Store analysis
```

For example:

``` text
Journal Entry
─────────────
"I couldn't focus on my project today..."

              ↓ AI

Analysis
────────
Topic: Project
Emotion: Frustration
Problem: Lack of focus
Activity: Programming
```

The analysis is stored separately or as a structured part of the journal
data.

### Important principle

> **The user's original text is permanent source data. AI analysis is
> derived data.**

This means you can re-run the AI analysis later without losing the
original journal.

------------------------------------------------------------------------

# 7. AI Service

Create an AI abstraction inside the backend instead of directly calling
an AI provider everywhere.

For example:

``` text
AIService
   │
   ├── analyzeJournalEntry()
   ├── answerQuestion()
   └── generateInsights()
```

This is important because you may change AI providers later.

For example:

``` text
NestJS
   ↓
AIService
   ↓
┌───────────────┐
│ AI Provider   │
│               │
│ Gemini        │
│ Groq          │
│ OpenAI        │
└───────────────┘
```

Your application should depend on **your AI interface**, not directly on
one provider.

------------------------------------------------------------------------

# 8. Personal AI Chat

Chat works differently from individual entry analysis.

### Entry analysis

``` text
One journal entry
        ↓
AI analysis
        ↓
Structured information
```

### Chat

``` text
User question
      ↓
Find relevant journal information
      ↓
Retrieve relevant entries / analysis
      ↓
Give context to AI
      ↓
Generate answer
      ↓
Return answer
```

Example:

``` text
User:
"What has been affecting my productivity?"

          ↓

Backend
          ↓

Search user's journal history
          ↓

Relevant entries
          ↓

AI
          ↓

"Your entries suggest that your productivity
drops when you take on too many tasks..."
```

The AI should **not blindly receive the entire database** for every
question.

------------------------------------------------------------------------

# 9. Insights Architecture

Insights are based on **multiple journal entries**.

``` text
Journal Entries
      ↓
Structured AI Analysis
      ↓
Pattern Detection
      ↓
Insight
      ↓
MongoDB
      ↓
Angular Insights Screen
```

Example:

``` text
Entry 1 → Difficulty focusing
Entry 2 → Too many tasks
Entry 3 → Difficulty focusing
Entry 4 → Feeling overwhelmed
Entry 5 → Too many tasks

              ↓

        Pattern detected

              ↓

"You frequently experience
difficulty focusing when
handling multiple tasks."
```

------------------------------------------------------------------------

# 10. Database --- MongoDB

For the MVP, MongoDB fits the application's flexible data.

At a high level:

``` text
User
 │
 └── Journal Entries
       │
       └── AI Analysis
```

Possible collections:

``` text
users
journal_entries
conversations
messages
insights
```

You don't necessarily need all of these immediately.

### MVP starting point

Start with:

``` text
users
journal_entries
```

Then introduce:

``` text
conversations
messages
insights
```

when those features are implemented.

------------------------------------------------------------------------

# 11. Data Ownership

This is one of the most important architectural rules.

Every personal resource must belong to a user.

For example:

``` text
JournalEntry
{
    _id,
    userId,
    content,
    category,
    createdAt,
    updatedAt,
    analysis
}
```

When retrieving data:

``` text
find({
    userId: authenticatedUserId
})
```

Not:

``` text
find({
    userId: request.body.userId
})
```

The backend determines the owner from the authenticated JWT.

------------------------------------------------------------------------

# 12. Asynchronous AI Processing

AI processing can be slow and unreliable compared with normal database
operations.

Therefore:

**Journal creation should not depend on AI completion.**

The desired behavior is:

``` text
                    ┌──► MongoDB
                    │
User → API ─────────┤
                    │
                    └──► AI Processing
```

The user should receive:

``` text
"Journal saved successfully."
```

without waiting for the entire AI analysis.

For the very first MVP, this can be implemented simply. As the system
grows, you can introduce:

``` text
Queue
  ↓
Worker
  ↓
AI Processing
```

using something such as Redis + BullMQ.

**Don't introduce a queue just because it sounds scalable. Add it when
asynchronous workload actually requires it.**

------------------------------------------------------------------------

# 13. API Structure

Keep the API resource-oriented.

For example:

``` text
POST   /auth/register
POST   /auth/login
POST   /auth/logout

POST   /journal
GET    /journal
GET    /journal/:id
PATCH  /journal/:id
DELETE /journal/:id

POST   /chat
GET    /insights
```

The exact endpoints can evolve during implementation.

------------------------------------------------------------------------

# 14. MVP Architecture Principle

Don't build the architecture for millions of users on day one.

Build for:

``` text
Correctness
     ↓
Security
     ↓
Maintainability
     ↓
Performance
     ↓
Scalability
```

Start with:

**Angular → NestJS → MongoDB → AI Provider**

Then introduce additional infrastructure only when the requirements
justify it.

------------------------------------------------------------------------

# Final Architecture

The complete MVP can therefore be summarized as:

``` text
                    USER
                      │
                      ▼
                ┌──────────┐
                │ Angular  │
                └────┬─────┘
                     │
                  HTTPS
                     │
                     ▼
                ┌──────────┐
                │ NestJS   │
                │   API    │
                └────┬─────┘
                     │
          ┌──────────┼──────────┐
          │          │          │
          ▼          ▼          ▼
       MongoDB    AI Service   Auth
          │          │
          │          ▼
          │      AI Provider
          │
          ▼
   Journal / Analysis
          │
          ├──────────────► Chat
          │
          └──────────────► Insights
```

### The architectural idea in one sentence

> **Angular handles interaction, NestJS controls the application and
> business logic, MongoDB stores the user's personal data and derived
> analysis, and an AI service transforms that data into useful
> understanding.**

This gives you a clean foundation without prematurely introducing Redis,
queues, microservices, WebSockets, or other infrastructure that the MVP
doesn't yet require.
