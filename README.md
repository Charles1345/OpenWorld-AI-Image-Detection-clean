# Open-World AI Image Detection with Abstention

Research code for an AI-image detector that can return **AI**, **Real**, or
**Abstain**. The project combines a CLIP-based classifier with calibration,
conformal prediction, and selective-risk evaluation under distribution shift.

## Authors

- **Zongchi Xie** — zongchix@andrew.cmu.edu
- Omar Ghabayen — oghabaye@andrew.cmu.edu
- Gorkem Yar — gyar@andrew.cmu.edu
- Abdullah Almansour — aalmanso@andrew.cmu.edu
- Youlin Qu — ynq@andrew.cmu.edu

## How to run

Install dependencies, then launch the demo with a saved run:

```bash
python3 -m pip install -r requirements.txt
make demo RUN=outputs/runs/<run_id>
```

Open the local Gradio URL shown in the terminal and upload an image. The
equivalent direct command is:

```bash
python3 demo/app.py --run outputs/runs/<run_id> --device cpu
```

## What this repository provides

- Frozen CLIP-style image encoder with a lightweight classification head.
- Temperature scaling and split conformal prediction for uncertainty handling.
- Threshold and conformal abstention policies.
- Evaluation configurations for VCT2, RAID, ARIA, CIFAKE, and AIArt.
- Optional DIRE-style residual features and fusion models.
- Artifact-backed prediction, evaluation, plotting, and summary scripts.

## Pipeline

```text
dataset → train detector → calibrate → predict with abstention → evaluate
```

Run artifacts are stored under `outputs/runs/<run_id>/`, including the config,
metadata, checkpoints, calibration files, split manifest, evaluation metrics,
and logs.

## Quick start

Install dependencies and run commands from the repository root:

```bash
python3 -m pip install -r requirements.txt
python3 scripts/train_baseline.py --config configs/baseline_clip.yaml
python3 scripts/calibrate_temperature.py --help
python3 scripts/build_conformal.py --help
python3 scripts/evaluate.py --help
```

Useful workflows:

```bash
make smoke       # compileall + tests
make test        # tests only
make plots       # figures from saved run artifacts
make summary     # results summary
make demo        # launch the local Gradio demo
```

See `DATASETS.md` for dataset setup, environment variables, and folder layouts.
See `configs/README.md` for configuration conventions.

## Important evaluation caveat

Conformal coverage guarantees rely on exchangeability between calibration and
test data. VCT2, RAID, and ARIA are intended to measure distribution shift, so
coverage on those datasets is empirical rather than distributionally
guaranteed. Risk-coverage behavior and point metrics should be reported
together.

## Repository map

```text
src/owaid/   Core package: data, models, training, calibration, inference, metrics
scripts/     Command-line entry points
configs/     Experiment YAML files
demo/        Local tri-state prediction UI
reports/     Paper-facing figures, tables, and summaries
tests/       Automated tests
```

## License and citation

See `LICENSE` and `CITATION.cff` for project licensing and citation metadata.
