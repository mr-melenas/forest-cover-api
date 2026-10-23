<h1 align="center">🌲 ForestVision — Forest Cover Type Classification API</h1>

<p align="center">
  Multiclass ML model served as a REST API and an interactive dashboard that predicts<br/>
  which of 7 forest cover types grows on a piece of land from its cartographic features.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white" />
  <img src="https://img.shields.io/badge/Plotly_Dash-3F4F75?logo=plotly&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?logo=supabase&logoColor=white" />
  <img src="https://img.shields.io/badge/Render-46E3B7?logo=render&logoColor=black" />
</p>

<p align="center">
  🌐 <a href="https://g5-ai-regresion-multiclase.onrender.com/"><b>Live dashboard</b></a> ·
  ⚡ <a href="https://forestvision.onrender.com/docs"><b>Live API (Swagger)</b></a>
</p>

> ⏳ Hosted on Render's free tier: the first request may take ~1 minute while the service wakes up.

---

## 🎯 The problem

Mapping forest cover over large areas with field surveys is slow and expensive. Using the [UCI Covertype dataset](https://archive.ics.uci.edu/dataset/31/covertype) (≈581k samples of 30×30 m cells in Colorado, 54 features: elevation, slope, distances to water/roads/fire points, hillshade, wilderness area and soil type), the model predicts the dominant tree cover type from data that is cheap to obtain.

## ✨ Features

- **End-to-end ML**: EDA → model comparison (from Logistic Regression to Random Forest) → class rebalancing with SMOTE → tuned Random Forest pipeline (200 trees)
- **REST API with FastAPI**: `/predict` for one sample, `/predict/batch` for many, `/info` for model metadata, validated with Pydantic schemas
- **Interactive dashboard** in Plotly Dash with input forms, charts and result tables
- **Every prediction stored** in Supabase (PostgreSQL)
- **Dockerised** and **deployed on Render**
- **Tests** for the API

## 🏗️ Architecture

```mermaid
flowchart LR
    U[User] --> D[Dash dashboard]
    U --> S[Swagger / API clients]
    D --> API[FastAPI]
    S --> API
    API --> M[Random Forest pipeline<br/>preprocessing + model]
    API --> DB[(Supabase)]
```

<p align="center"><img width="600" alt="Architecture diagram" src="https://github.com/user-attachments/assets/badc90b8-8794-410a-94db-98fe6045d9e3" /></p>

## 👤 My role

Team project of 4 at the Factoría F5 AI Bootcamp. **I created the repository and was the main contributor**:

- Project setup, EDA base and data encoding
- **FastAPI** service: model loading, prediction endpoints and schemas
- Model training script and final pipeline
- **Supabase** integration to save every prediction
- **Docker** setup and **deployment on Render**, including working around the model file size limits of the free tier
- API tests

## 🚀 Run it locally

```bash
git clone https://github.com/mr-melenas/forest-cover-api.git
cd forest-cover-api

# Option A — Docker
docker compose up --build

# Option B — manual
pip install -r requirements.txt
uvicorn main:app --reload          # API → http://localhost:8000/docs
python frontend/app_dash.py        # Dashboard
```

Environment variables: `SUPABASE_URL`, `SUPABASE_KEY`.

### Example request

```bash
curl -X POST https://forestvision.onrender.com/predict \
  -H "Content-Type: application/json" \
  -d '{"Elevation": 2596, "Aspect": 51, "Slope": 3, "Horizontal_Distance_To_Hydrology": 258, "...": "..."}'
```

## 👥 Team

Built at [Factoría F5](https://factoriaf5.org/) by [@mr-melenas](https://github.com/mr-melenas) (Max Beltrán), Andreina Suescum, Alejandro Rajado Martín and Orlando Alcalá ([@odar1997](https://github.com/odar1997)).
