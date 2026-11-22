# sokoban-solver-01-run-20261121

[![make.fun · sokoban-solver-01-run-20261121](https://make.fun/badge/sokoban-solver-01-run-20261121.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)
[![rank](https://make.fun/badge/sokoban-solver-01-run-20261121/catiglu/sokoban-solver-01-run-20261121-entry/rank.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)
[![reward](https://make.fun/badge/sokoban-solver-01-run-20261121/catiglu/sokoban-solver-01-run-20261121-entry/reward.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)

A push-optimal Sokoban solver for the make.fun `sokoban-solver-01-run-20261121` bounty.

## How it works

`main.ts` reads each level from `MAKEFUN_INPUT_DIR/<id>/level.txt` (default `/input`) and writes the player's moves to `MAKEFUN_OUTPUT_DIR/<id>/solution.txt` (default `/output`).

The solver performs a breadth-first search **over pushes**, so the first solution found is guaranteed to use the minimum number of pushes (P*). Two sound deadlock prunings keep the search small:

- **Dead squares** — a square from which no box can ever be pushed onto a goal (ignoring other boxes).
- **Frozen 2x2 blocks** — a 2x2 square of walls/boxes containing a box that is not on a goal.

Levels are split into independent rooms by reachability, and each room is solved separately. The resulting move string uses `u`, `d`, `l`, `r` (uppercase marks a push), which the checker accepts in either case.

## Run locally

```bash
mkdir -p out
MAKEFUN_INPUT_DIR=practice/input MAKEFUN_OUTPUT_DIR=out node main.ts
```

Requires Node.js 22 (uses native TypeScript type stripping; no build step).

## Score

Each instance scores 1000 points when the solution uses at most P* pushes, otherwise `500 * P* / pushes`. This solver reaches P* on every level, for the maximum 1,000,000 points.

## License

MIT — see [LICENSE](LICENSE).
