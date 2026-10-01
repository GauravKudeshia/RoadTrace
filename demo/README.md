# Reading the RoadTrace demo

This folder contains a saved run from October 1, 2026. Start with [the annotated video](traffic-demo.mp4), then use [the CSV](vehicle_data.csv) to follow an individual track frame by frame.

The video is the first eight seconds of the supplied traffic sample, processed at 960 × 540 and 25 FPS. It has been encoded as H.264 for playback in common browsers and video players. The animated preview uses a lower resolution and fewer frames; the full video retains all 200 frames and the original timing.

## What to look for

Follow one ID as it moves down the road. The short trail shows its recent image positions. A numeric speed appears after about one second of usable history inside the yellow road outline. All speeds are estimates in miles per hour.

“Warming up” means there isn't enough recent history. “Beyond calibration” means the tracked point is outside the modeled road area. “Partial view” means the box touches an image edge; the speed history is reset because the bottom-center of a clipped box can give a misleading position.

Some boxes or classes are imperfect. IDs may disappear or change through occlusion. Those cases are part of the saved output and matter when interpreting the measurements.

## Files and results

| File | Contents |
| --- | --- |
| [traffic-demo.mp4](traffic-demo.mp4) | Full eight-second annotated video |
| [traffic-preview.gif](traffic-preview.gif) | Animated README preview |
| [preview.jpg](preview.jpg) | Still frame from the same run |
| [vehicle_data.csv](vehicle_data.csv) | Frame-level positions and estimated mph |
| [speed_distribution.png](speed_distribution.png) | One median speed per track with usable measurements |

The run contains 803 observations across 14 IDs. Of those observations, 461 have numeric speeds, spanning six tracks. Taking one median speed from each of those six tracks gives a mean of 70.5 mph and a median of 74.0 mph.

Each CSV row has a `vehicle_id`, predicted `class`, zero-based `frame`, `timestamp_s`, image coordinates `x_px` and `y_px`, and `estimated_speed_mph`. A blank speed means it was unavailable. A calculated zero would mean no measured movement. The coordinates remain in pixels even though speed is calculated in road coordinates.

The input footage and approximate road geometry come from the sources listed in [the calibration notes](../SAMPLE_CALIBRATION.md). No independent speed reference was used. See [the validation record](../VALIDATION.md) for the software checks and limitations.

To reproduce the pipeline, run `python run_sample.py` from the repository root. Fresh results go to `output-perspective-mph/`; this saved demo stays unchanged.
