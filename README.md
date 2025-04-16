# MoveNet Dual Bicep Curl Tracker

This repository contains a Python script that uses the MoveNet Thunder model from TensorFlow Hub to track and analyze dual bicep curls in real-time via webcam. The script detects keypoints, calculates joint angles, evaluates exercise form, counts repetitions, and provides visual feedback through an OpenCV interface.

![Bicep Curl Tracker Screenshot](images/bicep_tracker_screenshot.png)

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Model Details](#model-details)
- [Output](#output)
- [Generating the Screenshot](#generating-the-screenshot)
- [Download](#download)
- [License](#license)

## Project Overview

The MoveNet Dual Bicep Curl Tracker uses the MoveNet Thunder model to detect human keypoints in real-time from a webcam feed. It analyzes bicep curl form by calculating elbow angles, checking arm synchronization, and monitoring shoulder, wrist, and torso alignment. The script provides a user interface with a stats box (reps, stage, form score, speed, rep quality) and a feedback box for form corrections.

## Features

- **Keypoint Detection**: Uses MoveNet Thunder to identify 17 keypoints (e.g., shoulders, elbows, wrists, hips).
- **Angle Calculation**: Computes elbow angles to track bicep curl range of motion.
- **Form Analysis**: Evaluates elbow stability, arm synchronization, shoulder height, wrist alignment, and torso sway.
- **Rep Counting**: Tracks repetitions based on elbow angle thresholds (down: >160°, up: <30°).
- **Smoothing**: Applies exponential moving average to stabilize keypoint coordinates.
- **UI**: Displays stats (reps, stage, form score, speed, rep quality) and real-time feedback via OpenCV.
- **Workout Summary**: Prints total reps, average rep time, and final form score after completion.

## Requirements

- Python 3.8+
- Libraries:
  - `tensorflow`
  - `tensorflow-hub`
  - `numpy`
  - `opencv-python`
- A webcam for real-time video input.

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/MoveNet-Dual-Bicep-Tracker.git
   cd MoveNet-Dual-Bicep-Tracker
   ```

2. Install the required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Ensure your webcam is connected and functional.

## Usage

1. Run the script:

   ```bash
   python bicep_curl_tracker.py
   ```

2. Perform dual bicep curls in front of the webcam. The script will:

   - Detect keypoints and draw them on the video feed.
   - Display a stats box with reps, stage, form score, speed, and rep quality.
   - Show feedback messages (e.g., "Fix left elbow!", "Sync arms!") in a feedback box.
   - Count reps and evaluate form in real-time.

3. Press `q` or `Esc` to exit. A workout summary will be printed to the console.

## Model Details

- **Model**: MoveNet Thunder (single-pose) from TensorFlow Hub.
- **Input**: Webcam frames resized to 256x256 pixels.
- **Output**: 17 keypoints with (y, x, confidence) coordinates.
- **Processing**: Keypoints are smoothed using an exponential moving average (alpha=0.7) for stability.
- **Form Metrics**:
  - Elbow angle thresholds: >160° (down), <30° (up).
  - Penalties for elbow movement, arm desync, incomplete range, shoulder height, wrist misalignment, and torso sway.
  - Form score calculated as 100 minus penalties (min: 0).

## Output

- **Real-Time UI**:
  - **Stats Box**: Shows reps, stage (up/down), form score (%), average rep time (s), and rep quality (Good/Bad).
  - **Feedback Box**: Displays form correction messages (e.g., "Curl higher!", "Slow down!").
  - **Keypoints**: Green circles drawn on detected joints (confidence > 0.3).
- **Console Summary**:
  - Total reps
  - Average rep time
  - Final form score

Example summary:

```
Workout Summary:
Total Reps: 10
Average Rep Time: 1.25s
Final Form Score: 85%
```

## Generating the Screenshot

The `bicep_tracker_screenshot.png` image is a screenshot of the webcam feed showing keypoints, the stats box, and the feedback box. To generate it:

1. Run the script (`python bicep_curl_tracker.py`).
2. Perform a few bicep curls to populate the UI with stats and feedback.
3. Take a screenshot of the OpenCV window (`MoveNet Dual Bicep Tracker`):
   - **Windows**: Use `Snipping Tool` or `PrtSc` key.
   - **macOS**: Use `Command + Shift + 4`.
   - **Linux**: Use `gnome-screenshot` or similar.
4. Save the screenshot as `bicep_tracker_screenshot.png` in the `images/` folder.
5. Ensure the README references the image correctly (`![Bicep Curl Tracker Screenshot](images/bicep_tracker_screenshot.png)`).

## Download

The project files, including the Python script, requirements, and screenshot, can be downloaded from the GitHub repository:  
[Download MoveNet-Dual-Bicep-Tracker](https://github.com/your-username/MoveNet-Dual-Bicep-Tracker/archive/refs/heads/main.zip)

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
