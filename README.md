# Hyderabad Air Quality – mlfs-book

This project adapts the MLFS air-quality workflow to **Hyderabad, India**, covering **12 WAQI sensors** (see `data/hyderabad_sensors_pipeline.csv`). Each sensor has its own feature group, feature view, and XGBoost model so we can monitor individual neighborhoods independently.

---

## Tools & Components

- Python/Jupyter notebooks (`notebooks/airquality/...`)
- Hopsworks Feature Store & Model Registry
- XGBoost for per-sensor PM2.5 forecasting
- GitHub Actions for daily automation
- GitHub Pages (`docs/air-quality/...`) for dashboards

---

## How to Run

1. **Setup**
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt

## Notebook Summaries

- `1_air_quality_feature_backfill.ipynb`: Ingest historical PM2.5 + weather data for each sensor into Hopsworks.
- `2_air_quality_feature_pipeline.ipynb`: Daily job that fetches new PM2.5 readings plus the shared weather forecast and appends them to the feature store.
- `3_air_quality_training_pipeline.ipynb`: Trains/updates each sensor’s XGBoost model and registers it in Hopsworks.
- `4_air_quality_batch_inference.ipynb`: Runs daily batch inference + monitoring; updates the `aq_predictions` feature group and refreshes forecast/hindcast PNGs under `docs/`.

## Dashboard

Latest Hyderabad forecasts & hindcasts: **https://lakshmisrinidhp.github.io/mlfs-book/**
