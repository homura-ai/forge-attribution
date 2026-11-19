# forge-attribution

The `gh` wrapper adds this model-attribution note when an agent posts a
GitHub body without one.

    > [!NOTE]
    > 🤖 **<model> responding on behalf of @01-1**

Install with `mkdir -p ~/.local/bin && install -m 755 gh ~/.local/bin/gh`.
Put `~/.local/bin` ahead of the underlying `gh` on `PATH`. To uninstall,
run `rm ~/.local/bin/gh`.

- Active in agent environments (`T3CODE_THREAD_ID`, `CLAUDECODE`,
  `CODEX_THREAD_ID`, `CODEX_SANDBOX`, `AI_AGENT`). Set `GH_ATTRIBUTION_MODEL`
  to override the detected model. The wrapper uses `~/.t3/bin/t3` to look up
  T3 thread models unless you set `T3CODE_CLI_PATH`.
- Covers `pr|issue comment/create/edit/review`, `release create/edit`, and
  `gh api` writes to comments/reviews/issues/pulls/releases/graphql
  (`-f/-F body=`, `--input` JSON incl. inline review comments, GraphQL
  mutation `body:"..."`).
- `GH_ATTRIBUTION=0` disables attribution
  for one command; `GH_ATTRIBUTION_DRYRUN=1` prints the rewritten argv.
