# MLB MVP Prediction Engine ⚾

## Project Objective

This project leverages machine learning to predict the winners of Major League Baseball's Most Valuable Player (MVP) award for both the American and National Leagues. By analyzing over two decades of comprehensive player statistics, the model identifies key performance indicators and generates a probability-based "MVP Ladder" to rank the top candidates for the current season.

-----

## 🚀 Key Features

  - **Automated Data Pipeline:** Programmatically scrapes and consolidates 25 seasons (2000-2025) of advanced batting and pitching data from FanGraphs using `pybaseball`.
  - **Hybrid Feature Engineering:** Employs a robust feature selection process that combines domain knowledge with automated, model-based importance ranking to identify the most predictive stats.
  - **Advanced Machine Learning:** Utilizes a tuned **XGBoost** classifier to handle the severe class imbalance inherent in predicting a rare award.
  - **Live Prediction Ladder:** Generates a real-time, probability-based ranking of the top MVP candidates for the current season.

-----

## ⚙️ Project Workflow

The project is structured into three distinct Jupyter notebooks:

1.  **`01-data_collection.ipynb`:** Fetches comprehensive batting and pitching statistics for every player from 2000 to the current season, saving the raw data to CSV files.
2.  **`02-data_cleaning.ipynb`:** Implements a "select first, merge second" strategy. It selects a wide range of potentially valuable features, merges the batting and pitching data, consolidates shared columns (like Name, Age, and WAR), and assigns the correct league to each player.
3.  **`03-modeling.ipynb`:**
      - **Feature Selection:** An initial Random Forest model is trained to identify the top 20 most impactful features from the wider set.
      - **Model Training:** An **XGBoost** model is trained on the curated feature set, using `scale_pos_weight` to effectively manage the class imbalance.
      - **Evaluation:** The model is evaluated on a time-series test set (seasons 2021-2024), demonstrating strong predictive power.
      - **Prediction:** The trained model is used to generate a ranked MVP probability ladder for the current (2025) season.

-----

## 🛠️ Technologies & Libraries

  - **Python 3**
  - **Core Libraries:**
      - `pybaseball`: For MLB data scraping.
      - `pandas`: For data manipulation and cleaning.
      - `scikit-learn`: For feature selection and model evaluation.
      - `XGBoost`: For the final classification model.
      - `imbalanced-learn`: For handling class imbalance during experimentation.

-----

## 📊 Results & Performance

The final XGBoost model demonstrated a strong ability to identify MVP winners while maintaining high precision. When evaluated on the 2021-2024 seasons for the American League, the model achieved:

  - **Recall (True):** 0.75 (Found 3 out of 4 actual MVPs)
  - **Precision (True):** 0.60 (Correct 60% of the time it predicted an MVP)

#### AL Test Set Confusion Matrix:

```
[[2593    2]  <- Correctly identified 2593 non-MVPs, had 2 false alarms.
 [   1    3]]  <- Missed 1 MVP, correctly identified 3 MVPs.
```

-----

## 🏆 2025 MVP Ladder (Live Projections)

*Live projections based on player performance as of September 25, 2025.*

### American League MVP Ladder

| Name | Team | WAR | wRC+ | OPS | MVP Probability |
|:---|:---|---:|---:|---:|---:|
| **Aaron Judge** | NYY | 9.2 | 199 | 1.121 | 0.856362 |
| **Cal Raleigh** | SEA | 8.8 | 160 | 0.945 | 0.645216 |
| **Byron Buxton** | MIN | 4.7 | 133 | 0.863 | 0.011242 |
| **Tarik Skubal** | DET | 6.6 | 0 | 0.000 | 0.000752 |
| **Bobby Witt Jr.**| KCR | 7.8 | 130 | 0.853 | 0.000321 |

### National League MVP Ladder

| Name | Team | WAR | wRC+ | OPS | MVP Probability |
|:---|:---|---:|---:|---:|---:|
| **Shohei Ohtani** | LAD | 7.2 | 171 | 1.011 | 0.998334 |
| **Corbin Carroll** | ARI | 6.4 | 139 | 0.886 | 0.091812 |
| **Kyle Schwarber** | PHI | 4.8 | 152 | 0.929 | 0.000514 |
| **Juan Soto** | NYM | 5.8 | 158 | 0.932 | 0.000476 |
| **James Wood** | WSN | 3.1 | 125 | 0.816 | 0.000385 |

-----

## 🚀 How to Use

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/mlb-mvp-predictor.git
    cd mlb-mvp-predictor
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run the notebooks in order:**
      - `01-data_collection.ipynb`
      - `02-data_cleaning.ipynb`
      - `03-modeling.ipynb`