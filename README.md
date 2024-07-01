#### Cloning the Repository and Installing Requirements

```bash
git clone https://github.com/30-A/botsort.git
cd botsort
pip install -r requirements.txt
```

#### Initialization
Provide the paths to the video file, configuration file, and checkpoint file.

```python
video_path = 'path/to/your/video.mp4'
config_path = 'path/to/your/config.py'
checkpoint_path = 'path/to/your/checkpoint.pth'

processor = Processor()
```

### Reducing Frame Rate (FPS)
**Explanation**: Reduces the video frame rate to the specified `new_fps`. The new video will have fewer frames per second.

```python
# Example: Run detector with FPS reduction
processor.run_detector(video_path, config_path, checkpoint_path, reduce_fps=30)
```

### Reducing Video Size
**Explanation**: Scales the video dimensions by the specified `scale_factor`. For example, a scale factor of 0.5 reduces the video resolution by half, changing a UHD (3840x2160) video to FHD (1920x1080).

```python
# Example: Run detector with size reduction
processor.run_detector(video_path, config_path, checkpoint_path, reduce_size=0.5)
```

### Reducing Both Frame Rate and Size
**Explanation**: Simultaneously reduces both the frame rate and video size.

```python
# Example: Run detector with both FPS and size reduction
processor.run_detector(video_path, config_path, checkpoint_path, reduce_fps=30, reduce_size=0.5)
```

### Running the Tracker
**Explanation**: Processes the detected objects for tracking and counting. This step should be run after `run_detector`.

```python
# Run tracker
processor.run_tracker()
```

### Running Only the Tracker
**Explanation**: If you already have detections and want to run only the tracker, set the `use_tracker_only` flag to `True` and provide the paths to the detections CSV and video file, as well as the config and checkpoint paths for initializing the detector.

```python
# Example: Run tracker only
processor.run_tracker(
    use_tracker_only=True,
    detections_path='path/to/detections.csv',
    video_path=video_path,
    config_path=config_path,
    checkpoint_path=checkpoint_path
)
```

**Detections CSV Format**: The detections CSV should have the following format:

| frame_id | x1         | y1         | x2         | y2         | score         | label |
|----------|------------|------------|------------|------------|---------------|-------|
| 1        | 441.856201 | 653.499573 | 522.625671 | 733.613220 | 0.9642648101  | 5     |
| 1        | 1293.729492| 534.785522 | 1366.824951| 614.397888 | 0.9637929797  | 4     |
| 1        | 523.415527 | 661.935974 | 588.016113 | 728.087829 | 0.9619662166  | 4     |

The columns are:
- `frame_id`: Frame number in the video.
- `x1`, `y1`: Coordinates of the top-left corner of the bounding box.
- `x2`, `y2`: Coordinates of the bottom-right corner of the bounding box.
- `score`: Confidence score of the detection.
- `label`: Class label of the detected object.


### Output Files
All outputs are saved in the `output` directory:
- **`reduced_fps.mp4`**: Video with reduced frame rate.
- **`reduced_size.mp4`**: Video with reduced size.
- **`reduced_fps_and_size.mp4`**: Video with both reduced frame rate and size.
- **`detections.csv`**: CSV file with detection results.
- **`counting_video.mp4`**: Video with tracking and counting annotations.
- **`tracker_output.csv`**: CSV file with tracking results.
