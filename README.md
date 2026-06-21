# Whisper ASR Noise Robustness (Diploma Project)

This repository contains the experimental code for my bachelor's thesis in Applied Mathematics. The project explores how different sizes of end-to-end speech recognition models (specifically OpenAI's Whisper) perform under various acoustic noise conditions.

## What's this about?
I wanted to compare Whisper **Tiny** (39M params) and **Small** (244M params) to see where the trade-off between speed and accuracy breaks down when background noise is introduced.

The script takes clean audio, dynamically adds White Gaussian Noise at different Signal-to-Noise Ratios (SNR: from 50dB down to -5dB), and calculates:
- **WER (Word Error Rate)** using the `jiwer` library.
- **RTF (Real-Time Factor)** to measure inference speed.

## Tech Stack
- Python, PyTorch
- `transformers` (Hugging Face)
- `librosa` for audio processing and spectrogram generation
- `evaluate` for metrics

## Quick Summary of Findings
- **Accuracy:** The Small model holds up much better when the noise gets heavy (SNR < 10 dB). Tiny starts dropping words or hallucinating much earlier.
- **Speed:** Tiny is roughly 3 times faster (lower RTF) than Small. If noise isn't an issue, Tiny is definitely the way to go for real-time processing.

## Running the code
The code is formatted as a Jupyter Notebook, specifically optimized for **Google Colab** (using a Tesla T4 GPU).

1. Open the `.ipynb` file in Colab.
2. Run the first cell to install dependencies (`transformers`, `librosa`, etc.).
3. The script will prompt you to upload a `.wav` or `.mp3` file (I used custom 15-20 second clips for my tests).
4. Type in the reference text when asked (this is needed to calculate the WER).
5. The notebook will run the stress test and plot the graphs (WER vs. Noise, RTF comparison, and spectrograms).

*Note: If you run this locally, you'll need to replace the `google.colab import files` block with standard local file loading.*
