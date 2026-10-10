# Automated Lyric Video Generator

An exploratory project for the TUM School of Management, Professorship of Digital Marketing application challenge.

This notebook implements an automated pipeline that takes an MP4 music video, extracts audio, transcribes vocals, estimates visual characteristics, generates timed karaoke-style subtitles, and renders an output video.

## Pipeline

1. Extract mono audio at 16 kHz with FFmpeg.
2. Transcribe audio and obtain word-level timestamps using Whisper large-v3.
3. Sample video frames and estimate colors and motion using OpenCV.
4. Optionally request visual-style suggestions from the Replicate-hosted LLaVA vision-language model.
5. Use local OpenCV-based style estimation when the vision API is unavailable.
6. Generate ASS subtitles with word highlighting and render the final MP4 using FFmpeg.
7. Save timing metadata, a style plan, and a quality report.

## Requirements

- Python 3
- FFmpeg with ffprobe and subtitle-rendering support
- `openai-whisper`
- `opencv-python-headless`
- `numpy`
- `pillow`
- `requests`
- Google Colab or a suitable local runtime
- A GPU is recommended for Whisper large-v3; CPU execution may be slow.

## Run the notebook

1. Open `Pipeline_Automated_Lyric_Video_Generator.ipynb` in Google Colab.
2. Run the notebook cells in order.
3. Upload an MP4 when prompted.
4. Optionally configure `REPLICATE_API_TOKEN` in Colab Secrets for vision-based style suggestions.
5. Download the rendered video and generated reports.

Never hard-code API credentials or commit secrets.

## Included outputs

The `output/` directory contains two generated videos and their corresponding quality reports:

- `lyric_video.mp4`
- `quality_report.json`
- `lyric_video-4.mp4`
- `quality_report-4.json`

See `report.md` for the reported metrics and limitations.

## Limitations

- Whisper word timestamps may be inaccurate for singing.
- Automated duration and transcript checks do not prove exact synchronization.
- The vision model, when used, sees only sampled frames.
- The OpenCV fallback estimates visual style from basic visual features.
- Results may vary with audio quality, language, and vocal clarity.

## Responsible use

This repository is private for the application challenge. Use source music videos only as permitted, and do not publish the challenge output.
