# 数据说明

## 已随仓库提供

- `../image/`：传球场景截图（模型输入），与论文实验一致。
- 仓库根目录：`label_annotation_sample (1).csv`（人工标注样本；notebook 中路径与此文件名一致）。

## 需自行放置（体积过大，不适合直接推 GitHub）

1. **`merged_matches_plus.xlsx`**  
   放在**仓库根目录**（与 `image/` 同级），与主 notebook 中的读取路径一致。  
   若你仍保留各场比赛原始文件夹（`match1` … `match11` 及其中 `coordinates.csv` / `passes.csv`），可运行 `main_pipeline.ipynb` 最前面的合并单元格重新生成该文件。

2. **`graduation_thesis_test.xlsx`**（若后续单元格使用）  
   同样放在仓库根目录，或按 notebook 内路径自行修改。

## 可选：原始逐场数据

若希望仓库更「可复现」，可将 `match1` … `match11` 放在 `data/raw/matches/`，并相应修改 notebook 第一段合并脚本中的路径（当前脚本期望这些文件夹位于**运行时的当前工作目录**，即仓库根目录）。
