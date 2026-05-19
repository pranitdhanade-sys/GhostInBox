# GhostInBox

An autonomous email-replying personality agent is essentially a **personal executive AI**.


# High-Level Architecture

```text id="nxxv86"
                         ┌────────────────────┐
                         │ Email Providers    │
                         │ Gmail / Outlook    │
                         └─────────┬──────────┘
                                   │
                                   ▼
                    ┌─────────────────────────┐
                    │ Email Ingestion Layer   │
                    │ webhook + polling       │
                    └──────────┬──────────────┘
                               │
                               ▼
                 ┌─────────────────────────────┐
                 │ Conversation Orchestrator   │
                 │ Agent Runtime               │
                 └──────────┬──────────────────┘
                            │
      ┌─────────────────────┼─────────────────────┐
      ▼                     ▼                     ▼

┌───────────────┐   ┌────────────────┐   ┌────────────────┐
│ Personality   │   │ Memory Engine  │   │ Safety Engine  │
│ Engine        │   │                │   │                │
│               │   │ - relationships│   │ - approval req │
│ - tone        │   │ - past mails   │   │ - hallucination│
│ - style       │   │ - user prefs   │   │ - risk scoring │
│ - humor       │   │ - emotional ctx│   │ - fraud detect │
└──────┬────────┘   └──────┬─────────┘   └────────┬───────┘
       │                   │                      │
       └────────────┬──────┴──────────────┬──────┘
                    ▼                     ▼

           ┌────────────────────┐
           │ Cognitive Planner  │
           │                    │
           │ - classify intent  │
           │ - decide strategy  │
           │ - draft response   │
           │ - schedule actions │
           └─────────┬──────────┘
                     │
                     ▼

           ┌────────────────────┐
           │ LLM Core           │
           │ GPT / Claude       │
           └─────────┬──────────┘
                     │
                     ▼

          ┌──────────────────────┐
          │ Approval Workflow    │
          │ Human-in-the-loop    │
          └─────────┬────────────┘
                    │
         ┌──────────┴───────────┐
         ▼                      ▼
 Auto-send low risk      Human approve
```

---

# Recommended Folder Structure

```text id="wobc6w"
executive-ai/
│
├── apps/
│   ├── api/
│   ├── dashboard/
│   ├── email-worker/
│   └── mobile/
│
├── agents/
│   ├── orchestrator/
│   ├── email_agent/
│   ├── planner/
│   ├── reflection/
│   ├── relationship_agent/
│   ├── safety_agent/
│   └── approval_agent/
│
├── personality/
│   ├── profiles/
│   ├── speech_patterns/
│   ├── tone_models/
│   ├── emotional_model/
│   └── identity_state/
│
├── memory/
│   ├── episodic/
│   ├── semantic/
│   ├── email_threads/
│   ├── relationship_graph/
│   ├── embeddings/
│   └── retrieval/
│
├── email/
│   ├── gmail/
│   ├── outlook/
│   ├── parsing/
│   ├── classification/
│   ├── threading/
│   └── signatures/
│
├── safety/
│   ├── hallucination/
│   ├── phishing/
│   ├── risk_scoring/
│   ├── approvals/
│   └── policy_engine/
│
├── workflows/
│   ├── autoresponder/
│   ├── escalation/
│   ├── scheduling/
│   └── followups/
│
├── tools/
│   ├── calendar/
│   ├── contacts/
│   ├── crm/
│   ├── browser/
│   └── search/
│
├── models/
│   ├── llm/
│   ├── embeddings/
│   ├── classifiers/
│   └── rerankers/
│
├── infra/
│   ├── docker/
│   ├── kubernetes/
│   ├── terraform/
│   └── monitoring/
│
├── datasets/
│   ├── historical_emails/
│   ├── writing_samples/
│   ├── contacts/
│   └── metadata/
│
├── configs/
├── docs/
├── tests/
└── README.md
```

---

# Email Cognition Pipeline

```text id="rtb3ce"
NEW EMAIL
    │
    ▼
Email Parsing
    │
    ▼
Intent Classification
    │
    ├── urgent?
    ├── emotional?
    ├── financial?
    ├── scheduling?
    ├── spam?
    └── requires approval?
    │
    ▼
Relationship Retrieval
    │
    ▼
Memory Retrieval
    │
    ▼
Personality Conditioning
    │
    ▼
Response Planning
    │
    ▼
Risk Analysis
    │
    ▼
Generate Draft
    │
    ▼
Confidence Scoring
    │
    ├── low risk → auto send
    └── high risk → human approval
```

---

# Core Algorithms

# 1. Relationship Modeling Algorithm

The AI must understand how “you” relate to people.

```json id="q6z1jo"
{
  "contact": "Sarah",
  "relationship": {
    "type": "coworker",
    "trust_level": 0.91,
    "formality": 0.72,
    "response_style": "concise",
    "emotional_tone": "warm-professional"
  }
}
```

---

# 2. Email Risk Scoring

