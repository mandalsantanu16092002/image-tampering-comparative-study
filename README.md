
# A Comparative Study of Deep Learning Models for Image Tampering Detection (CASIA V2.0)

This repository contains the implementation, trained models, and results for a comparative study of seven deep learning architectures — **ResNet-50**, **EfficientNet-B4**, **Vision Transformer (ViT)**, **Swin Transformer**, **ConvNeXt**, **CAT-Net**, and **ManTra-Net** — applied to image tampering (forgery) detection on the **CASIA V2.0** dataset.

> Detecting whether an image has been digitally altered (via splicing, copy-move forgery, or object removal) is an increasingly important problem in digital forensics, journalism, and criminal investigation. This project benchmarks CNN, transformer, and hybrid architectures under a single, consistent experimental setup to identify which approach offers the best trade-off between accuracy and computational efficiency.

## Authors

- **Santanu Mandal** — Department of Information Technology, Delhi Technological University
- **Dr. Dinesh Kumar Vishwakarma** (Supervisor) — Department of Information Technology, DTU
- **Dr. Ankit Yadav** (Joint Supervisor) — Department of Information Technology, DTU

## Abstract

Detecting images that have been edited or otherwise altered is a complex task given the wide availability of editing tools. This study evaluates ResNet-50, EfficientNet-B4, Vision Transformer, Swin Transformer, ConvNeXt, CAT-Net, and ManTra-Net on the CASIA V2.0 dataset, comparing their ability to differentiate between fake and real images. All models were trained under identical conditions and evaluated on accuracy, precision, recall, F1 score, AUC, and misclassification error. The **Swin Transformer** achieved the best results (86.96% accuracy, 0.9589 AUC), successfully identifying both large and subtle image manipulations. **ManTra-Net**, while less accurate, required substantially less compute — making it attractive for resource-constrained settings.

## Dataset

- **CASIA V2.0** — a widely used benchmark for image forgery detection, containing authentic and tampered images (splicing and copy-move forgery) across diverse scenes, object classes, and illumination conditions.
- Split: **80% training / 20% testing**

## Model Architectures

| Model | Type | Input Size | Notes |
|---|---|---|---|
| ResNet-50 | CNN | 224×224 | Residual learning baseline |
| EfficientNet-B4 | CNN | 380×380 | Compound scaling for fine forensic detail |
| Vision Transformer (ViT) | Transformer | 224×224 | Patch-based global self-attention |
| Swin Transformer | Transformer | 224×224 | Hierarchical, shifted-window attention |
| ConvNeXt | CNN (transformer-inspired) | 224×224 | Modernized convolutional design |
| CAT-Net | Hybrid | 224×224 | Forensic-specific architecture |
| ManTra-Net | Hybrid | 224×224 | Lightweight forensic-specific architecture |

All models used **ImageNet-pretrained weights** (transfer learning) with the final classification layer modified for binary classification (authentic vs. tampered).

## Training Setup

| Hyperparameter | Value |
|---|---|
| Optimizer | Adam |
| Learning Rate | 0.0001 |
| Batch Size | 16 / 32 (architecture-dependent) |
| Epochs | 30 |
| Loss Function | CrossEntropyLoss |
| Framework | PyTorch |
| Hardware | GPU-based training (Google Colab) |

## Results

### Classification Performance

| Model | Accuracy | Precision | Recall | F1 Score | AUC | MCE |
|---|---|---|---|---|---|---|
| ResNet-50 | 0.7768 | 0.7019 | 0.7834 | 0.7404 | 0.8433 | 0.2231 |
| EfficientNet-B4 | 0.7448 | 0.6903 | 0.6741 | 0.6821 | 0.8411 | 0.2552 |
| Vision Transformer | 0.7680 | 0.6767 | 0.8049 | 0.7351 | 0.8160 | 0.2319 |
| **Swin Transformer** | **0.8696** | **0.8385** | **0.8410** | **0.8397** | **0.9599** | **0.1304** |
| ConvNeXt | 0.7273 | 0.6653 | 0.6614 | 0.6634 | 0.8090 | 0.2727 |

### Computational Efficiency

| Model | Parameters | FLOPs | Inference Time (s) |
|---|---|---|---|
| ResNet-50 | 23.51 M | 4.13 G | 0.0113 |
| EfficientNet-B4 | 17.55 M | 4.61 G | 0.0165 |
| Vision Transformer | 85.61 M | 16.85 G | 0.0189 |
| Swin Transformer | 27.81 M | 4.46 G | 0.0223 |
| ConvNeXt | 27.50 M | 4.37 G | 0.0141 |

**Key finding:** The Swin Transformer achieves the best overall trade-off between classification accuracy and computational cost, thanks to its hierarchical feature representation and shifted-window self-attention — capturing both local manipulation traces and global inconsistencies. ManTra-Net, while not matching Swin's accuracy, is notably lighter computationally, making it a practical choice when resources are limited.

![Performance vs Computational Complexity](figures/performance_vs_complexity.png)

## Repository Structure

```
image-tampering-detection-casia/
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
├── paper/
│   └── A_Comparative_Study_of_Deep_Learning_Models_for_Image_Tampering_Detection.pdf
├── models/
│   ├── resnet50_model.py
│   ├── efficientnet_b4_model.py
│   ├── vit_model.py
│   ├── swin_transformer_model.py
│   ├── convnext_tiny_model.py
│   ├── catnet_model.py
│   └── mantranet_model.py
├── results/
│   ├── resnet50_results.txt
│   ├── efficientnet_b4_results.txt
│   ├── vit_results.txt
│   ├── swin_transformer_results.txt
│   ├── convnext_tiny_results.txt
│   ├── catnet_results.txt
│   ├── mantranet_results.txt
│   └── model_comparison.xlsx
└── figures/
    └── performance_vs_complexity.png
```

## Getting Started

### Requirements
```bash
pip install -r requirements.txt
```

### Training a model
```bash
python models/swin_transformer_model.py --data_dir /path/to/CASIA_V2.0 --epochs 30 --batch_size 16
```

*(Update the exact CLI args to match your actual scripts.)*

### Dataset access
The CASIA V2.0 dataset is not included in this repository due to size/licensing. Download it from the original source and place it under a `data/` directory before running training scripts.

## Citation

If you use this work, please cite:

```bibtex
@inproceedings{mandal2026casia,
  title     = {A Comparative Study of Deep Learning Models for Image Tampering Detection Using CASIA V2.0 Dataset},
  author    = {Mandal, Santanu and Vishwakarma, Dinesh Kumar and Yadav, Ankit},
  booktitle = {IEEE Conference},
  year      = {2026},
  institution = {Delhi Technological University}
}
```

## Acknowledgments

The authors thank Dr. Dinesh Kumar Vishwakarma and Dr. Ankit Yadav, Department of Information Technology, Delhi Technological University, for their guidance and supervision, and thank the creators of the CASIA V2.0 dataset and Google Colab for the computational platform used in this research.

## License

This project is released under the [MIT License](LICENSE) (or update as appropriate for your institution's policy).
=======
# image-tampering-comparative-study
A Comparative Study of Deep Learning Models for Image Tampering Detection (CASIA V2.0)
>>>>>>> origin/main
