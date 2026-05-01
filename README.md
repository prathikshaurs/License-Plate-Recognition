## 📌 Project Overview

This project tackles the accurate detection and recognition of vehicle license plates across varied 
lighting conditions, angles, and plate designs — with applications in traffic management, law 
enforcement, parking automation, and toll collection.

The pipeline uses **YOLOv8** for anchor-based bounding box detection and **EasyOCR** for 
alphanumeric character extraction from detected plate regions. Two YOLOv8 variants (YOLOv8n 
and YOLOv8x) were trained and benchmarked side-by-side to evaluate the speed-accuracy tradeoff.

---

## ✨ Key Features

- **Dual Model Training** — YOLOv8n (lightweight/fast) vs YOLOv8x (high-accuracy), both trained for 100 epochs
- **Structured Data Pipeline** — 395 images from Roboflow, split 70/20/10 (train/val/test), preprocessed to 640×640 with auto-orientation
- **Custom OCR Integration** — `predictWithOCR.py` chains YOLOv8 bounding box detection directly into EasyOCR for end-to-end plate reading
- **Video Support** — Processes `.mp4` frame-by-frame for near-real-time detection
- **Modular Inference** — Swap models (YOLOv8n vs YOLOv8x weights) without changing the prediction script

---

## 📊 Results

Both models were trained for 100 epochs on a T4 GPU (Google Colab).

| Metric | YOLOv8n | YOLOv8x |
|---|---|---|
| Precision | High | Higher ✅ |
| Recall | High | Higher ✅ |
| mAP@0.50 | ~0.95+ | ~0.98+ |
| mAP@0.50–0.95 | ~0.75+ | ~0.83+ |
| Speed | Faster ✅ | Slower |
| OCR Output | Good | Cleaner ✅ |

**Key findings:**
- Training loss for box, classification, and DFL all show a consistent downward trend across epochs, indicating stable learning without overfitting
- Validation losses remain low and stable throughout, confirming good generalization to unseen data
- Precision and recall are high for both models, with YOLOv8x outperforming YOLOv8n across all detection metrics
- mAP@0.50 and mAP@0.50–0.95 are both high, indicating the model performs consistently across varying IoU thresholds — not just at the standard 0.50 cutoff
- YOLOv8x produces noticeably cleaner bounding boxes and more accurate OCR reads, especially on partially obscured or angled plates
- Side-by-side predictions on the same test images confirm YOLOv8x as the stronger model for production use
