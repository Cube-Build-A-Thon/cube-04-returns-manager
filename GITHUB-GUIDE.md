# How to use this repository

This repo is shared by everyone working on **04 · Returns Manager**. About a hundred people work in it at once. That only works if everyone follows the same four rules:

1. **One branch per person.** Name it exactly your GitHub username.
2. **One folder per person.** Everything you add goes in `submissions/<your-github-username>/`.
3. **You never push to `main`.** You open a pull request (PR) from your branch into `main`.
4. **Only the organisers merge.** Your PR is reviewed and merged by **@Cube-Buildathon**. Nobody else can merge into `main`, and GitHub enforces this.

An automatic check runs on every PR. It **fails** if your branch name doesn't match your username, or if you changed any file outside your own folder. That check is what stops a hundred people from overwriting each other.

---

## 0. One-time setup

You need `git` installed and a GitHub account that has been added to this repository. If you can't push, you haven't been added yet. Ask an organiser.

Set your identity once, if you haven't before:

```sh
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"   # use the email on your GitHub account
```

If you use SSH, check it works with `ssh -T git@github.com`. It should greet you by username. If you'd rather use HTTPS, the easiest way to sign in is the GitHub CLI: `gh auth login`.

## 1. Clone the repo

```sh
git clone git@github.com:Cube-Build-A-Thon/cube-04-returns-manager.git
cd cube-04-returns-manager
```

HTTPS works too: `git clone https://github.com/Cube-Build-A-Thon/cube-04-returns-manager.git`

## 2. Create your branch

Use your **GitHub username** as the branch name. It is case-insensitive, but lowercase is safest.

```sh
git checkout main
git pull
git checkout -b <your-github-username>
```

Example: if your username is `priya-k`, your branch is `priya-k`.

## 3. Create your folder

```sh
mkdir -p submissions/<your-github-username>
cp submissions/_TEMPLATE/README.md submissions/<your-github-username>/README.md
```

Put everything in here: your customer letter, PR/FAQ, one-pager, CLAUDE.md, build brief, build log, eval report and code. The expected layout is in [`submissions/_TEMPLATE/README.md`](submissions/_TEMPLATE/README.md).

**Do not edit** anything outside your folder. That includes the shared `data/` files, the top-level docs, `.github/`, and other people's folders. If you think a shared file is wrong, open an **Issue** instead (see section 7).

## 4. Commit and push, often

```sh
git add submissions/<your-github-username>/
git commit -m "Face 1: customer letter first draft"
git push -u origin <your-github-username>     # -u is only needed the first time
```

After the first push, `git push` is enough. Push at least once a day. Your branch is your backup, and organisers read your build log from it.

Never commit secrets: API keys, `.env` files, passwords, tokens. Use a `.env` file and keep it out of git by adding it to `.gitignore` inside your folder. If you do push a key by accident, **revoke the key immediately**. Deleting the commit doesn't help, because it has already been exposed.

## 5. Open a pull request into `main`

Open a PR when you're ready to submit a deliverable, for example at the end of a face:

1. Go to `https://github.com/Cube-Build-A-Thon/cube-04-returns-manager`
2. GitHub usually shows a **"Compare & pull request"** banner for your branch. Click it. If there's no banner, go to **Pull requests → New pull request**, set **base: `main`** and **compare: `<your-github-username>`**.
3. Title it like this: `[<your-github-username>] Face 1 – customer letter, PR/FAQ, one-pager`
4. Fill in the PR template checklist.
5. Click **Create pull request**.

Or from the terminal: `gh pr create --base main --fill`

Keep **one open PR** for your branch. New pushes to the branch are added to the same PR automatically. There's no need to open a new one per commit.

## 6. What happens next

- The **submission-guard** check runs within a minute. A green tick means you're fine. A red X means it tells you exactly which file or branch-name problem to fix. Fix it, push again, and it re-runs.
- **@Cube-Buildathon** reviews and merges. You can't merge it yourself, and neither can other contestants.
- After it merges, keep working on the **same branch**. Run `git pull origin main` first to pick up everyone else's merged work.

## 7. Asking for help, or reporting a problem

- **Something in the shared data or docs is wrong or contradicts itself**: open an Issue with the label `finding`. The brief says contradictions are findings, so raise them rather than silently picking one.
- **Access or permission problems**: open an Issue with the label `access`, or message an organiser.
- **Cross-pod contract discussion** (how your record shape connects to other pods): use this repo's **Discussions** tab if it's enabled, otherwise an Issue with the label `contract`.

## Common problems

| Symptom | Fix |
|---|---|
| `remote: Permission to ... denied` | You haven't been added as a collaborator yet, or you're signed in as a different GitHub account. |
| `protected branch hook declined` when pushing | You tried to push to `main`. Push to your own branch: `git push origin <your-github-username>` |
| Check fails: *branch name does not match* | Rename the branch: `git branch -m <your-github-username>`, then `git push origin -u <your-github-username>`, then open a new PR from it and close the old one. |
| Check fails: *files outside submissions/<you>/* | Undo those changes, for example `git checkout origin/main -- data/receiving_sample.csv`, then commit and push. |
| `rejected ... (fetch first)` | Someone, or you on another machine, pushed to your branch. Run `git pull --rebase`, then `git push`. |
| Merge conflict after `git pull origin main` | This should only happen inside your own folder. Open the file, keep the version you want, `git add` it, then `git commit`. |

## Commands you'll use every day

```sh
git status                                   # what changed
git add submissions/<you>/ && git commit -m "..."
git push                                     # send to your branch
git pull origin main                         # pick up merged work from main
git log --oneline -10                        # recent history
```
