# garmin-smartwatch

This project is a **custom Garmin Connect IQ watch app** designed for the **Garmin Forerunner 165**, focused on **cadence-based running feedback**.

The app allows runners to define a **target cadence zone** and receive:

- Real-time visual feedback  
- Haptic alerts when cadence falls outside the target zone  
- Live run metrics including cadence, heart rate, distance, and time  

The goal is to support **cadence awareness and consistency during runs** without overwhelming the runner with complex data.

---

## ✨ Core Features

### 🏃‍♂️ Custom Cadence Zone
- User-defined **minimum and maximum cadence**
- Clear **in-zone / out-of-zone** visual feedback

### 🔔 Real-Time Alerts
- Visual indicators
- Haptic alerts when cadence drops below or exceeds the target range

### 📊 Live Run Metrics
- Cadence  
- Heart rate  
- Distance  
- Elapsed time  

### ⏺️ Activity Interaction
- Explicit start / stop cadence monitoring
- Visual indicator when monitoring is active
- No background execution unless explicitly started by the user

---

## 🧠 Experimental Feature: Cadence Quality (CQ)

This project includes an **experimental metric** called **Cadence Quality (CQ)**, designed to provide a **higher-level assessment of cadence consistency** over the course of a run.

Unlike instantaneous cadence alerts, Cadence Quality evaluates cadence **over time**, capturing not just whether the runner hits the target zone, but **how consistently and smoothly** they do so.

> **Cadence Quality is a pilot research-style metric**, not a clinical or prescriptive measure.

---

## 📐 How Cadence Quality Works

Cadence Quality is a **composite score (0–100)** derived from two components:

### 1️⃣ Time-in-Zone
- The proportion of recent cadence samples that fall within the configured cadence range
- Rewards sustained adherence to the target cadence

### 2️⃣ Cadence Smoothness
- Measures how stable cadence is between consecutive samples
- Large fluctuations reduce the smoothness score

### 🧮 Weighting Formula

```text
Cadence Quality = (Time-in-Zone × 70%) + (Cadence Smoothness × 30%)
This weighting reflects research priorities where consistency matters more than momentary precision.

---

### ⏱️ Warm-Up Window
To reduce early-run noise:

CQ is withheld during the initial warm-up period

A minimum data window (~30 seconds) must be collected before CQ is computed

During this phase, the UI displays:

text
Copy code
CQ: --
This prevents misleading early scores caused by sensor stabilization and pacing adjustments.

❄️ Frozen Final Score
CQ is computed live during cadence monitoring

When monitoring stops, the final CQ score is frozen

This produces one evaluative score for the completed session

This mirrors how higher-level performance metrics are treated in research and commercial running analytics.

🧩 UI Integration (Easter Egg)
Cadence Quality is intentionally designed as a secondary, low-salience metric:

Visible during cadence monitoring

Hidden during warm-up

Displays final frozen score after monitoring ends

This positions CQ as an advanced insight for curious or research-oriented users, without distracting from core cadence feedback.

🧪 Debugging & Diagnostics (Team Update Integration)
Significant development time was spent on debugging, validation, and traceability of the CQ metric.

What Was Added / Refined
Implemented Cadence Quality (CQ) as a new metric alongside live cadence

Built a debug + diagnostic flow so CQ behaviour is visible and traceable in the terminal:

Warm-up phase

Live CQ values

Final frozen summary

Added a warm-up phase to prevent early noisy calculations

Implemented final CQ freezing when cadence monitoring stops

Added CQ confidence levels:

High

Medium

Low
Based on cadence data completeness

Added a CQ trend indicator:

Improving

Stable

Declining
Using a rolling window of recent CQ values

Refactored start/stop logic so:

Cadence monitoring is explicit

Nothing runs in the background unintentionally

Ensured everything remains within Watch App constraints:

No activity recording

No FIT file generation

🎯 Why Cadence Quality Matters
Cadence Quality measures how consistently and smoothly a runner maintains cadence within an ideal range — not just how fast they step.

This is important because:

Consistent cadence is linked to running efficiency

Smooth cadence transitions reduce impact stress

Variability in cadence has been associated with injury risk

Stakeholders benefit from interpretable, higher-level insights rather than raw sensor noise

CQ is therefore positioned as a research-aligned exploratory metric with clear future potential.

🧠 Abandoned Experiment: “Hardcore Mode” (Postmortem)
An attempted hidden “hardcore mode” Easter egg was explored, intended to:

Dynamically tighten cadence thresholds

Adapt difficulty for advanced users

However:

This introduced significant platform constraints

Required shifting from a Watch App → Activity App

Had broader implications than initially anticipated

Ultimately delayed progress and was rolled back

This served as a valuable lesson in Connect IQ platform boundaries and app-type tradeoffs.

🛠️ Compilation Instructions
You must generate your own Garmin developer key before compiling.

From the project root:

bash
Copy code
monkeyc -o TestingCadence.prg -f monkey.jungle -y developer_key.der -w
Run in the simulator:

bash
Copy code
monkeydo TestingCadence.prg fr165
If fr165 is not available in your SDK version, a similar device (e.g. venu2) can be used for simulation.

📱 App Screenshots
Version 1 – Main Layout

Menu – Cadence Zone Selection

Running – Outside Target Zone

Running – Inside Target Zone

📌 Notes
Cadence Quality is experimental and intended for exploration and research

Thresholds, confidence bands, and weightings are configurable

The system is designed for iteration, validation, and future expansion

Copy code
