# SRAL Evaluation Checklist

Use this checklist to quickly evaluate any agent system.

## Score Legend

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  ✅ STRONG                                                   │
│     Architecturally enforced                                │
│     Framework guides correct usage by default               │
│     Doing it wrong requires deliberate effort               │
│                                                              │
│  ⚠️  MODERATE                                                │
│     Supported but optional                                  │
│     Capabilities exist but not enforced                     │
│     Discipline required from developer                      │
│                                                              │
│  ⚠️  WEAK                                                    │
│     Component is an afterthought                            │
│     Basic support exists                                    │
│     Defaults work against reliability                       │
│                                                              │
│  ❌ ABSENT                                                   │
│     Component doesn't exist                                 │
│     Must build it yourself                                  │
│     Or accept the limitation                                │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## Instructions

For each component, answer the architectural question. Score each as:
- ✅ **Strong** — Explicitly addressed in architecture
- ⚠️ **Weak** — Partially addressed or implicit
- ❌ **Absent** — Not addressed

---

## The Checklist

### 1. State

**Question:** Is state explicit and managed, or implicit and fragile?

| Criteria | Score | Notes |
|----------|-------|-------|
| State persists beyond context window | | |
| Critical information is pinned/protected | | |
| State is structured (not just raw text) | | |
| State survives session boundaries | | |
| Agent knows when state is incomplete | | |

**Overall State Score:** ___

---

### 2. Reason

**Question:** Is reasoning grounded in reality, or floating in abstraction?

| Criteria | Score | Notes |
|----------|-------|-------|
| Reasoning is interleaved with action | | |
| Agent verifies assumptions before acting | | |
| Agent can detect and recover from reasoning errors | | |
| Reasoning references current state explicitly | | |
| Planning includes contingencies | | |

**Overall Reason Score:** ___

---

### 3. Act

**Question:** Does action inform reasoning, or merely execute it?

| Criteria | Score | Notes |
|----------|-------|-------|
| Action results update state | | |
| Errors are caught and handled | | |
| Agent adapts based on observations | | |
| Feedback loop is closed | | |
| Tools provide rich observability | | |

**Overall Act Score:** ___

---

### 4. Learn

**Question:** Is learning architectural, or accidental?

| Criteria | Score | Notes |
|----------|-------|-------|
| Agent improves within session | | |
| Agent remembers across sessions | | |
| Successful patterns are captured | | |
| Failures inform future behavior | | |
| Learning transfers to similar tasks | | |

**Overall Learn Score:** ___

---

## Summary

| Component | Score | Root Cause Risk |
|-----------|-------|-----------------|
| State | ___ | High (if weak) |
| Reason | ___ | Medium |
| Act | ___ | Medium |
| Learn | ___ | Low (but limits growth) |

**Key Vulnerabilities:**

_List the weakest areas and their likely failure modes._

---

## Citation

Sharan, A. (2025). SRAL: A Framework for Evaluating Agentic AI Architectures. Zenodo https://zenodo.org/records/18049753
