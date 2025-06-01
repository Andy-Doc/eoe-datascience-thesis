

**Medical Images Analysis in Patients with Eosinophilic Esophagitis**  
_MSc Data Science Thesis Project_

---

## Overview

This repository contains the code, results and documentation for a Master of Data Science thesis focused on the trainig of machine learning models for the detection and classification of **Eosinophilic Esophagitis (EoE)** using [histopathology images / .svs files / WSI / etc.].

The goal is to assess the YOLO11 machine learning model’s effectiveness for automated 
eosinophil segmentation and detection in histological images to enhance EoE diagnostic accuracy 
in the real-world environment using histological images (digital pathology images) with different 
quality of staining, tissue fixation and sectioning techniques in order to assist pathologists and 
clinicians in diagnosing EoE, by helping pathologist to find and indicate hpf with the highest 
number of eosinophils for more accurate assessment of eosinophil counts (PEC = peak eosinophil count).

---

## Thesis Objectives/Tasks

- collect histological digital pathology images (histological images in .svs format of the 
whole slide images (WSI)) from real world clinical practice in collaboration with 
gastroenterologists, allergists, endoscopists and pathologists from Hospital (for adults) 
and Medical Research Center (for children); 
- create labeling protocol for digital pathology images (Appendix 1 of the thesis); 
- perform manual labeling of the digital pathology images in QuPath tool (Bankhead et al., 2017) for 3 distinct classes: 1) tissue/background, 2) intact eosinophils, 3) non-intact 
eosinophils/eosinophilic granules; 
- develop data set (using histological images from real world clinical practice with different 
quality of staining, tissue fixation and sectioning techniques); 
- train the YOLO11 model (Ultralytics YOLO11 Docs, date of access: 25.03.2025) for 
detection and segmentation of eosinophils on WSIs; 
- assess the efficacy of YOLO11 model (Ultralytics YOLO11 Docs, date of access: 
25.03.2025) trained on histological images with different quality of staining, tissue fixation 
and sectioning techniques using the following metrics: Intersection over Union (IoU), 
Precision, Recall, F1-measure; 
- develop inference for the YOLO11 (Ultralytics YOLO11 Docs, date of access: 
25.03.2025) pretrained model to generate GeoJSON files with predicted annotations 
(bounding boxes and polygons) and hpf box for more precise and convenient PEC 
calculation in QuPath application (Bankhead et al., 2017) by pathologist; additionally 
heatmap picture is generated to help pathologists find the most infiltrated by eosinophils 
part of the WSI and check the number of eosinophils. 
- the exploratory task aims to calculate PEC from generated GeoJSON files using data on 
intact intraepithelial eosinophils predicted by the YOLO11 model. 
---

## Materials and Methods

- Data preprocessing: [refer to convert_data.ipynb]
- Model(s):
  - YOLO 11  
- Evaluation Metrics: [IoU, Precision, Recall, F1-measure]

---

## 📁 Repository Structure

### eoe-datascience-thesis/        <-- main folder = root of the repository

- `svs_exp/`  
  Folder for raw data files.  
  ➤ Put your `.svs` files and corresponding `.GeoJSON` files with annotations here.  
  ➤ Required for dataset preparation using `convert_data.ipynb`.  
  ➤ Classes in annotations: `'eos'`, `'eosg'`, `'Tissue'`.  
  ⚠️ *This folder is empty by default!*



- `convert_data.ipynb`  
  Jupyter notebook for converting `.svs` files and generating:  
  - `yolo_dataset/` (YOLO-format dataset)  
  - `segmentation_dataset/` (segmentation-format dataset)


- `yolo11_eosinophil_seg5/`  
  Folder with trained YOLO11 model and results:  
  - `last.pt`, `best.pt` (weights)  
  - Training logs and graphs


- `Training.ipynb`  
  Jupyter notebook for training the YOLOv8 model using the `ultralytics` package.


- `svs_inf/`  
  Folder for inference input data.  
  ➤ Place `.svs` files here for processing by `inference.ipynb`.

  ⚠️ *This folder is empty by default!*


- `inference.ipynb`  
  Jupyter notebook for performing inference:  
  - Processes `.svs` files from `svs_inf/`  
  - Generates `.GeoJSON` files with predictions  
  - Output is compatible with [QuPath](https://qupath.github.io) for visualization
  
  ⚠️ open `.svs` file in QuPath, add `.GeoJSON` file to the corresponding `.svs` file -> view bboxes and polygons with predictions for 'eos' class


- `inference10/`  
  Output folder created by `inference.ipynb`.  
  ➤ Contains subfolders named after processed `.svs` files with generated `.GeoJSON` files (results of `'eos'` precitions).  
  ⚠️ *Empty until inference is run.*


- `geoparse/`  
  Folder for running post-processing on GeoJSON outputs.  
  ➤ Put here your generated `.GeoJSON` files from the subfolders of inference10/ folder.
  
  ➤ ⚠️ Make sure to update file paths in the notebook:  
    ```python
    file_path = '1007401_detections_merged.geojson'
    output_geojson = '1007401_peak_hpf_output14_20_90_dfs_poly_merged.geojson'
    ```
  ➤ Run `geoparse14_20_90_dfs_poly_merged.ipynb` here -> get output_geojson = '1007401_peak_hpf_output14_20_90_dfs_poly_merged.geojson, use it together with initial `.svs` file to find the Peak hpf area with the highest number of eosinophils per high power field which correspond to 0.3 mm^2 (2144*2144 pixels or 548*548μm @ 0.2555 μm/pixel)


- `thesis/`  
  Will contain the final thesis PDF.  
  ⚠️ *To be added later.*


- `README.md`  
  This file.


---

## Setup & Installation

1. Clone the repo:
   ```bash
   git clone https://github.com/yourusername/eoe-datascience-thesis.git
   cd EoE-MT

2. Create and activate a virtual environment:
```
python -m venv venv
source venv/bin/activate  # or `venv\Scripts\activate` on Windows
```

3. Install dependencies:
pip install -r requirements.txt <------- THIS FILE WILL TO BE UPDATED IF NEEDED


## Data preparation:

*for instructions see the structure of the repository above*

---
## Train the model:

*for instructions see the structure of the repository above*

---
## Model training results:

The model demonstrated high efficiency with a recall of 0.97669 and a Jaccard index (IoU) 
of 0.94, indicating a very good ability to accurately localize and segment eosinophils in the 
epithelial layer of the esophagus. F1-score reached 0.93 for masks and 0.95 for bounding boxes. 

More detailed visualizations and discussions are available in the `yolo11_eosinophil_seg5/` directory and in the thesis report.

---
## Thesis
The full thesis is not available publicly.

---
## Author
[Andy-Doc]

[National Research University Higher School of Economics, Faculty of Computer Science]

---
## License
This project is licensed under the MIT License – see the LICENSE file for details.

---
## Acknowledgements
Supervisors: [Name(s)] to be added later upon their agreement to mention the names here

Institution: [National Research University Higher School of Economics, Faculty of Computer Science]

Dataset Source: [Unique dataset from adult and clidren hospitals, see above]

Dataset Size and Number of Files: [58.783 gigabytes for 105 .svs files with only H&E staining]

Special thanks to [collaborators and/or contributors] to be added later upon their agreement to mention the names here

---
