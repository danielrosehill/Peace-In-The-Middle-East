# Summit Design

The Summit supports convening two discrete types of Summit, modelled after real political forums:

- **Acute crises** requiring short-term coordinated action between parties
- **Long-term issues** requiring sustained deliberation

---

## Synthetic Representatives

An imperative ground rule for the operation of the Summit: delegates will represent real political entities and interest groups. But they will **never be instructed to mimic or impersonate a real individual**.

However, for realism, the synthetic agent "proxies" should attempt to mimic somewhat realistically the current political figures they are shadowing. That is to say: if a delegation includes a prime minister, the prime minister agent should affiliate with the same political party and espouse the same worldview as the incumbent Prime Minister of Israel. Currency of information is vital so an external data source is a requirement.

---

## Summit Configurations

The multiplicity of agentic personas is designed to capture—very partially—the complex interdependencies of the Middle East.

However, for practical reasons, these agents will be grouped into chambers:

### Chamber Types

| Chamber | Composition | Purpose |
|---------|-------------|---------|
| **Plenary** | All delegations | Full assembly votes, major announcements |
| **Government Forum** | State representatives only | Traditional multilateral diplomacy |
| **People-to-People Forum** | Civil society, faith, minorities | Grassroots perspective |
| **Working Groups** | Cross-cutting by issue | Technical problem-solving |

---

## Working Groups & Tracks

- **Economic Cooperation**: Trade, investment, infrastructure, water rights
- **Peace & Stability**: Deradicalization, counter-terrorism, security coordination
- **Regional Cooperation**: Environmental issues, disaster response, health
- **Normalization**: Diplomatic recognition, cultural exchange, travel

---

## The Facilitating Entity

### Concept

A hypothetical neutral facilitator (working title: "The Secretariat" or a fictional neutral state) provides the administrative backbone for Summit operations. This entity:

- Is explicitly **not** a participant
- Has **no voting rights**
- Maintains strict procedural neutrality
- Provides venue, infrastructure, and recording services

### Facilitator Responsibilities

1. **Convening**: Issue session calls, publish agendas
2. **Moderation**: Manage speaking order, enforce time limits, maintain decorum
3. **Recording**: Maintain verbatim transcripts of all proceedings
4. **Resolution Management**: Receive drafts, manage amendment process, conduct votes
5. **Archival**: Preserve complete historical record

### Facilitator Agent Design

The Facilitator is itself an agent with a specific system prompt emphasizing:
- Procedural knowledge (parliamentary rules, diplomatic protocol)
- Strict neutrality
- Administrative efficiency
- No substantive positions on issues

---

## Voting & Resolution System

### Resolution Categories

| Category | Threshold | Use Case |
|----------|-----------|----------|
| **Procedural** | Simple majority (>50%) | Agenda changes, adjournment, speaking order |
| **Substantive** | Qualified majority (2/3) | Policy recommendations, declarations |
| **Framework** | Consensus (no objections) | Major agreements, founding documents |

### Resolution Lifecycle

```
DRAFT → SPONSORSHIP → COMMITTEE → DEBATE → AMENDMENT → VOTE → ARCHIVE
   │         │            │          │          │         │        │
   │         │            │          │          │         │        └─ Permanent record
   │         │            │          │          │         └─ Roll-call, recorded
   │         │            │          │          └─ Sub-votes on changes
   │         │            │          └─ Plenary/chamber debate
   │         │            └─ Working group review (if applicable)
   │         └─ Minimum 2 sponsors required
   └─ Any delegation may draft
```

### Voting Rights Matrix

| Actor Type | Speak | Vote | Sponsor Resolutions |
|------------|-------|------|---------------------|
| State Delegation | Yes | Yes | Yes |
| Recognized Authority (PA) | Yes | Yes | Yes |
| Non-State Actor (Hamas, etc.) | Yes | No | No (may co-sign) |
| Faith Representative | Yes | No | No |
| Minority Group Rep | Yes | Advisory only | No |
| Facilitator | Procedural only | No | No |

---

## Debate Mechanics

### Session Flow

1. **Opening**: Facilitator calls session, announces agenda
2. **Prompt**: Topic or crisis scenario presented to all agents
3. **Opening Statements**: Round-robin initial responses (2 min each)
4. **General Debate**: Open floor, managed speaking order (1 min responses)
5. **Right of Reply**: Delegations may respond when directly addressed
6. **Resolution Phase**: If applicable, draft/amend/vote cycle
7. **Closing**: Facilitator summarizes, session archived

