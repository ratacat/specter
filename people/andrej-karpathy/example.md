<!-- source: https://github.com/karpathy/autoresearch/blob/master/program.md -->
# autoresearch (`program.md`)

Human programs this file. Agent programs `train.py`. `prepare.py` is read-only.

## Setup

1. Agree a run tag (`mar5`). Branch `autoresearch/<tag>` must not exist.
2. `git checkout -b autoresearch/<tag>`
3. Read `README.md`, `prepare.py` (do not modify), `train.py` (the only edit).
4. Data in `~/.cache/autoresearch/` or tell the human to `uv run prepare.py`.
5. Create `results.tsv` header. First run is always the unmodified baseline.

## Constraints

- CAN: edit `train.py` — architecture, optimizer, hparams, batch, size.
- CANNOT: edit `prepare.py`, install packages, change `evaluate_bpb`.
- Goal: lowest **val_bpb**. Time budget is always **5 minutes**.
- Simpler is better. 0.001 gain that adds 20 hacky lines: discard. Same loss from deleting code: keep.

## Loop (never stop)

1. Note git state
2. Hack `train.py`
3. `git commit`
4. `uv run train.py > run.log 2>&1` (no tee — don't flood context)
5. `grep "^val_bpb:\|^peak_vram_mb:" run.log`
6. Empty grep → crash. `tail -n 50`. A few fixes then give up.
7. Append `results.tsv` (untracked): `commit val_bpb memory_gb keep|discard|crash description`
8. Improved (lower bpb) → keep the commit. Else `git reset` back.

Do NOT ask the human to continue. They may be asleep. ~12 experiments/hour, ~100 per night.

Timeout > 10 min: kill, discard, revert.

Karpathy's other spec shape: the README (nanochat) — one complexity dial, a file map, a single metric, no framework.
