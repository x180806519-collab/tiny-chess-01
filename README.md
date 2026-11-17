# tiny-chess-01 entry

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

## Local grade

Practice trials (kit env + scorer, run directly; Docker is not
available on this machine):
- trial 0: 4 wins, 1 draw, 1 loss, Elo 1545
- trial 1: 1 win, 3 draws, 2 losses, Elo 1191
- trial 2: 3 wins, 1 draw, 2 losses, Elo 1364
Mean practice Elo 1367, about level with the house sunfish baseline
(practice mean ~1365). A later variant with a draw contempt and a
passed-pawn bonus scored worse on trial 1 (Elo 1099) and was reverted.
