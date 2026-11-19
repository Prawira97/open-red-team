# Open Red Team

**Open-source AI agents that audit smart contracts and prove every bug.**

Smart-contract exploits steal billions of dollars from ordinary users every year.
A professional audit costs $50,000–$500,000 and takes weeks, so small teams and
independent builders — especially in emerging markets — ship unaudited code.
The people who lose the money are not the teams; they are the users who trusted
the contracts. Existing AI audit tools are closed and proprietary, or they produce
unproven claims with no reproducible proof.

Open Red Team is a multi-agent auditing system that works the way a human security
team does: a coordinator plans the audit, parallel specialist hunters examine
different programs and contracts at once, every candidate finding must pass a
runnable proof-of-concept, and validated findings are written to a strict report
standard. No finding is reported without proof. No proof, no report.

## Proven in production

This system runs daily against live bug-bounty programs. Since November 2026:

- **24 valid findings** across 21 live programs (lending, bridges, oracles, AMMs,
  rollups, and more)
- **14 submitted / filed**, including 11 High-severity and 1 Critical finding
- Every finding backed by a **passing, executed PoC** (Foundry / Jest) — never
  claimed without a run
- Duplicates and known issues are caught and discarded *before* submission

## How it works

```
Program page + scope
      │
      ▼
┌─────────────┐
│ Coordinator │  plans the audit, assigns programs, enforces the standard
└──────┬──────┘
       │ spawns parallel hunters
       ▼
┌──────────┐ ┌──────────┐ ┌──────────┐
│ Hunter 1 │ │ Hunter 2 │ │ Hunter N │  read scope → map attack surface →
└────┬─────┘ └────┬─────┘ └────┬─────┘  build test matrix → hunt
     │           │            │
     ▼           ▼            ▼
        Validation gate (5 checks — all must pass)
     │           │            │
     ▼           ▼            ▼
   Runnable PoC on a local fork (Foundry / Jest)
     │           │            │
     ▼           ▼            ▼
   Report draft (report standard — see docs/methodology.md)
```

See [docs/architecture.md](docs/architecture.md) for the full pipeline and
[docs/methodology.md](docs/methodology.md) for the validation gate and report standard.

## What's in this repo

- `docs/architecture.md` — the coordinator/hunter pipeline, end to end
- `docs/methodology.md` — the five-check validation gate and the report standard
- `docs/quickstart.md` — run your first audit
- `playbooks/web3-hunt-playbook.md` — the hunter playbook: attack-surface mapping,
  test matrices, local-fork PoCs, reachability from attacker-only state
- `examples/public-case-study.md` — a walkthrough of a real, already-public finding

## Quickstart

```bash
git clone https://github.com/Prawira97/open-red-team.git
cd open-red-team
# 1. Read docs/quickstart.md — pick a program, verify the scope.
# 2. Map the attack surface and build your test matrix.
# 3. Hunt. Every candidate goes through the validation gate.
# 4. Prove it with a runnable PoC on a local fork. No proof, no report.
# 5. Write the draft to the report standard and submit through the
#    program's own channel.
```

Full steps: [docs/quickstart.md](docs/quickstart.md).

## Security policy

- **Authorized testing only.** Use this framework exclusively on programs and
  contracts you are authorized to test — bug-bounty programs in scope, your own
  code, or code you have explicit written permission to audit.
- **Local forks only.** Never test on mainnet or a public testnet. Never touch
  other users' funds or data. Never run destructive tests.
- **Responsible disclosure.** Never publish a vulnerability before the affected
  program has resolved it or explicitly allowed disclosure. This repo contains
  no live vulnerability details and no exploit code for unpatched bugs —
  only methodology and one already-public case study.

## License

Apache License 2.0 — see [LICENSE](LICENSE). Free to use, modify, and ship,
including commercially, as long as the license and notices are kept.

## Status

Actively developed and used in production. The framework is being published as
a public good with support from the Sentient Foundation Open Source AGI Grant
Program (application pending).
