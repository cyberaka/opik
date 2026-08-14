# स्वर विज्ञान — Swara Vigyan POC

**Swara Vigyan Consultation & Prediction** के लिए एक proof-of-concept application और उसका
**canonical knowledge base**, जो Architecture Decision Records (ADRs) के रूप में रखा गया है।

यह repository अभी केवल **ADRs** रखती है — कोई application code नहीं। सभी requirements और
गुरु की teaching के canonical rules ADRs में capture किए गए हैं, ताकि implementation से पहले
scope, domain logic और design decisions पर सहमति बने।

> **Knowledge baseline:** *Consolidated Master Notes — Version 1* (Guru's teaching).
> जहाँ गुरु से exact rule नहीं मिला है, उसे **invent नहीं** किया गया — ऐसे बिंदु
> "Pending" के रूप में चिह्नित हैं (देखें ADR-0014, ADR-0010 §future)।

---

## यह क्या है?

एक **Swara Vigyan practice assistant** जिसमें **दो capabilities** हैं:

**1. Consultation & Prediction** — practitioner अपने वर्तमान **active nostril** (भरा स्वर) और
visitor की स्थिति/प्रश्न के समय की energy देखकर prediction करता है:

- **चार मूल नियम** (Bhara/Khali energy transition) — YES / NO / mixed outcomes
- **Rule 0** — practitioner की readiness के बिना कोई prediction नहीं
- **Modes** — Independent Room, Shared/Chamber, Sabha/Group, Remote/Behind
- **Signals** — Saguna/Nirguna breath, question addressing, position-swara, behind-position
- एक **raw-observation-first architecture** ताकि गुरु के भविष्य के rules आने पर पुराने
  observations को दोबारा interpret किया जा सके।

**2. Remedies & Therapeutic Practices** — Swara-based remedies (headache/anxiety/migraine, BP,
fever, cold, body pain), जैसा गुरु ने सिखाया वैसा ही (strength/duration सहित), optional personal
practice record के साथ — और teaching से अलग रखी गई health-safety notes के साथ।

दोनों capabilities एक **content-provenance convention** का पालन करती हैं:
**Guru Teaching** को कभी भी **Research/Safety Note** या **Needs Clarification** के साथ mix नहीं
किया जाता (ADR-0017)।

---

## Architecture Decision Records

### Foundations
| ADR | शीर्षक |
|-----|--------|
| [0000](docs/adr/0000-using-architecture-decision-records.md) | Using Architecture Decision Records |
| [0001](docs/adr/0001-product-scope-and-goals.md) | Product Scope & Goals (full model + phasing) |
| [0002](docs/adr/0002-swara-domain-model-and-terminology.md) | Swara Domain Model & Terminology (nadis, saguna/nirguna) |
| [0003](docs/adr/0003-room-layout-and-perspective-convention.md) | Room Layout & Perspective Convention |

### Prediction logic
| ADR | शीर्षक |
|-----|--------|
| [0004](docs/adr/0004-prediction-rule-engine.md) | Four-Rule Energy Engine (First → Second) |
| [0011](docs/adr/0011-rule-0-practitioner-readiness.md) | Rule 0 — Practitioner Readiness Gate |
| [0012](docs/adr/0012-consultation-modes.md) | Consultation Modes (A/B/C/Remote/Behind) |
| [0013](docs/adr/0013-additional-prediction-signals.md) | Additional Prediction Signals (breath, addressing, position, behind) |
| [0014](docs/adr/0014-signal-independence-and-conflict-handling.md) | Signal Independence, Conflicts & Pending Rules |
| [0016](docs/adr/0016-meethi-goli-symbolic-action.md) | Meethi Goli — Symbolic Action (non-causal) |

### Remedies & content integrity
| ADR | शीर्षक |
|-----|--------|
| [0017](docs/adr/0017-content-provenance-and-integrity.md) | Content Provenance & Integrity (Guru Teaching / Research-Safety / Needs Clarification) |
| [0018](docs/adr/0018-remedies-therapeutic-practices-module.md) | Remedies / Therapeutic Practices Module (catalogue as taught) |
| [0019](docs/adr/0019-health-safety-and-medical-disclaimer.md) | Health Safety & Medical Disclaimer |

### Engineering
| ADR | शीर्षक |
|-----|--------|
| [0005](docs/adr/0005-application-architecture-and-tech-stack.md) | Application Architecture & Tech Stack |
| [0015](docs/adr/0015-raw-observation-vs-interpretation.md) | Raw Observation vs Interpretation — Data Model & Rule Engine |
| [0006](docs/adr/0006-user-experience-and-consultation-flow.md) | User Experience & Consultation Flow |
| [0007](docs/adr/0007-content-i18n-and-accessibility.md) | Content, i18n & Accessibility |
| [0008](docs/adr/0008-privacy-state-and-data-handling.md) | Privacy, State & Data Handling |
| [0009](docs/adr/0009-repository-hosting-and-deployment.md) | Repository, Hosting & Deployment |
| [0010](docs/adr/0010-out-of-scope-and-future-work.md) | Out of Scope, Pending Rules & Future Work |

---

## Status

सभी ADRs वर्तमान में **Accepted (knowledge baseline v1)** हैं। किसी भी rule को implement या बदलने
से पहले संबंधित ADR update किया जाए। जो rules अभी गुरु से सीखने बाकी हैं, वे ADR-0010 §Pending और
ADR-0014 में सूचीबद्ध हैं और app में **invent नहीं** किए जाएँगे।

## Disclaimer

Swara Vigyan एक पारंपरिक/आध्यात्मिक अध्ययन है। यह tool practitioner की सहायता के लिए है और इसे
किसी चिकित्सीय, कानूनी या वित्तीय सलाह के रूप में प्रस्तुत नहीं किया जाता। देखें
[ADR-0010](docs/adr/0010-out-of-scope-and-future-work.md)।
