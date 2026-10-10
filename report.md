# Automated Lyric Videos — Solution Report

## Approach

I developed an automated pipeline that extracts audio from an input MP4, transcribes vocals with Whisper, estimates visual characteristics from sampled frames using OpenCV, and renders word-timed karaoke-style subtitles with FFmpeg.

Whisper provides transcription and word-level timestamps. OpenCV samples frames to estimate a palette and motion level. An optional Replicate-hosted LLaVA vision-language model can propose a visual style plan. If the API is unavailable or no token is configured, the pipeline falls back to local visual heuristics.

The generated output includes a rendered MP4, timing metadata, a style plan, and a quality report.

## Design decisions

- Used Whisper large-v3 for transcription.
- Requested word-level timestamps to support karaoke-style highlighting.
- Sampled video frames instead of processing every frame for style estimation.
- Added a local fallback so video rendering can continue without the external vision API.
- Used ASS subtitle styling and FFmpeg for rendering.
- Generated JSON metadata and basic automated quality checks.

## Results

The selected run's quality report records:
- Render success: true
- Output duration: 246.798 seconds
- Duration difference from input: 0 seconds
- Recognized words: 100
- Mean Whisper word probability: 0.924
- Timing anomalies: 1
- Vision API used: false
- Style source: OpenCV fallback

These checks indicate successful rendering and duration preservation. They do not establish that every lyric is perfectly synchronized.

## Limitations

Singing is challenging for speech-recognition systems, and word timestamps can be inaccurate. The quality checks are heuristic and do not verify synchronization throughout the entire video. The vision model, when enabled, sees only sampled frames. The OpenCV fallback estimates visual style but does not fully understand narrative context or musical rhythm. The current output also depends on the selected language and audio quality.

## What I would do next

I would evaluate alignment against manually verified lyric timings, test multiple languages and music genres, sample frames adaptively around scene changes, and incorporate audio rhythm into subtitle animation. I would also compare fallback styling with vision-model recommendations and report measurable synchronization and visual-consistency metrics.
