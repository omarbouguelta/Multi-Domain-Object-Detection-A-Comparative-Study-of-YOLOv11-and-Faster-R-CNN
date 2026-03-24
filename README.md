# Comparative analysis of the YOLO algorithm and R-CNNs for pattern recognition
**Master’s Thesis | University of Science and Technology of Oran Mohamed-BoudiaF (USTO-MB)**

##  1. Introduction
This research presents an in-depth comparative study between **Region-based Convolutional Neural Networks (Faster R-CNN)** and the **You Only Look Once (YOLOv11)** algorithm. As computer vision transitions from academic theory to real-world deployment, understanding the trade-off between spatial precision and temporal efficiency is critical. This project evaluates these architectures across three distinct, high-complexity datasets to provide a definitive guide on model selection for AI practitioners.

---

##  2. Theoretical Framework & Architectures
The project analyzes the evolution of object detection from traditional methods to deep learning breakthroughs:

### A. Faster R-CNN (Two-Stage Detector)
* **Backbone:** ResNet-50 for robust feature extraction.
* **Mechanism:** Utilizes a **Region Proposal Network (RPN)** to identify object candidates followed by a dedicated classification and bounding-box regression.
* **Focus:** Maximizing **IoU (Intersection over Union)** and spatial accuracy.

<img width="1193" height="670" alt="image" src="https://github.com/user-attachments/assets/6545b07d-53b2-4388-be14-e906c16190f4" />


### B. YOLOv11 (One-Stage Detector)
* **Architecture:** CSPDarknet-based backbone with an integrated head for simultaneous box prediction and class probability.
* **Mechanism:** Treats object detection as a single regression problem, enabling end-to-end optimization.
* **Focus:** Minimizing **Inference Latency** for real-time edge deployment.

<img width="1192" height="668" alt="image" src="https://github.com/user-attachments/assets/4a44c6bf-0d86-4c25-b111-0eeeaed837ce" />
<img width="1197" height="670" alt="image" src="https://github.com/user-attachments/assets/c9cf526d-1fcf-432a-a929-a983455070a9" />


---

##  3. Multi-Domain Dataset Analysis
To stress-test the models, three diverse datasets were curated and pre-processed:

### I. Public Safety: Scorpion Detection
* **Challenge:** High background camouflage and small object signatures.
* **Goal:** Early detection in residential areas to prevent biological threats.

### II. Infrastructure: Vehicle Classification
* **Classes:** Car, Van, Pickup, Truck, Camper.
* **Challenge:** High inter-class similarity (e.g., distinguishing a Van from a Pickup in motion).

### III. Remote Sensing: Satellite Imagery
* **Challenge:** Low-resolution features and extreme top-down perspectives.
* **Goal:** Strategic identification of assets in wide-area surveillance.

> <img width="1201" height="677" alt="image" src="https://github.com/user-attachments/assets/0463f51a-ed12-4611-acfe-255c8b5a9682" />

---

##  4. Training Methodology & Environment
Models were developed using a standardized pipeline to ensure fair comparison:
* **Frameworks:** PyTorch, Ultralytics, TensorFlow.
* **Pre-processing:** Image resizing, normalization, and data augmentation (flipping, color jittering).
* **Hardware:** Benchmarked on local GPU (RTX 4070) and cloud environments (Google Colab/Kaggle).
* **Optimization:** Evaluation of Loss Functions including GIoU (Generalized Intersection over Union) and Cross-Entropy.

---

##  5. Quantitative Results & Key Findings

### Performance Comparison Table
| Metric | YOLOv11 | Faster R-CNN |
| :--- | :--- | :--- |
| **mAP@0.5** | 76.53% | **98.2%** |
| **Inference Speed (ms)** | **355ms** | 1513ms |
| **F1-Score** | 0.45 | **1.0** |
| **Overall speed** | Faster | Slower |

### Critical Technical Insights
1. **The Efficiency Frontier:** YOLOv11 demonstrated a **4.3x speed advantage** over Faster R-CNN, confirming its dominance for real-time traffic monitoring systems.
2. **Precision vs. Recall:** Faster R-CNN achieved a perfect F1-score in specialized tasks, proving more reliable for "Zero-Failure" applications like satellite-based strategic planning.
3. **Class Confusion Analysis:** Through Normalized Confusion Matrices, it was observed that YOLOv11 struggled with **low-salience objects** and similar vehicle shapes, whereas Faster R-CNN’s two-stage refinement successfully differentiated between Vans and Trucks.

<img width="1192" height="673" alt="image" src="https://github.com/user-attachments/assets/c20ed266-1d74-4add-8ae2-acc191d1e1a9" />
<img width="1206" height="678" alt="image" src="https://github.com/user-attachments/assets/f58b7520-4fa3-45c6-900a-6ae228c64022" />
<img width="1206" height="677" alt="image" src="https://github.com/user-attachments/assets/b1879cff-fe1e-41d1-b2fd-cdca979d5c61" />



---

##  6. Conclusion & Recommendations
The research concludes that:
* **YOLOv11** is the optimal choice for **Dynamic Environments** (Self-driving cars, live surveillance).
* **Faster R-CNN** is the optimal choice for **Static, High-Stake Environments** (Medical imaging, Strategic aerial analysis).

---

##  Implementation & Experimental Demos

This repository provides a complete end-to-end pipeline, from camouflaged dataset training to real-world inference.
<br> <a href="https://drive.google.com/file/d/1UrSWufEi__7LWddw_j7Xks9RRu6uZ-5w/view?usp=sharing"> download Scrorpion detection model here </a>
### 1. Training Workflow (Scorpion Dataset)
* **[Scorpion Training Pipeline](./RCNN/scorpion_training_faster_rcnn.ipynb):** Comprehensive training script utilizing Faster R-CNN with a ResNet-50 backbone. 
  * **Highlights:** Custom loss tracking (RPN vs. Classification), data augmentation for low-salience targets, and loss convergence visualization.

### 2. Inference & Evaluation
* **[Single Image Test Bench](./RCNN/single_image_test_model.ipynb):** Used for precision verification on high-resolution stills. It automatically calculates **Inference Latency (ms)** and generates bounding boxes with confidence scores.
* **[Video Detection ](./RCNN/video_test_model_resnet.ipynb):** A frame-by-frame inference script designed to process recorded .mp4 or .avi files. This tool is essential for benchmarking model performance on long-duration footage, allowing for the analysis of temporal consistency and detection stability across pre-recorded environmental sequences.
