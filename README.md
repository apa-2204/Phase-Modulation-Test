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

## Python Code

```
# Phase Modulation (PM) Project in Google Colab

# STEP 1: Upload .wav file
from google.colab import files
uploaded = files.upload()  # Upload your 'message.wav' here

# STEP 2: Load and preprocess audio
import soundfile as sf
import numpy as np

message, fs = sf.read('message.wav')

# Convert stereo to mono
if message.ndim == 2:
    message = message.mean(axis=1)

# Normalize
message = message / np.max(np.abs(message))
t = np.arange(len(message)) / fs

# STEP 3: Perform Phase Modulation
fc = 10000            # Carrier frequency: 10 kHz
kp = np.pi / 2        # Phase sensitivity
carrier_amplitude = 1.0

pm_signal = carrier_amplitude * np.cos(2 * np.pi * fc * t + kp * message)

# STEP 4: Plot original and PM signal
import matplotlib.pyplot as plt

plt.figure(figsize=(12, 6))
plt.subplot(2, 1, 1)
plt.plot(t[:1000], message[:1000])
plt.title("Original Message Signal")
plt.subplot(2, 1, 2)
plt.plot(t[:1000], pm_signal[:1000])
plt.title("Phase Modulated (PM) Signal")
plt.tight_layout()
plt.show()

# STEP 5: Demodulate using Hilbert Transform
from scipy.signal import hilbert

analytic_signal = hilbert(pm_signal)
instantaneous_phase = np.unwrap(np.angle(analytic_signal))
demodulated = np.diff(instantaneous_phase) * fs / kp
demodulated = np.concatenate([[demodulated[0]], demodulated])
demodulated = demodulated / np.max(np.abs(demodulated))

# STEP 6: Save recovered audio
sf.write('recovered_pm.wav', demodulated, fs)
files.download('recovered_pm.wav')
```

## 🔊 Example

You say:  
> "Hello, this is a test signal for modulation."

The system modulates it in phase and recovers a close match.

---


