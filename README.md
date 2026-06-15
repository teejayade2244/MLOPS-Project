# MLOPS-Project

A complete end-to-end machine learning pipeline for wine quality prediction built with Python. This project demonstrates data ingestion, validation, transformation, model training, and evaluation with MLflow integration.

## 🚀 Quick Start

### Prerequisites
- Python 3.7+

### Installation

```bash
# Clone the repository
git clone https://github.com/teejayade2244/MLOPS-Project.git
cd MLOPS-Project

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Running the Pipeline

```bash
# Execute the complete ML pipeline
python main.py

# Start the Flask web app for predictions
python app.py
```

Once the Flask app is running, open your browser and navigate to `http://127.0.0.1:8080` to access the UI.

## 📋 Overview

This project implements a complete MLOps workflow for predicting wine quality. The pipeline automatically:

- ✅ Downloads and extracts wine quality dataset
- ✅ Validates data against a predefined schema
- ✅ Transforms and splits data for training
- ✅ Trains an ElasticNet regression model
- ✅ Evaluates performance metrics (RMSE, MAE, R²)
- ✅ Logs results with MLflow
- ✅ Serves predictions via Flask UI

## 📁 Project Structure

```
.
├── main.py                      # Pipeline orchestrator
├── app.py                       # Flask web application
├── config/
│   └── config.yaml             # Pipeline configuration
├── params.yaml                 # Model hyperparameters
├── schema.yaml                 # Data schema definition
├── src/
│   └── datascience/           # Pipeline stages and utilities
├── artifacts/                  # Generated outputs
│   ├── data_ingestion/        # Raw downloaded data
│   ├── data_validation/       # Validation results
│   ├── data_transformation/   # Train/test splits
│   ├── model_trainer/         # Trained model
│   └── model_evaluation/      # Performance metrics
└── requirements.txt            # Python dependencies
```

## 🔄 Pipeline Stages

### 1. Data Ingestion
- Downloads `winequality-data.zip` from a configured GitHub source
- Extracts `winequality-red.csv` to `artifacts/data_ingestion/`

### 2. Data Validation
- Validates dataset structure against `schema.yaml`
- Ensures all required columns and data types are correct
- Outputs validation status to `artifacts/data_validation/status.txt`

### 3. Data Transformation
- Performs train/test split on validated data
- Saves `train.csv` and `test.csv` to `artifacts/data_transformation/`

### 4. Model Training
- Trains ElasticNet regression model
- Uses hyperparameters from `params.yaml` (alpha, l1_ratio)
- Saves trained model to `artifacts/model_trainer/model.joblib`

### 5. Model Evaluation
- Evaluates model on test set
- Computes metrics: RMSE, MAE, R²
- Logs results via MLflow and saves to `artifacts/model_evaluation/metrics.json`

## ⚙️ Configuration

### config/config.yaml
Defines pipeline artifact directories, data source URL, and file paths.

### params.yaml
Model hyperparameters for ElasticNet:
```yaml
alpha: 0.1
l1_ratio: 0.5
```

### schema.yaml
Expected data schema and target column specification.

## 🔗 MLflow Integration

The pipeline includes built-in MLflow support for experiment tracking and model logging.

### Local Setup (Default)
Metrics are automatically logged to `artifacts/model_evaluation/metrics.json`.

### Remote Backend (DagsHub / Other)
Set environment variables before running the pipeline:

```bash
# Windows PowerShell
$env:MLFLOW_TRACKING_URI="https://dagshub.com/<owner>/<repo>.mlflow"
$env:MLFLOW_TRACKING_USERNAME="<username>"
$env:MLFLOW_TRACKING_PASSWORD="<token>"

# Linux/macOS
export MLFLOW_TRACKING_URI="https://dagshub.com/<owner>/<repo>.mlflow"
export MLFLOW_TRACKING_USERNAME="<username>"
export MLFLOW_TRACKING_PASSWORD="<token>"
```

Then run the pipeline:
```bash
python main.py
```

## 📦 Dependencies

Key packages (see `requirements.txt` for complete list):

- **pandas** — Data manipulation
- **numpy** — Numerical computing
- **scikit-learn** — Machine learning models and evaluation
- **mlflow** — Experiment tracking and model registry
- **Flask** — Web framework for UI
- **pyyaml** — YAML configuration parsing
- **joblib** — Model serialization
- **python-box** — Configuration objects

## 🌐 Web Interface

The Flask app provides a simple UI for:
- Training the model
- Making individual wine quality predictions

Start the app and visit `http://127.0.0.1:8080` to interact with it.

## 📊 Output Artifacts

After running `python main.py`, the following artifacts are generated:

- `artifacts/data_ingestion/winequality-red.csv` — Raw dataset
- `artifacts/data_validation/status.txt` — Validation report
- `artifacts/data_transformation/train.csv` — Training set
- `artifacts/data_transformation/test.csv` — Test set
- `artifacts/model_trainer/model.joblib` — Trained ElasticNet model
- `artifacts/model_evaluation/metrics.json` — Performance metrics

## 📝 Notes

- Currently implements a single **ElasticNet regression** model for wine quality
- Flask app is a lightweight UI wrapper around the prediction pipeline
- No advanced deployment or CI/CD configuration is included yet
- Designed as an educational MLOps project demonstrating best practices


**Getting Started?** Run `python main.py` to execute the full pipeline, or `python app.py` to start the web interface.
