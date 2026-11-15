# Data sources, licences and integrity checks

Three kinds of data are involved in this study. Only data whose licence allows redistribution are included in this repository.

## 1. Raw benchmark data

| Family | Repository and commit | Licence | Included here |
|---|---|---|---|
| Amazon Employee Access (32,769 requests), DLBAC copy; original: Kaggle "Amazon.com – Employee Access Challenge" (2013) | https://github.com/dlbac/DlbacAlpha @ `261df3eacc455f6c9adbba1338b9280bfd2aaf09` | No licence file; the Kaggle competition rules apply to the original data | **No** – downloaded by the notebook and verified by SHA-256 |
| DLBAC synthetic ABAC (8 datasets × 4 operations) | same repository and commit | No licence file | **No** – downloaded by the notebook and verified by SHA-256 |
| HP Labs RBAC (apj, customer, firewall-1 = `fire1`, firewall-2 = `fire2`, americas_small) | https://github.com/RoleMining/ConstrainedRM @ `7a8ecec5fb6b56096ea5b6b4a0a4620e55fd04e7` | MIT (see `hp_rbac/LICENSE`) | **Yes** – `data/hp_rbac/`, byte-identical to the source |

A repository without a licence is "all rights reserved" by default, so the DLBAC files (including the DLBAC copy of the Amazon data) must not be re-uploaded to GitHub, Zenodo or the journal. Anyone can obtain the identical files from the commit above; the checksums below prove that they are the files used.

## 2. Derived data (included)

`derived/hp_rbac_splits/` contains the 15 HP Labs RBAC request sets used in the experiments (5 datasets × seeds 11, 22, 33), exactly as built by `src/acdata.py::load_hp_rbac` with the pinned package versions. They are derived from MIT-licensed data and are redistributed under the same licence. Their test-set sizes match the archived results (`results/units/*.csv`, column `n_test`) for all 15 splits.

Columns: `uid` user id; `rid` = `perm` permission id; `ugroup` user group (clustering of training assignments); `pcluster` permission cluster; `is_test` 1 = test request, 0 = training request; `y` 1 = legitimate (granted), 0 = illegitimate (denied). `MANIFEST.csv` lists the size, class balance, number of users/permissions/groups and SHA-256 of every file.

Derived splits of the Amazon and DLBAC data are **not** included, because they would redistribute unlicensed data; they are re-created exactly by the notebook (Amazon: 5-fold stratified CV × seeds 11, 22, 33; DLBAC: the published train/test splits).

## 3. Results (included)

`results/` holds every output of the executed notebook: per-split results (`units/`, 62 files), all scenarios (`tables/all_units.csv`, 1,240 rows = 62 splits × 4 revocation sizes × 5 remedies), family means (`tables/summary_by_family_fraction_remedy.csv`, Supplementary Table S1), Wilcoxon tests (`tables/wilcoxon_tests.csv`, Supplementary Table S2), `summary.json`, `paper_numbers.txt`, `environment.json` and Figs. 2–6. Column definitions: `results/DATA_DICTIONARY.md`.

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
