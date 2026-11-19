# forge-attribution

The `gh` wrapper adds Homura's model-attribution note to agent-posted GitHub
bodies that need it.

    > [!NOTE]
    > 🤖 **<model> responding on behalf of @01-1**

Install with `mkdir -p ~/.local/bin && install -m 755 gh ~/.local/bin/gh`.
Put `~/.local/bin` ahead of the underlying `gh` on `PATH`. To uninstall,
run `rm ~/.local/bin/gh`.

- Active only in agent environments (`T3CODE_THREAD_ID`, `CLAUDECODE`,
  `CODEX_THREAD_ID`, `CODEX_SANDBOX`, `AI_AGENT`). You can also force attribution
  with `GH_ATTRIBUTION=1` and `GH_ATTRIBUTION_MODEL`. Set `T3CODE_CLI_PATH` to your `t3`
  executable if automatic model lookup cannot find it; `GH_ATTRIBUTION_REAL_GH`
  overrides the underlying `gh` executable (default `/usr/bin/gh`).
- Covers `pr|issue comment/create/edit/review`, `release create/edit`, and
  `gh api` writes to comments/reviews/issues/pulls/releases/graphql
  (`-f/-F body=`, `--input` JSON incl. inline review comments, GraphQL
  mutation `body:"..."`).
- Skips bodies that already contain the note. `GH_ATTRIBUTION=0` disables it
  for one command; `GH_ATTRIBUTION_DRYRUN=1` prints the rewritten argv.
