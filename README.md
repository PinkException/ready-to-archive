<div align="center">

# 📦 ready-to-archive

### The last gate before you archive a session — so nothing of consequence gets lost.

*A Claude skill. One clear GO / NO-GO, backed by evidence, not optimism.*

[![version](https://img.shields.io/badge/version-0.1.0-blue)](https://github.com/Kyarha/ready-to-archive/releases)
[![license](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Claude skill](https://img.shields.io/badge/Claude-skill-8A63D2)](https://support.anthropic.com/en/articles/12512140-get-started-with-skills-on-claude-ai)

</div>

---

You finish a session and go to archive it. But once it's archived, whatever lived **only in
that conversation** is gone — a root cause you figured out, a decision you made, a file you
never committed. **ready-to-archive** is the check you run first. It reads the repo, your
memory, and git — and tells you, plainly, whether it's safe.

It was built for one reason: **a session once got archived with things unrecorded**, because
the check trusted the conversation instead of the repo. This skill doesn't. Every "yes, that's
saved" points at a file it actually read or a `git` command it actually ran — and anything it
**can't** verify is reported as a gap, never waved through.

## 🚀 Quick start

1. **Install** — download the latest release zip and add it through Claude's **Upload skill**
   dialog (in Claude's settings, under **Capabilities → Skills**).
2. **Ask, before you archive:**
   > *"Ready to archive?"*  ·  *"Can I safely archive this?"*  ·  *"Is everything recorded?"*

You get back one verdict — ✅ SAFE, ⚠️ NOT YET, or ❓ CAN'T FULLY VERIFY — in a to-do-first
layout: what still needs you, then what's already done, then your options.

```markdown
🔎 Checked git + main (fetched now) + bug docs + memory · branch fix/parser, 3 commits

## ⚠️ NOT YET — 2 things to fix first

### 🔴 Needs you (2)
1. **Write the root cause into docs/bugs/041**
   → the finding only exists in this chat
2. **Merge fix/parser to main**
   → committed, but no PR and not merged

### ✅ Done
- ✅ **Saved:** all work committed, nothing loose
- 🔴 **Shipped:** fix/parser not on main (above)
- 🔴 **Written down:** 1 missing (above)

**Your call:**
- **a**: write the finding and hand off to jig:slice-land to merge
- **b**: only write the finding
- **c**: nothing, I'll handle it
```

## 🧭 How it works

It runs a grounded **three-pillar** audit, verifying each against git and the filesystem —
not the chat recollection:

| Pillar | The question | Where it looks |
| --- | --- | --- |
| **📝 Recorded** | Does every decision, conclusion, and consequential change live somewhere durable — not only in this chat? | decision log / ADRs, spec `STATUS`, inbox, `README` / `CLAUDE.md`, your memory files |
| **💾 Committed** | Is the git working tree clean — nothing modified, staged, or untracked-of-consequence — and pushed if it must live remotely? | `git status`, upstream, stashes |
| **🚀 Landed** | Did branch work reach main where it had to, or is the open PR named? | branch vs. `main`, remote, open PRs |

## 🔒 It diagnoses — you decide

The verdict is **advisory**, and the skill acts only when you ask it to:

- It **never** commits, pushes, merges, or opens a PR without your explicit go-ahead.
- When there are gaps, it offers the **shortest path to GO** — and, if you say yes, hands off
  to whatever owns the work (e.g. merging the branch, saving a learning to memory).
- A narrow *"yes, fix that one gap"* is never a blanket yes to commit-and-push everything.

## 🛡️ Why it defaults to caution

A false **GO** loses work; a false **NOT YET** just costs a second look. So when it's torn,
it picks NOT YET and names the doubt. When it genuinely can't reconstruct what happened this
session (context was summarized), it says so and asks you to glance — rather than papering
over it with a confident green light.

---

<div align="center">
<sub>MIT · made so a session never gets archived with something important still in the chat.</sub>
</div>
