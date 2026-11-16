# forge-attribution

Backstop `gh` wrapper: agents add the note themselves; this adds it to any
agent-posted GitHub body that lacks
Homura's model-attribution note:

    > [!NOTE]
    > 🤖 **<model> responding on behalf of @01-1**

- Installed on pbox as `~/.local/bin/gh` (ahead of `/usr/bin/gh` in PATH):
  `install -m 755 gh ~/.local/bin/gh`. Rollback: `rm ~/.local/bin/gh`.
- Active only in agent environments (`T3CODE_THREAD_ID`, `CLAUDECODE`,
  `CODEX_*`, `AI_AGENT`). Model comes from `t3 thread show $T3CODE_THREAD_ID`;
  override with `GH_ATTRIBUTION_MODEL`.
- Covers `pr|issue comment/create/edit/review`, `release create/edit`, and
  `gh api` writes to comments/reviews/issues/pulls/releases/graphql
  (`-f/-F body=`, `--input` JSON incl. inline review comments, GraphQL
  mutation `body:"..."`).
- Skips bodies that already contain the note. `GH_ATTRIBUTION=0` disables it
  for one command; `GH_ATTRIBUTION_DRYRUN=1` prints the rewritten argv.
