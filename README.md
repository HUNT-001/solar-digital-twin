# Yulara Solar Digital Twin

A cloud-based digital twin for the **Yulara Solar Farm (NT, Australia)**.
Integrates real-time solar power forecasting, electricity price prediction,
and anomaly detection through a React dashboard backed by a Flask REST API
deployed on AWS Elastic Beanstalk.

## Live Demo
- **Frontend**: https://musical-tapioca-408587.netlify.app
- **Backend API**: http://yulara-backend-env.eba-mt7aim3j.us-east-1.elasticbeanstalk.com/api/stats

## Architecture
- Frontend  : React.js + Plotly.js + Three.js  deployed on Netlify
- Backend   : Flask REST API                   deployed on AWS Elastic Beanstalk (EC2)
- ML Models : Prophet, XGBoost, Isolation Forest
- Data      : AEMO NEM price data + Desert Gardens solar + weather data

## Repository Structure
| File/Folder | Description |
|---|---|
| app.py | Flask REST API - all /api/* endpoints |
| preprocess.py | Raw CSV data cleaning and feature engineering |
| train_models.py | Trains Prophet (power), XGBoost (price), IsoForest (anomaly) |
| download_price_data.py | Downloads NEM electricity price data from AEMO |
| image_gen.py | Generates 12 ML evaluation plots (matplotlib) |
| models/ | Saved trained model .pkl and metrics .json files |
| yulara-frontend/ | React frontend application |

## Model Performance
| Model | Task | R2 Score | Accuracy |
|---|---|---|---|
| Prophet | Solar Power Forecast | 0.9905 | 99.05% |
| XGBoost | Electricity Price Forecast | 0.8986 | 89.86% |
| Isolation Forest | Anomaly Detection | 0.9700 | 97.00% |

## Setup

### Backend
pip install -r requirements.txt
python preprocess.py
python train_models.py
python app.py

### Frontend
cd yulara-frontend
npm install
npm start
