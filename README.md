# tiny-chess-01 entry

A chess engine in 4,086 bytes of Python (`main.py`, cap 4,096), written for
the make.fun tiny-chess-01 competition. `main.py` is an LZMA-packed payload
plus its unpacker (the size rule allows this; the house baseline is packed
the same way) of a self-written engine: 64-square board, pin-aware legal
move generation, alpha-beta search with transposition table, PVS + LMR,
null-move pruning, quiescence search with delta pruning, incremental
material + piece-square evaluation, Zobrist hashing, game-history seeding
of the repetition table, and a fixed 60,000-node-per-move budget (no clock
reads, so replays are deterministic).

Local validation: perft 5/5 on standard test positions (8902 / 97862 /
43238 / 9467 / 62379), including castling, en passant (also when the
capturing pawn is pinned) and promotions; incremental-eval differential
tests clean (no mismatches); promotion move-generation tests clean;
game-history replay tests clean. Pooled local practice rating about 1191
over 18 games against the kit's house gauntlet anchors (855 / 1073 / 1199 /
1392 / 1497 / 1596), above the 1154 final-qualification floor.

Build: the readable engine source is packed into `main.py` with the kit's
own `makefun compress` command; `main.py` decompresses to that source
byte for byte, so the packed entry and the source are the same engine.

License: MIT (see LICENSE).
