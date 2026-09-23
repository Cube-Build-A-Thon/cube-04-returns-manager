# Rules

There are two sets. The **repository rules** keep a hundred people from breaking each other's work, and GitHub enforces them. The **engineering rules** are part of what you are assessed on.

## Repository rules (enforced)

| # | Rule | How it's enforced |
|---|---|---|
| R1 | Nobody pushes directly to `main`. | Branch protection on `main` |
| R2 | Every change reaches `main` through a pull request. | Branch protection: PR required |
| R3 | Only **@Cube-Buildathon** can approve and merge into `main`. | Branch protection: merge restricted to @Cube-Buildathon; CODEOWNERS review required |
| R4 | Your branch name is your GitHub username. | `submission-guard` check, required to pass |
| R5 | You change files **only** inside `submissions/<your-github-username>/`. | `submission-guard` check, required to pass |
| R6 | `main` can't be force-pushed or deleted. | Branch protection |
| R7 | No secrets in the repo: API keys, tokens, passwords, `.env` files. | You. A leaked key is revoked, and it's noted against the submission. |
| R8 | Don't edit, delete or rename another person's branch or folder. | You. Doing so is grounds for removal from the event. |

The shared `data/` files and top-level docs are read-only for you. If one is wrong, open an Issue labelled `finding`.

## Engineering rules (not negotiable)

These are the craft part of the assessment. Each one is cheap to follow now and expensive to retrofit.

### 1. Tenancy isolation before any feature
Every table gets row-level security scoped to the organisation, **enabled and forced**. Test that a second organisation sees zero rows, and that it can't fetch another organisation's image by guessing a key. Row isolation with a shared, guessable image path is a leak that looks green.

*The sample data has two orgs (`org_demo_alpha`, `org_demo_bravo`) for exactly this test.*

### 2. Batch your model calls
Make **one** call per unit carrying all checks, never one call per check. At prep volumes that is the difference between a 90% gross margin and none.

### 3. Fail open
A model error or timeout still saves the capture and still produces a record, marked `pending`. Nothing blocks the operator. Anything that makes a warehouse line wait gets worked around within a day of deployment.

### 4. Uncertain is a valid verdict
It isn't a low-confidence pass. A model that declines to judge a bad photo is more credible to an operations person than one that is confidently wrong. Build it as a first-class outcome and show it in the interface.

*The sample data uses `uncertain` and `pending_review` as values on purpose.*

### 5. Look authoritative rules up
Where the channel publishes the requirement, retrieve it. Don't let a model recall it from memory, and don't infer it from examples. **That includes the sample CSVs in this repo.** Their requirement flags and fee amounts are dummy values.

## Honesty rules (assessed)

- **Say what you built, not what it sounds like.** You have a content hash. You don't have a tamper-evident, immutable or anchored record, unless you actually built one and can show it.
- **Overrides are data.** When an operator disagrees with the agent, capture the original verdict, the new verdict and a reason. Never discard those rows silently.
- **"It works well" isn't a result.** Report a number per check, with false positives and false negatives separately and the method written down. An honest 61% you can break down beats a 95% you can't.
- **Contradictions are findings.** Where the background documents disagree, raise it. Don't silently pick one side.
