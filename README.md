# Phase Modulation (PM) of Voice Signal – Python Project

This Colab-based project performs Phase Modulation (PM) and demodulation on a recorded voice message using Python.

## 🎯 Objective

- Modulate a recorded voice signal using Phase Modulation (PM)
- Visualize the modulated waveform
- Demodulate and recover the original audio signal

## 🛠️ Requirements

- Google Colab or Jupyter Notebook
- Libraries: numpy, matplotlib, scipy, soundfile

## 🔄 Steps Performed

1. Upload a mono or stereo `.wav` voice recording (`message.wav`)
2. Convert stereo to mono (if needed)
3. Apply Phase Modulation (PM):
   \[
   s(t) = A_c \cdot \cos(2\pi f_c t + k_p m(t))
   \]
4. Plot original vs modulated signals
5. Demodulate using Hilbert transform and derivative
6. Save and download recovered audio

## 📁 Files

- `phase_modulation_pm_colab.ipynb`: Main code notebook
- `message.wav`: Your input voice file (not shared publicly)
- `recovered_pm.wav`: Output audio after demodulation

## 🔊 Example

You say:  
> "Hello, this is a test signal for modulation."

The system modulates it in phase and recovers a close match.

---


