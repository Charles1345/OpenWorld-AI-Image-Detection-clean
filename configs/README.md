# Experiment configurations

This directory contains YAML configuration files for training, calibration,
evaluation, and model variants.

## Common sections

- `seed`, `deterministic`, `device`
- `data`: dataset, paths, batch size, workers, image size, and transforms
- `model`: detector type, CLIP settings, classification head, and optional DIRE/SGF settings
- `train`: optimization and training-loop settings
- `calibration`: temperature and conformal-prediction settings
- `eval`: prediction-export and evaluation settings
- `output`: run root and run name

## Dataset paths

Prefer configuration keys when available; otherwise loaders use:

- `HF_HOME` and `HF_DATASETS_CACHE` for Hugging Face datasets
- `VCT2_ROOT` for VCT2
- `RAID_ROOT` for RAID fallback data
- `ARIA_ROOT` for ARIA

See `DATASETS.md` for dataset-specific setup and expected layouts.

## Sample IDs

Dataset loaders emit stable `meta.id` values. These IDs are used consistently
by prediction exports, split manifests, and residual caches.
