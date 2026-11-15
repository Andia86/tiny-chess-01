[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Andia86/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Andia86/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01 entry

A chess engine in 3,642 bytes of Python (`main.py`, cap 4,096), written for
the make.fun tiny-chess-01 competition. `main.py` is an LZMA-packed payload
plus its unpacker (the size rule allows this; the house baseline is packed
the same way) of a self-written engine: 64-square board, pin-aware legal
move generation, alpha-beta search with transposition table, PVS + LMR,
null-move pruning, futility pruning, quiescence search with delta pruning,
incremental material + piece-square evaluation with phase interpolation
toward an endgame king table and a bishop-pair bonus, Zobrist hashing,
game-history seeding of the repetition table, and a fixed 60,000-node-per-
move budget (no clock reads, so replays are deterministic).

Local validation: perft 5/5 on standard test positions (8902 / 97862 /
43238 / 9467 / 62379), including castling, en passant (also when the
capturing pawn is pinned) and promotions; incremental-eval differential
tests clean (no mismatches, including the phase/bishop-pair bookkeeping);
promotion move-generation tests clean; game-history replay tests clean.
On a fixed 12-game screening gauntlet against the kit's house anchors
(855 / 1073 / 1199 / 1392 / 1497 / 1596) this build pools at 1191, the
same as the previous build, with a different win profile (checkmate wins
against the 100k- and 250k-node anchors as White) and no timeout losses;
worst single move on the local benchmark suite is 4.4 s of the 10 s limit.
The 1154 final-qualification floor is the bar this build is aimed over.

Build: the readable engine source is packed into `main.py` with the kit's
own `makefun compress` command; `main.py` decompresses to that source
byte for byte, so the packed entry and the source are the same engine.

License: MIT (see LICENSE).
