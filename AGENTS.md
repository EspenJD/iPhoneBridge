# AGENTS.md

Claude Code reads this file through `CLAUDE.md`.

## Two unrelated histories

- `origin/main`, `public-main` and `release/*` form a squashed public history
  rooted at a parentless commit. The development branches (local `main`,
  `refactor/native-hevc-mirror`, `fix/*`) share none of it, so `git merge-base`
  between the two is empty.
- A worktree cut from `origin/main` lands on the public history. Before you merge
  or fast-forward, check `git merge-base --is-ancestor`. Re-point a fresh,
  commit-less branch to the intended development tip; never merge across the two
  histories.

## Sessions and the installed app

- The app and every source checkout record sessions in one shared data
  directory. `status` names the owner of each session: read it before you touch
  a session. Never `stop` a session that another checkout or agent started
  unless asked; use `stop --own`.
- "USB port … is held by …" after the app quits usually means an `iproxy`
  forward that another project's session started by hand, not a leftover bridge
  session. The bridge never stops processes it did not record.
- To replace the installed app: quit it, move the old bundle to the Trash, then
  copy the new one with `ditto` from the build checkout.
