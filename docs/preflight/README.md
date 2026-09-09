# Preflight

Preflight is where Agent Airlock work is shaped **before** anyone implements it.

A mission does not start until the request is clear and the rules are reviewable. The same idea applies here: capture the problem, the gaps, and the proposed capabilities first. Code comes after.

## Layout

```text
docs/preflight/
  README.md                         This guide
  _templates/                       Copy these into your folder
  debchoudhury/                     Current developer folder
    requirement-closure.md          First exercise
    <idea-or-work-item>.md          Later submissions
```

For now, [`debchoudhury/`](./debchoudhury/) is the only developer folder in the tree. Other participants add their own folder in their own pull request. Use your GitHub handle as the folder name. Keep your ideas and work-item write-ups in that folder. Do not edit another participant's folder.

## How to submit

If you are adding yourself: include `docs/preflight/<your-github-handle>/` in your pull request.

1. Create `docs/preflight/<your-github-handle>/` (skip this if you already have a folder).
2. Copy the matching file from `_templates/`.
3. Rename it to match the exercise or work item.
4. Fill it in. Write in your own words. Ground claims in the current project overview.

| You want to… | Copy |
|---|---|
| Close requirements for the first exercise | [`_templates/requirement-closure.md`](./_templates/requirement-closure.md) |
| Propose an idea | [`_templates/idea.md`](./_templates/idea.md) |
| Propose a work item | [`_templates/work-item.md`](./_templates/work-item.md) |

## Current exercise: requirement closure

**Goal:** Decide what must be true before implementation starts.

Read the root [`README.md`](../../README.md). Then, in your own folder, list:

1. **Issues, gaps, and problems** you see in what the project claims today.
2. **Features or capabilities** that would address each one.

This is not a design spec and not a task breakdown. It is a personal inventory so the group can close requirements from several viewpoints.

Copy [`_templates/requirement-closure.md`](./_templates/requirement-closure.md) to:

```text
docs/preflight/<your-github-handle>/requirement-closure.md
```
