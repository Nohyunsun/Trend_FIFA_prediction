# 2026 FIFA World Cup Winner Prediction Analysis

This project predicts the potential winner of the **2026 FIFA World Cup** using historical international football match data and team performance indicators.

The analysis is implemented in a Google Colab notebook and uses multiple CSV datasets to preprocess match records, standardize country names, calculate team strength, and simulate the 2026 World Cup tournament.

---

## Project Overview

The main objective of this project is to estimate each national team's probability of winning the 2026 FIFA World Cup.

The prediction process is based on historical match results, shootout outcomes, goalscorer information, country name standardization, recent team performance, and Elo rating-based team strength.

---

## Dataset

This project uses four main datasets.

| Dataset            | Description                                                                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `results.csv`      | Contains international football match results, including match date, home team, away team, scores, tournament name, city, country, and neutral venue information. |
| `shootouts.csv`    | Contains penalty shootout results, including participating teams, shootout winner, and the team that took the first penalty.                                      |
| `goalscorers.csv`  | Contains goalscorer information, including scoring team, player name, goal time, own goal status, and penalty goal status.                                        |
| `former_names.csv` | Contains historical country/team name changes, used to standardize former country names into current names.                                                       |

The historical match dataset covers international football matches from 1872 to recent years and includes matches from various competitions such as the FIFA World Cup, qualifiers, and friendly matches.

---

## Data Sources

* International football results dataset: Kaggle
* FIFA Men's World Ranking: FIFA official website

---

## Column Definitions

### `results.csv`

| Column       | Description                                     |
| ------------ | ----------------------------------------------- |
| `date`       | Match date                                      |
| `home_team`  | Home team name                                  |
| `away_team`  | Away team name                                  |
| `home_score` | Final score of the home team                    |
| `away_score` | Final score of the away team                    |
| `tournament` | Tournament name                                 |
| `city`       | City where the match was held                   |
| `country`    | Country where the match was held                |
| `neutral`    | Whether the match was played at a neutral venue |

### `shootouts.csv`

| Column          | Description                      |
| --------------- | -------------------------------- |
| `date`          | Match date                       |
| `home_team`     | Home team name                   |
| `away_team`     | Away team name                   |
| `winner`        | Winner of the penalty shootout   |
| `first_shooter` | Team that took the first penalty |

### `goalscorers.csv`

| Column      | Description                                     |
| ----------- | ----------------------------------------------- |
| `date`      | Match date                                      |
| `home_team` | Home team name                                  |
| `away_team` | Away team name                                  |
| `team`      | Team that scored the goal                       |
| `scorer`    | Name of the goalscorer                          |
| `own_goal`  | Whether the goal was an own goal                |
| `penalty`   | Whether the goal was scored from a penalty kick |

### `former_names.csv`

| Column       | Description                         |
| ------------ | ----------------------------------- |
| `current`    | Current country/team name           |
| `former`     | Former country/team name            |
| `start_date` | Start date of the former name usage |
| `end_date`   | End date of the former name usage   |

---

## Methodology

### 1. Data Upload

The required CSV files are uploaded into the Colab environment.

Required files:

```text
results.csv
shootouts.csv
goalscorers.csv
former_names.csv
```

---

### 2. Data Preprocessing

The raw datasets are cleaned and standardized before analysis.

Main preprocessing steps include:

* Converting date columns into datetime format
* Removing unnecessary spaces and inconsistent text formats
* Standardizing country and team names
* Handling missing values
* Merging former country names with current country names
* Creating match-level features from historical results

---

### 3. Country Name Standardization

The `former_names.csv` dataset is used to match historical country names with their current names.

This step prevents the same national team from being treated as multiple different teams due to historical naming differences.

Example:

```text
Former country name → Current country name
```

---

### 4. Match Result Data Construction

The `results.csv` dataset is used as the base match result table.

It provides the core information needed to calculate each national team's historical performance, including:

* Wins
* Draws
* Losses
* Goals scored
* Goals conceded
* Goal difference
* Match location
* Tournament type

---

### 5. Goalscorer Data Integration

The `goalscorers.csv` dataset is combined with match results to reflect additional attacking information.

This data helps analyze:

* Goal-scoring patterns
* Scoring frequency by team
* Penalty goals
* Own goals
* Player-level scoring records

---

### 6. Shootout Result Adjustment

The `shootouts.csv` dataset is used to adjust matches that ended in a draw but had a final winner through a penalty shootout.

This is especially important for tournament simulations, where knockout-stage matches must produce a winner.

---

### 7. Elo Rating Calculation

An Elo rating system is applied to estimate each national team's relative strength.

Elo ratings are updated based on match results and are used as one of the main indicators for predicting future match outcomes.

The Elo-based approach reflects:

* Historical team strength
* Match outcomes
* Relative strength between opponents
* Performance changes over time

---

### 8. Recent Performance Reflection

Recent match results are considered to better reflect the current form of each national team.

Recent performance indicators may include:

* Recent win rate
* Recent goal difference
* Recent goals scored
* Recent goals conceded
* Recent match trends

---

### 9. Match Prediction Model

A match result prediction model is trained using team-level features generated from historical match data.

The model predicts the probability of each team winning a match based on features such as:

* Elo rating difference
* Historical performance
* Recent form
* Goals scored
* Goals conceded
* Goal difference

---

### 10. 2026 World Cup Simulation

The 2026 FIFA World Cup is simulated using the predicted match probabilities.

The simulation includes:

* Group stage matches
* Knockout stage matches
* Tournament progression
* Final winner prediction

By repeating the simulation multiple times, the model estimates each team's probability of winning the tournament.

---

## Analysis Workflow

```text
1. Upload CSV files
2. Preprocess datasets
3. Standardize country names
4. Construct match result dataset
5. Calculate Elo ratings
6. Generate team performance features
7. Train match prediction model
8. Simulate the 2026 FIFA World Cup
9. Calculate winning probabilities
10. Export results as CSV
```

---

## Output

The final output is a CSV file containing the predicted winning probability of each national team.

Example output columns:

| Column             | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `team`             | National team name                                       |
| `win_probability`  | Estimated probability of winning the 2026 FIFA World Cup |
| `simulation_count` | Number of tournament simulations won by the team         |

---

## Expected Result

The project provides a probability-based prediction of the 2026 FIFA World Cup winner.

Rather than predicting a single fixed winner, the model estimates each team's likelihood of winning based on historical data, recent performance, Elo rating, and tournament simulation results.

---

## Tools Used

* Python
* Google Colab
* Pandas
* NumPy
* Scikit-learn
* CSV
* Elo Rating
* Tournament Simulation

---

## Project Structure

```text
2026-fifa-worldcup-prediction/
│
├── fifa_worldcup_2026_prediction_colab.ipynb
├── results.csv
├── shootouts.csv
├── goalscorers.csv
├── former_names.csv
├── output/
│   └── worldcup_2026_champion_prediction.csv
|   └── worldcup_2026_team_strength.csv
└── README.md
```

---

## How to Run

1. Open the notebook in Google Colab.
2. Upload the required CSV files.
3. Run each cell in order.
4. Check the predicted winning probability results.
5. Download the final CSV output.

---

## Notes

This project is intended for analytical and educational purposes.
The prediction results may vary depending on data preprocessing, model settings, selected features, and simulation assumptions.
