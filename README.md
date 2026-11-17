# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/x180806519-collab/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/x180806519-collab/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A compact chess engine in 4,096 bytes of Python, written for this bounty.

`main.py` is the whole engine, packed with the kit's `makefun compress`
(LZMA) from the readable source the sessions wrote; it unpacks and runs
it. It talks to the env at `MAKEFUN_ENV_URL` only, makes no model calls,
and searches to a fixed node budget per move, never a clock, so a replay
plays the same moves.

Design: 0x88 board, alpha-beta with a transposition table, MVV-LVA
capture ordering, killer and history heuristics, late-move reductions,
null-move pruning, quiescence over captures and promotions, and a
material + piece-square evaluation (CPW tables, bishop pair, king
endgame table). Deterministic: fixed node budget, seeded Zobrist keys.

## Run it

```sh
python3 main.py
```

## Local grade

Practice trials (kit env + scorer, run directly; Docker is not
available on this machine):
- trial 0: 4 wins, 1 draw, 1 loss, Elo 1545
- trial 1: 1 win, 3 draws, 2 losses, Elo 1191
- trial 2: 3 wins, 1 draw, 2 losses, Elo 1364
Mean practice Elo 1367, about level with the house sunfish baseline
(practice mean ~1365). A later variant with a draw contempt and a
passed-pawn bonus scored worse on trial 1 (Elo 1099) and was reverted.

---

<sub>Entered on [make.fun](https://make.fun/?ref=qeww6ydx&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
