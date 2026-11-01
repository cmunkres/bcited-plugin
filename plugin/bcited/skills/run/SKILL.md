---
name: run
description: "Trigger an immediate run of one tracked prompt across ChatGPT, Claude and Perplexity for one of the user's b/cited projects, wait for the three engines to land, and show the results. Spends one run; capped at once per prompt per hour. Use only when the user explicitly asks to run, re-run or refresh a prompt now. Needs the b/cited account connection with the run permission."
---

# Run a tracked prompt now

This spends real provider calls and counts against the account's allowance, so run it only when asked, once, and never retry a cap error.

## Connection

If the `run_prompt_now` tool is not available, the account server is not connected or the sign-in did not grant the run permission:

```bash
claude mcp add --transport http bcited-account https://mcp.bcited.ai/mcp
```

Approve the "run tracked prompts" permission on the consent screen.

## How to run it

When invoked (`/bcited:run thedatagovernor-com <prompt_id>`):

1. If the prompt id is missing, call `list_prompts` for the project and, with one prompt, use it; with several, ask which.
2. Call `run_prompt_now` with `project` and `prompt_id`. It returns `since` and `providers_expected`.
3. On a cap error (`mcp_hourly_cap_reached`, `mcp_daily_cap_reached`, `free_aeo_run_cap_reached`), report the message and stop. Do not call it again.
4. Poll `get_run_status` with the same `project`, `prompt_id` and `since` every 5 seconds, up to 90 seconds, until `completed` reaches `expected`.
5. Call `get_prompt_runs` with `project`, `prompt_id` and the same `since`, and present the results in the `/bcited:runs` format.

## Output format

```
Queued a run of "[prompt]" for [project] at [since].
Landed: 3 of 3 engines in [seconds]s.

[then the /bcited:runs block for these three runs]
```

If the run has not fully landed after 90 seconds, say how many landed, show those, and tell the user to ask again in a minute for the rest.

## Where to go next

- All recent runs: `/bcited:runs <project>`.
- The composite score: `/bcited:score <project>`.
