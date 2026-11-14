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

Local validation: perft 5/5 on standard test positions; incremental-eval
differential tests clean; pooled local practice rating about 1191 against
the kit's house gauntlet anchors.

License: MIT (see LICENSE).
