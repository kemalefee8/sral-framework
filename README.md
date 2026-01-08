# SRAL Framework

**A minimal framework for evaluating agentic AI architectures.**

SRAL (State-Reason-Act-Learn) is an evaluation framework that foregrounds *State*—the constructed, persistent world-model that agents must explicitly maintain—as the foundational component of agent architecture.

## The Core Insight

Most agent failures trace not to reasoning or action, but to unmanaged state: context window overflow, lost constraints, and forgotten decisions.

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  STATE → REASON → ACT → LEARN                                │
│                                                              │
│  Each component depends on the previous one.                 │
│  When an agent fails, trace backward:                        │
│  - Visible failure usually in ACT or REASON                  │
│  - Root cause usually in STATE                               │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## The Four Questions

When evaluating any agent system, ask these questions in order:

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

| Component | Architectural Question |
|-----------|----------------------|
| **State** | Is state explicit and managed, or implicit and fragile? |
| **Reason** | Is reasoning grounded in reality, or floating in abstraction? |
| **Act** | Does action inform reasoning, or merely execute it? |
| **Learn** | Is learning architectural, or accidental? |

## The Dependency Model

```
State → Reason → Act → Learn
```

- Reason depends on State
- Act depends on Reason
- Learn depends on all three

When an agent fails, trace backward. The visible failure is usually in Act or Reason. The root cause is usually in State.

### Failure Tracing Example

```
┌─────────────────────────────────────────────┐
│  Visible Symptom (usually here):            │
│                                             │
│       ┌─────────┐                           │
│       │   ACT   │ ← Wrong output            │
│       └────┬────┘                           │
│            │                                │
│       ┌────▼────┐                           │
│       │ REASON  │ ← Bad decision            │
│       └────┬────┘                           │
│            │                                │
│  Root Cause (usually here):                 │
│                                             │
│       ┌────▼────┐                           │
│       │  STATE  │ ← Lost constraints        │
│       └─────────┘                           │
│                                             │
└─────────────────────────────────────────────┘
```

## Resources

- **Paper:** [SRAL: A Framework for Evaluating Agentic AI Architectures](https://zenodo.org/records/18049753)
- **Blog Post:** [The Four Questions I Ask About Every Agent](https://aakashsharan.com/sral-framework-four-questions-every-ai-agent/)
- **Visual Diagrams:** [Simple diagrams explaining SRAL concepts](docs/diagrams.md)
- **Evaluation Tools:**
  - [Quick Checklist](evaluation/SRAL-checklist.md) - Fast assessment tool
  - [Detailed Template](evaluation/SRAL-evaluation-template.md) - Comprehensive evaluation
  - [Scoring Guide](evaluation/SRAL-scoring-guide.md) - How to score each component
- **Complete Examples:**
  - [LangChain Evaluation](evaluation/examples/langchain-evaluation.md) - Full evaluation with scores

## Quick Start

1. **Learn SRAL:** Read the [paper](https://doi.org/10.5281/zenodo.18049753) or [blog post](https://aakashsharan.com/sral-framework-four-questions-every-ai-agent/)
2. **See it in action:** Review the [LangChain evaluation](evaluation/examples/langchain-evaluation.md)
3. **Understand scoring:** Read the [scoring guide](evaluation/SRAL-scoring-guide.md)
4. **Quick assessment:** Use the [checklist](evaluation/SRAL-checklist.md) for rapid evaluation
5. **Deep dive:** Use the [detailed template](evaluation/SRAL-evaluation-template.md) for comprehensive analysis

## Citation

If you use SRAL in your work, please cite:

```bibtex
@misc{sharan2025sral,
  author = {Sharan, Aakash},
  title = {SRAL: A Framework for Evaluating Agentic AI Architectures},
  year = {2025},
  publisher = {Zenodo},
  doi = {10.5281/zenodo.18049753},
  url = {https://doi.org/10.5281/zenodo.18049753}
}
```

## License

MIT License — see [LICENSE](LICENSE) for details.

## Author

**Aakash Sharan** — [LinkedIn](https://www.linkedin.com/in/aakashsharan) | [Website](https://aakashsharan.com/blog/)
