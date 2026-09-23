<div align="center">

# Face Detection

**Two small OpenCV scripts: draw boxes around faces in a photo, and in a live webcam feed.**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![Haar Cascades](https://img.shields.io/badge/Haar_Cascades-grey?style=flat-square)

</div>

---

## What it does

Classical Haar cascade detection, no neural network involved. Both scripts follow the same four steps:

```
read frame  ->  convert to greyscale  ->  detectMultiScale(1.1, 4)  ->  draw rectangles
```

Greyscale first because the cascade works on intensity, not colour, and running it on one channel instead of three is the cheap part of making it fast enough for video.

| Script | Input | Output |
|---|---|---|
| `detect_face_image.py` | `test1.jpg` | Window with boxes drawn, any key to close |
| `detect_face_video.py` | Webcam (device 0) | Live window, `Esc` to quit |

---

## The two tunables

`detectMultiScale(gray, 1.1, 4)` is where the behaviour lives:

- **`scaleFactor = 1.1`** shrinks the image 10% per pass to catch faces at different distances. Lower is more thorough and slower.
- **`minNeighbors = 4`** is how many overlapping detections are needed to accept a box. Raise it to cut false positives, lower it if real faces get dropped.

---

## Running it

```bash
pip install opencv-python
python detect_face_image.py     # still image
python detect_face_video.py     # webcam
```

Both scripts load their cascade from the working directory, so run them from the repo root.

---

## Swapping the cascade

`haarcascade_smile.xml` ships alongside the face one. Both scripts have the swap sitting commented on line 5:

```python
face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
# face_cascade = cv2.CascadeClassifier('haarcascade_smile.xml')
```

Smile detection is meant to run on an already cropped face region rather than a whole frame, so pointed at a full image it will be noisy.

`detect_face_video.py` also has a commented line for reading a video file instead of the webcam.

---

<sub>An early OpenCV exercise. Archived, not maintained.</sub>
