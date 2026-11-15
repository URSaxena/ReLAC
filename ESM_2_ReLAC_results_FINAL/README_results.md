# Data dictionary of the results

Decision convention: 1 = grant, 0 = deny. All rates are fractions in [0, 1]. Remedies: `stale` (unchanged model), `retrain` (full retraining), `weighted` (retraining with relabelled entries weighted 20×), `finetune` (50 additional boosting iterations, features and threshold kept), `overlay` (exact deny overlay in front of the unchanged model).

## `tables/all_units.csv` (one row per split × revocation size × remedy; 1,240 rows)

| Column | Meaning |
|---|---|
| `task` | split identifier (e.g. `hp-apj/s11`, `amazon-kaggle/s11/f0`, `u4k-r4k-auth11k/op1`) |
| `unit` | short identifier of the split |
| `dataset`, `kind` | dataset name; family: `real` = Amazon, `real-rbac` = HP Labs RBAC, `synthetic-abac` = DLBAC synthetic |
| `seed` | random seed of the split and of the revocation |
| `fraction` | revocation size: share of granted test requests revoked (0.01, 0.05, 0.10, 0.20) |
| `remedy` | remedy applied after the revocation |
| `n_test` | number of test requests |
| `n_revoked` | number of revoked test requests (\|Q_rev\|) |
| `n_relabelled_log` | number of training/validation log entries relabelled as denials (Eq. 2) |
| `revoked_seen_in_log` | share of revoked test requests whose combination occurs as a granted entry in the training log |
| `leak` | leakage Leak(d), Eq. (3): share of revoked test requests still granted |
| `leak_seen`, `leak_unseen` | leakage restricted to seen / unseen combinations (empty if there are none) |
| `stale_leak` | leakage of the stale model in the same scenario |
| `frr_kept` | false rejection rate on legitimate non-revoked test requests |
| `d_frr` | ΔFRR: change in `frr_kept` relative to the stale model |
| `far_orig` | false acceptance rate on originally illegitimate test requests |
| `changed_unrevoked` | collateral change Coll(d), Eq. (3): share of non-revoked test decisions that differ from the stale model |
| `ba` | balanced accuracy on the relabelled test set, Eq. (7) |
| `update_s` | wall-clock time of the remedy in seconds (machine-dependent) |
| `base_fit_s` | wall-clock time of fitting the initial model in seconds |

## `tables/summary_by_family_fraction_remedy.csv` (Supplementary Table S1)
Means over splits of the columns above by `kind`, `fraction` and `remedy`; `*_sd` columns are standard deviations over splits; `seen` is the mean of `revoked_seen_in_log`.

## `tables/wilcoxon_tests.csv` (Supplementary Table S2)
Two-sided Wilcoxon signed-rank tests over splits: `family`, `fraction`, `comparison` (metric in brackets: `leak` or `churn` = collateral change), `n` splits, `median_diff` median paired difference (first minus second remedy), `p_holm` Holm-corrected p-value within family and revocation size.

## `paper_numbers.txt`
Every number quoted in the article, printed by the notebook from the tables above.

# Data sources

The notebook downloads all input data from the original repositories at fixed commits and verifies each file by SHA-256 before any experiment runs:

| Family | Repository and commit | Licence |
|---|---|---|
| Amazon Employee Access (DLBAC copy) and DLBAC synthetic ABAC | https://github.com/dlbac/DlbacAlpha @ `261df3eacc455f6c9adbba1338b9280bfd2aaf09` | No licence (not redistributed) |
| HP Labs RBAC | https://github.com/RoleMining/ConstrainedRM @ `7a8ecec5fb6b56096ea5b6b4a0a4620e55fd04e7` | MIT |

## SHA-256 of every data file (verified by the notebook before any experiment runs)

