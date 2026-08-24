<!-- source: https://github.com/karpathy/nanochat/blob/master/README.md -->
# nanochat README (product spec)

Different from `program.md`. The README is the product: one `--depth` dial, a public metric, a speedrun.

## Product

Simplest experimental harness for training LLMs on one GPU node. Tokenization, pretrain, finetune, eval, inference. GPT-2-grade on 8×H100 in about two hours (~$48). All other hyperparameters computed from `--depth`.

## Metric

Primary: **time-to-GPT-2** — wall-clock on 8×H100 to beat GPT-2 (1.6B) DCLM CORE (0.256525). Leaderboard also prints `val_bpb`. Autoresearch rounds are rows on that board.

## Call contract

```
bash runs/speedrun.sh
python -m scripts.chat_cli
```

`runs/speedrun.sh` is the reference way to train and talk. Setup is `uv sync --extra gpu`.

## Out of scope of the README-as-spec

No giant config objects. No multi-file hyperparameter surface. Research extras (`scaling_laws.sh`, `miniseries.sh`) sit beside the speedrun, not inside it.
