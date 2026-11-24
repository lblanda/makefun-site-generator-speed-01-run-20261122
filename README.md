# makefun-site-generator-speed-01-run-20261122

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/lblanda/makefun-site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/lblanda/makefun-site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's makefun-site 1.0.0 static site generator: byte-identical output on every case, about 3× the speed of the house baseline on the practice set. One dependency-free ES module (`solve.js`) plus the harness driver (`main.ts`).

How it gets there: the Markdown lexer and renderer are fused into a single pass over the source lines, the inline renderer jumps between special characters with a native scan instead of escaping character by character, slugs take an ASCII fast path, and the template interpreter builds output in an array instead of concatenating strings node by node. Nothing is cached between cases; the output depends on the input alone.

Verified on the kit's practice set (3 cases, 250–480 sources each): outputs byte-identical to makefun-site 1.0.0 on every case, ~2.9× faster in steady state (~155–171 ms vs ~458–461 ms for the three cases together). Also checked against the baseline on 84 further cases drawn from the kit's own generator and 30 hand-made edge cases (template parse errors, include depth, slug and date edges, CRLF, shadowed statics, duplicate paths): all identical.

## Run it

```sh
MAKEFUN_INPUT_DIR=/input MAKEFUN_OUTPUT_DIR=/output node main.ts
```

The harness runs `node main.ts` (Node 22); it reads every case from `/input/cases.json`, answers each one alone with `run()` from `solve.js`, and writes `/output/answers.json`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=3zwarjv0&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