Critical for autonomy.

```text id="3w8xxi"
risk_score =
(
 financial_risk * 0.35 +
 legal_risk * 0.25 +
 emotional_sensitivity * 0.20 +
 ambiguity * 0.10 +
 external_domain * 0.10
)
```

---

# 3. Personality Conditioning

```text id="md9j11"
SYSTEM PROMPT
    +
PERSONALITY PROFILE
    +
RELATIONSHIP CONTEXT
    +
PAST THREAD STYLE
    +
CURRENT EMOTIONAL STATE
```

---

# 4. Memory Retrieval Ranking

```text id="6f8a0n"
score =
 semantic_similarity * 0.40 +
 relationship_relevance * 0.30 +
 recency * 0.20 +
 emotional_weight * 0.10
```

---

# Multi-Agent System

```text id="5y8nww"
                    MASTER AGENT
                           │
 ┌─────────────────────────┼────────────────────────┐
 ▼                         ▼                        ▼

EMAIL AGENT          SAFETY AGENT           RELATIONSHIP AGENT
- draft reply        - fraud detection      - social memory
- summarize          - approval routing     - interaction style
- schedule            - hallucination       - emotional modeling

          ┌──────────────────────────┐
          ▼                          ▼

   REFLECTION AGENT          CALENDAR AGENT
   - improve style           - meetings
   - learn preferences       - availability
```

---

# Human Approval System

Autonomous email systems MUST have this.

```text id="6z4r6x"
IF:
- legal language detected
- money involved
- contracts detected
- emotional conflict detected
- confidence < threshold

THEN:
→ require approval
```

---

# Recommended Tech Stack

| Layer             | Recommended                 |
| ----------------- | --------------------------- |
| LLM               | OpenAI GPT-4.1              |
| Agent Runtime     | LangGraph                   |
| Email Integration | Gmail API + Microsoft Graph |
| Memory DB         | PostgreSQL + pgvector       |
| Vector DB         | Qdrant                      |
| Queue             | Redis                       |
| Backend           | FastAPI                     |
| Workflow Engine   | Temporal                    |
| Auth              | OAuth2                      |
| Monitoring        | LangSmith                   |
| Deployment        | Kubernetes                  |

---

# Gmail Integration Architecture

```text id="f42s72"
GMAIL WEBHOOK
      │
      ▼
Pub/Sub Listener
      │
      ▼
Email Parser
      │
      ▼
Agent Runtime
      │
      ▼
Draft Generator
      │
      ▼
Approval Engine
      │
      ▼
Gmail Draft API
```

---

# Personality Mimicry Sources

Train from:

* sent emails
* Slack/Teams messages
* documents
* voice transcripts
* meeting notes
* tweets/posts
* texting style

---

# Personality Extraction Pipeline

```text id="vlj8qe"
Historical Emails
       │
       ▼
Style Analysis
       │
       ├── tone
       ├── sentence length
       ├── greetings
       ├── closings
       ├── politeness
       ├── emotional patterns
       └── conflict style
       │
       ▼
Trait Embedding Generation
       │
       ▼
Prompt Conditioning + Fine-Tuning
```

---

# Reflection Loop

This is what makes it improve over months.

```text id="1hgbui"
sent email
    │
    ▼
user edits tracked
    │
    ▼
diff analysis
    │
    ▼
learn preferred style
    │
    ▼
update personality profile
```

---

# Long-Term Cognitive State

The system should maintain:

```json id="of0w0e"
{
  "current_stress": 0.31,
  "social_energy": 0.74,
  "focus_topics": [
    "fundraising",
    "hiring"
  ],
  "recent_conflicts": [],
  "communication_mode": "efficient"
}
```

This prevents robotic inconsistency.

---

# Autonomous Levels

## Level 1 — Draft Assistant

* suggests replies only

---

## Level 2 — Semi-Autonomous

* auto-replies to low-risk emails

---

## Level 3 — Autonomous Executive AI

* handles inbox
* schedules meetings
* follows up
* prioritizes relationships

---

# Recommended MVP

Start with:

```text id="d3crsj"
1. Gmail Integration
2. Email Classifier
3. Personality Prompting
4. RAG Memory
5. Human Approval UI
6. Reflection Learning
```

Do NOT start with:

* fine tuning
* fully autonomous sending
* emotional simulation

---

# Most Important Engineering Insight

The hardest part is NOT generating emails.

The hardest parts are:

1. relationship modeling
2. risk management
3. memory consistency
4. approval routing
5. long-term behavioral continuity

That’s what separates:

* “AI email assistant”
  from
* “digital executive clone”

---

# Production-Grade Cognitive Loop

```text id="jlwm65"
Observe
  ↓
Classify
  ↓
Retrieve memories
  ↓
Model relationship
  ↓
Plan response
  ↓
Risk evaluate
  ↓
Generate
  ↓
Self critique
  ↓
Human approve if needed
  ↓
Send
  ↓
Learn from edits
```