| File | SHA-256 |
|---|---|
| `ConstrainedRM/datasets/realWorld/apj.txt` | `7f4106402caf47f6cef0b9df0ddca64529df8529b226f81c47c3cafe0f854fa4` |
| `ConstrainedRM/datasets/realWorld/customer.txt` | `6001fedab56a38b3e871d9ec69e9c2e726d221a9637bac67b37fc1a5fe045106` |
| `ConstrainedRM/datasets/realWorld/fire1.txt` | `a2e536e793846101ad7c7a7d97345466cc134e11c9b6b79261ca3f95db181099` |
| `ConstrainedRM/datasets/realWorld/fire2.txt` | `c2a34e45b55747d4d5b4c6dbcf5145b8058a6502ad25f5a25af655239833592d` |
| `ConstrainedRM/datasets/realWorld/americas_small.txt` | `dfdd68ceedda7f7153b1e908f9b616f24cf8c55a146de73d67e81c1bfcd57770` |
| `DlbacAlpha/dataset/real-world/amazon1/train_test_amazon1.sample` | `4f2269d05fef4056b6480b6db103e306b676c694192f02b37c291411657a4afe` |
| `DlbacAlpha/dataset/synthetic/u4k-r4k-auth11k/train_u4k-r4k-auth11k.sample` | `fd0ea117a427328d9c9cacbdd6bab595285abaefcf05efba8d4c846c7545876f` |
| `DlbacAlpha/dataset/synthetic/u4k-r4k-auth11k/test_u4k-r4k-auth11k.sample` | `eb4ba88ed3fdb29ff26a5eed764a7de1ae86c2fafcaf925c7cd23cfed3303e5c` |
| `DlbacAlpha/dataset/synthetic/u5k-r5k-auth12k/train_u5k-r5k-auth12k.sample` | `fa4bdad710d2a1579f720225dbb7a1c40c130c6954cdd7b20d2f9492846aff7a` |
| `DlbacAlpha/dataset/synthetic/u5k-r5k-auth12k/test_u5k-r5k-auth12k.sample` | `a04316f19936ec54bce761f176dc1c0057c3c2c7ca88150bb54eb78e123bbbee` |
| `DlbacAlpha/dataset/synthetic/u5k-r5k-auth19k/train_u5k-r5k-auth19k.sample` | `598ae1040facfaf389d71c395fd40433f393904ce4816a5a4d46f4ece9bf7c98` |
| `DlbacAlpha/dataset/synthetic/u5k-r5k-auth19k/test_u5k-r5k-auth19k.sample` | `ad3b0344405702818ae2459166033f59de030e2983e92bf5fe64ca1b7f4b14db` |
| `DlbacAlpha/dataset/synthetic/u4k-r4k-auth21k/train_u4k-r4k-auth21k.sample` | `f1c17eeeeda0ebc7f5caab673e5dc45a2a298e450ea959ae26f504d54faa8ea1` |
| `DlbacAlpha/dataset/synthetic/u4k-r4k-auth21k/test_u4k-r4k-auth21k.sample` | `4875b2d88f843e6f5b3d9968f9395babfe4ef5ad0d29deba8da28fae3d7d3ae7` |
| `DlbacAlpha/dataset/synthetic/u4k-r7k-auth20k/train_u4k-r7k-auth20k.sample` | `8adb2fc5e5e3192ad3370d2fe7a8fe3aa4137c0caf69e0a7a5143b08fa6b7508` |
| `DlbacAlpha/dataset/synthetic/u4k-r7k-auth20k/test_u4k-r7k-auth20k.sample` | `db4e1ccc548190d38fb62b1d8892c5b2f95e09aa171f2b25828ece55d99f9284` |
| `DlbacAlpha/dataset/synthetic/u4k-r4k-auth22k/train_u4k-r4k-auth22k.sample` | `895eaffadd7cac4252458d21d9bbf230d3cdaf70bcdcf4d245d38625aad276ad` |
| `DlbacAlpha/dataset/synthetic/u4k-r4k-auth22k/test_u4k-r4k-auth22k.sample` | `ddce7b244dba0d4d34f9ecd15e1da2c9b5b49125751ba7b33783b9a1574c6541` |
| `DlbacAlpha/dataset/synthetic/u4k-r6k-auth28k/train_u4k-r6k-auth28k.sample` | `699aafb423e898bdd73f1ac07c41a97d879df59f176656f3be59a30ec1b45204` |
| `DlbacAlpha/dataset/synthetic/u4k-r6k-auth28k/test_u4k-r6k-auth28k.sample` | `528de29d36eda89e89b73d690400679b624f89cb45385fa72c6caca2b39da6b3` |
| `DlbacAlpha/dataset/synthetic/u6k-r6k-auth32k/train_u6k-r6k-auth32k.sample` | `96807f5cd7572d10c71958254de8cf32ab4c78e3c0ebd64f9a500b799b1046fc` |
| `DlbacAlpha/dataset/synthetic/u6k-r6k-auth32k/test_u6k-r6k-auth32k.sample` | `c4e1d1fb244768551c234c3a8a0f664ba9ee561c76c63fe013b0e41e0348478d` |
