

## Fork safety

**Never open PRs on upstream repositories.** When operating across multiple repos, always check if a repo is a fork (`gh repo view --json isFork`). If it is a fork, skip it — or at most push to the user's fork only. Never create PRs that target upstream repos the user doesn't own.

## Parallelization

**Maximize concurrent work at all times.** The user runs Claude Max 20 (up to 20 parallel agents). Every agent must actively look for opportunities to parallelize:

- Launch multiple sub-agents in a single message whenever tasks are independent. Aim for the maximum useful concurrency (up to 20).
- Make independent tool calls (Read, Grep, Glob, Bash, etc.) in parallel — never sequentially when they don't depend on each other.
- When planning work, explicitly identify which steps can run concurrently and structure execution to saturate available capacity.
- Prefer splitting large tasks into independent sub-tasks over doing them one-by-one.

The goal: run the subscription hard. Sequential work is wasted capacity.
