# 🎵 WaveSplit  
## Extraction and Analysis of Musical Elements from Audio Signals

WaveSplit is a Python-based audio analysis framework designed for extracting and analyzing important musical elements from audio recordings.

The main goal of the project is to develop an intelligent system capable of automatically analyzing songs by combining **Digital Signal Processing (DSP)** techniques and modern **Deep Learning-based audio separation models**.

The system performs:

- 🎼 Instrument separation using **Demucs**
- 🎹 Musical key detection
- 🥁 Tempo / BPM estimation
- 🎵 Real-time note extraction
- 📊 Audio feature analysis using spectrogram representations
- 🔊 Individual instrument analysis (drums, bass, vocals, etc.)

The project was developed as part of the thesis project:

> **"Ekstrakcija i analiza muzičkih elemenata iz audio signala - tutorijal"**

---

# Project Overview

Modern music analysis systems require understanding different components of an audio signal. A mixed audio recording contains multiple overlapping sources:

- vocals
- drums
- bass
- harmonic instruments
- melodies

Analyzing these elements directly from the original waveform is challenging because all instruments interfere with each other.

WaveSplit solves this problem by introducing an audio preprocessing stage where the original track is separated into individual stems before performing musical analysis.

The general pipeline:

```
Audio Input
      |
      v
Audio Preprocessing
      |
      v
Instrument Separation (Demucs)
      |
      +----------------+
      |                |
      v                v
Key Detection     Tempo Detection
      |                |
      v                v
CQT Analysis      Drum Analysis
      |
      v
Note Extraction
      |
      v
Musical Information Output
```

---

# Features

## Audio Source Separation

WaveSplit uses the pretrained:

**Demucs - Hybrid Transformer/Convolutional Network**

model for separating the input audio into independent stems:

- Vocals
- Drums
- Bass
- Other instruments

This allows individual analysis of specific musical components.

Example:

```
input_song.wav

        |
        v

Demucs

        |
        +---- vocals.wav
        |
        +---- drums.wav
        |
        +---- bass.wav
        |
        +---- other.wav
```

---

# Musical Key Detection

The system estimates the tonal center of the song using spectral analysis.

Two approaches were evaluated:

## 1. Chromagram-based analysis

The traditional chroma representation maps frequencies into 12 pitch classes:

```
C
C#
D
D#
E
F
F#
G
G#
A
A#
B
```

The detected pitch distribution is compared with major/minor key templates.

---

## 2. Constant-Q Transform (CQT)

The final implementation uses **CQT-based analysis** because it provides better musical frequency representation.

Advantages of CQT:

- logarithmic frequency resolution
- better alignment with musical pitch
- improved key detection accuracy
- closer representation of human perception

The best results were achieved by applying CQT on:

- original audio signal
- Demucs isolated stems

especially:

```
CQT + isolated instruments
```

---

# Tempo / BPM Detection

Tempo estimation is performed using rhythmic information extracted from audio.

Different approaches were evaluated:

- full song analysis
- HPSS separated percussion component
- Demucs isolated drums

The best performance was achieved using:

```
Demucs drums stem
        +
Beat tracking analysis
```

because drums contain the strongest rhythmic information.

The system extracts:

- BPM value
- beat positions
- rhythmic patterns

---

# Real-Time Note Detection

WaveSplit includes a real-time note extraction module capable of detecting played notes from isolated instruments.

The process:

```
Audio Stream

      |
      v

FFT / CQT Analysis

      |
      v

Frequency Detection

      |
      v

Frequency -> MIDI Mapping

      |
      v

Musical Note Output
```

Example output:

```
Detected notes:

C4
E4
G4
B4
```

The system can analyze isolated instrument tracks such as:

- bass
- piano
- guitar

allowing cleaner pitch detection compared with the original mixed signal.

---

# Technologies Used

## Programming Language

- Python 3.10+

---

## Audio Processing

- librosa
- NumPy
- SciPy

Used for:

