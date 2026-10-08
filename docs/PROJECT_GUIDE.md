# RoadTrace — reviewer guide

## Quick demonstration

1. Open [the browser demo](https://roadtrace-analytics.netlify.app/) on a phone, allow camera access from a safe and stationary position, or choose a prerecorded video.
2. See vehicle boxes, classifications and approximate speed estimates where usable.
3. Explore the separate [hosted Streamlit dashboard](https://roadtrace-analytics-d.streamlit.app/).
4. Check the [recorded validation](VALIDATION.md), [calibration guidance](usage.md), [browser setup](../web/README.md), and [original sample](../demo/README.md).

## Source structure

- `web/` — browser runtime, automatic approximate speed estimation, lightweight tracker, context and tests.
- `core/` — packaged Python detection, ByteTrack and explicit road calibration.
- `dashboard/` — Streamlit analysis, export, and multi-recording aggregation.
- `data_layers/` — public road-safety and weather adapters.
- Root-level Python files and `demo/` — original video pipeline and saved output, preserved.

## Reported reproducible example

| Observation | Value |
| --- | ---: |
| Sample duration | 8 seconds |
| Frames processed | 200 |
| Software track IDs | 14 |
| Trajectory observations | 803 |
| Numeric speed observations | 461 |
| Tracks contributing speed summary | 6 |
| Python core tests reported as passing | 24 |

Source: [docs/VALIDATION.md](VALIDATION.md). These values are not independently measured counts or radar-verified speeds.

## Running locally

For the existing sample:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python run_sample.py
python -m unittest -v test_pipeline.py
```

For the extended dashboard, preferably in a separate environment due to differences in OpenCV builds:

```bash
pip install -r requirements-analytics.txt
streamlit run dashboard/app.py
```

For static web execution, the ONNX model is *not* included. Follow [web/README.md](../web/README.md) to export `web/models/yolo11n.onnx` and serve `web/` over HTTP(S).

## Limits and source notice

Real-world counts and speeds require independent reference measurements. Perspective, camera motion, occlusion, lighting, and frame timing all matter. Optional location context is queried from third-party public services. The hosted Streamlit route handles uploads on a server unlike the local-browser camera path.

This migration substitutes a vector web icon because binary PWA icons could not be transferred through the GitHub connection. Production raster icons should be regenerated before release. See [ATTRIBUTION.md](../ATTRIBUTION.md) for the source and licensing notice.
