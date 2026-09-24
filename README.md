## Alexandre Pinoteau

**I build agents that investigate, and I measure when they get it wrong.**

AI × threat intelligence. I work where CTI, OSINT and SOC meet LLM agents. The question I care about
is not *"can an agent do threat intel?"* but *"how do you prove it didn't hallucinate an attribution?"*

---

### Selected work

**[Bounce-CTI](https://bounce.alexandre-pinoteau.fr/)** · [source](https://github.com/Iskandeur/bounce-cti)
An autonomous CTI investigation agent. Give it one observable (domain, IP, hash, JARM, even the bare
filename of a malicious binary) and a headless Claude Code agent pivots across ~50 public sources,
using MCP tools only. Each run is capped at 3 hops and ~60 calls, and the infrastructure graph streams
live to the browser. CDN ranges, parking nameservers and sinkholes are defused *before* anything gets
pivoted on. Anything the model proposes from its own knowledge stays a **lead**: its confidence is
capped at 0.35, it is kept out of every export (STIX, blocklists, detection rules), and it only becomes
a finding once a primary source corroborates it.
It ships with **[EVAL_PROTOCOL v3](https://github.com/Iskandeur/bounce-cti/blob/main/EVAL_PROTOCOL.md)**:
12 real-world cases scored separately on capability and recall, with benign seeds that test whether
the agent knows when to stop. A single hallucinated node or edge fails the whole run. Latest published
run: capability 92.9/100 on the fresh subset, no hallucinated nodes.

**[System 1 / System 2](https://iskandeur.github.io/system1-system2/)** · [study](https://iskandeur.github.io/system1-system2/study.html) · [source](https://github.com/Iskandeur/system1-system2)
When should a cheap decision model hand an input over to a frontier LLM? Eight recorded tasks, with
every item answered by both models, so the router is judged on real answers. On 600 MASSIVE
utterances, the small model's confidence is well calibrated (ECE 4.5 %, AUROC 0.83). The prompt
injection result is the important one: a one-line *"annotation team re-labelled this"* payload flips
GPT-5.2 on **80 of 80** items, against 26 of 80 for the small model. Sending attacked inputs "up" to
the bigger model therefore makes the hybrid *worse*.

**[Swarm Studio](https://iskandeur.github.io/swarm-studio/)** · [source](https://github.com/Iskandeur/swarm-studio)
Design, run and watch multi-agent swarms in the browser. The topology is the object you work on:
who may talk to whom, human approval gates, shared memory, and typed decision nodes that escalate to
an LLM only when they are unsure. There is no backend, and a demo provider runs it without an API key.

**[splunk-lab-in-a-box](https://github.com/Iskandeur/splunk-lab-in-a-box)**
A self-hosted Splunk lab. It indexes the official Buttercup Games dataset (109,864 events,
time-shifted so "last 24 hours" still returns data) and has nine labs whose answer keys were measured
on the running instance. `lab.sh verify` runs ten readiness checks. An AI coding agent can drive and
grade the labs through `AGENTS.md`.

**[CyberZap](https://github.com/Iskandeur/cyber-zap-public)**
A CTI triage pipeline on n8n. It pulls CISA KEV, CERT-FR, ZDI and ransomware.live, has an LLM score
and summarise each item, and sends the alerts to chat.

**[compagnon-starter](https://github.com/Iskandeur/compagnon-starter)**
A starter kit for a persistent Claude Code agent. Its identity, memory and procedures live in
versioned Markdown, and the agent runs its own onboarding on the first session.

---

### How I work

- **A lead is not a finding.** If no source backs it, it stays labelled as a lead and never reaches an export.
- **Hallucination is a gate, not a metric.** One invented node fails the run.
- **Restraint gets a score too.** An agent that pivots on Cloudflare or Wikipedia is wrong, even when it's busy.
- **Negative results get published.** "Escalation buys nothing on this task" is a result.

**Toolbox:** Claude Code (headless), MCP servers, OpenRouter · Python / FastAPI, TypeScript / React,
Node · STIX 2.1, OpenCTI, passive DNS / CT / RDAP pivoting · Splunk SPL, Sigma, KQL, YARA, ELK ·
Volatility, Zimmerman tools, MITRE ATT&CK.

[Website](https://alexandre-pinoteau.fr/) · [LinkedIn](https://www.linkedin.com/in/p1n0t34u/) · [Email](mailto:alexandre.pinoteau@protonmail.com)
