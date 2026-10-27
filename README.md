# Convolutional Autoencoder for Image Colorization

This project implements a Convolutional Autoencoder (CAE) for self-supervised image colorization on the CelebA dataset.
The model receives the L (lightness) channel of an image and predicts the AB chrominance channels in the LAB color space.

**Project Repository:** https://github.com/Ariana-Sauvan/Project-Colorization

---

## Project Structure

```
ProjectColorization-ArianaSauvan/
│
├── ColorizationNotebook_Sauvan.ipynb
│  
│
├── ColorizationReport_Sauvan.pdf
│ 
│
├── README.md
└── requirements.txt
```

---

## Installation

Create a virtual environment (recommended):

```bash
python3 -m venv venv
source venv/bin/activate   # Linux/Mac
venv\Scripts\activate      # Windows
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Dataset (CelebA)

You can obtain the CelebA dataset in two ways:

### **Option 1 — Manual Download**

The CelebA dataset must be downloaded manually from the official source:
https://mmlab.ie.cuhk.edu.hk/projects/CelebA.html

Download the `img_align_celeba.zip` file and place the extracted folder next to the notebook:

```
ProjectColorization-ArianaSauvan/
├── ColorizationNotebook_Sauvan.ipynb
└── Data/
    └── img_align_celeba/
        └── *.jpg
```

If running on Google Colab, upload the zip to your Google Drive and use the extraction cell provided at the top of the notebook.

### **Option 2 — Automatic Download (PyTorch)**
The dataset can also be downloaded automatically using the code snippet already included in your project:

```python
datasets.CelebA(
    root="data/",
    split="train",
    transform=transforms.Compose([
        transforms.Resize((64, 64)),
        transforms.ToTensor()
    ]),
    download=True
)
```
---

## How to Run

### Locally

1. Clone or download this repository
2. Set up the virtual environment and install dependencies
3. Place the CelebA dataset at the correct path (see above)
4. Open `ColorizationNotebook.ipynb` in Jupyter or VS Code
5. Run all cells in order

### Google Colab

1. Upload the notebook to Colab
2. Upload `img_align_celeba.zip` to your Google Drive
3. Run the Drive mounting and extraction cells at the top of the notebook
4. Set the runtime to GPU: Runtime > Change runtime type > T4 GPU
5. Run all cells in order

---

## Model Overview

- **Architecture**: Convolutional Autoencoder
- **Input**: Grayscale L channel (1, 64, 64)
- **Output**: Predicted AB channels (2, 64, 64)
- **Color space**: LAB
- **Loss function**: Mean Squared Error (MSE)
- **Optimizer**: Adam (lr=0.001)
- **Training**: 20 epochs on 162,770 images

---

## Results

**Data split** (CelebA, 202,599 images): 162,770 train / 19,867 validation / 19,962 test.

| Metric | Value |
|---|---|
| Training loss (epoch 1) | 0.0089 |
| Training loss (epoch 20) | 0.0033 |
| Validation loss (after epoch 20) | 0.0080 |
| Test loss | [à compléter si tu l'évalues] |

The model was trained for 20 epochs on the full training set (Google Colab GPU, about 25 minutes). The small gap between training and validation loss indicates mild overfitting, which is expected for a simple autoencoder without skip connections.

The model colorizes facial regions well (skin tones, hair colors). Backgrounds remain the main challenge: MSE-based regression tends to produce desaturated, averaged colors where several colors are plausible.

![Qualitative results](results/figure1.png)
---

## Google Colab Version

A Google Colab version of this project is available here:

🔗 **Google Colab Notebook:** https://colab.research.google.com/drive/1WnCfFCKgOXLS5QpIlitaww5l9Sd9_Ztg?usp=sharing

This notebook contains a slightly different implementation adapted for Colab (dataset loading, paths, GPU setup).


---


## Requirements

See `requirements.txt` for the full list of dependencies. Main libraries:

- torch
- torchvision
- scikit-image
- numpy
- matplotlib
- tqdm
- Pillow
EOF
echo "Done"

Sortie
Done
