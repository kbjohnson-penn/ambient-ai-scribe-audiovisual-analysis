# Audio Analysis

## Script

The script `audio_analysis.ipynb` is a Jupyter notebook designed to process clinical visit transcripts and matching audio files. It synchronizes text-based dialogue logs with silence detection data to compute precise conversation metrics, including individual speaker durations (Provider vs. Patient vs. Other), behavioral proficiencies (device usage), psychological affects, and laughter frequency.

## Inputs

- Audio Files (.wav): Audio recordings of clinical sessions used to extract silence timestamps via sound threshold analysis.

- Transcripts (.xlsx): Structured Excel spreadsheet logs mapping clinical conversations, expected to contain columns such as Speaker (e.g., Doctor, Patient), Timestamp (in [mm:ss] format), Affect, Proficiency, Transcript, and visit_length_seconds.

- Cached Silences Data (silences_03_duration.csv): A pre-computed CSV file storing a list of detected silence intervals to bypass the resource-intensive audio processing step on recurring runs.

## Outputs

- Consolidated Metrics DataFrame (result_df): A structural pandas.DataFrame pulling together speaking durations, silence allocations, standardized behavioral affects, device usage timelines, and laugh counts for every visit.

- Distribution Pie Charts (.png): Session-specific visualization figures mapping out the proportional time slice of the Provider speaking, the Patient speaking, and periods of relative silence.

## Dependencies

Install the audio dependencies in the active Python environment:

```bash
pip install openpyxl pydub moviepy ffmpeg-python
```

## Run

1. File Paths: Define target file paths inside the glob.glob("") initializers for AUDIO_FILES and TRANSCRIPTS.

2. Silence Processing Execution Option:

- Option A (Fresh Run): Uncomment and execute get_silence_timestamps(AUDIO_FILES) to generate silence intervals directly from the source audio files (Note: processing takes ~40 minutes).

- Option B (Cached Run): Ensure silences_03_duration.csv is present in the working directory to instantly parse pre-processed intervals.

3. Execute Calculations: Run the final cells sequentially to cycle through the transcript segments via speaker_durations(), build the consolidated metrics table, and render the session distribution charts.

## Notes

- Silence Threshold Rules: Silence detection is specifically configured to isolate drops in audio that fall below -45 dB lasting for a minimum duration of 300 ms (0.3 seconds).

- Data Cleanup: The code natively handles structural anomalies, normalizing varying string formats (e.g., misspellings like "Reponsiveness" or "Attentivness" are programmatically mapped to standardized behavioral categories).

- Zero-Duration Buffers: If two subsequent timestamps result in a computed delta of 0 seconds, the script introduces a fallback buffer of 0.5 seconds to preserve sequence continuity.
