# Extraction and Analysis of Musical Elements from Audio Signals

A Python-based project for extracting and analyzing musical elements from audio recordings using Digital Signal Processing (DSP), audio feature extraction, and deep learning-based source separation.

The project explores how separating individual musical sources can improve the analysis of musical properties such as key, tempo, and pitch.

Developed as part of the bachelor's thesis:

**"Ekstrakcija i analiza muzičkih elemenata iz audio signala – tutorijal"**

## Overview

A mixed music recording contains overlapping sources, including vocals, drums, bass, and harmonic instruments. Analyzing these components directly can make it difficult to identify reliable musical characteristics.

This project combines source separation with signal processing techniques to analyze both complete recordings and isolated audio stems.

The general workflow consists of:

1. Loading and preprocessing audio recordings.
2. Separating musical sources using Demucs.
3. Extracting relevant audio features.
4. Estimating musical key and tempo.
5. Comparing analysis methods and evaluating their performance.
6. Extracting musical notes from audio streams in real time.

## Features

### Audio Source Separation

Uses the pretrained **Demucs** model to separate recordings into four stems:

- Vocals
- Drums
- Bass
- Other instruments

These stems enable individual analysis of musical components.

### Musical Key Detection

Evaluates chromagram-based analysis and the Constant-Q Transform (CQT) for estimating the musical key of a recording.

The experiments compare the original audio with separated stems to investigate how source separation and different spectral representations affect key detection.

### Tempo Estimation

Estimates tempo in beats per minute (BPM) using beat-tracking techniques.

The evaluated approaches include:

- Analysis of the original recording
- Harmonic-Percussive Source Separation (HPSS)
- Analysis of the Demucs drum stem

### Real-Time Note Detection

Includes a real-time audio analysis module that estimates musical pitches and maps detected frequencies to musical notes.

The module uses spectral analysis and CQT-based features to support pitch detection from audio input and isolated instrument recordings.

### Experimental Analysis

The project evaluates different combinations of audio preprocessing, source separation, and feature extraction methods.

The experiments use a dataset of 110 songs across five genres, with manually annotated reference values for musical key and tempo.

## Methodology

The project combines deep learning-based source separation with traditional digital signal processing.

The main techniques include:

- **Demucs** for music source separation
- **HPSS** for harmonic-percussive separation
- **STFT** for time-frequency analysis
- **Chroma features** for pitch-class analysis
- **CQT** for musical frequency representation
- **Beat tracking** for tempo estimation

Experimental results indicate that CQT-based analysis of separated instrumental audio provides the strongest results among the evaluated approaches for key detection. For tempo estimation, analyzing the isolated drum stem produces the best results among the tested methods.

## Technologies

- Python
- PyTorch
- Demucs
- Librosa
- NumPy
- SciPy
- Pandas
- Matplotlib
- Jupyter Notebook

## Getting Started

### Prerequisites

- Python 3.10 or later, subject to dependency compatibility
- Git
- A working audio processing environment

### Installation

Clone the repository:

```bash
git clone https://github.com/maslesa/WaveSplitNotebook.git
cd WaveSplitNotebook
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Windows:

```bash
.venv\Scripts\activate
```

Install the project dependencies:

```bash
pip install -r requirements.txt
```

If a dependency file is not available in the repository, install the required libraries separately.

### Running the Analysis

Open the notebooks in Jupyter:

```bash
jupyter notebook
```

Run the notebook cells in sequence to reproduce the audio preprocessing, source separation, feature extraction, and experimental analysis.

## Future Improvements

Potential extensions include:

- More accurate pitch and key estimation
- Automatic chord recognition
- MIDI generation and music transcription
- Expanded evaluation on larger datasets
- A real-time desktop or web application

## References

- [Demucs](https://github.com/facebookresearch/demucs) — Music source separation
- [Librosa](https://librosa.org/) — Audio and music analysis
- Brown, J. C. (1991). *Calculation of a Constant Q Spectral Transform.*

## Author

**Ljubomir Masleša**

BSc in Information Systems and Technologies  
University of Belgrade – Faculty of Organizational Sciences

## License

This project was developed for educational and research purposes.