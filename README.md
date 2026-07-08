# Cardiac MRI Segmentation and Clinical Parameter Estimation with VQA

Web-based application for automatic cardiac MRI segmentation, clinical functional parameter estimation, and VQA-based natural language querying using deep learning models.

The system segments key anatomical structures from short-axis cardiac MR images, estimates EDV, ESV, and EF values, and presents the results through an interactive React-based web interface.

> This repository is a personal fork of the original graduation project repository, prepared for individual contribution tracking and portfolio presentation.

---

## Demo Preview
<img width="3006" height="2012" alt="image1" src="https://github.com/user-attachments/assets/e1741103-ff3b-4275-84b4-0ab7e59f9486" alt="Cardiac MRI Segmentation Web Interface"/>
<img width="2787" height="2012" alt="image2" src="https://github.com/user-attachments/assets/bc94922d-db9e-4a7b-8e72-1a1d04eccb31"/>
<p align="center">
  <em>Web interface for selecting patient cases and visualizing segmentation outputs with clinical parameters.</em>
</p>

---

## 📌 Project Overview

This project provides an end-to-end pipeline for:

- Automatic segmentation of:
  - Left Ventricle (LV)
  - Right Ventricle (RV)
  - Myocardium (MYO)
- Estimation of cardiac functional parameters:
  - End-Diastolic Volume (EDV)
  - End-Systolic Volume (ESV)
  - Ejection Fraction (EF)
- Visualization of segmentation overlays in a web interface

The system consists of a FastAPI-based backend that performs model inference and a React-based frontend that allows users to interactively view results.

---

## 📌 Proje Özeti

Bu proje, kalp MR görüntülerinin derin öğrenme tabanlı otomatik bölütlenmesi ve fonksiyonel kardiyak parametrelerin hesaplanması için uçtan uca bir sistem sunmaktadır.

Sistem şu işlemleri gerçekleştirmektedir:

- Sol ventrikül (LV), sağ ventrikül (RV) ve miyokard (MYO) bölütlemesi
- Kardiyak fonksiyonel parametrelerin hesaplanması:
  - Diyastol Sonu Hacim (EDV)
  - Sistol Sonu Hacim (ESV)
  - Ejeksiyon Fraksiyonu (EF)
- Web arayüzü üzerinden segmentasyon çıktılarının görselleştirilmesi

Backend FastAPI ile, frontend ise React (Vite) kullanılarak geliştirilmiştir.

---

## 🏗 System Architecture

```text
Frontend (React + Vite)
        |
        | HTTP API Requests
        v
Backend (FastAPI)
        |
        | Model Inference
        v
Deep Learning Segmentation Model
        |
        v
Overlay Images + EDV/ESV/EF Results


Model & Dataset
Dataset
-ACDC (Automated Cardiac Diagnosis Challenge) – MICCAI 2017
-Short-axis cardiac MRI volumes
-Ground truth labels for LV, RV, and MYO

Model
-2D Residual U-Net based architecture
-Slice-based inference with volume-level aggregation
-Post-processing for ED/ES phase detection and volume computation

🧰 Tech Stack
Backend
-Python
-FastAPI
-PyTorch
-NumPy
-SimpleITK / NiBabel (for medical image processing)

Frontend
-React
-Vite
-Axios
-Material UI (MUI)

Tools
-Git & GitHub
-VS Code


📤 API Outputs
Backend returns:
-ED overlay image URL
-ES overlay image URL
-EDV (ml)
-ESV (ml)
-EF (%)

Pull Request submitted and merged:
👉 Integrate frontend and backend with UI updates

📄 License
This project is provided for academic and educational purposes.

⭐ Acknowledgements
MICCAI ACDC Challenge organizers
Open-source PyTorch and FastAPI communities
