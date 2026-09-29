<div align="center">

# 🎨 Hanuman Ji Art: Sequential Part Draw & Fill

**Watch an image draw itself, outline by outline, color by color.**

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-5C3EE8?logo=opencv&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-required-013243?logo=numpy&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

</div>

---

## ✨ Overview

This project turns a normal image into a live drawing animation using **OpenCV**. A custom cursor traces the outline of each region, glides to its center, and fills it with color, one part at a time, until the full picture appears.

The sample run uses `hanumanji.jpg`, but the script works with any image.

## 🚀 Features

- 🖊️ Live outline drawing with a custom arrow cursor
- 🎯 Automatic region detection using **K-Means color segmentation**
- 🧩 Big shapes first (base, skin, background areas), fine details last
- 🖼️ Auto-resize to fit your screen (700 px height, aspect ratio preserved)
- ⌨️ Press `Esc` any time to stop
- ⚙️ Easy to tweak: segments, speed, noise filter, edge sensitivity

## 🧠 How It Works

| Step | What happens |
|------|--------------|
| 1. Resize | Image is scaled to 700 px height |
| 2. Edges | Bilateral filter + Canny edge detection |
| 3. Segment | K-Means groups pixels into color clusters (default 18) |
| 4. Extract | Connected components become individual parts; regions under 120 px are dropped as noise |
| 5. Sort | Parts are ordered by area, largest first |
| 6. Animate | For each part: draw outline → move cursor to center → fill with original color |
| 7. Finish | Final image is shown until you press a key |

## 📦 Installation

```bash
# 1. Clone the repository
git clone https://github.com/suman9834/Hanuman_Ji_art.git
cd Hanuman_Ji_art

# 2. (Optional) create a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # macOS / Linux

# 3. Install dependencies
pip install -r requirements.txt
```

## ▶️ Usage

Run the script from the project folder:

```bash
python main.py
```

To use a different image, edit the last lines of `main.py`:

```python
if __name__ == "__main__":
    part_by_part_draw_and_fill("your_image.jpg", num_segments=18)
```

### Controls

| Key | Action |
|-----|--------|
| `Esc` | Stop the animation and close the window |
| Any key | Close the window after the animation ends |

## 🖼️ Output

![Hanuman Ji Art](hanumanji.png)

## ⚙️ Configuration

| Setting | Where | Effect |
|---------|-------|--------|
| `num_segments` | function argument | More segments = more color detail, but slower |
| `target_height = 700` | inside the function | Output window height in pixels |
| `area > 120` | part extraction loop | Minimum region size; raise it to skip small details |
| `range(1, len(cnt), 3)` | outline loop | Step along the contour; larger = faster drawing |
| `cv2.waitKey(35)` | fill step | Pause after each fill (ms) |
| `Canny(blurred, 40, 130)` | edge detection | Lower and upper edge thresholds |

## 📁 Project Structure

```
Hanuman_Ji_art/
├── main.py             # Main script
├── hanumanji.jpg       # Sample image
├── hanumanji.png       # Output screenshot
├── requirements.txt    # Dependencies
├── LICENSE             # MIT License
└── README.md
```

## 💡 Tips

- K-Means starts from random centers, so each run looks slightly different.
- Large images and high `num_segments` make segmentation slower.
- Images with clear, bold colors give the best results.
- A wrong image path raises `FileNotFoundError`.

## 🤝 Contributing

Contributions are welcome!

1. Fork the repo
2. Create a branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "Add my feature"`
4. Push: `git push origin feature/my-feature`
5. Open a Pull Request

## 👤 Author

**Suman Kumar**

- GitHub: [@suman9834](https://github.com/suman9834)


<div align="center">

If you liked this project, give it a ⭐ on GitHub!

</div>