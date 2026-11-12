# PreMo-Bench

A fixed split and scoring settings for evaluating neonatal early-warning models on the public PreMo dataset (very-low-birth-weight infants from four neonatal intensive care units; University of Virginia Dataverse, doi:10.18130/V3/KCBTMS). The benchmark scores what a model catches, and how early, at a fixed alarm budget.

This repository holds the split and the scoring settings described in the preprint below. The analysis code is released when the paper is accepted.

## Contents

- `splits/premo_bench_v1.csv`: one row per infant (`subject`, the de-identified PreMo identifier; `split`: train, val or test). 3,835 infants: 2,320 train, 766 validation, 749 test. Frozen on 28 October 2026 (seed 20261028, stratified on site and outcome signature). MD5 a2f3219cf6e770d6e780ee2e38294f10.
- `splits/premo_bench_v1_val_roles.csv`: one row per validation infant (`subject`, `val_role`: selection or calibration). 527 selection and 239 calibration infants. Frozen on 30 October 2026 (seed 20261030). MD5 97ef2ca49e16bbf40df690a51d908971.
- `configs/scoring.yaml`: the outcome rules, warning horizons, alert rules, alarm budgets and endpoint definitions the scorer applies.

Six identifiers in the split file have a vitals file with no samples in PreMo v1.0, so they carry no score and no evaluable event; the modelling cohort is the other 3,829 infants.

## How to use it

1. Obtain PreMo from the University of Virginia Dataverse under its terms (doi:10.18130/V3/KCBTMS).
2. Train on the training infants. Choose every configuration, alert rule and threshold on the selection infants only; the calibration infants are reserved for calibration methods such as conformal risk control.
3. Freeze the configuration, alert rule and threshold at each alarm budget.
4. Score the test infants once with the scorer (alert_metrics, https://github.com/ryanfmccullough/alert_metrics) at the fixed budgets, and report the frozen points with the per-site and all-events rows.

The test labels are public, so the protocol rests on the user, as for other public clinical benchmarks.

## Citation

McCullough RF. Early warning of late-onset sepsis at a fixed alarm budget: a benchmark of prediction models in 3,829 very-low-birth-weight infants from four NICUs. Preprint, Zenodo, 2026. doi:10.5281/zenodo.24173152. See `CITATION.cff`.

Contains information from PreMo (UVA Dataverse, doi:10.18130/V3/KCBTMS), made available under the ODC Attribution License.

## Licence

MIT (see `LICENSE`).
