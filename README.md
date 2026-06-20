# Video-Text Data Filtering Pipeline

A pipeline that curates high-quality video–caption pairs from a large, noisy dataset — scoring each clip on caption–video alignment (CLIP) and visual quality (DOVER) so only the best pairs are kept for multimodal model training.

> 🏆 2nd place (50+ teams) — NTU EEE MLDA Deep Learning Week 2024 Hackathon

## Overview
Large multimodal models are only as good as the data they train on. As datasets grow, low-quality or poorly-aligned video–caption pairs waste compute and hurt model performance. This pipeline automatically filters a raw dataset down to its highest-quality pairs. It builds on an exploratory dataset (captions + corresponding YouTube URLs) provided by TikTok.

## How it works
`JSON → parse → pre-filter → download clips → CLIP alignment + DOVER quality → combined score → top-N`

1. Parse the source `.json` into `.csv` (video URLs, clip timings, captions).
2. Sample a subset of videos (compute/time/memory constraints).
3. Pre-filter — drop clips with low FPS or abnormally short durations.
4. Download videos from YouTube and process into `.mp4` clips + keyframes.
5. **Caption–video alignment** — average CLIP score between the first/middle/last frames and the caption.
6. **Video quality** — aesthetic + technical scoring via DOVER (open-source pre-trained video QA model).
7. Combine into a single overall score per clip.
8. Apply a cutoff threshold to select the top-N caption–clip pairs.

## Pre-trained Models
 - CLIP (OpenAI)
 - DOVER

## Design decisions
To fit hackathon time and hardware limits, the pipeline uses lightweight, pre-trained, open-source models (CLIP, DOVER) rather than training from scratch — keeping inference fast enough to run on local machines / Colab.

## Results
- 🏆 2nd place out of 50+ teams (MLDA Deep Learning Week 2024)
- ~12% improvement in downstream training-data quality
- Lower compute/energy vs. a train-from-scratch approach by relying on lightweight pre-trained models

## Demo
▶️ https://youtu.be/iRGKJqZFatM

## Acknowledgements
Dataset and problem inspiration provided by **TikTok**.
