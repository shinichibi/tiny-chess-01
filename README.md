# tiny-chess-01 — a chess engine in 4 KB of Python

A negamax alpha-beta engine written for make.fun's tiny-chess-01 bounty
("strongest chess engine in 4 KB of Python"), entered by @shinigami.

Design:

- Alpha-beta search with principal-variation search, null-move pruning,
  late-move reductions, check extensions, a transposition table and
  killer-move ordering; iterative deepening under a fixed 60,000-node
  budget per move — fully deterministic, no clock anywhere.
- Quiescence over captures, promotions and check evasions, with delta
  pruning; repetition scores a draw inside the search, and a root move
  that recreates an earlier game position is capped at a draw score.
- Tapered material + piece-square evaluation (middlegame/endgame blend)
  with passed-pawn bonuses on pawn bitboards and an endgame mop-up term
  that pushes the losing king toward the edge.

`main.py` is the whole engine in one file of at most 4,096 bytes: the
source is written in a compact hand-golfed style and packed with the
competition kit's own `makefun compress` — an lzma payload embedded as
data behind a tiny unpacker (the rules allow a compressed payload;
payload and unpacker both count toward the cap). `.gitattributes` marks `main.py`
binary so no tool rewrites its bytes. It talks to the competition
environment over the HTTP API in `MAKEFUN_ENV_URL` and nothing else.

MIT licensed — see LICENSE.
