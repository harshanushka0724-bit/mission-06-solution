# Squadron Shannon — Mission 06: The Autonomous Warp State Machine & Deliberation Loop

- **Course:** Conversational AI — Winter Semester 2026/27
- **Module:** Week 6 — The Agentic Shift: System 1 vs. System 2 Thinking
- **Galactic Waypoint:** Sector SEC-06-CAR (Eta Carinae & Homunculus Nebula)
- **Active Squadron:** Squadron Shannon
- **GitHub Solution Repository:** https://github.com/harshanushka0724-bit/mission-06-solution
- **Primary Deliverable Notebook:** `ps06_solution.ipynb`

---

## 1. Digital Station Sign-Off Roster

| Station Role | Domain | Assigned Cadet | Status |
| :--- | :--- | :--- | :--- |
| **Systems Architect (Lead Engineer)** | Orchestration & State Machine Core | Harsh Soni | Verified & Signed Off |
| **Communications & Protocol Officer** | Interoperability & Tool Contracts | Mansi Purohit | Verified & Signed Off |
| **Data & Payload Specialist** | Grounding, MDP Logging & Return Evaluation | Ankit Kumar | Verified & Signed Off |
| **Security & Ethics Sentinel** | Safety, Cycle Detection & Guardrails | Garmi Swami | Verified & Signed Off |

---

## 2. System Architecture Diagram

```mermaid
flowchart TD
    Start["Agent(max_steps=20) — IDLE"] --> P["PERCEIVING"]
    P --> D["DELIBERATING"]
    D --> A["ACTING (JSON-Schema Validator)"]
    A --> E{"Tool Execution & Error Boundary"}
    E -->|"Valid Execution"| O["OBSERVING (Append Result)"]
    E -->|"Exception / Invalid Args"| Err["OBSERVING (Tool Execution Error)"]
    O --> R["REFLECTING"]
    Err --> R
    R --> G{"Cycle Detected (Floyd) OR Steps > 20?"}
    G -->|"Yes (Emergency Tripwire)"| H["HALTED"]
    G -->|"No & Task Incomplete"| D
    G -->|"No & Task Complete"| H