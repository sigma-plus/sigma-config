# Sigma's agent instructions

Common instructions for Sigma's agents across all scenarios.

## General Guidelines

- Commit messages: never auto-add your agent name as co-author.
- Markdown: for long files, put each full sentence on its own line; preserve normal Markdown structure, but don't wrap multiple sentences on one physical line.
- Technical decisions: prioritize quality, simplicity, robustness, scalability, and long-term maintainability over development cost.
- Bug fixes: reproduce first in an E2E setting aligned with the end user's expected resolution.
- Quality bar: be picky and obsessive about UI and pixel perfection in E2E testing; fix clearly visible issues even if unrelated. Apply the same standard to lint, test failures, and test flakiness.
- Diagram alignment: prefer plain ASCII (`+ - | < > ^ v`) and English text; avoid CJK, full-width, emoji, or ambiguous-width box-drawing characters. Verify visual alignment; don't rely on `len()`.
- Network access: if direct external network access fails, try using the local proxy at `127.0.0.1:xxxxx` (e.g., set `http_proxy` / `https_proxy` accordingly).


## Manual Correction Retrospective Workflow (Mandatory for All Coding Agents)

After the user manually corrects an agent's output, in addition to fixing the issue itself, you must complete the following retrospective and put the conclusions into practice; do not stop after merely fixing the problem:

1. **Why was it not done right the first time?** Distinguish between user preference and incomplete reasoning. If it is a user preference (a practice the user expects but did not explicitly state), record it in project documentation (AGENTS.md, etc., committed with the repository). If it is incomplete reasoning, identify the missed signals (repository conventions, existing code, verification steps).
2. **Is the code repository itself misleading?** If multiple styles or conventions coexist in the repository, or a missing convention caused the wrong choice, determine whether it can be fixed along the way (add specification documentation, clean up ambiguous code) so that future agents get it right the first time.
3. **Can existing hook gates catch this in advance?** Evaluate whether automated checks such as `.githooks/` pre-commit can intercept this kind of issue. If so, add a gate; if not, explain why (e.g., runtime or visual verification is required).
4. **Should it be captured as a skill?** If it is general and can be handled with a script or a fixed process, capture it as an engineering skill (place it in `.agents/skills/`). A single rule can simply be written into the corresponding AGENTS.md; do not force it into a skill.

> Background: The project fully adopts coding agents for development. Work that paves the way for agents to become increasingly intelligent (supplementing documentation, fixing repository ambiguity, adding gates, and capturing skills) is a worthwhile investment.