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

## How to Run the Code

### 1. System Requirements
- **Language**: Python 3.x
- **Tools**: Jupyter Notebook or Google Colab (The project supports running on Colab with Drive mounting features).
- **Key Libraries**: 
  - Data Processing: `pandas`, `numpy`, `scipy`
  - Visualization: `matplotlib`, `seaborn`
  - Machine Learning: `xgboost`, `scikit-learn` (optional for baselines)

### 2. Clone the Project
```bash
git clone https://github.com/thaindepu-xdt/DTRP-DP.git
cd DTRP-DP
```

### 3. Data Structure
Ensure you have loaded the taxi trip data into the `DemandPrediction/Input/` directory. Required files:
- `train.csv`
- `test.csv`

### 4. Execution
1. **Demand Prediction**: Open and run the notebook in `DemandPrediction/source_code/` to perform data cleaning and generate prediction files.
2. **Routing Optimization**: Use the prediction result files to run the notebooks in `Routing/source_code/`.

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
