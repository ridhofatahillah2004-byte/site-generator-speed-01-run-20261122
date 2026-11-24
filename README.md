# site-generator-speed-01-run-20261122

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/ridhofatahillah2004-byte/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/ridhofatahillah2004-byte/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A fast, dependency-free drop-in for makefun-site 1.0.0: a from-scratch reimplementation of its static site generator with byte-identical output. On the practice set it runs about 1.6x faster than the house baseline (median CPU ~0.85 s vs ~1.34 s on this machine), and it passes every practice case plus 9 extra cases drawn from fresh seeds.

How it gets faster, without changing a single output byte:

- **Bulk HTML escaping** — plain text is escaped in one regex pass per chunk instead of one regex call per character.
- **Char-dispatch Markdown lexer** — block detection by first character instead of seven regexes per line.
- **Regex-driven inline rendering** — the scanner jumps from one markup character to the next instead of walking every character.
- **Compiled templates** — each template is compiled once to a JS function (loops become real loops, includes become calls); loop scopes are reused and mutated per item instead of allocated per item.
- **Cached, ASCII-fast slugs** — pure-ASCII titles skip Unicode normalisation; repeated titles, tags and headings hit a cache.
- **Manual front-matter and word counting** — no regexes on the hot paths.

## Run it

```sh
MAKEFUN_INPUT_DIR=./input MAKEFUN_OUTPUT_DIR=./output node main.ts
```

`main.ts` reads every case from `$MAKEFUN_INPUT_DIR/cases.json`, answers each one with `run()` from `solve.js`, and writes `$MAKEFUN_OUTPUT_DIR/answers.json`. Inside the harness container the input and output directories are `/input` and `/output`. Node 22 or later, nothing to install.

---

<sub>Entered on [make.fun](https://make.fun/?ref=xbc8h78c&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
