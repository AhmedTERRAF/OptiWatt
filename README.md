# OptiWatt

# Household Energy Consumption Anomaly Detection

This project focuses on preprocessing and modeling household electricity consumption data using LSTM Autoencoders to detect anomalies in appliance-specific energy usage.

## Dataset

The dataset used is derived from the **Individual household electric power consumption** dataset, which contains measurements of electric power consumption in one household with a one-minute sampling rate over several years.

**Dataset License:**  
This dataset is shared under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license.
Here is the Link for the dataset: (https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption)

**Attribution:**  
> Individual household electric power consumption dataset licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The dataset may have been modified for processing purposes.  

---

## Project Workflow

This repository contains:

- `household_power_consumption.csv` — The dataset file  
- `notebook.ipynb` — Python notebook containing all data processing, modeling, and result generation steps  
- `saved_models/` — Folder where trained models are saved  
- `saved_scalers/` — Folder where normalization scalers are saved  

---

## Notebook Contents Explained

The notebook follows these steps:

### 1. **Data Loading and Cleaning**
- Load dataset with `pandas`
- Combine `Date` and `Time` columns into a single datetime field
- Convert relevant columns to numeric types
- Handle missing values using linear interpolation

### 2. **Exploratory Data Analysis**
- Compute and visualize the correlation matrix using `seaborn`
- Drop redundant columns (e.g., `Global_intensity`)

### 3. **Feature Engineering**
- Convert energy readings from Wh to kWh
- Calculate estimated CO₂ emissions based on an emission factor for electricity in France
- Structure the dataset separately for each submeter (`Sub_metering_1`, `Sub_metering_2`, `Sub_metering_3`)

### 4. **Data Normalization**
- Apply MinMax normalization independently to each submeter's dataset
- Store normalization scalers for future inverse transformations

### 5. **Sequence Generation**
- Create rolling window sequences (length = 60 timesteps) for time-series modeling per submeter

### 6. **Data Splitting**
- Chronological train-test split (80% train, 20% test) for each submeter

### 7. **Model Building: LSTM Autoencoder**
- Build and compile a simple LSTM Autoencoder for each submeter's data
- Train the model to learn patterns in normal consumption behavior

### 8. **Model Saving**
- Save trained Autoencoder models in `saved_models/`
- Save corresponding normalization scalers in `saved_scalers/`

---

## Requirements

You can install dependencies using:

```bash
pip install -r requirements.txt
