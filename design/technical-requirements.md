# Technical Requirements

This document outlines the technical infrastructure required to operate the PITME multi-agent simulation, with particular attention to LLM capabilities, information currency, and persistent record-keeping.

---

## Large Language Model Requirements

### Core Agentic Capabilities

The simulation requires LLMs with robust agentic behaviors:

| Capability | Requirement | Rationale |
|------------|-------------|-----------|
| **Role Adherence** | Strong system prompt following | Agents must maintain consistent personas throughout sessions |
| **Context Retention** | Extended context windows (128K+) | Full session transcripts must be processable |
| **Multi-Turn Reasoning** | Sophisticated dialogue modeling | Diplomatic exchanges require nuanced responses to prior statements |
| **Structured Output** | Reliable JSON/YAML generation | Metadata extraction (tone, positions, red lines) must be machine-readable |
| **Tool Use** | Function calling capability | Agents may need to query external data, propose resolutions, call votes |
| **Instruction Following** | Precise adherence to procedural rules | Facilitator must enforce speaking order, time limits, voting thresholds |

### Recommended Model Tiers

| Tier | Use Case | Example Models |
|------|----------|----------------|
| **High-capability** | State delegations, major powers, Facilitator | Claude Opus/Sonnet, GPT-4, Gemini Ultra |
| **Mid-capability** | Non-state actors, civil society | Claude Haiku, GPT-4o-mini, Gemini Pro |
| **Specialized** | Archival summarization, transcript processing | Fine-tuned models for specific tasks |

---

## Information Currency: The Critical Requirement

### The Problem

For agents to realistically represent current political positions, they must be grounded in **up-to-date geopolitical context**. Training data cutoffs render agents incapable of addressing recent developments—a fatal flaw for simulating live negotiations.

### Solution: Endogenous Web/Search Capabilities

**Preferred approach**: Use LLMs with built-in, real-time web access capabilities rather than manually injecting context.

| Approach | Pros | Cons |
|----------|------|------|
| **Endogenous search (preferred)** | Agents autonomously fetch current context; reduces orchestration complexity; ensures all agents access same knowledge base | Requires models with this capability; may have rate limits |
| **RAG injection** | Full control over sourced data; can curate authoritative sources | Requires per-session context preparation; may miss breaking news |
| **Hybrid** | Endogenous for currency, RAG for specialized/archival data | Additional complexity |

### Models with Endogenous Search

As of late 2024/early 2025:

- **Claude**: Web search available via tool use
- **GPT-4**: Browsing capability in certain configurations
- **Gemini**: Grounding with Google Search
- **Perplexity**: Native search-first architecture

### Currency Requirements by Data Type

| Data Type | Freshness | Source Examples |
|-----------|-----------|-----------------|
| **Breaking news** | Real-time (hours) | News APIs, live feeds |
| **Official statements** | Same-day | Government websites, MFA releases |
| **Political positions** | Weekly refresh | Policy documents, manifestos |
| **Treaty/legal references** | Monthly or on-change | UN document repositories, treaty databases |
| **Historical context** | Static | Academic sources, established records |

---

## Multi-Agent Orchestration

### Architecture Options

| Architecture | Description | Suitability |
|--------------|-------------|-------------|
| **Centralized orchestrator** | Single controller dispatches to agents, collects responses | Good for structured sessions with clear turn-taking |
| **Message-passing** | Agents communicate via shared message bus | Good for working groups with cross-talk |
| **Hierarchical** | Facilitator agent manages sub-agents | Natural fit for Summit structure |

### Recommended: Hierarchical with Facilitator Agent

```
┌─────────────────────────────────────────────────────────────┐
│                    SESSION ORCHESTRATOR                      │
│  (Technical layer: session lifecycle, transcript capture)   │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                    FACILITATOR AGENT                         │
│  (In-simulation: manages debate, calls on speakers, votes)  │
└────────────────────────────┬────────────────────────────────┘
                             │
          ┌──────────────────┼──────────────────┐
          ▼                  ▼                  ▼
     ┌─────────┐       ┌─────────┐       ┌─────────┐
     │ Agent A │       │ Agent B │       │ Agent C │
     │ (Israel)│       │ (Egypt) │       │  (UN)   │
     └─────────┘       └─────────┘       └─────────┘
```

### Shared Context Grounding

**Critical**: All agents in a session must share the same factual grounding.

Options:
1. **Pre-session briefing**: All agents receive identical current-events briefing before session
2. **Shared search context**: Facilitator performs searches, results distributed to all
3. **Common knowledge base**: Curated daily briefing all agents reference
4. **Synchronized search**: All agents use same search tool with cached results

**Recommendation**: Combination of pre-session briefing (for baseline) + endogenous search (for agent-specific queries) + result caching (for consistency within session).

---

## Data Storage & Record-Keeping

### The Institutional Memory Imperative

If PITME simulates an ongoing deliberative body, it must maintain records as any real institution would:

- **Complete transcripts** of all proceedings
- **Voting records** with full roll-call
- **Resolution archive** (proposed, amended, passed, failed)
- **Delegation statements** indexed and searchable
- **Position evolution** tracking how stances shift over sessions

