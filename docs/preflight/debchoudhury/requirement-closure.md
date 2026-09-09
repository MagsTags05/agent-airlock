# 2026-09-09

## Problems
1. **Unclear permissions.** Someone asks the agent to investigate a bug, fix it, and complete the change without interrupting them. One run only edits local files. The next run also does `git push origin main`, because "complete" never named tools, branch, or online write.
2. **Rules live in prompts.** The org says ask before changing anything outside the computer, but that line sits in a system prompt. Platform's agent pauses on `git push`. Apps' agent has a shorter prompt and pushes to origin on the same request.
3. **Approval fatigue, then /yolo.** The agent asks to confirm `pytest`, then each file edit, then `git status`. Tired of the clicks, the user sends `/yolo` or "do everything automatically." The agent treats that as skip-all-approvals and pushes to the protected branch.
4. **Logs without a decision.** After the run the log says `tool: git push, status: ok`. A reviewer cannot tell if the push was allowed, user-approved, or should have been blocked as a write to `main`.
5. **Conflict found too late.** The task is a read-only investigation, but the tool list still includes `git commit` and `az deployment`. The agent starts anyway, then fails or writes in prod. The clash was visible before takeoff.
6. **Model used when a repo script would do.** A teammate asks to format the tree or regenerate a changelog. The agent calls Azure AI. The repo already has `scripts/format.ps1` and `scripts/changelog.ps1`. The run costs money, drifts from the team's script, and cannot be replayed.
7. **No model catalog.** A bug-fix run uses whatever model is in the environment. The next run sends the same private repo to a public model. Nothing in the rules named the allowed models, the default, or what needs approval to override.

## Capabilities
1. **Agent contract before start.** Before work begins, show Goal, Data, Tools, Changes, Approvals, and Limits. Local read, edit, test, and branch are allowed. Simulated push waits. `git push origin main` and production writes are blocked. The request does not grant permission.
2. **Org rules file, not a prompt.** One local file lists allow, ask-first, and block. Two agents load the same file. Change the file, rerun the same request, and the new decision applies without editing the prompt.
3. **Runtime allow, ask first, or block.** Read, edit, test, and local branch run with no prompt. Simulated `git push` waits. `git push origin main` is denied and the agent is pointed at a branch-and-review path.
4. **Approval names the action.** The pause screen shows the exact command, the rule that paused it, and what happens if the user approves or rejects.
5. **Activity summary.** After the run, list requested, ran locally, needed approval, blocked, reason, and final result. Example: blocked `git push origin main` because of the org rule, not because the model refused.
6. **/yolo does not grant rights.** `/yolo`, skip-permissions, auto-approve, and "do everything automatically" cannot turn a block into allow or skip ask-first on an online write. Those flags only skip extra questions inside the already-allowed set.
7. **Check before takeoff.** If a read-only contract still includes a write tool, or a production write is requested where production writes are blocked, do not start. Show the conflict.
8. **Prefer repo scripts over Azure AI.** For a task class the team marks as deterministic, allow the script in the repo and block the Azure AI call. Ask first if someone still wants a model on that path.
9. **Model catalog with override.** Org or team rules name, for a kind of task, the default model, which models are allowed, and which endpoints are blocked. Using something else is ask-first. `/yolo` cannot pick a blocked model.


