# Brain Tumor Detection

A deep learning project for classifying brain MRI scans into three tumor categories using **ResNet50 Transfer Learning** and a **Flask web application**.

> **Status:** The application structure is ready. The trained model weights (`.pt`) are not included yet. A custom model will be trained from the Brain Tumor Dataset and added to the project.

## Overview

This project uses a fine-tuned ResNet50 model to classify T1-weighted contrast-enhanced brain MRI images into:

- Glioma
- Meningioma
- Pituitary Tumor

The project is intended for **educational and research purposes** and is not a medical diagnostic system.

## Workflow

```text
MRI Image
   │
   ▼
Image Preprocessing
(Resize → Normalize → Tensor)
   │
   ▼
ResNet50
(Transfer Learning)
   │
   ▼
3-Class Classification
   │
   ├── Glioma
   ├── Meningioma
   └── Pituitary
   │
   ▼
Prediction + Confidence
   │
   ▼
Flask Web Application
```

## Dataset

This project uses the **Brain Tumor Dataset by Jun Cheng**, available through Figshare.

| Property | Details |
|---|---|
| Dataset | Brain Tumor Dataset |
| Author | Jun Cheng |
| Images | 3,064 T1-weighted CE-MRI scans |
| Patients | 233 |
| Format | MATLAB `.mat` files |
| Classes | Meningioma, Glioma, Pituitary |

The dataset is distributed across four parts:

```text
brainTumorDataPublic_1-766
brainTumorDataPublic_767-1532
brainTumorDataPublic_1533-2298
brainTumorDataPublic_2299-3064
```

Dataset source:

- [Brain Tumor Dataset — Figshare](https://figshare.com/articles/dataset/brain_tumor_dataset/1512427)

Each `.mat` file contains information such as:

- `cjdata.image` — MRI image
- `cjdata.label` — tumor class label
- `cjdata.tumorBorder` — tumor boundary coordinates
- `cjdata.tumorMask` — tumor-region mask

## Model

The planned model uses **ResNet50 pretrained on ImageNet** with a custom classification head for the three tumor classes.

```text
Input Image
224 × 224 × 3
      │
      ▼
ResNet50 Backbone
      │
      ▼
2048-dimensional Features
      │
      ▼
Custom Classifier
      │
      ▼
3 Classes
```

### Model Status

The trained model file is currently **not included in the repository**.

Planned file:

```text
models/
└── brain_tumor_model.pt
```

The model will be trained separately and added to the project after the training pipeline has been completed.

## Project Structure

```text
BRAIN_TUMOR_DETECTION/
│
├── Brain-Tumor-Test-Images/     # Sample MRI images for testing
│
├── models/
│   └── README.md                # Model information
│
├── static/
│   └── b.jpg                    # Static application assets
│
├── templates/
│   ├── Diseasedet.html
│   ├── error.html
│   ├── MainPage.html
│   ├── pred.html
│   └── uimg.html
│
├── app.py                       # Flask application
├── requirements.txt             # Python dependencies
└── README.md
```

## Installation

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd BRAIN_TUMOR_DETECTION
```

### 2. Create a virtual environment

Windows:

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

## Training

The model training pipeline will be added to the project.

The planned training process is:

1. Extract the four dataset archives.
2. Read the `.mat` MRI files.
3. Convert and preprocess MRI images.
4. Create training, validation, and test sets.
5. Load an ImageNet-pretrained ResNet50.
6. Replace the final classifier for three classes.
7. Train and validate the model.
8. Evaluate the model on the test set.
9. Save the trained weights as:

```text
models/brain_tumor_model.pt
```

## Running the Application

Once the trained model has been added:

```bash
python app.py
```

Then open:

```text
http://127.0.0.1:5000
```

Upload an MRI image to obtain a model prediction.

## Technologies

- **Python**
- **PyTorch**
- **Torchvision**
- **ResNet50**
- **Flask**
- **Pillow**
- **HTML / CSS**
- **Bootstrap**

## Medical Disclaimer

This project is developed for **educational and research purposes only**.

It is not intended to provide, replace, or support medical diagnosis or treatment decisions. Predictions produced by the model should not be considered a clinical diagnosis. Always consult a qualified medical professional for medical interpretation.

## References

- [Jun Cheng Brain Tumor Dataset — Figshare](https://figshare.com/articles/dataset/brain_tumor_dataset/1512427)
- [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385)
- [PyTorch Transfer Learning Tutorial](https://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html)

## License

This project follows the license specified by the repository.
