# Codex Web Start Here

Verified on `2026-04-02`.

Repository:
- GitHub: `sebaboubou-max/Smash_App`
- Default branch in local checkout: `main`

This file is the shortest reliable handoff for working in Codex Web when you do not have terminal access.

## 1. Connect Codex Web to GitHub

1. Open `https://chatgpt.com/codex`
2. Connect your GitHub account.
3. Grant access to `sebaboubou-max/Smash_App`.
4. Select the repository and start from `main` unless you explicitly want another branch.

OpenAI docs verified on `2026-04-02`:
- Codex Web overview: `https://developers.openai.com/codex/cloud`
- Cloud environments: `https://developers.openai.com/codex/cloud/environments`
- GitHub integration: `https://developers.openai.com/codex/integrations/github`

What is current in the official docs:
- Codex Web works from `chatgpt.com/codex`.
- You connect GitHub from the Codex app.
- Cloud tasks run in an isolated environment with your repository checked out.
- Codex follows `AGENTS.md` files inside the repo.
- You can open pull requests from the web result.
- GitHub code review can be enabled and called with `@codex review`.

## 2. Environment To Configure In Codex Web

Create one environment for this repo in Codex settings.

Recommended setup script:

```bash
bash apps/backend/scripts/codex_web_setup.sh
```

Recommended maintenance script:

```bash
bash apps/backend/scripts/codex_web_setup.sh --maintenance
```

Recommended internet policy:
- Default: `off`
- Turn it on only for facts that can drift: docs, prices, laws, releases, live runtime checks, external citations

## 3. What Codex Should Read First

For a serious task, instruct Codex Web to read in this order:

1. `AGENTS.md`
2. `CLAUDE.md`
3. `docs/notepads/TRANSMISSION.md`
4. `docs/notepads/briefings/DIAPASON.md`
5. `docs/guides/CODEX_MULTI_AGENT_GUIDE.md`
6. `STATE_OF_FORGE.json`

Working directory rule:

```bash
cd /workspace/Smash_App/apps/backend && source venv/bin/activate
```

Inside Codex cloud the absolute path may differ, but the repo-relative working directory stays `apps/backend`.

## 4. First Activation Prompt To Paste

Use this as the first serious Codex Web prompt:

```text
Read AGENTS.md, CLAUDE.md, docs/notepads/TRANSMISSION.md, docs/notepads/briefings/DIAPASON.md, docs/guides/CODEX_MULTI_AGENT_GUIDE.md, and STATE_OF_FORGE.json. Then work from apps/backend with the project venv. Before editing shared or long-running fronts, inspect git status and follow the repo’s multi-agent conventions. Prefer precise local changes, append-only behavior on living docs, and report with file paths plus verification.
```

## 5. GitHub Workflows You Can Use

From Codex Web:
- delegate a coding task and open a PR from the result
- inspect logs and diffs before accepting changes
- continue a previous task with follow-up prompts

From GitHub:
- enable Codex code review in Codex settings for this repo
- request a review with:

```text
@codex review
```

- launch a task from a PR or issue comment with:

```text
@codex fix the CI failures
```

Repository-specific rule:
- this repo is often dirty and multi-agent
- do not ask Codex Web to mass-format or rewrite central living docs unless that is the explicit front

## 6. What To Avoid

- Do not start from repo root and guess the stack.
- Do not let Codex invent a new workflow when `AGENTS.md` and `TRANSMISSION.md` already define one.
- Do not enable internet by default.
- Do not let Codex touch shared hot files casually: `CODEX_LOGIC.md`, `COMPOSITIONS_META_WORKFLOW.md`, `DIAPASON.md`, central boards.

## 7. Repo-Specific High-Leverage Fronts For Codex Web

Good fits:
- bounded script work in `apps/backend/scripts`
- tests in `apps/backend/tests/scripts`
- evidence packs, validators, generators, harnesses
- review and PR comments on GitHub

Use caution:
- central notepads
- LHC runtime surfaces while Ralph or another governed batch is alive
- shared JSON stores without the repo’s safety helpers

## 8. Quick Reality Check

If Codex Web starts behaving like a generic repo agent, redirect immediately:

```text
Stop. This is not a standard codebase. Re-read AGENTS.md and TRANSMISSION.md, then restate the working assumptions before changing files.
```
