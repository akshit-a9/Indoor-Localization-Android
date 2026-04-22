# Notebooks

Jupyter notebooks that drive the offline pipeline: from raw scans to trained
models, ONNX exports, and evaluation against live walk tests.

## Layout

```
Notebooks/
└── Wifi/   WiFi-fingerprint pipeline (preprocessing → training → export → testing)
```

Other modalities (e.g. BLE, IMU) would live alongside `Wifi/` as sibling
folders if added.

## Running

A virtualenv at the repo root (`.venv/`) is expected. Install dependencies with:

```bash
pip install -r ../localization_api/requirements.txt
```

Then open the notebooks in order — see [Wifi/README.md](Wifi/README.md) for the
pipeline details.
