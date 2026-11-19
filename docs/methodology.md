# Methodology

Two instruments: the validation gate (decides whether a candidate is a finding)
and the report standard (decides whether a finding is submittable).

## The five-check validation gate

Run every candidate through **all five checks** before drafting anything.
Drop it if any check fails.

1. **In scope.** The asset is fully in scope per the program page. Out-of-scope
   is out — no exceptions, no "close enough".
2. **Real impact.** The flaw breaks confidentiality, integrity, or availability
   in a meaningful way. A style issue, a header, or a theoretical concern is
   not a finding.
3. **Reproducible.** The issue reproduces reliably from a clean state with
   minimal steps, on a local fork only.
4. **Understood root cause.** You can name the cause: a missing ownership check,
   an unchecked state transition, a stale value read on a privileged path.
   "Something looks wrong" is not a root cause.
5. **Not a duplicate, not intended.** The finding is not a duplicate, not
   boilerplate, not intended behavior, and not a documented trust assumption.
   Check disclosed reports, changelogs, and past audits **before** writing a PoC.

Challenge your own assumptions on every finding. Check the impact against known
issues and past audits before calling it new.

## Severity honesty

Severity must match the **proven** impact, never the theoretical impact.

- A valid finding can still be Low if no harm is demonstrated.
- A finding that needs a privileged action plus a price move plus a stale
  position is not Critical, however dramatic it sounds.
- A finding that drains one victim per transaction from a stateless router is
  High, not Critical.
- Never inflate severity. Credibility with triage teams is the asset; one
  inflated report costs more than one honest Low earns.

Use the program's own severity system when it has one (some use CVSS, others
their own matrix). State the severity with a short justification, and add a
CVSS 3.1 vector string with its calculated score when the program uses CVSS.

## The report standard

Every draft has, in this order:

1. **Title** — specific: flaw type + feature + impact, 128 characters or fewer.
   Bad: "XSS in website". Good: "Stored XSS in the comment field of
   /posts/{id} allows session takeover".
2. **Summary** — two to three sentences: flaw, location, impact.
3. **Affected contracts** — exact contract, function, and parameters, plus the
   entrypoint and any canonical addresses.
4. **Vulnerability details** — root cause plus the numbered attack sequence, and
   how it differs from sibling findings.
5. **Impact** — quantified (funds, users, state) plus honest bounds: what the
   attack *cannot* do, and why likelihood is what it is.
6. **Reproduction** — numbered deterministic steps a stranger can follow from
   zero, with exact commands and expected output (repo + commit, toolchain +
   version, test names, pass counts, verification date). **The reproduction
   section IS the proof of concept**: steps, commands, test file, and observed
   result, all in one place. A PoC file name alone is not a reproduction section.
7. **Adversarial self-check** — every plausible objection with a rebuttal:
   "the owner signed it", "the audit already noted this", "duplicate of
   sibling X", "too contrived". An unanswered objection is a missing section.
8. **Recommendation** — family-level fix plus the narrow fix, and how to verify
   the fix (re-run which PoC tests).

Target roughly 1,300 words for the description (never over the program limit).
Keep the tone professional and neutral. One report = one bug, unless a chain
is explained as a chain. Match the program's own format — read the program page
first; do not force another program's format onto a new program.

## Before writing

- Read the scope and the program rules; confirm the bug is in scope.
- Check duplicates in disclosed reports and changelogs.
- Test safely: your own accounts only, never touch other users' data, avoid DoS.
- Re-verify. No false positives.

## After submitting

- Answer triage questions quickly and politely.
- Never publish before the program resolves the issue or allows disclosure.
- Record the outcome in the finding log: accepted, rejected, duplicate, or
  awaiting triage — with the date and the program's words, not yours.
