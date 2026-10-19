# Reports

Paper-facing material generated from saved run artifacts.

- `paper.md`: working manuscript
- `paper_outline.md`: manuscript structure
- `figures/`: generated figures
- `tables/`: generated tables
- `results_summary_template.md`: summary template

Generate reports from the repository root:

```bash
python3 scripts/make_plots.py --runs outputs/runs --out reports/figures
python3 scripts/generate_summary.py --run outputs/runs/<run_id> --out reports/results_summary.md
```

Figures and summaries should be derived from `outputs/runs/<run_id>/` so the
reported results remain reproducible.
