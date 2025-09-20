# TF-Net: Deep Learning Empowered Tiny Feature Network for Night-Time UAV Detection  

[![Paper](https://img.shields.io/badge/Conference-WiSATS%202023-blue)](https://link.springer.com/chapter/10.1007/978-3-031-34851-8_1)  

This repository contains the official implementation, dataset links, and experimental results of our paper:  

**TF-Net: Deep Learning Empowered Tiny Feature Network for Night-Time UAV Detection**  
*by Maham Misbah, Misha Urooj Khan, Zhaohui Yang & Zeeshan Kaleem*  

---

## 📖 Abstract  

Unmanned Aerial Vehicles (UAVs) have gained popularity across military and commercial domains, but their unauthorized usage poses serious security concerns. Detecting UAVs at **night in complex backgrounds** is especially challenging due to poor visibility.  

We propose **TF-Net (Tiny Feature Network)**, an **improved version of YOLOv5s**, specifically designed for **night-time UAV detection using infrared (IR) images**. TF-Net introduces kernel-based modifications in the **backbone** and **neck** of YOLOv5s, improving detection accuracy and robustness under challenging weather conditions.  

**Highlights:**  
- Built on YOLOv5s with optimized kernel sizes.  
- Lightweight (10.8 MB model size).  
- Achieves **95.7% precision, 84% mAP@0.5, and 44.8% IoU**.  
- Outperforms YOLOv5 (s, m, l, n) in accuracy and robustness.  

---

## 📂 Dataset  

We created a dataset of **~3,900 IR images** of UAVs captured at night across **various environmental conditions**:  
- 🌆 Urban scenes  
- ☁️ Dense clouds  
- 🏠 Indoor  
- 🌫️ Foggy  
- 🌿 Shrubs  
- ✈️ Different altitudes  

- **Train/Test split:** 80/20 (3100 training, 791 testing images)  
- **Annotations:** Bounding boxes + labels in YOLO format  
- **Preprocessing:** Resized to 416×416, contrast enhancement, mosaic augmentation  

Dataset is available on **[Roboflow](https://universe.roboflow.com/uav-project-eia1l/uav_ir)**.  

---

## ⚙️ Architecture  

TF-Net consists of **four main blocks**:  

1. **Input Block**: Mosaic Data Augmentation (MDA) & Adaptive Image Filling (AIF)  
2. **Backbone**: Cross Stage Partial Networks (CSP) + Spatial Pyramid Pooling (SPP)  
3. **Neck**: Feature Pyramid Network (FPN) with optimized kernel sizes  
4. **Head**: Multi-scale anchor-based detection  

<div align="center">  
  <img src="aaf16ddd-a06a-403c-94c5-816dcc4f1838.png" width="600"/>  
  <p><em>Proposed TF-Net architecture</em></p>  
</div>  

---

## 🛠️ Training Setup  

- Framework: **PyTorch (YOLOv5 as base)**  
- Input size: `416×416`  
- Epochs: `300` (early stopping applied)  
- Optimizer: Adam + SGD  
- Learning rate: `0.01 → cosine decay`  
- Hardware: Google Colab (Tesla K80 / T4, 12GB RAM)  

---

## 📊 Results  

### Performance vs YOLOv5 variants  

| Model   | Precision (%) | Recall (%) | mAP@0.5 (%) | IoU (%) | Size (MB) |
|---------|--------------|------------|-------------|----------|-----------|
| **TF-Net** | **95.7** | 77.4 | **84.0** | **44.8** | **10.8** |
| YOLOv5s | 93.1 | 78.4 | 80.3 | 43.4 | 14.8 |
| YOLOv5m | 91.2 | 78.1 | 83.6 | 43.3 | 42.1 |
| YOLOv5l | 90.8 | 75.3 | 82.9 | 42.2 | 92.8 |
| YOLOv5n | 92.3 | 76.0 | 80.5 | 43.5 | 3.8 |

---

### Graphical Results  

<div align="center">  
  <img src="results_precision_recall.png" width="450"/>  
  <p><em>Precision and Recall trends across epochs</em></p>  
</div>  

<div align="center">  
  <img src="results_map_iou.png" width="450"/>  
  <p><em>mAP@0.5 and IoU comparison with YOLOv5 models</em></p>  
</div>  

---

### Qualitative Results  

- ✅ Robust across **complex backgrounds** (urban, fog, shrubs, cloudy)  
- ✅ Detects **multi-size UAVs** (small, medium, large) with high accuracy  
- ✅ Achieves **98 FPS** inference speed on Tesla T4 GPU  

<div align="center">  
  <img src="sample_detections.png" width="600"/>  
  <p><em>Sample detections on IR UAV dataset under challenging conditions</em></p>  
</div>  

---

## 🚀 Reproduction  

1. Clone repository:  
```bash
git clone https://github.com/your-username/TF-Net-UAV-Detection.git
cd TF-Net-UAV-Detection

2. Install dependencies:
pip install -r requirements.txt

3. Download dataset from Roboflow: https://app.roboflow.com/tfnet-night-vision/mul/4

4. Train TF-Net:
python train.py --img 416 --batch 16 --epochs 300 --data data.yaml --cfg tfnet.yaml --weights ''

5.Run inference:
python detect.py --weights runs/train/exp/weights/best.pt --img 416 --source data/test/images

##📜 Citation

If you use this work, please cite:

@inproceedings{misbah2023tfnet,
  title={TF-Net: Deep Learning Empowered Tiny Feature Network for Night-Time UAV Detection},
  author={Misbah, Maham and Khan, Misha Urooj and Yang, Zhaohui and Kaleem, Zeeshan},
  booktitle={Wireless and Satellite Systems (WiSATS 2023)},
  pages={3--18},
  year={2023},
  publisher={Springer}
}

📌Acknowledgments
This work was supported by the Higher Education Commission (HEC), Pakistan under the NRPU 2021 Grant 15687.
