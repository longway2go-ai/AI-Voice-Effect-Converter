# 🎤 AI Voice Effect Converter (Gradio Version)
AI-powered tool for transforming voices with Slowed Reverb, Party Mashup, and Animated Voice effects, optimized for Google Colab deployment with the fastest processing and cached YouTube downloads.

Built with Gradio, yt-dlp, librosa, and advanced DSP (Digital Signal Processing).

## ✨ Features
🎵 YouTube Downloader (fast + cached): Download up to 90 seconds of audio clips quickly.
🎙️ Vocal Separation: Extract vocals from audio intelligently for cleaner transformations.

## ⚡ Optimized Effects:
Animated Voice – Bright, energetic, cartoon-like vocal effect.
Slowed + Reverb – Atmospheric slowed reverb with spacious ambience.
Party Mashup – Club-style mashup with drums, bass, and electronic effects.

## 📂 File Upload Support: Process upoaded audio directly.
## 🎛️ Mix Controls: Adjust voice level and music level in the final mix.
## ⚡ Performance Optimized: Fast DSP math routines, GPU-ready on Colab.

## 🚀 Installation
Run this in Google Colab:
```bash
!pip install -q gradio yt-dlp librosa soundfile scipy numpy torch
!apt-get update -qq && apt-get install -y -qq ffmpeg
```

## ▶️ Usage
Launch in Colab:
```python
!python app.py
```

## Interface:
1. Paste a YouTube URL or upload an audio file.
2. Choose an effect: Animated Voice, Slowed + Reverb, or Party Mashup.
3. Adjust voice and music levels if needed.
4. Click TRANSFORM VOICE.
5. 🎧 Listen, download, or share the transformed audio.

## 📊 Example Inputs
```
https://www.youtube.com/watch?v=L_jWHffIx5E → Animated Voice
https://www.youtube.com/watch?v=JGwWNGJdvx8 → Slowed + Reverb
https://www.youtube.com/watch?v=example1 → Party Mashup
```
## ⚡ Performance Notes
Works best at default 22,050 Hz sample rate for fast DSP.
Optimized to avoid artifacts (chipmunk effect, chirps, distortions).
Cached downloads save time on repeated conversions.

## 💻 Requirements
``` Python 3.8+
Libraries:
gradio
yt-dlp
librosa
soundfile
numpy
scipy
torch
```
## 📌 Limitations
Designed for 90 sec clips (to keep processing fast).
Real-time streaming not supported yet.
Some rare YouTube links may fail if restricted.

## 🧑‍💻 Author
Developed for fast, creative voice transformations with AI + DSP, optimized for Google Colab / Gradio apps.

## 📜 License
MIT License – Free to use, modify, and distribute.
