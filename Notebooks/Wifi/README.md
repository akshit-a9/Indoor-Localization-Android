# Notebooks / Wifi

End-to-end WiFi-fingerprint pipeline. The notebooks are numbered and intended
to be run in order; each one consumes the artifacts produced by the previous
step.

## Pipeline

| # | Notebook | Inputs | Outputs |
|---|----------|--------|---------|
| 01 | [01_Data_Preprocessing.ipynb](01_Data_Preprocessing.ipynb) | `Data/01_Wifi_Daytime/*.csv` | `Data/02_Processed_Wifi_Daytime/fingerprints.csv`, EDA plots |
| 02 | [02_Feature_Extraction.ipynb](02_Feature_Extraction.ipynb) | `fingerprints.csv` | `splits/` (train/val/test arrays, scaler, label map, feature BSSIDs) |
| 03 | [03_Model_Training.ipynb](03_Model_Training.ipynb) | `splits/` | `models/*.joblib`, `models_registry.json`, evaluation plots |
| 04 | [04_Export_ONNX.ipynb](04_Export_ONNX.ipynb) | `models/*.joblib` | `models/*.onnx` |
| 05 | [05_Testing_Statistics.ipynb](05_Testing_Statistics.ipynb) | `Data/04_Testing/walk_test_*.csv`, `Data/03_Map_Data/` | `Data/04_Testing/figures/` |

## Notes

- Notebook 01 controls AP-coverage filtering. Adjusting the threshold changes
  the `feature_bssids.json` produced by notebook 02, which in turn invalidates
  every downstream artifact (models, ONNX exports, the API and the Flutter app
  assets) — always rerun the full chain after touching it.
- Notebook 03 writes `models_registry.json`; this is the file the FastAPI server
  reads at startup to discover available models.
- Notebook 04's ONNX outputs are copied into
  [`Demo_Flutter/assets/models/`](../../Demo_Flutter/assets/models/) for
  on-device inference.
- Notebook 05 is the only notebook that depends on field data
  (`Data/04_Testing/`); the first four can be rerun without leaving the desk.
