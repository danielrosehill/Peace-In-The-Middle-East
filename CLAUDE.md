# CLAUDE.md - Peace In The Middle East (PITME)

## Project Overview

PITME is a multi-agent AI experiment simulating geopolitical negotiations in the Middle East. AI agents embody state actors, non-state actors, and civil society representatives to explore diplomatic scenarios that would be prohibitively expensive or politically impossible in reality.

## Core Principles

### Synthetic Representation Rules

1. **No Individual Impersonation**: Agents represent political entities and worldviews, never specific named individuals
2. **Current Alignment**: Agents shadow real political positions (e.g., "Prime Minister of Israel" aligns with current incumbent's party/worldview)
3. **Reality-Based**: The simulation starts from geopolitical reality, not idealized versions
4. **Parallel Representation**: Where de jure and de facto control differ, multiple representatives may participate

### Operational Philosophy

- **Inclusive but Not Endorsing**: Inclusion of actors (including designated terrorist organizations) is for simulation fidelity, not endorsement
- **Agent Autonomy**: Agents may refuse to engage with certain actors, following their represented entity's real policies
- **Transparency**: All proceedings are recorded; this is explicitly NOT closed-door diplomacy

---

## Summit Architecture

### Summit Types

| Type | Purpose | Duration Model |
|------|---------|----------------|
| **Crisis Summit** | Acute crises requiring immediate coordinated action | Short, intensive sessions |
| **Strategic Summit** | Long-term structural issues | Extended deliberation periods |

### Chambers & Configurations

1. **Plenary** - Full assembly of all delegations
2. **Government Chamber** - State representatives only (traditional diplomacy model)
3. **People-to-People Forum** - Civil society, faith groups, minority representatives
4. **Working Groups** - Issue-specific committees (cross-cutting membership)

### Working Groups (Tracks)

- Economic Cooperation
- Peace & Stability (deradicalization, counter-terrorism)
- Regional Cooperation
- Normalization

---

## Facilitator Entity

### The Facilitating State

A hypothetical neutral state ("Neutralia" or similar placeholder) provides:
- Summit venue and administrative infrastructure
- Procedural oversight
- Recording and archival services
- Resolution drafting assistance

The Facilitator is NOT a participant and has no voting rights. It enforces procedural rules impartially.

### Facilitator Responsibilities

1. **Convening**: Call sessions, set agendas
2. **Moderating**: Manage speaking order, time limits, decorum
3. **Recording**: Maintain official transcript of all proceedings
4. **Resolution Processing**: Receive draft resolutions, manage voting procedures
5. **Archival**: Preserve all debate records, votes, and outcomes

---

## Voting & Resolution Mechanism

### Resolution Types

| Type | Required Majority | Scope |
|------|-------------------|-------|
| **Procedural** | Simple majority | Summit operations, agenda items |
| **Substantive** | 2/3 majority of participating states | Policy recommendations |
| **Consensus** | No objections | Framework agreements |

### Resolution Lifecycle

1. **Drafting**: Any delegation may draft a resolution
2. **Sponsorship**: Resolution requires at least 2 sponsors to proceed
3. **Committee Review**: Working group review if applicable
4. **Debate**: Plenary or chamber debate with speaking order
5. **Amendment**: Amendments may be proposed and voted on
6. **Vote**: Roll-call vote with recorded positions
7. **Archival**: Result and full debate transcript preserved

### Voting Rights

- **Full Vote**: State delegations, recognized authorities
- **Observer Status**: Non-state actors, faith groups (may speak, cannot vote)
- **Advisory Vote**: Minority group representatives (recorded but non-binding)

---

## Debate Flow Model

### Session Structure

```
┌─────────────────────────────────────────────────────────┐
│                    SESSION OPENS                         │
│  Facilitator calls session, states agenda               │
└────────────────────────┬────────────────────────────────┘
                         ▼
┌─────────────────────────────────────────────────────────┐
│                  INITIAL PROMPT                          │
│  Topic/crisis presented to all agents simultaneously    │
└────────────────────────┬────────────────────────────────┘
                         ▼
┌─────────────────────────────────────────────────────────┐
│               OPENING STATEMENTS                         │
│  Each delegation responds to prompt (round-robin)       │
└────────────────────────┬────────────────────────────────┘
                         ▼
┌─────────────────────────────────────────────────────────┐
│                   DEBATE ROUNDS                          │
│  Agents respond to each other's statements              │
│  Facilitator manages speaking order                     │
└────────────────────────┬────────────────────────────────┘
                         ▼
┌─────────────────────────────────────────────────────────┐
│              RESOLUTION PHASE (if any)                   │
│  Draft resolutions, amendments, voting                  │
└────────────────────────┬────────────────────────────────┘
                         ▼
┌─────────────────────────────────────────────────────────┐
│                  SESSION CLOSES                          │
│  Facilitator summarizes, archives proceedings           │
└─────────────────────────────────────────────────────────┘
```

### Speaking Rules

- **Time Limits**: Configurable per session type (e.g., 2 minutes opening, 1 minute responses)
- **Right of Reply**: Delegations may request right of reply when directly addressed
- **Points of Order**: Any delegation may raise procedural objections
- **Yielding**: Delegation may yield remaining time to another

### Response Model

Each agent receives:
1. The session prompt/topic
2. Full transcript of prior statements in the session
3. Their delegation's position briefing
4. Relevant current events context (via external data source)

Agent outputs:
1. Statement text (in character)
2. Metadata: tone, key positions, red lines, openings for negotiation
3. Optional: draft resolution text, amendment proposals

---

## Proceedings Recording

### Transcript Format

All sessions produce structured transcripts:

```yaml
session:
  id: "PITME-2025-001"
  type: "crisis"
  date: "2025-12-03"
  chamber: "plenary"
  topic: "Humanitarian corridor negotiations"

proceedings:
  - speaker: "Israel"
    timestamp: "10:00:00"
    statement: "..."
    metadata:
      tone: "firm"
      key_positions: ["security guarantees", "hostage priority"]

  - speaker: "Egypt"
    timestamp: "10:02:30"
    statement: "..."

votes:
  - resolution_id: "RES-2025-001"
    title: "..."
    result: "passed"
    tally:
      for: ["Egypt", "Jordan", ...]
      against: ["..."]
      abstain: ["..."]
```

### Archive Structure

```
/proceedings/
  /2025/
    /sessions/
      PITME-2025-001.yaml
      PITME-2025-002.yaml
    /resolutions/
      RES-2025-001.md
      RES-2025-002.md
    /summaries/
      monthly-2025-01.md
```

---

## Technical Implementation Notes

### Agent Configuration

Each agent requires:
- **Identity File**: Role, entity represented, core positions
- **Briefing Document**: Current political stance, red lines, negotiating flexibility
- **Context Window**: Access to real-time news/data for currency

### External Data Requirements

- Current news feeds (for geopolitical currency)
- Official government positions (updated periodically)
- Treaty/agreement reference database

### Session Orchestration

The orchestrator (not an agent) manages:
- Agent instantiation per session
- Prompt distribution
- Speaking order enforcement
- Transcript compilation
- Vote tallying

---

## Development Priorities

1. [ ] Finalize actor list with detailed position briefings
2. [ ] Design agent system prompts for each delegation type
3. [ ] Build session orchestration framework
4. [ ] Implement transcript/archive system
5. [ ] Create voting mechanism
6. [ ] Develop facilitator agent
7. [ ] Test with simple bilateral scenario
8. [ ] Scale to multilateral crisis simulation

---

## Ethical Considerations

- This is an **experiment**, not a policy recommendation engine
- Outputs should be treated as exploratory, not predictive
- The simulation cannot capture full human complexity
- Results may reflect training data biases
- Transparency about limitations is mandatory in any publication of results
