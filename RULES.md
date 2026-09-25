# Rules

These rules define how you should build, test and submit your **Returns Manager** for **Cube Buildathon — Round 2**.

Round 2 is an **individual build**. Your solution is assessed on both the quality of the working agent and the engineering practices behind it.

---

# 1. Round 2 Repository Rules

## R1 — Individual Build

Round 2 is an **individual build**.

Each participant must independently build the **04 · Returns Manager** solution they selected.

Do not submit another participant's work.

---

## R2 — Use Your Own Fork

Fork this official repository into your own GitHub account.

Your fork is your Round 2 development and submission repository.

The intended workflow is:

```text
Official Repository
        ↓
      Fork
        ↓
 Your GitHub Fork
        ↓
 Build + Test
        ↓
 Commit + Push
        ↓
 Final Submission
```

---

## R3 — No Shared Repository Workflow

You do not need to:

* create a participant branch in the organiser repository,
* create `submissions/<your-github-username>/`,
* open a pull request into the organiser repository,
* wait for the organisers to merge your work.

Build your complete solution inside your own fork.

---

## R4 — Build-Phase Commits Only

All code commits that form your Round 2 submission must be made during the **authorised Round 2 build phase**.

Once the build phase ends:

* do not continue making Round 2 code changes,
* do not add new implementation features,
* do not silently replace the submitted implementation with a later version.

Your submitted repository should represent work completed during the authorised build phase.

---

## R5 — Final Submission Deadline

The final Round 2 submission deadline is:

**1 October 2026 · 6:00 PM IST**

The submission form closes permanently at this time.

There will be **no reopening and no resubmission**.

---

## R6 — No Resubmission

Once you submit the official submission form, your submission is **final**.

You cannot replace the repository, code, demo, documentation or other submitted information after submission.

Check everything before submitting.

---

## R7 — No Secrets

Do not commit:

* API keys,
* access tokens,
* passwords,
* private credentials,
* `.env` files containing secrets,
* private keys.

Use environment variables or appropriate secret-management practices.

If you accidentally expose a credential, revoke it immediately.

---

## R8 — Do Not Damage the Official Repository

Do not attempt to modify, delete or interfere with the organiser's official repository, other participants' forks, or other participants' work.

Your development work should remain inside your own fork.

---

# 2. Engineering Rules

These are part of the technical assessment.

## 1. Tenancy Isolation Before Features

If your implementation stores persistent data, organisation/client data must remain isolated.

Test that:

* a second organisation sees zero rows belonging to another organisation,
* one organisation cannot access another organisation's images or evidence by guessing a key,
* identifiers cannot be used to bypass tenant boundaries.

The sample data contains two organisations:

```text
org_demo_alpha
org_demo_bravo
```

Use them to test isolation.

Row isolation combined with a shared, guessable image path is still a data leak.

---

## 2. Batch Your Model Calls

Use model calls efficiently.

Where multiple related checks can be safely evaluated together, avoid unnecessary repeated calls.

Do not automatically create one expensive model request for every small field when a well-structured batched request can perform the related reasoning safely.

Think about both:

* latency,
* cost.

---

## 3. Fail Open

A model error, timeout or temporary dependency failure should not silently discard the capture or incoming record.

The system should preserve the available information and move the case into an appropriate state such as:

```text
pending
review
uncertain
```

The operator should not lose the case simply because a dependency failed.

---

## 4. Uncertain Is a Valid Verdict

`UNCERTAIN` is a first-class outcome.

It is **not** a low-confidence PASS.

Use it when the available evidence does not support a reliable judgment.

For example:

```text
Poor / ambiguous evidence
          ↓
      UNCERTAIN
          ↓
    Human Review
```

A system that correctly refuses to make an unsupported judgment is preferable to one that confidently produces the wrong decision.

The sample data intentionally includes values such as:

```text
uncertain
pending_review
```

---

## 5. Look Authoritative Rules Up

Where an external channel publishes the relevant requirement, retrieve the authoritative rule.

Do not rely on:

* model memory,
* assumptions,
* synthetic examples,
* or sample CSV values

as the source of truth.

The data in this repository is synthetic.

Requirement flags, condition information and other sample values are provided for engineering and evaluation, not as authoritative external rules.

---

# 3. Returns Manager Evidence Rules

## 1. Capture Decision Evidence

Your agent should produce evidence that supports its decisions.

A reviewer should be able to understand:

```text
Returned Item
      ↓
Identity Check
      ↓
Completeness Check
      ↓
Condition Check
      ↓
Disposition
      ↓
Evidence / Decision Record
```

Do not make important decisions impossible to explain.

---

## 2. Use the Official Evidence Contract

