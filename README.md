#Football Player Tracking and Match Analytics

A complete end-to-end pipeline for detecting, tracking, and analyzing players, referees, and the ball in football (soccer) match footage.
The system uses YOLO, ByteTrack, and multiple custom modules to generate detailed match analytics, including:

Player, referee, and ball detection
Multi-object tracking across frames
Ball possession estimation
Team assignment based on jersey colors
Player speed and distance estimation
Camera movement compensation
Annotated output video with all overlays

Features
1. Object Detection
Uses Ultralytics YOLO to detect:
Players
Referees
Goalkeepers (auto-converted to players)
Ball

2. Multi-Object Tracking
Implements ByteTrack to assign consistent track IDs across frames.

3. Ball Interpolation
Missing ball coordinates are automatically interpolated to maintain temporal consistency.

4. Team Assignment
A dedicated module determines each player's team by analyzing jersey colors frame by frame.

5. Ball Possession Estimation
Identifies which player controls the ball in every frame and aggregates possession statistics per team.

6. Speed & Distance Estimation
Each player’s motion is analyzed to compute:
Running speed
Distance covered

7. Camera Movement Estimation
Compensates for camera panning and adjusts player movement accordingly.

8. Annotated Output Video
The final output video overlays:
Player IDs and team-colored markers
Ball markers
Referee markers
Ball possession statistics
Speed and distance metrics (if enabled)
Camera movement visualization

Project Structure (Typical)
project/
│
├── main.py
├── tracker/
│   ├── tracker.py
│   ├── camera_movement_estimator.py
│   ├── speed_and_distance_estimator.py
│   ├── team_assigner.py
│   └── ball_assigner.py
│
├── utils/
│   ├── geometry.py
│   └── helpers.py
│
├── input_videos/
├── output_videos/
├── models/
│   └── yolov8_model.pt
└── README.md

How It Works (Pipeline Overview)

Load video → extract all frames
Detect objects using YOLO
Track objects using ByteTrack
Add world positions (foot position for players, center for the ball)
Interpolate ball trajectory to avoid gaps
Estimate camera movement
Assign teams based on jersey color clusters
Determine ball possession per player per frame
Estimate speed & distance for all players
Render output frames with overlaid annotations
Export annotated video

Requirements
Python 3.8+
Ultralytics
supervision
NumPy
OpenCV
Pandas
pickle

A YOLO model trained for: players / referees / goalkeepers / ball

Install via:
pip install ultralytics supervision opencv-python numpy pandas

Usage
1. Place your YOLO model
models/yolov8_model.pt

2. Run the main script
python main.py

3. Find result in
output_videos/output_video.avi
