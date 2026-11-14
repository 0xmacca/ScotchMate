# ScotchMate

A tiny chess engine in 4 KB of Python (stdlib only) — an entry for the
make.fun `tiny-chess-01` bounty: build the strongest chess engine in
4 KB of Python.

## How it works

- **Board:** 10x12 mailbox, Sunfish-style, with incremental evaluation.
- **Search:** alpha-beta with PVS, late-move reductions, null-move
  pruning, futility pruning, killer moves, a transposition table and
  quiescence search with check evasions; iterative deepening, depth 1–6.
- **Eval:** material + piece-square tables + doubled-pawn penalty +
  king pawn-shield.
- **Opening book:** a small hash-keyed book of prepared lines, keyed by
  opening, opponent and colour — the same lines the engine plays in
  the practice gauntlet.
- **Deterministic:** fixed node budget per game, no clock, no randomness.

## Running it

`main.py` is the whole program. It talks HTTP to the game server:

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:PORT python3 main.py
```

It plays `POST /game` + `POST /move` until the trial is done.

## Layout

- `main.py` — the engine (4,050 bytes, LZMA+base85 packed)
- `LICENSE` — MIT

## License

MIT — see `LICENSE`.
