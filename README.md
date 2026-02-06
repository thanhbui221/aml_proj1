# Applied Machine Learning – Football Match Outcome Prediction

## 📌 Project Overview
Over the past two decades, professional sports have increasingly adopted data-driven decision-making. Football, in particular, sits at the center of the sports analytics revolution, with rich historical and real-time data used by broadcasters, fantasy players, professional teams, and betting platforms.

In this group project for **Applied Machine Learning**, we tackle a **football match result prediction** problem using real historical data provided by **Sportmonks**, a leading sports data provider. The project is based on the **QRT Football Data Challenge**, which focuses on predicting match outcomes across multiple leagues and competitive levels worldwide.

Our goal is to build robust machine learning models that generalize well across leagues, teams, and geographies—reflecting real-world sports analytics challenges.

---

## 🎯 Problem Statement
Given historical **team-level** and **player-level** statistics for football matches, predict the outcome of a match as one of the following:

- **Home Win**
- **Draw**
- **Away Win**

This is formulated as a **multi-class classification** problem.

---

## 🏁 Challenge Objectives
- Predict match outcomes using structured football data
- Build models that generalize across different leagues and divisions
- Apply end-to-end ML workflow:
  - Data understanding & preprocessing
  - Feature engineering
  - Model training & evaluation
  - Performance comparison and interpretation

---

## 📊 Dataset Description

### Data Source
- Provided by **Sportmonks**
- Used exclusively for this challenge (external data is **not allowed**)

### Input Data
The dataset is split into training and test sets:
- X_train.zip
- X_test.zip
- Y_train.csv
- Y_train_supp.csv


#### Team-Level Data
Each team dataset includes:
- **Identifiers**:
  - `ID`
  - `LEAGUE`
  - `TEAM_NAME` (not included in test set)
- **25 team statistics**, aggregated by **sum**, **average**, and **standard deviation**, including:
  - Attacks, possession, passes
  - Shots (on/off target, inside/outside box)
  - Goals, fouls, cards, corners, saves
  - Game outcomes (won/draw/lost)

#### Player-Level Data
Each player dataset includes:
- **Identifiers**:
  - `ID`
  - `LEAGUE`
  - `TEAM_NAME`
  - `POSITION`
  - `PLAYER_NAME` (not included in test set)
- **52 fine-grained player statistics**, aggregated similarly to team statistics

All features are **standardized**, and team/player/league names are removed from the test set.

---

## 🎯 Output Labels
The target variable is a **3-class outcome vector**:

| Outcome      | Encoding |
|--------------|----------|
| Home Win     | [1, 0, 0] |
| Draw         | [0, 1, 0] |
| Away Win     | [0, 0, 1] |

The evaluation metric is **classification accuracy**.

---

## 🔁 Additional Targets
The supplementary file `Y_train_supp.csv` includes alternative targets such as:
- `GOAL_DIFF_HOME_AWAY`

These can be used to experiment with:
- Regression models
- Multi-task learning
- Richer feature representations

---

## 🧠 Machine Learning Approach
This project focuses on:
- Feature aggregation across home vs away teams
- Handling high-dimensional structured data
- Comparing multiple ML models (e.g. logistic regression, tree-based models, ensemble methods)
- Model evaluation and interpretability

---

## 📁 Project Structure
.
├── data/ # Dataset files (ignored by git)
├── notebooks/ # EDA, feature engineering, modeling
├── src/ # Reusable ML code
├── README.md
└── .gitignore


---

## ⚠️ Important Setup Instructions (READ THIS)
**All team members must do the following before starting:**

1. Go to the official challenge page:  
   👉 https://challengedata.ens.fr/participants/challenges/143/

2. Download **all dataset files**

3. Create a local folder named:
data/


4. Place all downloaded files inside the `data/` folder

5. Add the following line to `.gitignore`:
data/


⚠️ **Do NOT commit the dataset to GitHub**  
⚠️ **Do NOT use any external data** (risk of disqualification)

---

## 📜 Disclaimer
The data provided is strictly for use within this challenge and academic project. Any use beyond this scope is prohibited. All applicable terms of service apply.

---

## 👥 Team
Applied Machine Learning – Group Project  
(Team members to be added)


