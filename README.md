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

## Understaind the dataset more (Train_Data folder)

This section explains how the data is organized so you can load and use it correctly.

### What you have on disk

In this project, the data lives under `data/`:
- Training features (inputs): `data/Train_Data/` (4 csv files)
- Training labels (target): `data/Y_train_1rknArQ.csv`
- Test features: `data/Test_Data/` (4 csv files)
- Example test submission: `data/Y_test_random_sEE2QeA.csv`

The same 4 csvs exist for both train and test; only the folder name and file prefix change (`train_*` vs `test_*`).

### The 4 input files (per match: HOME vs AWAY, team vs player)

Each **match** is indentifed by a unique **ID**. For each match you get:
- `train_home_team_statistics_df.csv`: **Home team** stats (one row per match) | 1 row per ID (match ID)
- `train_away_team_statistics_df.csv`: **Away team** stats (one row per match) | 1 row per ID (match ID)
- `train_home_player_statistics_df.csv`: **Home team's players** (one row per player per match) | many rows per ID (match ID)
- `train_away_player_statistics_df.csv`: **Away team's players** (one row per player per match) | many rows per ID (match ID)

For **Team/Match files:** One row per match. Same IDS as in `Y_train`, you can join directly on `ID`.

For **Player files:** Several rows per match (one per player in the squad). To get one row per match, you must/should **aggregate by `ID`** (e.q. mean, sum, or customer features per team).

So for each match you have: ome home team row, one away team row, any many home/away player rows. The **target** for that match is in `Y_train`: one row per `ID` with values as `HOME_WINS`, `DRAW`, `AWAY_WINS`.

### How the feature columns are built

Statistics are not single columns; each metric is expanded into **serveral columns** depending on:
1. **Time window** (look at the middle part of the name: `__season__` vs `_5_last_match_`)
  - **Season so far**: stats for the curren seaon up to **(but not including)** the match to predict.
  - **Last 5 match**: stats over the 5 games immediately **before** that match

2. **Aggregation** (look at the end: `_sum`, `_average`, `_std`)
  - **sum**: total over the window
  - **average**: mean per game
  - **std**: standard deviation over the window

**Example for team data:** A single `TEAM_GOALS` metric becomes 6 columns - the name tells you the window and aggregation method:
- `TEAM_GOALS_season_sum`: season so far, total goals
- `TEAM_GOALS_season_average`: season so far, average per game
- `TEAM_GOALS_season_std`: season so far, standard deviation
- `TEAM_GOALS_5_last_match_sum`: last 5 games, total goals
- `TEAM_GOALS_5_last_match_average`: last 5 games, average per game
- `TEAM_GOALS_5_last_match_std`: last 5 games, standard deviation

### Train vs Test: whats diff
- **Train (Train_Data):** includes `LEAGUE`, `TEAM_NAME` (and in player files `PLAYER_NAME`, `POSITION`). Useful for EDA and understadning the data. 
- **Test (Test_Data):** Only `ID` (and in player files `POSITION`) are kept as indentifiers. No league or team or player name, so our model must rely on the numerical stats only.

Values in the CSVs are **standardized** (scaled), so the numbers you see are not raw counts.

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

5. Extract zip files in `data/`


⚠️ **Do NOT commit the dataset to GitHub**  
⚠️ **Do NOT use any external data** (risk of disqualification)

---

## 📜 Disclaimer
The data provided is strictly for use within this challenge and academic project. Any use beyond this scope is prohibited. All applicable terms of service apply.

---

## 👥 Team
Applied Machine Learning – Group Project  
(Team members to be added)


