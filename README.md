garmin-smartwatch

This project is a custom Garmin Connect IQ watch app designed for the Garmin Forerunner 165, focused on cadence-based running feedback.

The app allows runners to define a target cadence zone and receive:

real-time visual feedback

haptic alerts when cadence falls outside the target zone

live run metrics including cadence, heart rate, distance, and time

The goal is to support cadence awareness and consistency during runs without overwhelming the runner with complex data.

✨ Core Features

Custom Cadence Zone

User-defined minimum and maximum cadence

Clear in-zone / out-of-zone feedback

Real-Time Alerts

Visual indicators

Haptic alerts when cadence drops below or exceeds the target range

Live Run Metrics

Cadence

Heart rate

Distance

Elapsed time

Activity Recording

Start/stop run recording

Visual recording indicator during activity

🧠 Experimental Feature: Cadence Quality (CQ)

This project includes an experimental metric called Cadence Quality (CQ), designed to provide a higher-level assessment of a runner’s cadence consistency over the course of a run.

Unlike instantaneous cadence alerts, Cadence Quality evaluates cadence over time, capturing not just whether the runner hits the target zone, but how consistently and smoothly they do so.

How Cadence Quality Works

Cadence Quality is a composite score (0–100) derived from two components:

Time-in-Zone

The proportion of recent cadence samples that fall within the configured cadence range.

Cadence Smoothness

A measure of how stable the runner’s cadence is between consecutive samples.

Large fluctuations reduce the smoothness score.

The final Cadence Quality score is computed as a weighted combination:

70% Time-in-Zone

30% Cadence Smoothness

Warm-Up Window

To reduce early-run noise, Cadence Quality is only computed after a minimum data window (≈30 seconds) has been collected.
Before this threshold, the metric is intentionally withheld.

Frozen Final Score

Cadence Quality is computed live during the run, but frozen when the activity ends, producing a single evaluative score for the session.

This mirrors how higher-level performance metrics are treated in research and commercial running analytics.

UI Integration (Easter Egg)

Cadence Quality is surfaced as a subtle, secondary UI element rather than a primary metric.

Visible during activity

Displays CQ: -- during warm-up

Displays the final frozen score after the run ends

This design intentionally positions CQ as an advanced insight for curious or research-oriented users, without distracting from core cadence feedback.

🛠️ Compilation Instructions

You must generate your own Garmin developer key before compiling.

From the project root:

monkeyc -o TestingCadence.prg -f monkey.jungle -y developer_key.der -w


Run in the simulator:

monkeydo TestingCadence.prg fr165


If fr165 is not available in your SDK version, a similar device (e.g. venu2) can be used for simulation.

📱 App Screenshots

Version 1 – Main Layout


Menu – Cadence Zone Selection


Running – Outside Target Zone


Running – Inside Target Zone


📌 Notes

Cadence Quality is an experimental metric, intended for exploration and research rather than clinical or prescriptive use.

Thresholds and weightings are configurable and designed to be iterated on.