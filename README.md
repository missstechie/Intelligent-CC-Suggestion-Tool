# Intelligent Closed Caption (CC) Suggestion Tool (MVP)

This project presents a Minimum Viable Product (MVP) for an intelligent tool designed to assist in generating closed caption (CC) suggestions, specifically focusing on non-speech audio events within video/audio content.

## Project Goal

The primary objective of this tool is to **reduce the manual effort** involved in identifying and annotating meaningful non-speech audio events in video content. Instead of requiring human annotators to listen through entire recordings, this prototype automatically detects significant audio events and generates timestamped caption suggestions.

## How It Works

The tool operates by processing a given video URL through the following steps:

1.  **Video Download**: Utilizes `yt-dlp` to download the video content from the provided URL.
2.  **Audio Extraction**: Extracts the audio track from the downloaded video using `moviepy`.
3.  **Audio Event Detection**: Employs `librosa` to analyze the audio for 'loud sounds' by detecting peaks in audio energy that exceed a calculated threshold.
4.  **Event Filtering**: Filters the detected events to reduce redundancy, ensuring that only significant, distinct events are captured (e.g., by ensuring a minimum time difference between consecutive events).
5.  **SRT File Generation**: Compiles the identified events into a standard SubRip Subtitle (SRT) format, with each entry indicating a 'Loud Sound Detected' along with its timestamp.

## Setup and Usage (Google Colab)

This project is designed to run in a Google Colab environment. 

### Installation

Run the following `pip` commands in your Colab notebook to install the necessary libraries:

```python
!pip install moviepy librosa yt-dlp
```

### Running the Tool

1.  **Specify Video URL**: In the relevant code cell, update the `video_url` variable with the YouTube link of the video you wish to analyze.
2.  **Execute Cells**: Run all the code cells sequentially. The notebook will handle video download, audio processing, event detection, and SRT file generation automatically.

### Output

Upon successful execution, an `output.srt` file will be generated in your Colab environment. This file contains the timestamped caption suggestions. An example entry looks like this:

```
1
00:00:00,272 --> 00:00:02,272
[Loud Sound Detected]

2
00:00:02,602 --> 00:00:04,602
[Loud Sound Detected]
```

## Limitations

*   **Simple Detection**: The current version relies on a basic energy-based detection method, which may not semantically distinguish different types of sounds (e.g., a clap vs. a door slam).
*   **No Visual Analysis**: There is no integration for visual reaction detection.
*   **Irrelevant Sounds**: The tool may detect irrelevant loud sounds that are not pertinent to the context of closed captions.

## Future Work

*   **Integrate Sound Classification**: Incorporate advanced sound classification models (e.g., YAMNet) to semantically identify different audio events.
*   **Visual Reaction Detection**: Implement visual analysis using libraries like OpenCV to detect and timestamp relevant visual cues.
*   **Improve Filtering Logic**: Enhance the event filtering algorithm to provide more precise and contextually relevant caption suggestions.
