# Quickstart — run your first audit

## Prerequisites

- A local EVM toolchain: [Foundry](https://book.getfoundry.sh/) (`forge`, `cast`,
  `anvil`) for smart-contract PoCs, or Jest for off-chain services.
- `git`, Node.js 20+.
- An RPC endpoint for forking mainnet state (any public endpoint works for
  read-only forking; you never send transactions to it).
- A bug-bounty program whose scope you have read in full.

## 1. Pick a program and verify the scope

Read the program page end to end: assets in scope, assets out of scope, rules
(PoC required? KYC? severity system? disclosure policy?), and rewards.
Write down the scope before touching any code. If an asset is not named, it is
not in scope.

## 2. Map the attack surface

Clone the target repo at the program's pinned commit. Enumerate the assets the
program names, then trace data flow across contracts, roles, and states.
Note: complex state-changing features, fund/balance logic, multi-role access
paths, third-party integrations — in that order of priority.

## 3. Build the test matrix

For every core feature, list:
- Actors who can reach it (unauthenticated → low privilege → cross-tenant → admin).
- Input vectors (parameters, bodies, headers, cross-contract calls).
- The guards and middleware on each path.

For smart contracts, trace user-controlled sources to dangerous sinks.

## 4. Hunt

Work in waves: one wave covers several programs or contract families, Critical
first, then High. Record what you checked even when you find nothing — a
negative result with evidence is a finished wave; silence is not.

## 5. Validate (the gate)

Run every candidate through the five checks in `docs/methodology.md`.
Drop it if any check fails. Check duplicates against disclosed reports and
past audits **before** writing a PoC.

## 6. Prove it on a local fork

```bash
# Example: Foundry test against a pinned commit
forge test --match-contract <YourPoC> -vvv
# Expected: all tests pass, with the exploited effect visible in the output
# (funds moved, state frozen, access gained) — from attacker-only state.
```

Record the exact commands, the fork block, the attacker address, the executed
transactions, and the observed on-chain effect. Re-run after any change.

## 7. Write the draft and submit

Write the draft to the report standard (`docs/methodology.md`), run the
completeness check, then submit through the program's own channel.
Log the outcome. Never publish before the program resolves it or allows
disclosure.

## Rules

- Local forks only. Never mainnet, never a public testnet.
- Your accounts only. Never other users' funds or data.
- No proof, no report. No inflated severity. One bug per report.
