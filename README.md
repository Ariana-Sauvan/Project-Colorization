# Convolutional Autoencoder for Image Colorization

This project implements a Convolutional Autoencoder (CAE) for self-supervised image colorization on the CelebA dataset.
The model receives the L (lightness) channel of an image and predicts the AB chrominance channels in the LAB color space.

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

The model was trained for 20 epochs on the full CelebA training set using a Google Colab GPU.
The training loss decreased from 0.0089 (epoch 1) to 0.0034 (epoch 20), a reduction of approximately 62%.

The model successfully colorizes facial regions with accurate skin tones and hair colors.
Background regions remain the main challenge, which is a known limitation of MSE-based colorization.

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
