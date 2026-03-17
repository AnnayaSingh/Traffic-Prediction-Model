<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=13&duration=3000&pause=500&color=64748B&center=true&vCenter=true&width=600&lines=YOLOV8+%C2%B7+OPENCV+%C2%B7+NUMPY+%C2%B7+PYTHON+3.8%2B" alt="stack"/>

# 🚦 Traffic Detection System

**Detect vehicles and classify traffic light color from images using YOLOv8 and OpenCV.**

[![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-F5A623?style=flat-square)](https://github.com/ultralytics/ultralytics)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.8%2B-5C3EE8?style=flat-square&logo=opencv&logoColor=white)](https://opencv.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-22C55E?style=flat-square)](LICENSE)

<br/>

![header](https://capsule-render.vercel.app/api?type=waving&color=0:4ade80,50:facc15,100:f87171&height=180&section=header&text=Traffic%20Detection%20System&fontSize=36&fontColor=fff&fontAlignY=38&desc=YOLOv8%20%2B%20OpenCV%20%2B%20Python&descAlignY=58&descColor=ffffffaa&animation=fadeIn)

</div>

---

## Features

- **Car & motorcycle counting** — filters COCO class labels from YOLOv8 bounding boxes
- **Traffic light color detection** — HSV masking with dual red-hue range (0–10 and 170–180)
- **CLI interface** — configurable image path, model path, and `--no-display` headless flag
- **Modular design** — all functions are independently importable and unit-testable

---

## Installation

```bash
git clone https://github.com/AnnayaSingh/traffic-prediction-model.git
cd traffic-prediction-model
pip install -r requirements.txt
```

> `yolov8n.pt` downloads automatically on first run and is excluded from git via `.gitignore`.

---

## Usage

```bash
# Basic
python traffic_flow_prediction.py --image traffic_image.jpg

# Custom model weights
python traffic_flow_prediction.py --image traffic_image.jpg --model yolov8s.pt

# Headless — no GUI window (servers / CI pipelines)
python traffic_flow_prediction.py --image traffic_image.jpg --no-display
```

**Sample output**

```
🚗 Cars:               4
🏍️  Bikes:              2
🚦 Traffic Light:      RED
```

---

## How It Works

### 1 — Object Detection (YOLOv8)

`yolov8n.pt` runs inference and returns bounding boxes with COCO class labels. The script filters for `car`, `motorcycle`, and `traffic light`.

### 2 — Traffic Light Color (HSV Masking)

The traffic light bounding box is cropped and converted to HSV. Pixel counts within each range determine the active light:

| Color  | Hue Range     | Note                      |
|--------|---------------|---------------------------|
| Red    | 0–10, 170–180 | Full HSV wrap-around      |
| Yellow | 15–35         |                           |
| Green  | 40–90         |                           |

Returns `UNKNOWN` if fewer than 10 pixels match any range.

---

## Project Structure

```
traffic-detection/
├── traffic flow prediction.py   # Main detection script
├── requirements.txt       # Python dependencies
├── .gitignore             # Excludes *.pt weights, venvs, outputs
└── README.md
```

---

## Requirements

| Package        | Min Version |
|----------------|-------------|
| ultralytics    | 8.0.0       |
| opencv-python  | 4.8.0       |
| numpy          | 1.24.0      |

---

## Limitations

- Static images only — no video or webcam support yet
- Only the first detected traffic light is classified per image
- Accuracy degrades in low-light or overexposed conditions

---

## Roadmap

- [ ] Video / webcam streaming support
- [ ] Draw labelled bounding boxes on output image
- [ ] Truck and bus counting
- [ ] Export results to JSON / CSV
- [ ] Night-mode HSV tuning

---

## Acknowledgements

- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics)
- [COCO Dataset](https://cocodataset.org/)
- [OpenCV](https://opencv.org/)

---

<div align="center">

![footer](https://capsule-render.vercel.app/api?type=waving&color=0:f87171,50:facc15,100:4ade80&height=120&section=footer&animation=fadeIn)

MIT License &nbsp;·&nbsp; Built with YOLOv8, OpenCV, and Python

</div>
