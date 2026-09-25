# How to Use This Repository

This repository is the official starting point for:

**Cube Buildathon · 04 · Returns Manager**

Round 2 is an **individual build**. Each participant works in their **own GitHub fork** of this repository.

---

## 1. The GitHub Workflow

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

You do **not** need to:

* create a branch in the organiser's repository,
* create `submissions/<your-username>/`,
* open a PR into the organiser repository,
* wait for the organisers to merge your code.

Your own fork is your Round 2 development and submission repository.

---

## 2. One-Time Setup

You need:

* A GitHub account
* Git installed on your computer
* A development environment suitable for your chosen technology stack

Set your Git identity if you have not already:

```sh
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

You can verify it with:

```sh
git config --global --list
```

If you use SSH, test it with:

```sh
ssh -T git@github.com
```

For HTTPS, you can authenticate using GitHub CLI:

```sh
gh auth login
```

---

## 3. Fork the Repository

Open the official repository:

```text
https://github.com/Cube-Build-A-Thon/cube-04-returns-manager
```

Click:

**Fork → Create fork**

Create the fork under your own GitHub account.

---

## 4. Clone Your Fork

Clone **your fork**, not the organiser repository.

### HTTPS

```sh
git clone https://github.com/<your-github-username>/cube-04-returns-manager.git
cd cube-04-returns-manager
```

### SSH

```sh
git clone git@github.com:<your-github-username>/cube-04-returns-manager.git
cd cube-04-returns-manager
```

Replace `<your-github-username>` with your GitHub username.

---

## 5. Start Building

After cloning:

1. Read [`README.md`](README.md).
2. Read [`RULES.md`](RULES.md).
3. Review the sample data in [`data/`](data/).
4. Understand the Returns Manager workflow.
5. Build your solution in your fork.
6. Test and evaluate it.
7. Document your architecture and results.
8. Deploy where applicable.
9. Submit your final repository through the official submission form.

A recommended workflow is:

```text
Understand
    ↓
Build
    ↓
Test
    ↓
Evaluate
    ↓
Document
    ↓
Deploy / Demo
    ↓
Submit
```

---

## 6. Repository Structure

You are free to choose your own application structure.

For example:

```text
cube-04-returns-manager/
│
├── data/
├── src/
├── tests/
├── README.md
├── RULES.md
├── GITHUB-GUIDE.md
├── ARCHITECTURE.md
└── ...
```

This is only an example. Your final structure should be clear and easy to run.

---

## 7. Commit and Push

Commit your work regularly.

```sh
git status
git add .
git commit -m "Implement returns condition assessment"
git push origin main
```

You may also use your own development branches:

```sh
git checkout -b feature/returns-assessment
```

The branch structure inside **your own fork** is your choice.

Use meaningful commit messages such as:

```text
Implement identity matching
Add completeness checks
Add condition assessment
Implement disposition logic
Add uncertainty handling
Add evaluation metrics
Document architecture
```

Avoid unclear messages such as:

```text
update
changes
final
final2
fix
```

---

## 8. Build-Phase Commit Rule

All code commits that form your Round 2 submission must be made during the **authorised build phase**.

Round 2 build begins:

**25 September 2026 · 9:00 AM IST**

Once the build phase ends, do not continue making Round 2 code changes.

Your submitted repository should represent the work completed during the authorised build phase.

---

## 9. Do Not Commit Secrets

Never commit:

* API keys
* passwords
* access tokens
* private keys
* real credentials
* `.env` files containing secrets

Use environment variables instead.

If you accidentally expose a credential, revoke it immediately.

---

## 10. Testing Before Submission

Before submitting, test the complete workflow:

```text
Return Input
     ↓
Identity
     ↓
Completeness
     ↓
Condition
     ↓
Disposition
     ↓
Evidence / Decision
```

Test both normal and difficult cases, including:

* missing evidence,
* ambiguous cases,
* contradictory evidence,
* invalid identifiers,
* model/dependency failures.

---

## 11. Recommended API Interface

You may choose your own framework and technology stack.

For HTTP-based solutions, these interfaces are recommended:

```text
POST /agent
```

for the main Returns Manager operation.

```text
GET /health
```

for service health.

These are recommendations, not requirements to use a specific framework.

Document your actual implementation in `README.md`.

---

## 12. Submission

The official submission form opens from:

**27 September 2026**

Final deadline:

**1 October 2026 · 6:00 PM IST**

The submission form closes permanently at the deadline.

There will be:

**No reopening and no resubmission.**

Your submission should contain the required:

* GitHub repository
* README
* architecture documentation
* evaluation results
* demo video
* deployment URL, where applicable
* LinkedIn post URL

---

## 13. Mandatory LinkedIn Post

Your Round 2 LinkedIn post must:

* mention your Returns Manager build,
* explain what you built,
* tag **CodeQuesters**,
* tag **Sydon.AI**.

Include the live LinkedIn post URL in the submission form.

The organisers will share the official LinkedIn post template separately.

---

## 14. Common Git Commands

Check status:

```sh
git status
```

View recent commits:

```sh
git log --oneline -10
```

Add changes:

```sh
git add .
```

Commit:

```sh
git commit -m "Add returns evidence handling"
```

Push:

```sh
git push origin main
```

Create a branch:

```sh
git checkout -b feature/my-change
```

Switch back to main:

```sh
git checkout main
```

---

## 15. Common Problems

| Problem                         | What to check                                                                               |
| ------------------------------- | ------------------------------------------------------------------------------------------- |
| `repository not found`          | Make sure you cloned your own fork and the repository URL is correct.                       |
| `permission denied`             | Check that you are authenticated to the GitHub account that owns the fork.                  |
| Push rejected                   | Run `git pull` and resolve any conflicts before pushing again.                              |
| Environment not working         | Check dependencies, environment variables and the README setup instructions.                |
| Model/API failure               | Preserve the available information and use an appropriate review/uncertain state.           |
| Missing evidence                | Do not invent evidence. Return an appropriate uncertain/review outcome.                     |
| Accidentally committed a secret | Revoke the credential immediately and remove it from the repository history as appropriate. |

---

## 16. Final Checklist

Before submitting:

```text
[ ] Working Returns Manager
[ ] Working in my own GitHub fork
[ ] Required code commits completed during the build phase
[ ] README.md complete
[ ] RULES.md reviewed
[ ] ARCHITECTURE.md complete
[ ] Identity tested
[ ] Completeness tested
[ ] Condition tested
[ ] Disposition tested
[ ] UNCERTAIN / review handling tested
[ ] Evidence trace implemented
[ ] Evaluation completed
[ ] Failure modes documented
[ ] Demo ready
[ ] Deployment URL verified, if applicable
[ ] LinkedIn post published
[ ] CodeQuesters tagged
[ ] Sydon.AI tagged
[ ] Submission links verified
[ ] Final submission ready before 1 October 2026 · 6:00 PM IST
```

---

## Final Reminder

**Fork → Build → Test → Evaluate → Document → Submit**

Your fork is your Round 2 repository.

Build independently, keep your work traceable, and make sure the final submission is ready before the deadline.

**Cube Buildathon · 04 · Returns Manager**
