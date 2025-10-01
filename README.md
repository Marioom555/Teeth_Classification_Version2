
# 🦷 Teeth Classification using Transfer Learning + Gradio Deployment

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.1+-red.svg)](https://pytorch.org/)

This project implements a **teeth classification pipeline** using **transfer learning** on dental diseases images.  
It includes preprocessing, augmentation, training, evaluation, single-image inference, and a **Gradio web app** for deployment.

---
<img width="1351" height="629" alt="Image" src="https://github.com/user-attachments/assets/0c7880a1-0fa0-48c2-87f8-41d4c51875f0" />
<img width="1351" height="629" alt="Image" src="https://github.com/user-attachments/assets/0c7880a1-0fa0-48c2-87f8-41d4c51875f0" />
## 📂 Project Structure
```
src/
  dataset.py     # Dataset loader + Albumentations transforms
  models.py      # Model factory (EfficientNet, ConvNeXt, Swin, etc.)
  utils.py       # Metrics, checkpointing, plotting
  train.py       # Training script
  evaluate.py    # Evaluate test set
  predict.py     # Single image prediction
  gradio_app.py  # Gradio web interface for deployment
```

---

## ⚙️ Installation

### Option 1 — Using Conda (recommended)
```bash
conda env create -f environment.yml
conda activate teeth-class
```

### Option 2 — Using pip/venv
```bash
python -m venv .venv
# Activate:
# Windows: .\.venv\Scripts\activate
# Linux/Mac: source .venv/bin/activate
pip install -r requirements.txt
```

---

## 📊 Dataset Structure
```
dataset/
  train/
    class_0/
    ...
    class_6/
  val/
    class_0/
    ...
    class_6/
  test/
    class_0/
    ...
    class_6/
```

---

## 🚀 Steps to Run Project

### 1. Train Model
```bash
python src/train.py --data_dir dataset --epochs 20 --batch-size 16
```
➡️ Saves checkpoints in `runs/` (`best.pth` is the best model).

### 2. Evaluate Model
```bash
python src/evaluate.py --data_dir dataset --checkpoint runs/best.pth
```
➡️ Prints accuracy & classification report, saves confusion matrix (`runs/confusion.png`).

### 3. Predict Single Image (CLI)
```bash
python src/predict.py --checkpoint runs/best.pth --image path/to/image.jpg
```

### 4. Launch Gradio Web App
```bash
python src/gradio_app.py
```
➡️ Opens browser at [http://127.0.0.1:7860](http://127.0.0.1:7860)  
➡️ Upload an image → get predicted illness class + probabilities.

To share a public link, edit the last line in `gradio_app.py`:
```python
iface.launch(server_name="0.0.0.0", server_port=7860, share=True)
```




