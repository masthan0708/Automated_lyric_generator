# Automated Lyric Video Generator

An exploratory AI-powered pipeline developed for the TUM School of Management, Professorship of Digital Marketing application challenge.

The pipeline takes a music video and automatically produces a lyric video with timed word-level subtitles, visual styling, and a quality report.

## Features

- Audio extraction using FFmpeg
- Vocal transcription and word timestamps using OpenAI Whisper
- Frame sampling and visual feature analysis using OpenCV
- Optional Replicate-hosted LLaVA vision-language model for style suggestions
- OpenCV-based fallback styling when the vision API is unavailable
- Karaoke-style subtitle generation using ASS subtitles
- Final video rendering using FFmpeg
- JSON timing metadata and quality reporting

## Requirements

- Python 3
- FFmpeg, including ffprobe
- A compatible runtime with sufficient memory for Whisper large-v3
- Google Colab is recommended for running the provided notebook
- Optional: a Replicate API token for vision-based style suggestions

## How to run

1. Open `Pipeline_Automated_Lyric_Video_Generator.ipynb` in Google Colab.
2. Install the dependencies as specified in the notebook.
3. If using Replicate, store `REPLICATE_API_TOKEN` in Colab Secrets. Never hard-code credentials.
4. Run the notebook and upload an MP4 when prompted.
5. Download the generated lyric video and JSON reports.

## Output

The `output/` directory contains the generated lyric video and quality report from the selected run.

## Limitations

- Whisper timestamps may be inaccurate for singing.
- Automated checks cannot guarantee exact synchronization.
- The vision model only sees sampled video frames.
- The local fallback estimates style from visual features and may not capture the full visual language or rhythm of a video.
- Transcription accuracy varies with audio quality, language, and vocal clarity.

## Future improvements

- Improve singing-specific alignment and evaluate synchronization more thoroughly.
- Analyze more frames and incorporate rhythm and scene changes into styling.
- Add multilingual controls and configurable subtitle layouts.
- Evaluate results across different music genres and languages.
- Improve automated quality metrics.

## Responsible use

Use source videos and music only when permitted. This repository is private for the application challenge. Do not publish the challenge output.
