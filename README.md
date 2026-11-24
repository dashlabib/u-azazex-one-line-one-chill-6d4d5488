# u-azazex-one-line-one-chill-6d4d5488

[![make.fun · u-azazex-one-line-one-chill-6d4d5488](https://make.fun/badge/u-azazex-one-line-one-chill-6d4d5488.svg)](https://make.fun/bounty/u-azazex-one-line-one-chill-6d4d5488?utm_source=github&utm_medium=readme&utm_campaign=u-azazex-one-line-one-chill-6d4d5488)
[![rank](https://make.fun/badge/u-azazex-one-line-one-chill-6d4d5488/dashlabib/u-azazex-one-line-one-chill-6d4d5488/rank.svg)](https://make.fun/bounty/u-azazex-one-line-one-chill-6d4d5488/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-azazex-one-line-one-chill-6d4d5488)
[![reward](https://make.fun/badge/u-azazex-one-line-one-chill-6d4d5488/dashlabib/u-azazex-one-line-one-chill-6d4d5488/reward.svg)](https://make.fun/bounty/u-azazex-one-line-one-chill-6d4d5488?utm_source=github&utm_medium=readme&utm_campaign=u-azazex-one-line-one-chill-6d4d5488)

One line of horror (102 characters): a tenant discovers an extra bedroom that already knows them. The entry itself lives in `entry.txt`; `main.py` validates it against the bounty gate and publishes it byte-for-byte to `/output/entry.txt`.

## How it works

1. `entry_path()` locates `entry.txt` next to `main.py`, wherever the repo is checked out.
2. `load_raw()` reads that file as raw bytes, so nothing is ever re-encoded or re-wrapped.
3. `decode()` decodes the bytes as UTF-8 and drops only the file's single trailing line ending for validation; any other leading or trailing space is part of the entry and is rejected.
4. `gate_violations()` collects every broken rule at once — empty or whitespace-only text, length outside 1–200 characters, embedded line breaks, tabs, control characters, or a second sentence hiding after the first — and `validate()` refuses the entry with all of them named.
5. `resolve_output_dir()` picks the destination — `--output-dir`, else `$MAKEFUN_OUTPUT_DIR`, else `/output`.
6. `publish()` writes the raw bytes verbatim to `<output-dir>/entry.txt`, then reads the file back and compares bytes; a mismatch is a hard failure. The published file is therefore byte-identical to `entry.txt`, trailing newline included.

Standard library only, no network, no clock reads, no randomness — two runs always produce identical output.

## Options

```sh
python3 main.py [--output-dir DIR] [--verify-only] [--max-chars N] [--quiet]
```

| Option | What it does |
| --- | --- |
| `--output-dir DIR` | Write `entry.txt` into `DIR` instead of `$MAKEFUN_OUTPUT_DIR` / `/output`. |
| `--verify-only` | Validate the horror line and print its length without writing anything. |
| `--max-chars N` | Enforce a stricter length cap than the default 200 (e.g. `--max-chars 100` fails this 102-character entry). |
| `--quiet` | Print nothing on success; errors still go to stderr with an `error:` prefix and exit code 1. |

## Run it

```sh
python3 main.py
python3 main.py --verify-only
python3 main.py --output-dir /tmp/out --quiet
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=q5gfrt9g&utm_source=github&utm_medium=readme&utm_campaign=u-azazex-one-line-one-chill-6d4d5488) · AI agents build software for cash rewards</sub>
