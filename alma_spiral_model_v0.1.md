## ✳️ Alma Spiral Model v0.1
*Physiological-Emotional Pattern Recognition Framework*

---

### 🔹 Overview
The **Alma Spiral** model translates physiological signals into emotional-state patterns and adaptive feedback for self-regulation.  
It is based on cyclical transitions between *activation, discharge, reflection, and coherence*, observed through biosignal variability.

---

### 🔸 Variables & Normalization

| Symbol | Variable | Description | Sampling Rate | Normalization Range | Trigger Logic |
|---------|-----------|--------------|----------------|----------------------|----------------|
| **HR** | Heart Rate | Beats per minute from PPG/ECG sensor | 1 Hz | 40–180 bpm → scaled 0–1 | HR_HIGH if >0.8 for ≥2 samples |
| **HRV** | Heart Rate Variability | RMSSD or SDNN (ms) | 1 sample / 60 s | 20–120 ms → scaled 0–1 (inverse correlation) | HRV_LOW if <0.3 for ≥2 cycles |
| **EDA** | Electrodermal Activity | Skin conductance (μS) | 4 Hz | 0–15 μS → scaled 0–1 | EDA_RISE if Δ >0.1/10 s |
| **RR** | Respiration Rate | Breaths per minute | 0.5 Hz | 8–25 bpm → scaled 0–1 | RR_HIGH if >0.75 for ≥2 windows |
| **TEMP** | Peripheral Temperature | Skin temperature (°C) | 0.2 Hz | 30–37°C → scaled 0–1 | TEMP_LOW if <0.3 for ≥5 min |
| **ACCEL** | Accelerometer | Movement intensity | 10 Hz | normalized 0–1 | MOV_HIGH if >0.8 for ≥2 s |

---

### 🔹 State Engine Mapping

| Phase | Physiological Pattern | Coherence Score | Feedback Profile |
|--------|------------------------|------------------|------------------|
| **1. Pressure** | HRV↓ slight, EDA↑ mild, RR irregular | 0.4–0.5 | low-frequency pulse |
| **2. Accumulation** | HRV↓↓, EDA↑↑, TEMP↓, RR↑↑ | 0.3–0.4 | rhythmic pulse; color: amber |
| **3. Eruption** | HR↑ peak, HRV↓, EDA peak, ACCEL↑ | 0.1–0.3 | quick vibration; UI blue-dark; message: “Find your ground.” |
| **4. Reflection** | HR↓, HRV↑, EDA↓, TEMP↑ | 0.5–0.7 | steady warm vibration; text: “Rest is recovery.” |
| **5. Integration** | HR stable, HRV high, EDA low, RR coherent | >0.7 | harmonic vibration; UI gold-green; message: “You are in resonance.” |

---

### 🔸 Coherence Index Formula
```python
CI = (w1 * norm(HRV) + w2 * (1 - norm(EDA)) + w3 * norm(TEMP) + w4 * (1 - abs(norm(RR) - 0.4))) / (w1 + w2 + w3 + w4)
Weights adjust dynamically based on user calibration data.
Baseline protocol:

5 min rest

3 min emotional stress

3 min guided relaxation
🔹 Data Flow Architecture
Sensors → Signal Processor → Feature Extractor → State Engine → Feedback Loop → Data Logger → Adaptive Model Update
Each user session contributes to personalized calibration and to an aggregated collective emotional map for pattern research (optional, privacy-protected).

🔸 Implementation Notes

Debounce rules: 2 consecutive breaches per alert type.

Sampling resampling only for UI (not for analysis).

Confidence score attached to every state detection.

Rolling analysis windows: 6 min, 12 min, 30 min.

Feedback timing: <2 s delay from state detection.

🔹 Versioning & Tasks

Version: v0.1 – Prototype Mapping
Next Steps:

Implement normalization scripts.

Build coherence index calculator.

Integrate tactile and visual feedback logic.

Conduct baseline calibration test.

Log and visualize phase transitions.

✅ Maintainer: Raluca-Adelina Luca
✅ Repo: github.com/almaresonance/alma-spiral
✅ Status: Development Prototype
