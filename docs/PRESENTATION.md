# RoadTrace Analytics — 7-slide visual project overview

**[Try the live browser app](https://roadtrace-analytics.netlify.app/)** · **[Open the Streamlit dashboard](https://roadtrace-analytics-d.streamlit.app/)** · [Project setup](PROJECT_GUIDE.md) · [Validation record](VALIDATION.md) · [Source code](https://github.com/GauravKudeshia/RoadTrace)

This page accompanies the editable seven-slide presentation and makes its key claims accessible to anyone viewing the repository, even without PowerPoint. The PPTX file is **not yet hosted in this repository**; this page will link to it once uploaded.

## 01 — What if traffic observation started with a phone?

RoadTrace is a working prototype for detecting and tracking road vehicles and producing approximate speed observations with a browser. The viewer can test the live camera or use an existing video.

## 02 — A practical research question

Can accessible, consumer-device traffic observation support preliminary traffic studies without dedicated roadside equipment? It is **not** claimed to be as accurate as surveyed measurements or certified enforcement systems.

## 03 — One project, two workflows

| Browser live camera | Python and Streamlit |
| --- | --- |
| On-device browser inference | Python video processing |
| Lightweight JS track association | ByteTrack in the Python core |
| Automatic approximate speed scaling with scene cues and fallbacks | Explicit calibrated road-plane speed estimates |
| Real-time browser overlays | CSV, charts, annotated video and aggregated reports |

These workflows have different tracking and calibration methods. The browser app is not a direct field-accuracy benchmark of the Python pipeline.

## 04 — Real-world examples

Three mobile camera screenshots from real street scenes were provided for the presentation. They show orange boxes, classes such as car and truck, and example approximate speed labels. They demonstrate **interface operation**, not radar-verified speed readings or independently checked vehicle counts.

## 05 — Engineering work

Key implemented areas include vehicle track continuity, automatic scale estimation, perspective considerations, interrupted tracks, and reporting when estimates are uncertain. See [web/src/tracker.js](../web/src/tracker.js), [web/src/calibration.js](../web/src/calibration.js), [web/src/speed.js](../web/src/speed.js), and [core/speed_estimator.py](../core/speed_estimator.py).

## 06 — The documented sample, in numbers

| Metric | Recorded result |
| --- | ---: |
| Core Python tests recorded as passing | **24** |
| Video duration | **8 seconds** |
| Frames processed | **200** |
| Distinct software track IDs | **14** |
| Trajectory observations | **803** |
| Numerical speed observations | **461** |
| Tracks with valid per-track speed statistics | **6** |

Source: [docs/VALIDATION.md](VALIDATION.md), dated October 1, 2026. **These are software results**, not verified physical vehicle counts or speed accuracy.

## 07 — What should be researched next?

Collect reference video with manual ground-truth counts and independently measured speeds. Compare errors by road position, camera motion, lighting, and occlusion. Benchmark the browser and explicitly calibrated Python paths separately.

---

### How to run it

- **Online:** [live browser](https://roadtrace-analytics.netlify.app/) or [hosted analysis dashboard](https://roadtrace-analytics-d.streamlit.app/).
- **Original local demo:** `python run_sample.py` from the repository root.
- **Extended Streamlit path:** `pip install -r requirements-analytics.txt` then `streamlit run dashboard/app.py`.
- **Browser locally:** follow [web/README.md](../web/README.md); the model binary must be exported.

### Accuracy and data-handling note

The browser processes camera imagery on the device, but optional public-data lookups may send location information to external services. The hosted Streamlit path processes uploaded video remotely. Some sources provide country-level or county-level context rather than road-specific observations.

### Attribution

RoadTrace integrates existing pretrained detection/tracking methods and prior project work. Read [ATTRIBUTION.md](../ATTRIBUTION.md) for provenance and the outstanding code-licensing considerations.
