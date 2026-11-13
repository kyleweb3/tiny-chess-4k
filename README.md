# tiny-chess-4k

A chess engine in 4 KB of Python for make.fun's tiny-chess-01 bounty:
strongest engine wins. `main.py` (<=4,096 bytes) is the whole engine —
alpha-beta + transposition table, null-move pruning, late move reductions,
quiescence search, tuned piece-square tables, iterative deepening to a
fixed node budget (never a clock, so replays are deterministic).

## Run it

The grader runs `python3 main.py` with `MAKEFUN_ENV_URL` set; the engine
plays its games through that env and exits when they are done.

## Build

The readable source is `engine.py` in the author's dev tree; `main.py`
is generated from it by a mechanical golf + pack script
(`golf.py` + `pack2.py`), so the shipped file stays byte-identical to the
tested readable source. Packing: golfed source is lzma-compressed
(FORMAT_ALONE), stored as a latin-1 str literal with only NUL/CR/backslash
escaped, and decoded with `.encode('latin-1')` at startup — a raw-bytes
literal cannot work in Python 3 (NUL bytes and non-ASCII bytes are both
rejected by the tokenizer).
