# Cardiac MRI Segmentation, Clinical Parameter Estimation, and Structured VQA

> This repository documents a portfolio-oriented version of a collaborative two-person Computer Engineering graduation project. The original project was completed with equal contribution. This version focuses on system architecture, implementation details, experimental results, and my individual contribution areas.

This project presents a web-based application for automatic cardiac MRI segmentation, clinical functional parameter estimation, and structured natural-language querying based on deep learning outputs.

The system segments key anatomical structures from short-axis cardiac MR images, estimates EDV, ESV, and EF values, and presents the results through an interactive React-based web interface.

## My Contributions

Key areas I worked on include:

- Development and evaluation of 2D and 3D cardiac MRI segmentation models
- Clinical parameter estimation from LV segmentation masks
- Integration of patient-level structured outputs with a natural language query module
- Frontend interface design and backend API integration
- Preparation of visual outputs and project documentation for academic presentation

---

## Demo Preview
<img width="3006" height="2012" alt="image1" src="https://github.com/user-attachments/assets/e1741103-ff3b-4275-84b4-0ab7e59f9486" alt="Cardiac MRI Segmentation Web Interface"/>
<img width="2787" height="2012" alt="image2" src="https://github.com/user-attachments/assets/bc94922d-db9e-4a7b-8e72-1a1d04eccb31"/>
<p align="center">
  <em>Figure 1. Web-based cardiac MRI analysis interface for selecting patient cases and segmentation models, estimating clinical parameters, generating VQA-based clinical interpretations, and visualizing ED/ES segmentation overlays.</em>
</p>

---

## Project Overview

This project provides an end-to-end pipeline for cardiac MRI analysis:

- Automatic segmentation of cardiac anatomical structures:
  - Left Ventricle (LV)
  - Right Ventricle (RV)
  - Myocardium (MYO)

- Estimation of clinical functional parameters:
  - End-Diastolic Volume (EDV)
  - End-Systolic Volume (ESV)
  - Ejection Fraction (EF)

- Visualization of segmentation overlays through a web interface

- VQA-based natural language querying over structured segmentation and clinical metric outputs

The system consists of a FastAPI-based backend for inference and result processing, and a React + Vite frontend for interactive visualization.

---

## Example Segmentation Output

<p align="center">
  <<img width="997" height="589" alt="Segmentation outputs" src="https://github.com/user-attachments/assets/f6399d8b-5364-422b-baea-4623c2017c97" />
</p>

<p align="center">
  <em>Figure 2. Representative cardiac MRI segmentation output comparing the original MR slice, ground-truth mask, model prediction, and overlay visualizations for RV, MYO, and LV structures.</em>
</p>


---

## Key Features

- Deep learning-based cardiac MRI segmentation
- Support for LV, RV, and MYO anatomical classes
- EDV, ESV, and EF estimation from segmentation masks
- ED and ES phase-based analysis
- Web-based visualization of segmentation overlays
- Natural language querying over patient-level structured results
- FastAPI backend and React frontend integration
- Modular project structure for backend, frontend, and model notebooks

---

## System Architecture

```mermaid
flowchart TD
    A["Frontend<br/>React + Vite"] -->|HTTP API Requests| B["Backend<br/>FastAPI"]

    B --> C["Model Inference Layer"]
    C --> D["Deep Learning Segmentation Models<br/>2D U-Net / 2D ResU-Net / Attention ResU-Net / 3D U-Net / 3D ResU-Net"]

    D --> E["Segmentation Outputs<br/>LV / RV / MYO Masks"]

    E --> F["Clinical Parameter Estimation<br/>EDV / ESV / EF"]
    E --> G["Segmentation Overlay Visualization"]

    F --> H["VQA / Natural Language Query Module"]

    G --> I["Web Interface Results"]
    H --> I
```

The system consists of a React + Vite frontend for user interaction, a FastAPI backend for inference and result processing, deep learning segmentation models for cardiac MRI analysis, a clinical parameter estimation module for EDV, ESV, and EF computation, and a VQA module for natural language querying over structured patient-level outputs.

## Dataset

This project uses the ACDC MICCAI 2017 dataset, which contains short-axis cardiac MRI volumes with expert annotations.

| Property | Description |
|---|---|
| Dataset | ACDC - Automated Cardiac Diagnosis Challenge |
| Source | MICCAI 2017 |
| Image Type | Short-axis cardiac MRI |
| Classes | Background, RV, MYO, LV |
| Phases | End-Diastole (ED), End-Systole (ES) |


## Deep Learning Models

The following architectures were evaluated during the research phase:

| Model | Purpose |
|---|---|
| 2D U-Net | Baseline encoder-decoder segmentation model |
| 2D ResU-Net | Residual U-Net architecture for improved feature learning |
| Attention ResU-Net | Residual U-Net with attention mechanisms |
| 3D U-Net | Volumetric segmentation using 3D spatial context |
| 3D ResU-Net | Residual 3D U-Net architecture |

The final web interface focuses on patient-level visualization, clinical metric presentation, and natural language querying.


## Experimental Results

The segmentation models were evaluated on the test set using Dice score, IoU, HD95, and test loss. Among the evaluated architectures, the 2D ResU-Net and 2D Attention ResU-Net achieved the highest overall Dice scores, while the 3D U-Net produced competitive boundary-based HD95 results.

### Overall Test Performance

| Model | Test Loss | Mean Dice |
|---|---:|---:|
| 2D U-Net | 0.111 | 0.917 |
| 2D ResU-Net | 0.102 | 0.924 |
| 2D Attention ResU-Net | 0.099 | 0.924 |
| 3D U-Net | 0.206 | 0.845 |

