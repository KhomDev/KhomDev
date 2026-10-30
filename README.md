# KhomDev

### Bounty economics & triage forensics

I study why security findings don't get paid — and build the tooling that fixes it.

---

**113 logged rejections. 78 of them — 69% — were preventable before I read a line of code.**

That number is the thesis. Most bug-bounty effort is not lost to hard bugs. It is lost to findings
that were dead on arrival — duplicates, excluded roles, prior audits, payout floors — all knowable
*before* anyone opens an editor.

So I logged every rejection I ever got, classified each one by the gate that should have caught it,
and built the gates.

| Repo | What it is |
|---|---|
| **[rejection-taxonomy](https://github.com/KhomDev/rejection-taxonomy)** | 113 real rejections — **what the bug was**, why it failed, and the earliest gate that could have caught it. The dataset behind the 69%. |
| **[bounty-economics](https://github.com/KhomDev/bounty-economics)** | Payout-tier and exclusion-clause taxonomies as data, plus a validator for your own private program ledger. |
| **[viability-gate](https://github.com/KhomDev/viability-gate)** | Rust CLI scoring a draft finding against 22 rejection anti-patterns and 7 pre-hunt gates. Offline, deterministic, no API key. |
| **[realism-gate](https://github.com/KhomDev/realism-gate)** | Rust CLI that reads a Foundry PoC and flags what makes a passing test prove less than it claims — privileged pranks, state written with cheatcodes, assertions that cannot fail. 14 rules, measured on 886 public exploit reproductions. |

---

### What the data says

Across 113 rejections:

| Triage outcome | Count | Share |
|---|---:|---:|
| Duplicate / previously reported | 43 | 38.1% |
| Out of scope — boundary or exclusion clause | 26 | 23.0% |
| Informational — no security impact | 24 | 21.2% |
| Intentional design / not a bug | 16 | 14.2% |
| **Valid, but below the payout floor** | **3** | **2.7%** |
| SPAM — fabricated impact contradicted by my own PoC | 1 | 0.9% |

**Duplicates and scope alone are 69 of 113.** Three findings were confirmed valid and still paid
nothing, because the program had no tier at that severity. The bottleneck was never analysis.

Every row also records *what the bug was*:

| Bug family | Count | | Bug family | Count |
|---|---:|---|---|---:|
| `accounting` | 18 | | `panic` / `rewards` | 5 each |
| `input_validation` | 13 | | `fees` | 4 |
| `liveness` | 9 | | `signature_binding` / `liquidation` / `replay` | 3 each |
| `config` | 8 | | `reentrancy` / `governance` / `rounding` | 2 each |
| `state_machine` / `access_control` / `token_integration` / `oracle` / `async_ordering` | 7 each | | `secrets` | 1 |

Accounting and input validation are over a quarter of everything — not exotic cryptography, just
value counted wrong and input trusted when it should not be.

### Where they died

| Earliest gate that would have caught it | Count |
|---|---:|
| Duplicate / known-family check | 41 |
| Exclusion-clause transcription | 20 |
| No-attacker-win analysis | 14 |
| Intentional design / no-impact review | 13 |
| Prior-audit sweep | 7 |
| Payout-tier check | 5 |
| Out-of-scope file tree | 4 |
| Realism gates | 3 |
| Below severity floor | 2 |
| Program ceiling | 1 |
| Cooperating-party exit | 1 |
| Test-suite intention grep | 1 |
| Headline-vs-evidence mismatch | 1 |

**The six pre-hunt gates account for 78 of 113.** All runnable before you open an editor.

The three rows that died at the realism gates are the ones that hurt most: the bug was real, and
the proof of concept proved something the attacker could not do. That is what
[realism-gate](https://github.com/KhomDev/realism-gate) now checks before I submit.

---

### Background

Vyper and DeFi security first — stablecoins, vaults, DEXs, invariant-first. That is where I learned
to read a system rather than a function, and it is why the economics interest me: a finding that
cannot be paid for is a finding that does not exist.

Now I work a deliberately unfashionable lane: **non-EVM ecosystems where the audit supply is thin
and the same bug classes are far less picked over.** That is where a researcher's marginal hour buys
the most, and it is the same reasoning as the gate work above — go where the crowd is not.

I also build the audit infrastructure I use: evidence-gated pipelines, generated invariant
harnesses, and adversarial validation — because the gates above only work if something enforces them.

---

### Elsewhere

- Site — [khomdev.org](https://khomdev.org)
- Writing — [Paragraph](https://paragraph.com/@yuriykhomenkov@gmail.com)
- X — [@YKhomenkov](https://x.com/YKhomenkov)

If you are a researcher: the data is free, and the taxonomy is the part worth stealing.
If you are a team: I am available for scoped review, and I will tell you what I could not break.
