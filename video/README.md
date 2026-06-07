# Video Analysis

This directory contains the provider-view video analysis code for estimating visible time associated with people and workstation displays.

## Script

`get_time_for_provider_views.py` processes provider-view videos frame by frame and records the duration of three detection states:

- Person only
- Workstation display only
- Person and workstation display

The clinic visits analyzed here did not include a television. The script treats `laptop` and `tv` detections as proxy labels for workstation displays because YOLO sometimes labeled the workstation as one of those COCO classes.

## Inputs

The script accepts an input video directory as a command-line argument. It includes files ending in `.mp4` or `.MP4`.

## Outputs

The script writes an Excel workbook to the selected output directory:

```text
video_detection_times.xlsx
```

The output table contains one row per video with:

- `video_file`
- `num_frames`
- `fps`
- `duration_s`
- `total_time_s`
- `avg_time_per_frame_s`
- `throughput_fps`
- `time_person_s`
- `time_computer_s`
- `time_both_s`
- `pct_frames_person`
- `pct_frames_computer`
- `pct_frames_both`

The script also saves compressed annotated detection frames in one subdirectory per source video.

## Dependencies

From this directory, install the video dependencies in the active Python environment:

```bash
pip install -r requirements.txt
```

Ultralytics will download `yolo11n.pt` automatically if the model weights are not already present.

## Run

From this directory:

```bash
python get_time_for_provider_views.py "../Provider Views" "Provider_Views_Output"
```

Use `--model` to provide a different YOLO weights file:

```bash
python get_time_for_provider_views.py "../Provider Views" "Provider_Views_Output" --model yolo11n.pt
```

## Notes

- Timing estimates depend on the source video's frame rate and model detections.
- Frames without target labels are ignored in the reported exposure-time categories.
- The script appends one row per processed video to `video_detection_times.xlsx`.
