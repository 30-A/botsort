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

### Output Files
All outputs are saved in the `output` directory:
- **`reduced_fps.mp4`**: Video with reduced frame rate.
- **`reduced_size.mp4`**: Video with reduced size.
- **`reduced_fps_and_size.mp4`**: Video with both reduced frame rate and size.
- **`detections.csv`**: CSV file with detection results.
- **`counting_video.mp4`**: Video with tracking and counting annotations.
- **`tracker_output.csv`**: CSV file with tracking results.