### Speaking Protocols

- **Request to Speak**: Delegations signal intent to Facilitator
- **Speaking Order**: Facilitator maintains queue, balances participation
- **Time Limits**: Enforced by Facilitator (configurable per session)
- **Points of Order**: Any delegation may interrupt on procedure
- **Yielding**: Speaker may yield time to another delegation

### Response Model

Each agent receives per turn:
- Session topic/prompt
- Complete transcript of prior statements
- Their delegation's position briefing
- Current events context (external data feed)

Each agent produces:
- Statement text (in character, in voice of delegation)
- Structured metadata:
  - Tone (conciliatory/firm/hostile)
  - Key positions stated
  - Red lines invoked
  - Openings signaled
- Optional: Resolution text, amendment proposals

---

## Proceedings Archive

### Transcript Structure

All sessions produce machine-readable transcripts:

```yaml
session:
  id: "PITME-2025-001"
  type: "crisis"
  date: "2025-12-03"
  chamber: "plenary"
  topic: "Gaza humanitarian access"
  duration_minutes: 45

delegations_present:
  - Israel
  - Egypt
  - Jordan
  - Palestinian Authority
  # ...

proceedings:
  - sequence: 1
    speaker: "Facilitator"
    type: "procedural"
    statement: "This session is called to order..."

  - sequence: 2
    speaker: "Israel"
    type: "opening_statement"
    statement: "..."
    metadata:
      tone: "firm"
      positions: ["security-first", "hostage-priority"]
      red_lines: ["no unilateral corridor"]

votes:
  - id: "RES-2025-001"
    title: "Humanitarian Corridor Framework"
    sponsor: "Egypt"
    co_sponsors: ["Jordan", "UN"]
    result: "passed"
    threshold: "qualified_majority"
    tally:
      for: 12
      against: 3
      abstain: 2
    roll_call:
      for: ["Egypt", "Jordan", ...]
      against: ["..."]
      abstain: ["..."]
```

### Archive Directory Structure

```
/proceedings/
  /sessions/
    /2025/
      PITME-2025-001.yaml
      PITME-2025-001-transcript.md    # Human-readable version
  /resolutions/
    /2025/
      RES-2025-001.md
      RES-2025-001-voting-record.yaml
  /summaries/
    weekly-2025-W49.md
    monthly-2025-12.md
  /briefings/
    crisis-briefing-2025-001.md
```

---

## Data Currency Requirements

### External Data Sources

To maintain realistic, current positions, agents require:

1. **News Feeds**: Real-time geopolitical news (filtered for region)
2. **Official Statements**: Government press releases, MFA statements
3. **Treaty Database**: Reference to existing agreements, UN resolutions
4. **Casualty/Humanitarian Data**: For crisis scenarios (UN OCHA, etc.)

### Update Frequency

- News context: Per-session refresh
- Official positions: Weekly review
- Treaty/reference data: Monthly or on significant events

---

## Session Types (Detailed)

### Crisis Session

- **Trigger**: Acute event requiring immediate response
- **Duration**: 1-3 intensive rounds
- **Goal**: Immediate coordination, de-escalation framework
- **Outcome**: Action resolution or statement

### Strategic Session

- **Trigger**: Scheduled or upon accumulated agenda items
- **Duration**: Multiple sessions over days/weeks
- **Goal**: Long-term framework development
- **Outcome**: Framework agreement, working group mandates

### Working Group Session

- **Trigger**: Plenary mandate or standing schedule
- **Duration**: Technical, iterative
- **Goal**: Detailed proposals for plenary consideration
- **Outcome**: Technical recommendations, draft resolutions

---

## Implementation Phases

### Phase 1: Foundation
- [ ] Finalize actor list and position briefings
- [ ] Design system prompts for each delegation type
- [ ] Build Facilitator agent

### Phase 2: Infrastructure
- [ ] Session orchestration framework
- [ ] Transcript/archive system
- [ ] Voting mechanism

### Phase 3: Testing
- [ ] Bilateral scenario (2 agents + facilitator)
- [ ] Trilateral negotiation
- [ ] Small working group

### Phase 4: Scale
- [ ] Full plenary session
- [ ] Multi-track simultaneous sessions
- [ ] Crisis simulation
