# SRAL Framework Diagrams

Simple visual representations of the SRAL framework concepts.

## 1. The Dependency Chain

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  STATE → REASON → ACT → LEARN                                │
│                                                              │
│  Each component depends on the previous one                  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## 2. The Four Questions

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  1. STATE:  What does it remember?                          │
│             Is state explicit and managed?                  │
│                                                             │
│  2. REASON: How does it decide?                             │
│             Is reasoning grounded in reality?               │
│                                                             │
│  3. ACT:    How does it affect the world?                   │
│             Does action inform reasoning?                   │
│                                                             │
│  4. LEARN:  How does it improve?                            │
│             Is learning architectural?                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## 3. Failure Tracing Methodology

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Visible Symptom (usually here):                            │
│                                                             │
│       ┌─────────┐                                           │
│       │   ACT   │ ← Wrong tool call                         │
│       └────┬────┘                                           │
│            │                                                │
│       ┌────▼────┐                                           │
│       │ REASON  │ ← Incoherent plan                         │
│       └────┬────┘                                           │
│            │                                                │
│  Root Cause (usually here):                                 │
│                                                             │
│       ┌────▼────┐                                           │
│       │  STATE  │ ← Lost constraints, context overflow      │
│       └─────────┘                                           │
│                                                             │
│  Trace backward from symptoms to root cause                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## 4. Agent Failure Pattern

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  DEMO:                      PRODUCTION:                      │
│                                                              │
│  ┌──────────┐              ┌──────────┐                     │
│  │   10     │              │   50+    │                     │
│  │ messages │              │ messages │                     │
│  └──────────┘              └──────────┘                     │
│       ↓                          ↓                          │
│  Context                    Context                         │
│  fits fine                  overflows                       │
│       ↓                          ↓                          │
│  Agent                      Agent loses                     │
│  works                      constraints                     │
│                                  ↓                          │
│                            Contradictory                    │
│                            decisions                        │
│                                                              │
│  The capability is the same.                                │
│  The architecture is different.                             │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## 5. Scoring System

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

## 6. State Management Example

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  IMPLICIT STATE (fragile):                                  │
│                                                              │
│     All state in → [Context Window] → Overflow = Loss       │
│                                                              │
│  ─────────────────────────────────────────────────────────  │
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

## 7. The ReAct Pattern (Closed Loop)

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

## Usage

These diagrams are intentionally simple ASCII art to work in:
- GitHub markdown
- Terminal displays
- Documentation systems
- Copy-paste into presentations

For polished visuals, consider creating versions in:
- Mermaid (GitHub renders these)
- Draw.io / Excalidraw
- Design tools (Figma, etc.)

## License

These diagrams are part of the SRAL Framework and are available under the MIT License.
