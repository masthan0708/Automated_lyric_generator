# Automated Lyric Videos — Solution Report

## Approach

I developed an automated pipeline that extracts audio from an input MP4, transcribes vocals with Whisper large-v3, estimates visual characteristics from sampled frames using OpenCV, and renders karaoke-style subtitles with FFmpeg.

Whisper supplies transcription and word-level timestamps. OpenCV samples frames to estimate a color palette and motion level. An optional Replicate-hosted LLaVA vision-language model can suggest a visual style. When the vision API is unavailable or no token is configured, the pipeline uses a local OpenCV-based fallback.

The pipeline also writes timing metadata, a style plan, and a quality report.

## Key design decisions

- Used Whisper large-v3 for multilingual-capable transcription, with the language configurable in the notebook.
- Requested word-level timestamps for karaoke-style highlighting.
- Sampled frames instead of analyzing every frame.
- Added a local fallback to allow rendering without the optional vision API.
- Used ASS subtitles and FFmpeg for subtitle rendering and video encoding.
- Generated JSON quality reports to document basic checks and known limitations.

## Results

Both selected runs report successful rendering and an output duration matching the input duration.

| Metric | `lyric_video.mp4` | `lyric_video-4.mp4` |
|---|---:|---:|
| Output duration | 274.314 s | 246.798 s |
| Recognized words | 323 | 100 |
| Mean Whisper word probability | 0.740 | 0.924 |
| Timing anomalies | 3 | 1 |
| Vision API used | No | No |
| Style source | OpenCV fallback | OpenCV fallback |

These values are taken from the corresponding quality reports. Mean Whisper word probability is not a guarantee of transcription correctness. The two videos have different durations and word counts, so the metrics alone do not establish which output is better.

## Limitations

Singing is challenging for speech-recognition systems, and word-level timestamps may be inaccurate. The automated checks verify basic conditions such as output existence and duration, but do not establish exact synchronization throughout the video. The optional vision model sees only sampled frames, and the OpenCV fallback does not fully capture narrative context or musical rhythm.

## Future improvements

With more time or budget, I would evaluate synchronization against manually verified lyric timings, test multiple languages and music genres, sample frames around scene changes, and incorporate audio rhythm into animation. I would also compare vision-model styling against the fallback and introduce measurable synchronization and visual-consistency metrics.
