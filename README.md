# Ambient AI Scribe Audiovisual Analysis

This repository accompanies the paper's audiovisual analysis workflow. It is organized into separate audio and video sections.

## Repository Structure

```text
ambient-ai-scribe-audiovisual-analysis/
├── audio/
│   └── README.md
├── video/
│   ├── README.md
│   ├── requirements.txt
│   └── get_time_for_provider_views.py
└── README.md
```

- `audio/` contains the audio analysis section.
- `video/` contains the provider-view video analysis script.

## Video Workflow

The current video script estimates the amount of time each provider-view video contains:

- a detected person only
- a detected workstation display only
- both a detected person and workstation display

The script uses OpenCV for frame access, Ultralytics YOLO11n for object detection, and pandas to export the per-video timing summary to an Excel workbook.

See [video/README.md](video/README.md) for setup notes, inputs, and output details.

## Audio Workflow

The audio section is documented in [audio/README.md](audio/README.md).

## Requirements

Dependencies are listed separately within each analysis section. The current video dependencies can be installed with:

```bash
pip install -r video/requirements.txt
```

See the README in each section for script-specific setup and run commands.

## Notes

- Avoid committing raw media, derived sensitive files, or local system files.