### Per-Class Dice Scores

| Model | BG | RV | MYO | LV |
|---|---:|---:|---:|---:|
| 2D U-Net | 0.998 | 0.908 | 0.885 | 0.957 |
| 2D ResU-Net | 0.998 | 0.920 | 0.890 | 0.959 |
| 2D Attention ResU-Net | 0.998 | 0.926 | 0.888 | 0.958 |
| 3D U-Net | 0.998 | 0.825 | 0.796 | 0.913 |

The 2D ResU-Net and 2D Attention ResU-Net models achieved the strongest overall segmentation performance. The LV class obtained the highest anatomical Dice scores, while MYO and RV were more challenging due to thinner structures and higher anatomical variability.

### 2D ResU-Net Training Curves

The 2D ResU-Net model showed stable convergence, with training and validation loss decreasing consistently throughout the training process. Per-class Dice curves indicate strong LV segmentation performance, while RV and MYO remained more challenging due to anatomical variability and smaller structure size.

| Loss Curve | Per-Class Dice Curve |
|---|---|
| ![2D ResU-Net loss curve]<img width="717" height="510" alt="image" src="https://github.com/user-attachments/assets/f51a95b2-7951-455c-94a7-22da9f40f3b0" /> | ![2D ResU-Net per-class Dice curve] |




## Clinical Parameter Estimation

Clinical functional parameters are calculated from the predicted Left Ventricle (LV) segmentation masks.

| Parameter | Description |
|---|---|
| EDV | End-Diastolic Volume |
| ESV | End-Systolic Volume |
| EF | Ejection Fraction |

The ejection fraction is calculated as:

```text
EF (%) = ((EDV - ESV) / EDV) × 100
```

## Results Summary

The experimental evaluation showed that 2D-based models provided more stable segmentation performance on the ACDC dataset. Among the evaluated architectures, the 2D ResU-Net model achieved the most reliable overall performance for cardiac structure segmentation.

### Clinical Metric Error

| Metric | Mean Absolute Error |
|---|---:|
| EDV | 6.58 mL |
| ESV | 6.27 mL |
| EF | 3.11 percentage points |

> These results are based on the final evaluation setup used in the graduation project.

## VQA-Based Natural Language Querying

The VQA module allows users to query patient-level cardiac MRI analysis results using natural language.

Instead of directly interpreting raw MRI images, the module uses structured outputs obtained from:

- Segmentation masks
- Clinical parameter calculations
- Patient-level EDV, ESV, and EF values
- Rule-based clinical interpretation outputs

Example queries:

- What is the ejection fraction of this patient?
- Is the EF value within the normal range?
- What are the EDV and ESV values?
- Which cardiac structures were segmented?
- Can these results be clinically interpreted?

This design makes the system more interpretable and traceable because the answers are based on measurable segmentation and clinical metric outputs rather than unrestricted image interpretation.

## Example VQA Queries

| Query Type | User Query | System Response |
|---|---|---|
| Numerical parameter query | What are the EDV, ESV, and EF values of patient001? | EDV: 297.9 mL, ESV: 240.1 mL, EF: 19.4%. |
| Patient summary query | Can you briefly summarize the results for patient001? | For patient001, EDV was calculated as 297.9 mL, ESV as 240.1 mL, and EF as 19.4%. |
| Clinical boundary query | Is the left ventricle dilated? | A definitive classification requires indexed LV volume, BSA, and sex-specific reference ranges. |
| Out-of-scope clinical query | What treatment should be applied to this patient? | Treatment decisions must be made by a qualified medical professional. |

## Tech Stack

| Layer | Technologies |
|---|---|
| Backend | Python, FastAPI, PyTorch, NumPy, SimpleITK, NiBabel |
| Frontend | React, Vite, Axios, Material UI |
| Tools | Git, GitHub, VS Code, Jupyter Notebook |

## Repository Structure

```text
cardiac-mri-segmentation-vqa/
├── backend/
│   ├── app/
│   ├── models/
│   ├── services/
│   ├── main.py
│   └── requirements.txt
│
├── frontend/
│   ├── src/
│   ├── public/
│   └── package.json
│
├── notebooks/
│   └── model_training_and_evaluation.ipynb
│
├── README.md
└── .gitignore
```

> Large generated files, trained model checkpoints, and dataset files are not included in this repository.

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/zehra-kaya16/cardiac-mri-segmentation-vqa.git
cd cardiac-mri-segmentation-vqa
```

### 2. Backend setup

```bash
cd backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload
```

The backend runs at:

```text
http://127.0.0.1:8000
```

### 3. Frontend setup

```bash
cd frontend
npm install
npm run dev
```

The frontend runs at:

```text
http://localhost:5173
```

## Notes

Large generated files, trained model checkpoints, and dataset files are not included in this repository.

This repository focuses on:

- Source code
- Web application structure
- Model integration logic
- Example visual outputs
- Project documentation

## Academic Context

This project was developed as a Computer Engineering graduation project. It combines medical image segmentation, clinical parameter estimation, and natural language querying for cardiac MRI analysis.

## Medical Disclaimer

This project is intended for academic and research purposes only. The outputs are generated from automatic segmentation results and are not intended for direct clinical decision-making.

## Limitations

- The system was developed for academic and research purposes.
- Trained model checkpoints and the full ACDC dataset are not included due to size and access limitations.
- The VQA module answers questions based on structured segmentation and clinical metric outputs, not direct free-form image diagnosis.
- Clinical outputs should not be used for medical decision-making.

## License

This project is provided for academic and educational purposes.

## Acknowledgements

- ACDC MICCAI 2017 Challenge organizers
- PyTorch community
- FastAPI community
- React and Vite communities
