# SRAL Scoring Guide

How to score each component of the SRAL framework when evaluating agent architectures.

---

## Understanding the Scores

| Score | Meaning | Key Indicator |
|-------|---------|---------------|
| ✅ **Strong** | Architecturally enforced | Framework guides correct usage by default |
| ⚠️ **Moderate** | Supported but optional | Capabilities exist but not enforced |
| ⚠️ **Weak** | Afterthought | Defaults work against reliability |
| ❌ **Absent** | Not present | Must build it yourself |

**Critical Distinction:** The difference between **supported** and **enforced**.

- **Supported:** The framework provides the capability. You can use it if you choose.
- **Enforced:** The framework requires it. Doing it wrong takes deliberate effort.

SRAL evaluates what frameworks **guarantee**, not what they **allow**.

---

## Component 1: State

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  IMPLICIT STATE (fragile):                                  │
│                                                              │
│     All state in → [Context Window] → Overflow = Loss       │
│                                                              │
│  ─────────────────────────────────────────────────────────────  │
│                                                              │
│  EXPLICIT STATE (robust):                                   │
│                                                              │
│     ┌─────────────┐                                         │
│     │  Pinned     │  ← Never truncated                      │
│     │Requirements │                                         │
│     └─────────────┘                                         │
│                                                              │
│     ┌─────────────┐                                         │
│     │  External   │  ← Survives sessions                    │
│     │  Memory     │                                         │
│     └─────────────┘                                         │
│                                                              │
│     ┌─────────────┐                                         │
│     │Conversation │  ← Can be trimmed safely                │
│     │   History   │                                         │
│     └─────────────┘                                         │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### What to Evaluate

- Where does state live? (context window, external memory, both)
- Is state management required or optional?
- What happens when state exceeds storage capacity?
- Does the agent know when state is incomplete?
- Can state survive session boundaries?

### Scoring Criteria

**✅ Strong:**
- State is separate from context window by default
- Critical information automatically persisted
- Agent aware of state completeness
- Overflow handling is automatic
- State survives restarts without extra configuration

**⚠️ Moderate:**
- External state management available but optional
- Requires developer to configure persistence
- Some automatic handling but gaps remain
- Agent may not know when state is truncated

**⚠️ Weak:**
- State primarily in context window
- External persistence exists but rarely documented/used
- No overflow handling by default
- Silent degradation when state lost

**❌ Absent:**
- Only context window available
- No persistence mechanisms
- No state management primitives

### Red Flags

- Documentation says "memory is optional"
- Examples show only context-window usage
- No discussion of overflow handling
- Agent can't detect incomplete state

---

## Component 2: Reason

### What to Evaluate

- How does the agent form plans and decisions?
- Are assumptions verified against reality?
- Can reasoning proceed without environmental feedback?
- How are reasoning errors detected and corrected?
- Is grounding enforced or optional?

### Scoring Criteria

**✅ Strong:**
- Reasoning always interleaved with verification
- Cannot proceed without checking assumptions
- Errors automatically trigger replanning
- Hallucinations caught before action

**⚠️ Moderate:**
- Verification patterns available (e.g., ReAct)
- Optional to use—can build ungrounded chains
- Some error detection but not comprehensive
- Quality depends on developer discipline

**⚠️ Weak:**
- Reasoning primarily abstract/internal
- Verification possible but not common pattern
- Easy to build reasoning that never checks reality
- Hallucination cascade risk is high

**❌ Absent:**
- Pure chain-of-thought with no grounding
- No verification mechanisms
- No way to check reasoning against environment

### Red Flags

- Can build long reasoning chains without tool calls
- No mention of verification or grounding
- Examples show abstract reasoning without checks
- No discussion of hallucination prevention

---

## Component 3: Act

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│                  GROUNDED REASONING                          │
│                                                              │
│     ┌─────────┐                                             │
│     │ REASON  │ ← "I think X is true"                       │
│     └────┬────┘                                             │
│          │                                                  │
│     ┌────▼────┐                                             │
│     │   ACT   │ ← Use tool to verify X                      │
│     └────┬────┘                                             │
│          │                                                  │
│     ┌────▼────┐                                             │
│     │ OBSERVE │ ← X was actually false                      │
│     └────┬────┘                                             │
│          │                                                  │
│     ┌────▼────┐                                             │
│     │  STATE  │ ← Update world model                        │
│     └────┬────┘                                             │
│          │                                                  │
│          └─────────► Next reasoning grounded in reality     │
│                                                              │
│  Feedback loop prevents hallucination cascade               │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### What to Evaluate

- What tools/actions are available?
- How are tool results handled?
- Do observations update agent state?
- Is the feedback loop closed?
- How are errors handled?