- waveform processing
- FFT analysis
- spectrogram calculation
- CQT transformation
- beat tracking


---

## Deep Learning

### Demucs

Used for:

- source separation
- extracting individual instruments


Framework:

- PyTorch


---

## Data Analysis

- Pandas
- Matplotlib


---

# Project Structure

```
WaveSplit/

│
├── notebooks/
│   │
│   ├── wavesplit.ipynb
│   └── analysis.ipynb
│
├── audio/
│   │
│   ├── input/
│   └── separated/
│
├── models/
│
├── src/
│   │
│   ├── separation.py
│   ├── key_detection.py
│   ├── tempo_detection.py
│   └── note_detection.py
│
├── requirements.txt
│
└── README.md
```

---

# Installation

Clone the repository:

```bash
git clone https://github.com/username/WaveSplit.git

cd WaveSplit
```

Create virtual environment:

```bash
python -m venv venv
```

Activate environment:

### Windows

```bash
venv\Scripts\activate
```

### Linux / macOS

```bash
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Required Libraries

Main dependencies:

```
torch
torchaudio
demucs
librosa
numpy
scipy
pandas
matplotlib
jupyter
```

---

# Usage

## 1. Audio Separation

Run Demucs:

```bash
python separation.py --input song.wav
```

Output:

```
separated/

├── vocals.wav
├── drums.wav
├── bass.wav
└── other.wav
```

---

## 2. Key Detection

Example:

```python
from key_detection import detect_key

key = detect_key(
    "separated/other.wav"
)

print(key)
```

Example output:

```
Detected key:

F minor
```

---

## 3. BPM Detection

Example:

```python
from tempo_detection import detect_bpm

bpm = detect_bpm(
    "separated/drums.wav"
)

print(bpm)
```

Output:

```
Estimated BPM:

128 BPM
```

---

## 4. Note Detection

Example:

```python
from note_detection import detect_notes


notes = detect_notes(
    "separated/bass.wav"
)

print(notes)
```

Output:

```
C2
E2
G2
A2
```

---

# Experimental Results

During development, multiple combinations were evaluated.

## Key Detection Comparison

Tested approaches:

| Method | Input |
|-|-|
| Chromagram | Full song |
| Chromagram | Demucs stems |
| CQT | Full song |
| CQT | Demucs stems |

The best performance was obtained using:

```
CQT representation
+
Demucs separated instruments
```

---

## BPM Detection Comparison

Evaluated approaches:

| Method | Input |
|-|-|
| Beat tracking | Full song |
| HPSS percussion |
| Demucs drums |

Best results:

```
Demucs drums
+
Beat tracking
```

---

# Methodology

The project combines classical DSP approaches with modern neural networks.

The workflow:

1. Load audio signal
2. Normalize waveform
3. Separate sources using Demucs
4. Extract spectral features
5. Analyze individual components
6. Estimate musical parameters
7. Present extracted information

---

# Goals Achieved

Implemented:

✅ Automatic instrument separation  
✅ Key detection  
✅ BPM estimation  
✅ CQT-based musical analysis  
✅ Real-time note extraction  
✅ Individual instrument processing  

---

# Future Improvements

Possible future extensions:

## Better Pitch Detection

Implement advanced models:

- CREPE
- Spotify Basic Pitch
- Neural pitch estimation models


## Automatic Chord Recognition

Add:

- chord progression detection
- harmonic analysis


## Music Transcription

Extend note detection into:

- MIDI generation
- sheet music creation


## Real-Time Application

Develop:

- desktop application
- web interface
- live microphone analysis


---

# References

- Demucs: Music Source Separation Model  
  https://github.com/facebookresearch/demucs

- Librosa Audio Analysis Library  
  https://librosa.org/

- Constant-Q Transform  
  Brown, J. C. (1991). Calculation of a constant Q spectral transform.

---

# Author

**Ljubomir Masleša**

Bachelor of Information Systems and Technologies  
University of Belgrade - Faculty of Organizational Sciences

---

# License

This project is intended for educational and research purposes.