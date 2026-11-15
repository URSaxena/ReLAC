# ReLAC: supplementary material

Supplementary material for the article *ReLAC: Measuring and Eliminating the Leakage of Revoked Access in Learned Access Control for Cloud Environments*.

## Contents

| Path | Content |
|---|---|
| `ESM_1_ReLAC_reproduce_all_executed.ipynb` | Jupyter notebook that downloads and verifies the benchmark data (SHA-256) and reproduces every number, table and figure of the article, with the outputs of the reported run. Open it in Google Colab and choose *Runtime → Run all* (CPU, about 30–40 min). |
| `ESM_2_ReLAC_results_FINAL/tables/` | All 1,240 scenario–remedy results (`all_units.csv`), family means (`summary_by_family_fraction_remedy.csv`) and Wilcoxon signed-rank tests with Holm correction (`wilcoxon_tests.csv`). |
| `ESM_2_ReLAC_results_FINAL/paper_numbers.txt` | Every number quoted in the article. |
| `ESM_2_ReLAC_results_FINAL/README_results.md` | Column definitions, data sources and SHA-256 checksums. |
| `ESM_3_ReLAC_data/data/hp_rbac/` | HP Labs RBAC benchmarks (MIT licence, unchanged from the source). |
| `ESM_3_ReLAC_data/data/derived/hp_rbac_splits/` | The 15 RBAC request sets used in the experiments (gzip-compressed CSV; see `MANIFEST.csv`). |
| `ESM_3_ReLAC_data/data/DATA_SOURCES.md` | Sources, licences and SHA-256 checksums of all 22 input files. |

## Third-party data

The Amazon Employee Access data (DLBAC copy) and the DLBAC synthetic datasets are not redistributed because their source repository has no licence. The notebook downloads them from https://github.com/dlbac/DlbacAlpha at commit `261df3eacc455f6c9adbba1338b9280bfd2aaf09` and verifies them against the checksums in `DATA_SOURCES.md`.

## Licence

MIT (`LICENSE`). The HP Labs RBAC data keep their original MIT licence (`ESM_3_ReLAC_data/data/hp_rbac/LICENSE`).
