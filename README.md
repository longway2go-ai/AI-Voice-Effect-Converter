# 🎤 AI Voice Effect Converter (Gradio Version)
A powerful Python application that transforms vocals with advanced AI-powered voice effects including Animated Voice, Slowed + Reverb, and Party Mashup. Features intelligent vocal separation, professional audio processing, and a user-friendly Gradio interface.

## ✨ Features

### 🎵 Voice Effects
- **Animated Voice**: Bright, energetic character voice with pitch shifting and sparkle enhancement
- **Slowed + Reverb**: Atmospheric effect with gentle slowdown and complex reverb chambers
- **Party Mashup**: Electronic dance music enhancement with synthesized instruments and beats

### 🔧 Technical Capabilities
- **Smart Vocal Separation**: Advanced spectral processing with style-specific optimization
- **Professional Audio Processing**: Butter filters, dynamic compression, and frequency enhancement
- **Intelligent Caching**: Automatic download caching for faster repeated processing
- **Multi-Source Support**: YouTube URLs and direct audio file uploads
- **Real-time Progress**: Live processing status with detailed feedback

### 🚀 Performance Optimizations
- Memory-efficient processing with automatic cleanup
- Multi-strategy YouTube downloading for reliability
- Optimized audio processing pipeline
- Professional mixing and mastering algorithms

## 📋 Requirements

### System Dependencies
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install ffmpeg libsndfile1 python3-dev

# macOS (with Homebrew)
brew install ffmpeg libsndfile

# Windows (with Chocolatey)
choco install ffmpeg
```

### Python Requirements
```python
gradio>=4.0.0
torch>=1.9.0
librosa>=0.10.0
soundfile>=0.12.0
numpy>=1.21.0
yt-dlp>=2023.1.0
scipy>=1.7.0
pathlib
```

## 🛠️ Installation

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/enhanced-voice-converter.git
cd enhanced-voice-converter
```

### 2. Create Virtual Environment
```bash
python -m venv voice_env
source voice_env/bin/activate  # Linux/macOS
# voice_env\Scripts\activate     # Windows
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Verify FFmpeg Installation
```bash
ffmpeg -version
```

## 🚀 Quick Start

### Basic Usage
```bash
python app.py
```

The application will start on `http://localhost:7860`

### Command Line Interface (Advanced)
```python
from voice_converter import OptimizedVoiceConverter

converter = OptimizedVoiceConverter()

# Convert from YouTube
output_path, title, time = converter.convert_voice_effect(
    "https://youtube.com/watch?v=example",
    "Animated Voice",
    vocal_vol=1.3,
    music_vol=0.5,
    progress_fn=lambda x, y: print(f"{x:.1%}: {y}")
)

# Convert from file
output_path, title, time = converter.convert_voice_effect_from_file(
    "input.wav",
    "Slowed + Reverb",
    vocal_vol=1.2,
    music_vol=0.6,
    progress_fn=lambda x, y: print(f"{x:.1%}: {y}")
)
```

## 🎯 Voice Effect Details

### Animated Voice
- **Pitch Shift**: +9 semitones for bright character voice
- **Speed**: 1.15x for energetic delivery
- **Frequency Enhancement**: Boosted 2-5kHz for clarity and sparkle
- **Effects**: Character vibrato (6Hz) and dynamic compression
- **Best For**: Character voices, energetic content, animation dubbing

### Slowed + Reverb
- **Pitch Shift**: -1 semitone for warmth
- **Speed**: 0.90x for relaxed delivery
- **Reverb**: Complex multi-delay system with 6 delay stages
- **Filtering**: Warm 180Hz-4kHz band emphasis
- **Effects**: Subtle chorus and gentle saturation
- **Best For**: Chill music, atmospheric content, dreamy vocals

### Party Mashup
- **Electronic Elements**: Synthesized kick drums, snare, and bass lines
- **Melodic Components**: Lead synths, chord pads, and pluck sounds
- **Effects**: Frequency sweeps and controlled electronic processing
- **Mixing**: Professional ducking and electronic mastering
- **Best For**: Dance music, party content, electronic remixes

## ⚙️ Configuration

### Audio Settings
- **Sample Rate**: 22050 Hz (optimized for voice processing)
- **Max Duration**: 90 seconds per track
- **Bit Depth**: 16-bit WAV output
- **Processing**: Mono and stereo input support

### Voice Volume Ranges
- **Voice Level**: 0.8 - 2.0 (recommended: 1.3)
- **Music Level**: 0.2 - 1.0 (recommended: 0.5)

### Cache Configuration
```python
TEMP_DIR = "/tmp/voice_temp"      # Temporary processing files
OUTPUT_DIR = "/tmp/voice_output"  # Final output location
CACHE_DIR = "/tmp/voice_cache"    # Download cache storage
```

