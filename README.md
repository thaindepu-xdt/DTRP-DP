# DTRP-DP: Demand Prediction and Optimization Routing

## Project Introduction
The **DTRP-DP** project focuses on solving smart transportation problems, specifically demand forecasting (Demand Prediction) and route optimization (Routing Optimization) for taxi or ride-hailing services. By using historical taxi trip data (specifically NYC Taxi 2016 data), the system aims to reduce waiting times, increase operational efficiency, and optimize profits for the fleet.

The project is divided into two main phases:
1. **Phase 1: Demand Prediction** - Analyzing historical data to forecast the number of ride requests in different areas and time periods.
2. **Phase 2: Optimization Routing** - Using forecasting results to plan vehicle movement and dispatching in the most optimal way (Static & Dynamic Routing).

---

## Main Components

The project is organized into two separate functional directories:

### 1. DemandPrediction
This directory is responsible for processing raw data and building forecasting models.
- **Input/**: Contains input data files (`train.csv`, `test.csv`) including GPS information, trip start/end times, passenger count, etc.
- **source_code/**: 
  - `PHASE_1_Static&Dynamic_routing_V1.ipynb`: A notebook that performs Data Cleaning (filtering faulty GPS coordinates, filtering invalid trip times), EDA (Exploratory Data Analysis), and development of initial forecasting models.

### 2. Routing
This directory implements dispatching algorithms based on results from the prediction phase.
- **Input/**: Contains intermediate results such as forecasts from XGBoost and LSTM models, clustering data, and daily data snapshots.
- **source_code/**:
  - `dynamic_routing_ver1.ipynb`: Version 1 of the dynamic routing dispatching algorithm.
  - `dynamic_routing_ver2.ipynb`: An updated version, more optimized for real-time vehicle and customer assignment.

---

## Installation and Execution

Follow these steps to set up the environment and run the project locally after cloning.

### 1. Prerequisites
- **Python**: 3.8 or higher
- **Git**: Installed on your system

### 2. Set Up Environment
It is recommended to use a virtual environment to manage dependencies:

```bash
# Create a virtual environment
python -m venv venv

# Activate the environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Data Structure (Manual Setup)
Since raw data and intermediate results are not included in the repository, you must manually place them in the correct directories:

#### **Demand Prediction Inputs**
Place NYC taxi trip data in `DemandPrediction/Input/`:
- `train.csv` (Raw training data)
- `test.csv` (Raw test data)

#### **Routing Optimization Inputs**
Place generated results and model files in `Routing/Input/`:
- `last_month_daily/last_month_daily_eff_3/requests_{date}.csv`
- `clusters/n20_init20/centroids_k20_n20.csv`
- `BASELINES/xgboost/xgboost_next15min_predictions.csv`

### 4. Running the Notebooks
You can run the notebooks using Jupyter Lab/Notebook or inside VS Code.

1.  **Phase 1: Demand Prediction**
    *   Open `DemandPrediction/source_code/PHASE_1_Static&Dynamic_routing_V1.ipynb`.
    *   Run all cells to perform data cleaning and generate prediction outputs.
2.  **Phase 2: Routing Optimization**
    *   Open `Routing/source_code/dynamic_routing_ver1.ipynb` (Basic) or `dynamic_routing_ver2.ipynb` (Optimized).
    *   These notebooks will read from `Routing/Input` and save results to `Routing/Output`.

---

## Data Processing Workflow
1. **Cleaning**: Remove GPS points outside the NYC area, filter trips with unrealistic speeds or durations.
2. **Clustering**: Group pickup points to identify high-demand areas.
3. **Forecasting**: Use XGBoost or LSTM (found in `Input/LSTM`) to forecast demand for the next 15-30 minutes.
4. **Dispatching**: The dispatching algorithm assigns the nearest empty vehicles to high-demand areas or directly to customers to minimize empty vehicle mileage (Empty distance).

---

## Detailed Directory Structure
```text
DTRP-DP/
│
├── DemandPrediction/           # Demand prediction phase
│   ├── Input/                  # Raw train/test data
│   ├── Output/                 # Results after model forecasting
│   └── source_code/            # Data processing and model code
│
├── Routing/                    # Routing optimization phase
│   ├── Input/                  # Forecasts from XGBoost, LSTM, Cluster data
│   ├── Output/                 # Dispatching results, route logs
│   └── source_code/            # Dynamic Routing algorithms (V1, V2)
│
└── README.md                   # Project documentation
```
