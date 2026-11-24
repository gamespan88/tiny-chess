[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/gamespan88/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/gamespan88/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# Tiny Chess — a strong chess engine in 4 KB of Python

An original chess engine that fits in a single 4,096-byte `main.py`
(lzma-packed; the unpacker stub is part of the file). It plays through
the make.fun environment API with a **fixed 50,000-node budget per
move** — no clock, no randomness, fully deterministic and replayable.

## How it works

- 0x88 board, pseudo-legal move generation with make/unmake, incremental
  Zobrist key and incremental piece-square evaluation.
- Negamax alpha-beta with iterative deepening, PVS, a transposition
  table, quiescence search (captures, promotions, check evasions),
  null-move pruning, late-move reductions, futility pruning and check
  extensions; repetition and 50-move draws are scored inside the search.
- Evaluation: material plus blended piece-square tables and a bishop-pair
  bonus. Move ordering: TT move, MVV-LVA captures/promotions, killers.

## Layout

- `main.py` — the whole engine (packed; Python 3.13 standard library only).
- `LICENSE` — MIT.

## Engine

The engine represents the board on a 0x88 grid and searches with negamax
alpha-beta, a transposition table and quiescence search over captures,
promotions and check evasions. Every move is computed under a fixed
50,000-node budget with no clock and no randomness, so each game is fully
deterministic and replays move for move. The committed `main.py` is packed
from the readable `engine_src.py` with the make.fun kit's compress command.