### Scoring Criteria

**✅ Strong:**
- Tool results automatically update state
- Feedback loop enforced by architecture
- Errors trigger automatic handling
- Cannot proceed without processing observations
- Rich tool ecosystem with standard interfaces

**⚠️ Moderate:**
- Extensive tools available
- Feedback mechanisms exist but optional
- Can execute tools and ignore results
- Error handling available but not enforced
- Quality depends on implementation

**⚠️ Weak:**
- Limited tool support
- Feedback loops are manual
- Easy to lose tool results
- Minimal error handling

**❌ Absent:**
- No tool support
- No action capabilities
- Pure reasoning with no environment interaction

### Red Flags

- Tool results don't update state automatically
- Can build agents that ignore tool outputs
- No discussion of feedback loops
- Error handling is developer's responsibility

---

## Component 4: Learn

### What to Evaluate

- Does performance improve over time?
- Are successful patterns captured?
- Do mistakes inform future behavior?
- Is learning within-session, cross-session, or both?
- Is learning architectural or manual?

### Scoring Criteria

**✅ Strong:**
- Automatic learning from experience
- Patterns captured without developer intervention
- Cross-session improvement
- Transfer learning to similar tasks
- Learning is architectural, not accidental

**⚠️ Moderate:**
- Within-session adaptation exists
- Some pattern capture but manual
- Limited cross-session memory
- Learning requires developer implementation

**⚠️ Weak:**
- Minimal learning capability
- Mostly manual pattern extraction
- Each session independent
- No transfer between tasks

**❌ Absent:**
- No learning mechanisms
- Each session starts fresh
- Mistakes repeated indefinitely
- No improvement over time

### Red Flags

- Documentation doesn't mention learning
- "Persistence" confused with "learning"
- No discussion of improvement mechanisms
- Examples show no learning between sessions

---

## Common Scoring Mistakes

### Mistake 1: Confusing Capability with Architecture

**Wrong:** "It has memory modules, so State is Strong"  
**Right:** "Memory modules exist but are optional, so State is Moderate"

The question isn't "can you do it?" but "does the architecture guide you there?"

### Mistake 2: Not Tracing to Root Cause

**Wrong:** "Actions work well, so Act is Strong"  
**Right:** "Actions work but feedback doesn't update state reliably, so Act is Moderate"

Test the full loop, not just one component.

### Mistake 3: Optimistic Scoring

**Wrong:** "With enough effort, you could make it work, so it's Moderate"  
**Right:** "The defaults fail, and fixing requires significant effort, so it's Weak"

Score what the framework provides by default, not what's theoretically possible.

### Mistake 4: Conflating Storage with Learning

**Wrong:** "It stores conversation history, so Learn is present"  
**Right:** "It stores data but doesn't extract patterns, so Learn is Absent"

Storage ≠ learning. Learning requires improvement from experience.

---

## Scoring Worksheet

Use this when evaluating a framework:

### State Checklist
- [ ] State persists beyond context window
- [ ] External memory is default, not optional
- [ ] Overflow handling is automatic
- [ ] Agent aware of state completeness
- [ ] State survives sessions

**Score:** ___

### Reason Checklist
- [ ] Verification is enforced, not optional
- [ ] Reasoning grounded in observations
- [ ] Hallucinations caught before action
- [ ] Error detection built-in
- [ ] Cannot build ungrounded chains easily

**Score:** ___

### Act Checklist
- [ ] Tool results update state automatically
- [ ] Feedback loop is closed by default
- [ ] Error handling is architectural
- [ ] Cannot ignore observations easily
- [ ] Rich tool ecosystem

**Score:** ___

### Learn Checklist
- [ ] Improves from experience automatically
- [ ] Successful patterns captured
- [ ] Mistakes inform future behavior
- [ ] Cross-session learning supported
- [ ] Transfer learning possible

**Score:** ___

---

## Examples of Each Score

### State

**✅ Strong Example:**
Framework requires explicit state schema. Automatically persists to database. Agent queries state at each step. Overflow triggers smart summarization while preserving critical data.

**⚠️ Moderate Example:**
Framework provides checkpointing but it's opt-in. Developer must configure external storage. Context window is default. Overflow handling manual.

**⚠️ Weak Example:**
Framework uses context window. External memory exists but undocumented. Most examples don't show state management. Silent truncation on overflow.

**❌ Absent Example:**
Only context window. No persistence. No external memory option. Each session completely fresh.

---

## Citation

This scoring guide is part of the SRAL Framework:

Sharan, A. (2025). SRAL: A Framework for Evaluating Agentic AI Architectures. Zenodo. https://zenodo.org/records/18049753