## 🔧 Advanced Usage

### Custom Voice Effect
```python
class CustomVoiceEffect(OptimizedVoiceModeler):
    @staticmethod
    def my_custom_effect(vocals, sr):
        # Custom pitch shifting
        vocals = librosa.effects.pitch_shift(vocals, sr=sr, n_steps=5)
        
        # Custom filtering
        b, a = butter(2, [1000, 3000], btype='band', fs=sr)
        vocals = filtfilt(b, a, vocals)
        
        # Custom effects
        vocals = np.tanh(vocals * 1.2) * 0.9
        
        return librosa.util.normalize(vocals) * 0.95

# Register new effect
converter.voice_modeler.custom_effect_processing = CustomVoiceEffect.my_custom_effect
converter.styles["Custom Effect"] = "custom_effect_processing"
```

### Batch Processing
```python
import os
from pathlib import Path

def batch_process_directory(input_dir, output_dir, voice_style="Animated Voice"):
    converter = OptimizedVoiceConverter()
    
    for audio_file in Path(input_dir).glob("*.wav"):
        try:
            output_path, title, time = converter.convert_voice_effect_from_file(
                str(audio_file),
                voice_style,
                vocal_vol=1.3,
                music_vol=0.5,
                progress_fn=lambda x, y: print(f"{audio_file.name}: {x:.1%}")
            )
            
            # Move to output directory
            final_path = Path(output_dir) / f"{audio_file.stem}_{voice_style}.wav"
            shutil.move(output_path, final_path)
            print(f"✅ Processed: {audio_file.name} -> {final_path.name}")
            
        except Exception as e:
            print(f"❌ Failed: {audio_file.name} - {e}")

# Usage
batch_process_directory("./input_audio", "./output_audio", "Slowed + Reverb")
```

## 🐛 Troubleshooting

### Common Issues

#### Download Failures
```bash
# Update yt-dlp
pip install --upgrade yt-dlp

# Check URL validity
yt-dlp --list-formats "YOUR_YOUTUBE_URL"
```

#### Memory Issues
```python
# Reduce processing duration
converter.max_duration = 60  # seconds

# Force garbage collection
import gc
gc.collect()
```

#### Audio Quality Issues
```python
# Increase sample rate (requires more memory)
y, sr = librosa.load(audio_path, sr=44100)

# Adjust processing parameters
vocal_vol = 1.1  # Lower for cleaner sound
music_vol = 0.7  # Higher for better balance
```

#### FFmpeg Not Found
```bash
# Ubuntu/Debian
sudo apt install ffmpeg

# Add to PATH (Windows)
# Download from https://ffmpeg.org/download.html
# Add bin folder to system PATH
```

### Performance Optimization

#### For Low-Memory Systems
```python
# Reduce STFT parameters
S = librosa.stft(y, n_fft=1024, hop_length=256)  # Instead of 2048/512

# Process in chunks
chunk_size = sr * 30  # 30 seconds
for i in range(0, len(audio), chunk_size):
    chunk = audio[i:i+chunk_size]
    # Process chunk
```

#### For Faster Processing
```python
# Use lower quality for testing
ydl_opts['format'] = 'worstaudio[abr<64]'

# Skip effects for testing
def test_processing(vocals, sr):
    return vocals  # No processing

converter.styles["Test"] = "test_processing"
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Librosa**: For advanced audio processing capabilities
- **Gradio**: For the intuitive web interface
- **yt-dlp**: For reliable YouTube audio extraction
- **SciPy**: For professional signal processing filters

## 🔄 Changelog

### Version 2.1.0 (Current)
- ✨ Enhanced Party Mashup with electronic elements
- 🎵 Improved Slowed + Reverb timing and atmosphere
- 🚀 Optimized vocal separation algorithms
- 🐛 Fixed high-frequency artifacts in Party Mashup
- 📈 Performance improvements and memory optimization

### Version 2.0.0
- 🎤 Added Animated Voice effect
- 🔧 Redesigned audio processing pipeline
- 🎯 Style-specific vocal separation
- 🎨 Enhanced Gradio interface

### Version 1.0.0
- 🎵 Basic voice effects (Slowed + Reverb)
- 📥 YouTube download functionality
- 🎛️ Simple Gradio interface

---

<div align="center">

**Made with ❤️ by the Enhanced Voice Converter Team**

[⭐ Star this repo](https://github.com/yourusername/enhanced-voice-converter) • [🐛 Report Bug](https://github.com/yourusername/enhanced-voice-converter/issues) • [✨ Request Feature](https://github.com/yourusername/enhanced-voice-converter/issues)

</div>
