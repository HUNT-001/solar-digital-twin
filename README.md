# ?? Yulara Solar Digital Twin

[![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-REST%20API-lightgrey?logo=flask)](https://flask.palletsprojects.com)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react)](https://reactjs.org)
[![AWS](https://img.shields.io/badge/AWS-Elastic%20Beanstalk-FF9900?logo=amazonaws)](https://aws.amazon.com/elasticbeanstalk/)
[![Netlify](https://img.shields.io/badge/Netlify-Deployed-00C7B7?logo=netlify)](https://netlify.com)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

A **cloud-based digital twin platform** for the **Yulara Solar Farm (Northern Territory, Australia)**.

This system integrates **machine learning forecasting, electricity price prediction, anomaly detection, and a 3D simulation dashboard** into a full-stack cloud architecture.

The platform demonstrates how **AI + cloud infrastructure can optimize renewable energy operations**, providing real-time insights and predictive analytics for solar farm performance.

---

# ?? Live Deployment

| Service | URL |
|------|------|
| Frontend (Netlify) | https://musical-tapioca-408587.netlify.app |
| Backend API (AWS Elastic Beanstalk) | http://yulara-backend-env.eba-mt7aim3j.us-east-1.elasticbeanstalk.com/api/stats |

---

# ??? System Architecture

            DATA INGESTION

AEMO NEM CSV + Solar Farm + Weather Data
¦
?
DATA PIPELINE
preprocess.py ? feature engineering
? yulara_master.csv
¦
?
ML TRAINING
train_models.py
+-- Prophet ? power forecasting
+-- XGBoost ? electricity price prediction
+-- Isolation Forest ? anomaly detection
¦
?
BACKEND (Flask REST API)
AWS Elastic Beanstalk
+-- /api/stats
+-- /api/alerts
+-- /api/forecast/prophet
+-- /api/forecast/price
+-- /api/anomalies
+-- /api/historical
+-- /api/simulation/3d
+-- /api/predict/revenue
¦
HTTP / JSON
¦
?
FRONTEND (React)
Netlify Cloud Deployment
+-- Power Forecast Dashboard
+-- Price Forecast Dashboard
+-- Anomaly Detection Panel
+-- 3D Solar Farm Simulation
+-- Revenue Prediction Tool


---

# ?? Repository Structure


solar-digital-twin
¦
+-- app.py
¦ Flask REST API serving all /api/* endpoints
¦
+-- preprocess.py
¦ Data preprocessing and feature engineering pipeline
¦
+-- train_models.py
¦ Trains ML models and saves artifacts in models/
¦
+-- download_price_data.py
¦ Downloads electricity price data from AEMO
¦
+-- image_gen.py
¦ Generates model evaluation plots
¦
+-- requirements.txt
¦ Python dependencies
¦
+-- models/
¦ Serialized ML model artifacts
¦ +-- best_power_model.pkl
¦ +-- best_price_model.pkl
¦ +-- isolation_forest_model.pkl
¦ +-- anomaly_scaler.pkl
¦ +-- power_metrics.json
¦ +-- price_metrics.json
¦ +-- anomaly_metrics.json
¦ +-- revenue_config.json
¦ +-- training_summary.json
¦
+-- yulara-frontend/
React application
¦
+-- src/
¦ +-- api/
¦ ¦ +-- index.js
¦ ¦
¦ +-- components/
¦ ¦
¦ +-- App.jsx
¦
+-- public/
¦ +-- _redirects
¦
+-- package.json


---

# ?? Machine Learning Model Performance

| Model | Task | R² Score | Accuracy | MAE |
|-----|------|------|------|------|
| Prophet | Solar Power Forecast | **0.9905** | **99.05%** | 24.33 kW |
| XGBoost | Electricity Price Prediction | **0.8986** | **89.86%** | 14.73 $/MWh |
| Isolation Forest | Anomaly Detection | **0.97** | **97%** | ~3% anomaly rate |

---

# ?? Local Setup

## Prerequisites

- Python 3.10+
- Node.js 18+
- pip

---

## Clone Repository

`ash
git clone https://github.com/HUNT-001/solar-digital-twin.git
cd solar-digital-twin
Backend Setup
pip install -r requirements.txt
python preprocess.py
python train_models.py
python app.py

API runs at:

http://localhost:5000
Frontend Setup
cd yulara-frontend
npm install
npm start

Frontend runs at:

http://localhost:3000
?? API Reference
MethodEndpointDescriptionExample Payload
GET/api/statsSolar farm statistics—
GET/api/alertsActive anomaly alerts—
POST/api/forecast/prophetSolar power forecast{ "hours": 24 }
POST/api/forecast/priceElectricity price forecast{ "hours": 24 }
POST/api/anomaliesRetrieve anomaly records{ "n_records": 100 }
POST/api/historicalHistorical power data{ "hours": 168 }
POST/api/simulation/3dData for 3D solar simulation{ "hours": 24 }
POST/api/predict/revenueRevenue prediction{ "power_kw": 500 }
?? Cloud Deployment
Backend — AWS Elastic Beanstalk
zip -r yulara-deploy.zip app.py requirements.txt models/
eb deploy
Frontend — Netlify
cd yulara-frontend
npm run build

Upload the build/ folder to Netlify.

?? Dataset Sources
DatasetSourceDescription
Solar GenerationDesert Gardens Solar Farm15-minute power generation data
Weather DataBureau of MeteorologyTemperature, irradiance, humidity
Electricity PriceAEMO NEM5-minute settlement prices

Raw datasets are not included due to size (~400MB).

?? Technology Stack
LayerTechnology
FrontendReact, Plotly.js, Three.js
BackendPython, Flask
ML ForecastingProphet
ML Price PredictionXGBoost
ML Anomaly DetectionIsolation Forest
CloudAWS Elastic Beanstalk
HostingNetlify
Data ProcessingPandas, NumPy
?? License

MIT License

?? Project Context

This project demonstrates a cloud-based digital twin architecture for renewable energy infrastructure, integrating:

• Machine learning forecasting
• anomaly detection
• real-time APIs
• interactive visualization
• scalable cloud deployment

