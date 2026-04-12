---
description: 'Generate a comprehensive threat model for any application or system. Use when: threat modeling, security review, STRIDE analysis, trust boundary analysis, attack tree creation, executive security briefing, CISO presentation, application security assessment.'
---

# Threat Model Generator

Generate a comprehensive, executive-ready threat model for the target system using Microsoft STRIDE, OWASP, Adam Shostack's Four Question Framework, and the Threat Modeling Manifesto.

## Inputs

Ask the user for:
1. **What system/application** is being modeled?
2. **What sensitive data** flows through it? (PII, secrets, AI prompts, financial, classified)
3. **Who is the adversary?** (opportunistic, organized crime, nation-state, insider)
4. **What is the deployment context?** (cloud, on-prem, containers, hybrid)
5. **Who is the audience?** (CISO briefing, dev team, compliance audit)

If the user provides source code, analyze it directly. If not, ask for an architecture description.

## Procedure

### Phase 1: System Decomposition (Shostack Q1: "What are we building?")

1. **Identify all components** — services, libraries, databases, message queues, APIs, config sources
2. **Map all data flows** — how data enters, transforms, and exits the system
3. **Identify trust boundaries** — where data crosses between different trust levels:
   - Application code → framework/library
   - Internal process → external network
   - Config/classpath → runtime pipeline
   - User input → processing engine
   - Memory/runtime → persistent storage
4. **Create a Level 0 DFD** (system context) as a Mermaid flowchart
5. **Create a Level 1 DFD** with trust boundaries labeled and color-coded

### Phase 2: STRIDE Analysis (Shostack Q2: "What can go wrong?")

For EACH trust boundary crossing, analyze all six STRIDE categories:

| Category | Question to Ask |
|---|---|
| **Spoofing** | Can an attacker forge identity, fake entries, or impersonate components? |
| **Tampering** | Can data be modified in transit, at rest, or in the processing pipeline? |
| **Repudiation** | Can an attacker deny their actions? Is there cryptographic proof of events? |
| **Information Disclosure** | Can sensitive data leak via network, storage, memory, logs, or side channels? |
| **Denial of Service** | Can the system be overwhelmed, starved, or made unavailable? |
| **Elevation of Privilege** | Can an attacker gain capabilities beyond their authorization? |

For each threat found, document:
- **ID** (category letter + number, e.g., S-1, T-2, I-3)
- **Description** — one sentence
- **Trust boundary** crossing
- **Severity** — CRITICAL / HIGH / MEDIUM / LOW
- **Code reference** — file path and line number if source available
- **Attack scenario** — how an attacker exploits this

### Phase 3: Attack Trees

Create 3-4 attack trees as Mermaid diagrams covering the most impactful goals:
1. **Data Exfiltration** — all paths to steal sensitive data
2. **Evidence Destruction** — all paths to cover tracks or tamper with audit trails
3. **Remote Code Execution** — all paths to execute arbitrary code
4. **Supply Chain** — all paths to persistent access via dependencies or build pipeline

Each tree should have:
- Root node = attacker goal (red)
- Category nodes = attack strategy (color-coded by severity)
- Leaf nodes = specific technique (light gray)
- Use `classDef` for consistent styling

### Phase 4: Risk Register

Create a risk register table with:
- Risk description
- Likelihood (1-5)
- Impact (1-5)
- Score (Likelihood × Impact)
- Owner (team responsible)
- Mitigation status

### Phase 5: Remediation Roadmap (Shostack Q3: "What are we going to do about it?")

Create a phased roadmap:
- **P0 (Immediate, Week 1)** — address CRITICAL threats with quick wins
- **P1 (Short-term, Weeks 2-4)** — address HIGH threats requiring code/config changes
- **P2 (Medium-term, Months 1-2)** — address threats requiring infrastructure changes
- **P3 (Long-term, Months 2-4)** — defense-in-depth completion

Create a controls diagram mapping mitigations to trust boundaries.

### Phase 6: Validation (Shostack Q4: "Did we do a good job?")

Include:
- Validation checklist
- Residual risk statement
- OWASP Top 10 mapping table
- Communication flow matrix (source, destination, protocol, encrypted?, authenticated?, integrity?)

## Output Format

### Markdown Version
Create `security-audit/THREAT-MODEL.md` with all sections, Mermaid diagrams, and tables.

### HTML Version
Create `security-audit/THREAT-MODEL.html` as a self-contained executive briefing with:
- Dark gradient header with classification banner
- Metric cards for key numbers
- Color-coded severity badges (CRITICAL=red, HIGH=orange, MEDIUM=yellow, LOW=green)
- Mermaid diagrams rendered via CDN (`https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.min.js`)
- Phase roadmap as colored cards
- Print-friendly CSS for PDF export
- All diagrams use `flowchart` (not `graph`), `classDef` for styles, emoji icons on key nodes

### Diagram Standards

Use these Mermaid conventions for clean rendering:
```
- Use `flowchart TD` or `flowchart LR` (not `graph`)
- Use `classDef` for styles (not inline `style` per node)
- Use emoji in node labels for visual scanning
- Keep node labels short (3-5 words max)
- Use `:::className` syntax for applying styles
- No `\n` in node labels — causes rendering breaks
- Attack tree roots: red with bold border
- Leaf nodes: light gray
- Use `-.->` for optional/conditional flows
- Use `~~~` for invisible links in layout
```

Color palette:
```
goal/critical:  fill:#dc3545, stroke:#a71d2a (red)
high:           fill:#e67e22, stroke:#d35400 (orange)  
medium:         fill:#f39c12, stroke:#d68910 (amber)
safe/green:     fill:#27ae60, stroke:#1e8449 (green)
info/blue:      fill:#4a90d9, stroke:#3a7bd5 (blue)
neutral/leaf:   fill:#f8f9fa, stroke:#adb5bd (light gray)
```

## Quality Checklist

Before delivering, verify:
- [ ] All trust boundaries have at least one threat identified
- [ ] All CRITICAL threats have remediation in P0 or P1
- [ ] All 6 STRIDE categories analyzed
- [ ] All diagrams render without errors
- [ ] Attack trees have clear goal → strategy → technique hierarchy
- [ ] Risk scores are consistent (Likelihood × Impact)
- [ ] OWASP Top 10 mapping is complete
- [ ] Communication flow matrix covers all data paths
- [ ] Residual risks are explicitly stated
- [ ] Document is appropriate for stated audience
