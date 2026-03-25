
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

<img width="3179" height="4494" alt="你的段落文字" src="https://github.com/user-attachments/assets/33102dcb-adcf-4383-99aa-e29b973de182" />