Use the official Buildathon evidence contract as the baseline for interoperability.

Relevant evidence concepts include:

* `record_id`
* `schema_version`
* `organization_id`
* `client_id`
* `agent`
* `subject`
* `captured_at`
* `operator_label`
* `images`
* `checks`
* `outcome`
* `overrides`
* `status`
* `content_hash`

Where applicable, checks should include useful information such as:

* `check_key`
* `verdict`
* `confidence`
* `detail`
* `model_version`
* `latency_ms`

---

## 3. Overrides Are Data

When an operator disagrees with an agent decision, preserve the disagreement.

Where your system supports overrides, capture:

* the original verdict,
* the revised verdict,
* the reason for the override.

Do not silently replace the original decision.

---

# 4. Returns-Specific Decision Rules

The Returns Manager should reason about four core questions:

```text
1. Is this the item that was sold?

2. Is it complete?

3. What condition is it in?

4. What should happen to it next?
```

The implementation should support appropriate outcomes for:

* identity,
* completeness,
* condition,
* disposition.

Use the published condition scale where required. Do not invent a different condition taxonomy and present it as the official scale.

---

# 5. Evaluation Rules

Evaluation is part of the Round 2 assessment.

Your evaluation should demonstrate whether the agent performs its required checks reliably.

## Evaluate the important checks

Where applicable, report performance for:

* identity,
* completeness,
* condition,
* disposition.

Also evaluate uncertainty and review handling.

---

## Use Appropriate Evaluation Data

Where applicable, use an unseen/held-out evaluation set rather than repeatedly tuning against the final evaluation cases.

For the vision-oriented portions of the task, the recommended evaluation approach includes:

* at least **50 unseen units** where applicable,
* two independent human labels,
* measurement of human agreement where practical,
* varied image conditions,
* genuinely ambiguous cases.

---

## Report the Results

Report:

* results per important check,
* false positives,
* false negatives,
* `UNCERTAIN` / review rate,
* important failure modes,
* latency/cost where relevant.

Explain how the numbers were calculated.

Do not report only selected examples that make the system appear successful.

---

# 6. Honesty Rules

## 1. Say What You Built

Describe the actual implementation.

For example, having a `content_hash` does not automatically mean that your records are:

* tamper-evident,
* immutable,
* anchored,
* or independently verifiable.

Only make those claims if you actually implemented and demonstrated them.

---

## 2. "It Works Well" Is Not a Result

Use measured results.

For example:

```text
Identity
Accuracy: 91%
FP: 4
FN: 5

Completeness
Accuracy: 87%
FP: 6
FN: 7
```

Then explain the important failure modes.

An honest result that you can break down is more useful than a high number without methodology.

---

## 3. Contradictions Are Findings

If source documents, datasets or requirements contradict one another:

**raise the contradiction.**

Do not silently choose whichever interpretation produces the desired result.

Document what conflicts and how your implementation handles the uncertainty.

---

# 7. Submission Rules

Your final submission should contain the required:

* GitHub repository,
* working implementation,
* `README.md`,
* `ARCHITECTURE.md`,
* evaluation results,
* demo video,
* deployment URL where applicable,
* LinkedIn post URL.

The LinkedIn post is **mandatory** for Round 2.

Your post must tag:

**CodeQuesters**

and

**Sydon.AI**

---

# 8. Final Deadline

## 1 October 2026 · 6:00 PM IST

The official submission form closes permanently at this time.

Everything required for Round 2 should be complete before the deadline.

---

# 9. Final Submission Policy

Once you submit:

**Your submission is final.**

There is:

* no resubmission,
* no replacement submission,
* no reopening of the form after the deadline.

Verify your repository, demo, documentation and links before clicking Submit.

---

# 10. Round 2 → Round 3

Round 2 is an **individual build**.

Participants selected for Round 3 will work in five-person Pods combining:

```text
Receiving Manager
+
Prep Manager
+
Pack Manager
+
Returns Manager
+
Recovery Manager
```

Round 3 focuses on integrating the five specialised agents into one connected end-to-end commerce system.

Your Round 2 implementation should therefore have clear outputs, evidence and interfaces that another system can understand.

---

# 11. Round 2 Scoring

Round 2 is scored out of **100 points**.

| Criterion                                    |  Points |
| -------------------------------------------- | ------: |
| Problem Understanding & Solution Relevance   |  **15** |
| Agent Functionality & Decision Quality       |  **25** |
| Evaluation, Accuracy & Uncertainty Handling  |  **25** |
| Evidence, Traceability & Engineering Quality |  **20** |
| UX, Demo & Documentation                     |  **15** |
| **TOTAL**                                    | **100** |

For participants who reach
