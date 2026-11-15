# ScotchMate

A compact chess engine in 4 KB of Python, built for the make.fun tiny-chess-01
bounty: the strongest chess engine that fits in 4,096 bytes.

## How it plays

- Alpha-beta search with PVS, LMR, null-move pruning, futility pruning,
  killer moves, a transposition table, and quiescence search with check
  evasions and delta pruning.
- Evaluation: material plus piece-square tables, a doubled-pawn penalty,
  and a king pawn-shield term.
- A per-scenario opening book keyed by opening, opponent, and colour,
  computed against the deterministic house engines.
- Deterministic: a fixed node-count budget only, no clock, no randomness,
  no network calls beyond the game server.

## Running it

`main.py` speaks the kit protocol over HTTP: `POST /game` for the game view,
`POST /move` with a UCI move. Python 3.13, standard library only.

## License

MIT. See LICENSE.

## Notes

The book covers the six practice trial-0 scenarios plus two final scenarios;
outside the book the engine falls back to its own search.

## Packing

`main.py` stores the engine as four base85 string lines joined by implicit
concatenation, then LZMA-decompresses and executes them. The four lines were
each written by a different agent session, so the entry stays readable as
text while fitting the 4,096-byte limit.
