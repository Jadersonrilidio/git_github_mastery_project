# 📄 reset-vs-revert.md

> **Module:** Git Core Commands  
> **Topic:** Resetting history safely and professionally

---

## Understanding Local vs Remote History

Given the following `git log --oneline` output:

```bash
    a80880f (HEAD -> master) second commit
    ab1e021 (origin/master) first commit
```

This means:
- The local `master` branch is **ahead by one commit**
- The remote branch (`origin/master`) does **not** contain the latest commit

The goal is to return the local branch to the **first commit state**, aligning it with the remote.

---

## Available Strategies

### Option 1 — Hard Reset (Rewrite Local History)

```bash
    git reset --hard ab1e021
```

**Behavior:**
- Moves `HEAD` and `master` back to the first commit
- Discards the local commit completely
- Working directory becomes clean

**Use when:**
- The commit was never pushed
- You are working alone
- You want the commit to never exist

✅ **Best practice for local-only mistakes**

---

### Option 2 — Soft Reset (Keep Changes Staged)

```bash
    git reset --soft ab1e021
```

**Behavior:**
- History is rewritten
- Changes remain staged (seen with `git status`)

**Use when:**
- You want to rewrite or split a commit
- You plan to recommit differently

---

### Option 3 — Mixed Reset (Default)

```bash
    git reset ab1e021
```

**Behavior:**
- History is rewritten
- Changes remain unstaged (seen with `git status`)

**Use when:**
- You want to rework the changes manually

---

### Option 4 — Revert (Preserve History)

```bash
    git revert a80880f
```

**Behavior:**
- Creates a new commit that undoes the changes
- Keeps history intact

**Result:**
```bash
    <new_hash> revert second commit
    a80880f second commit
    ab1e021 first commit
```

**Use when:**
- The commit was already pushed
- You are working on a shared or protected branch

✅ **Mandatory in team environments**

### Option 5 — Reset to remote directly (same as option 1 but most explicit)

```bash
    git reset --hard origin/master
```

**Behavior:**
- Resets local master to match origin/master
- Ignores commit hashes

**Use when:**
- You want local branch to match remote exactly
- You trust the remote state

✅ Very common in professional workflows.

---

## Best Practice Summary

| Scenario | Recommended Command |
|--------|--------------------|
| Local-only mistake | `git reset --hard origin/master` |
| Rewriting commits + stagged changes | `git reset --soft <target_hash>` |
| Rewriting commits + unstagged changes | `git reset --mixed <target_hash>` |
| Undoing shared commits | `git revert <target_hash>` |
| Align local with remote | `git reset --hard origin/master` |

---

## Safety Tip — Recovery

Even after a hard reset, commits can usually be recovered:

```bash
git reflog
git reset --hard <commit-hash>
```

This makes Git a **safe tool even when mistakes happen**.

---

## Key Takeaway

> **Professional Git usage is not about avoiding mistakes, but about knowing how to recover cleanly and safely.**

Understanding `reset` vs `revert` is a milestone in Git mastery.

---

📌 *This document is part of my Git & GitHub Mastery learning roadmap and reflects real-world Git workflows used in professional software development.*
