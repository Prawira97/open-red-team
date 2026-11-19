# Public case study — ethrex issue #7553

This is a walkthrough of a real finding from this system, chosen because it is
already public: it was filed as a public GitHub issue by the researcher, so
describing it here discloses nothing new.

- **Issue:** https://github.com/lambdaclass/ethrex/issues/7553
- **Program:** Ethereum execution-client security (public disclosure via GitHub issue)
- **Status:** filed 2026-11-19; awaiting triage at the time of writing

## What the system did

1. **Scoped the target.** The hunt covered the ethrex execution client at a
   pinned commit, against the Ethereum bug-bounty rules.
2. **Mapped the surface.** The hunter traced the relevant execution path across
   the client instead of auditing one function in isolation.
3. **Built the candidate.** A concrete flaw was identified with a named root cause.
4. **Validated.** The candidate passed the five-check gate: in scope, real
   impact, reproducible from a clean state, understood root cause, and — checked
   first — not a duplicate of any disclosed report or known issue.
5. **Proved it.** A runnable proof was built and executed on a local setup, with
   exact commands and observed output recorded.
6. **Reported.** The draft followed the eight-section report standard
   (summary, affected contracts, vulnerability details, impact, reproduction,
   adversarial self-check, recommendation) and was filed as a public issue.

## Why this case study matters

It shows the whole pipeline working on a real target: scope → surface map →
candidate → gate → runnable proof → standard report → public filing. The
finding itself is visible at the link above; what this repo adds is the
method that produced it, so anyone can run the same pipeline on their own
targets.

## What is NOT in this repo

Live vulnerability details and exploit code for unpatched bugs are deliberately
absent. Findings under triage stay private until the affected program resolves
them or allows disclosure — publishing them early would put users at risk and
can void bounty eligibility. Only methodology and already-public cases are
published here.
