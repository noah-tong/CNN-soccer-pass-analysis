<<<<<<< HEAD
# Modeling Tactical Value of Football Passes with CNN

This project is my Master’s thesis completed at Utrecht University (Applied Data Science, 2024), in cooperation with Forward Football BV. The project focuses on identifying whether a football pass is tactically valuable by combining spatial situational images with Convolutional Neural Networks (CNN), rather than relying solely on traditional numerical features.

---

## Core Idea

A valuable pass is defined not only by whether it is successful, but by whether it creates attacking potential, generates time advantage, and breaks the opponent’s defensive structure. To capture these tactical elements, tracking data is transformed into spatial situational images, and a CNN is trained to classify whether a pass is tactically valuable directly from spatial configurations.

---

## Data

The dataset consists of professional tracking data collected from 11 matches. Two core tables are used throughout the project. The `passes.csv` table contains pass events and contextual information such as players involved, pressure level, and pass outcome. The `coordinates.csv` table contains full-frame tracking data of all players and the ball, enabling reconstruction of the spatial situation at the exact moment of each pass.

---

## Label Construction

A total of 500 passes were manually labeled as valuable or not valuable based on spatial diagrams and tactical judgment. A logistic regression model was then used to construct a continuous `pass_score` using four core variables: `xT_change`, `pass_speed`, `pass_length`, and `pressure_level`. The final binary label is defined as:

```python
is_valuable = 1 if pass_score > 0.5 else 0

```
## Agreement with Human Labels

The automatically constructed `pass_score` achieves strong agreement with manual annotations, reaching an F1-score of approximately 0.87 on the 500 labeled passes. This indicates that the rule-based scoring system provides a reliable proxy for human tactical judgment and can be used as a stable supervision signal for CNN training.

---

## Image-Based CNN Model

Each passing event is converted into a 224×224 spatial situational image constructed from tracking data. The image encodes the passer, receiver, teammates, and opponents, together with the pass trajectory, the pressure zone around the passer, the blocked passing lane, and the approaching direction of the nearest defender.

The CNN model adopts ResNet-50 as the backbone network and performs binary classification to predict whether a pass is tactically valuable (`is_valuable`).

---

## Results

| Model | Input | Validation AUC |
|--------|--------|----------------|
| Logistic Regression | Structured features | ~0.66 |
| CNN (raw positions) | Images | ~0.50 |
| **CNN (enhanced images)** | Images + tactical overlays | **~0.77** |

---

## Grad-CAM Interpretation

Grad-CAM visualizations indicate that the trained CNN consistently attends to tactically meaningful regions, including key passing corridors, dense defender clusters, and high-pressure zones around the passer. This suggests that the model is learning interpretable spatial patterns aligned with real tactical decision-making.

=======
# 毕业论文 · CNN / ResNet 传球价值分类

足球比赛传球数据与球场截图，结合 **CNN（含 ResNet50）**、传统机器学习（Random Forest、XGBoost 等）与可解释性分析（SHAP、Grad-CAM 等）的完整实验流程。

## 仓库结构

```text
graduation-thesis-cnn/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── main_pipeline.ipynb   # 主实验（由原 final_test 整理，已清空输出、便于 Git）
│   └── archive/              # 早期草稿 notebook（test / test-2），一般不必再跑
├── image/                    # 传球截图数据集（约 5000+ 张）
├── figures/                  # 论文用图（从原工程根目录汇总的 PNG）
├── models/                   # 本地训练得到的 .h5 权重（默认被 git 忽略）
├── data/
│   └── README.md             # 大数据文件放置说明
└── label_annotation_sample (1).csv
```

## 快速开始

1. **创建环境**（示例使用 venv）：

   ```bash
   python -m venv .venv
   .venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. **准备数据**  
   将 `merged_matches_plus.xlsx` 放到**本仓库根目录**。说明见 [`data/README.md`](data/README.md)。

3. **运行主流程**  
   在仓库根目录启动 Jupyter，打开 `notebooks/main_pipeline.ipynb`。  
   第一个代码单元会根据当前工作目录自动切换到仓库根，保证 `image/` 与数据路径与原先一致。

## 关于 GitHub

- **不要提交** `*.h5` / 超大 `*.xlsx`（已在 `.gitignore` 中排除）。权重可放在 [GitHub Releases](https://docs.github.com/repositories/releasing-projects-on-github)、网盘或 [Zenodo](https://zenodo.org/) 等。
- 若仍觉得仓库过大，可在 `.gitignore` 中取消注释 `# image/` 行，改为单独发布图像压缩包。

## 许可证

如对外公开，请自行补充 `LICENSE`（与学校/导师要求一致）。
>>>>>>> ee0a5bd (Initial commit: thesis CNN pipeline layout and cleaned main notebook)
