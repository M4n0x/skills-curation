# Security Audit Skills Framework

A modular security audit system composed of 8 specialized sub-skills orchestrated by a wrapper skill.

## Architecture

```
security-audit (orchestrator)
├── Reconnaissance → detect app type & stack
├── Skill Selection → choose relevant auditors
├── Execution → run auditors (parallel or sequential)
├── Synthesis → CISO Synthesizer consolidates findings
└── Delivery → present unified report

Sub-skills:
┌─────────────────────┬─────────────────────────────────────────────┐
│ Frontend Sentinel   │ XSS, DOM manipulation, client-side storage  │
│ Backend Fortifier   │ Injection, SSRF, API security, business logic│
│ Data Warden         │ SQL/NoSQL injection, encryption, PII exposure│
│ Identity Manager    │ Auth, JWT, OAuth, sessions, access control   │
│ AI/LLM Guardian     │ Prompt injection, tool abuse, data leakage   │
│ Infra Sentry        │ Docker, K8s, secrets, CI/CD, network policies│
│ Supply Chain Auditor│ CVEs, malicious packages, dependency health  │
│ CISO Synthesizer    │ Risk scoring, attack chains, executive report│
└─────────────────────┴─────────────────────────────────────────────┘
```

## Installation

Copy each skill folder into your skills directory.

## Usage

Tell your prefered tooling: "Run a security audit on this codebase" — the orchestrator will handle the rest.

## Skill Selection by App Type

| App Type         | FS | BF | DW | IM | AG | IS | SC | CS |
|------------------|----|----|----|----|----|----|----|----|
| Full-Stack Web   | ✅ | ✅ | ✅ | ✅ | ?  | ✅ | ✅ | ✅ |
| API Backend      | ❌ | ✅ | ✅ | ✅ | ?  | ✅ | ✅ | ✅ |
| AI/LLM App       | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Static/Jamstack  | ✅ | ?  | ❌ | ❌ | ❌ | ?  | ✅ | ✅ |
| Microservices    | ✅ | ✅ | ✅ | ✅ | ?  | ✅ | ✅ | ✅ |

✅ = Always  ❌ = Skip  ? = If detected

## Output

Each sub-skill produces a structured JSON report. The CISO Synthesizer combines them into:
- Executive summary with overall risk level
- Top 5 prioritized risks in business language
- Attack chain analysis (chained vulnerabilities)
- Compliance mapping (OWASP, CIS, NIST, SOC 2, GDPR)
- Phased remediation roadmap (immediate → long-term)
- Full technical appendix
