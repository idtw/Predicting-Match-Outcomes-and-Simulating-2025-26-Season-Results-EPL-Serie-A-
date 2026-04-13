# Predicting Match Outcomes and Simulating 2025/26 Season Results - EPL & Serie A

A multi-season football data science project modeling match outcomes and simulating the remaining 2025/26 Premier League and Serie A seasons using xG-based Poisson distributions and Monte Carlo methods.

---

## What This Project Does

This notebook pulls five seasons of team-level xG and xGA data (2021/22 through 2025/26) for the Premier League and Serie A, builds normalized attack and defense strength ratings for every team, and uses those ratings to power two things:

1. A Poisson match outcome model that generates Win/Draw/Loss probabilities for any head-to-head fixture
2. A Monte Carlo simulator that runs the remaining 2025/26 fixtures 10,000 times and converts the results into finish probabilities per position per team - title race, European spots, and relegation included

---

## Why EPL and Serie A

Both leagues offer genuine top-four competition across multiple seasons. Unlike the Bundesliga or Ligue 1 - where Bayern and PSG historically dominate - the EPL and Serie A produce meaningful variance at the top of the table year over year, making them more analytically interesting to model and simulate.

---

## Methodology

### Strength Ratings
Each team's xG per match and xGA per match are normalized against the league average for that season, producing an attack rating and a defense rating. A rating above 1.0 means above average; below 1.0 means below average.

### Poisson Model
Expected goals for each fixture are calculated by combining the home team's attack rating, the away team's defense rating, the league average scoring rate, and a 1.1x home advantage multiplier. Goals are then modeled as Poisson-distributed random variables - a standard and well-validated approach in football data science.

### Monte Carlo Simulation
The remaining 2025/26 fixtures are simulated 10,000 times. Each iteration samples a scoreline from the Poisson distribution for each match, updates the points table, and records the final standings. Finish probabilities are the aggregated results across all iterations.

---

## Project Structure

```
pl_predictor/
├── pl_predictor.ipynb          - Main notebook
├── requirements.txt            - Python dependencies
├── README.md                   - This file
├── LICENSE                     - MIT License
├── competition_data/
│   ├── epl_2021.csv            - Premier League 2021/22 (Understat)
│   ├── epl_2022.csv            - Premier League 2022/23 (Understat)
│   ├── epl_2023.csv            - Premier League 2023/24 (Understat)
│   ├── epl_2024.csv            - Premier League 2024/25 (Understat)
│   ├── epl_2025.csv            - Premier League 2025/26 (Understat)
│   ├── seriea_2021.csv         - Serie A 2021/22 (Understat)
│   ├── seriea_2022.csv         - Serie A 2022/23 (Understat)
│   ├── seriea_2023.csv         - Serie A 2023/24 (Understat)
│   ├── seriea_2024.csv         - Serie A 2024/25 (Understat)
│   ├── seriea_2025.csv         - Serie A 2025/26 (Understat)
│   └── schedules_epl_seriea_2025.csv  - 2025/26 fixture list (FBref)
└── outputs/                    - Generated charts and visualizations
```

---

## Notebook Structure

| Part | Cells | Description |
|------|-------|-------------|
| 1 - Setup | 1-6 | Imports, data loading, cleaning, feature engineering |
| 2 - Historical EDA | 7-10 | Attack/defense scatter plots, xPTS overperformance heatmap, xG trends |
| 3 - Poisson Model | 11-14 | Distribution explainer, current strength ratings, rivalry simulations |
| 4 - Monte Carlo | 15-21 | Schedule parsing, simulation engine, finish probability tables and heatmaps |

---

## Key Outputs

- Attack vs defense rating scatter plots colored by points tally (2021/22 - 2025/26)
- xPTS overperformance heatmap identifying which clubs consistently beat or miss their expected points
- Poisson distribution explainer built from real xG quantiles across both leagues
- Monte Carlo finish probability heatmap per league - title, Champions League, Europa League, Conference League, and relegation
- Race summary with per-category probabilities for every meaningful finishing threshold

---

## Data Sources

- xG and xGA data: [Understat](https://understat.com)
- 2025/26 fixture schedule: [FBref](https://fbref.com)

No proprietary data used.

---

## Requirements

```bash
pip install jupyter pandas numpy scipy seaborn matplotlib scikit-learn aiohttp nest_asyncio
```

---

## Author

Created by Isaiah Woram

Feel free to reach out at idw2005@nyu.edu