### Storage Architecture

```
/data/
  /proceedings/
    /sessions/
      /2025/
        PITME-2025-001/
          session.yaml           # Structured metadata
          transcript.md          # Human-readable full transcript
          speakers.json          # Per-speaker statement index
          votes.yaml             # Voting records
    /resolutions/
      RES-2025-001/
        resolution.md            # Final text
        amendments.yaml          # Amendment history
        voting-record.yaml       # Roll-call vote
        debate-excerpts.md       # Key debate moments
    /indices/
      by-delegation.json         # All statements by delegation
      by-topic.json              # Sessions indexed by topic
      by-date.json               # Chronological index
  /briefings/
    /daily/
      2025-12-03.md              # Daily context briefing
    /position-papers/
      israel-security-doctrine.md
      egypt-regional-strategy.md
  /archives/
    /annual/
      2025-summary.md            # Year in review
```

### Database Considerations

For queryable access:

| Option | Use Case |
|--------|----------|
| **PostgreSQL** | Complex queries, relational data (votes, delegations, sessions) |
| **MongoDB** | Flexible document storage for transcripts, briefings |
| **SQLite** | Lightweight option for smaller deployments |
| **Vector DB (Pinecone, Weaviate)** | Semantic search across statements, finding similar positions |

### Retention Policy

- **Transcripts**: Permanent (core archive)
- **Session metadata**: Permanent
- **Raw agent outputs**: 1 year (for debugging/analysis)
- **Context briefings**: Permanent (historical record of what agents "knew")
- **Voting records**: Permanent

---

## Public Access & API

### Transparency by Design

Unlike real closed-door diplomacy, PITME proceedings are explicitly public. This enables:

- External analysis of agent behaviors
- Academic research access
- Public engagement with simulation outputs
- Accountability for the experiment itself

### Public API Specification

```yaml
# Example API endpoints

/api/v1/sessions
  GET /                          # List all sessions
  GET /{session_id}              # Get session details
  GET /{session_id}/transcript   # Full transcript
  GET /{session_id}/votes        # Voting records

/api/v1/resolutions
  GET /                          # List all resolutions
  GET /{resolution_id}           # Resolution details
  GET /{resolution_id}/history   # Amendment history

/api/v1/delegations
  GET /                          # List all delegations
  GET /{delegation}/statements   # All statements by delegation
  GET /{delegation}/votes        # Voting record

/api/v1/search
  GET /?q={query}                # Full-text search across proceedings
  GET /?topic={topic}            # Filter by topic
  GET /?date_range={start},{end} # Filter by date

/api/v1/live
  GET /current-session           # Active session (if any)
  WebSocket /stream              # Real-time session updates
```

### Access Tiers

| Tier | Access | Rate Limits |
|------|--------|-------------|
| **Public** | Read-only, proceedings only | 100 req/hour |
| **Researcher** | Full archive, bulk download | 1000 req/hour |
| **Admin** | Write access, session management | Unlimited |

### Data Formats

- **Primary**: JSON (API responses)
- **Archive**: YAML (structured), Markdown (human-readable)
- **Bulk export**: JSON-LD, CSV for tabular data

---

## Infrastructure Recommendations

### Minimum Viable Setup

For initial testing/development:

- Single orchestrator script (Python)
- LLM API access (OpenRouter for flexibility)
- File-based storage (YAML/Markdown)
- No public API (local only)

### Production Setup

For ongoing operation:

| Component | Recommendation |
|-----------|----------------|
| **Orchestration** | Dedicated agent framework (LangGraph, AutoGen, or custom) |
| **LLM Access** | Multiple provider accounts for redundancy |
| **Storage** | PostgreSQL + S3-compatible object storage |
| **API** | FastAPI or similar, behind CDN |
| **Hosting** | Cloud VMs or containers (Docker/K8s) |
| **Monitoring** | Session logging, cost tracking, error alerting |

### Cost Considerations

Multi-agent simulations are token-intensive:

- Long transcripts passed to each agent per turn
- Multiple agents per session (10-50+)
- Extended sessions (potentially hours of simulated debate)

**Mitigations**:
- Summarize transcript for later turns (sacrifice some fidelity)
- Use cheaper models for lower-stakes agents
- Cache repeated context (news briefings, position papers)
- Limit session length with clear procedural time limits

---

## Security & Ethics

### Data Handling

- No real personal data in simulation
- Agent outputs clearly marked as synthetic
- Disclaimers on all public outputs
- No pretense of predictive accuracy

### API Security

- Authentication for write operations
- Rate limiting to prevent abuse
- Audit logging of all API access
- HTTPS only

### Model Access

- API keys secured (not in code)
- Per-agent token budgets
- Fallback providers for redundancy

---

## Implementation Priorities

1. **Proof of concept**: 2-3 agents + facilitator, file-based storage, manual orchestration
2. **Basic infrastructure**: Automated orchestration, structured transcripts, local API
3. **Public access**: Hosted API, web interface for proceedings
4. **Scale**: Full multi-chamber operation, parallel sessions, real-time updates
