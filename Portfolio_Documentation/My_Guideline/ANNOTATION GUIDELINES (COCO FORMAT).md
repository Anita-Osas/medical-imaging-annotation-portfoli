# Annotation Guidelines (COCO Format)

## Medical Chest X-ray Annotation

**Project Pathologies:**  
Pericardial Effusion, Pneumothorax, Pleural Effusion, Bronchopneumonia, Lobar Pneumonia  

**Dataset Size:** 50 chest X-ray images (10 per pathology)  

**Annotation Types:**  
- Polygon segmentation  
- Bounding boxes  

**Export Format:** COCO JSON  

**Annotation Tool:** Label Studio  

---

## 1. Project Overview

This document outlines the annotation guidelines followed during the annotation of five common thoracic pathologies on chest X-rays.

A total of **50 de-identified radiographs** were annotated, with **10 images per pathology**, using clinically grounded radiology principles. The objective was to produce **high-quality, clinically meaningful training data** suitable for healthcare computer vision models.

This project demonstrates:

- Strong understanding of chest X-ray anatomy and pathology  
- Precision and consistency in medical image annotation  
- Ability to work with industry-standard formats (COCO JSON)  
- Careful clinical reasoning and attention to edge cases  

All annotations were completed in **Label Studio**, with deliberate review of anatomical boundaries, disease presentation patterns, and ambiguous regions.

---

## 2. General Annotation Approach

### Image Sources
All images were obtained from **publicly available, fully de-identified medical imaging datasets**.

### Core Principles Followed

#### 2.1 Polygon-Based Annotation for Accuracy
Most thoracic pathologies do not have sharp or rectangular boundaries. Polygon segmentation was used to accurately trace:

- Fluid collections and their meniscus curves  
- Areas of lung consolidation  
- The pleural line in pneumothorax  
- Irregular, patchy opacity patterns in pneumonia  

#### 2.2 Respect for Anatomical Boundaries
Annotations were strictly confined to pathological regions and were carefully kept within anatomical limits.

**I avoided crossing into:**
- Ribs and other bony structures  
- The spine  
- The contralateral lung hilum  
- Normal mediastinal structures  
- Normal lung tissue (except where directly affected)

**I excluded:**
- Normal lung markings and vessels  
- Air-filled lung spaces  
- Artifacts and overlying external structures  
- The diaphragm unless directly involved by pathology  

Natural opacity transitions were followed rather than forcing artificially sharp borders.

---

## 3. Pathology-Specific Guidelines

### 3.1 Pericardial Effusion

**Radiographic Indicators:**
- Enlarged, globular (“water bottle”) cardiac silhouette  
- Symmetrical widening of the heart borders  
- Loss of normal cardiac contour definition  

**Annotation Method:**
- A **bounding box** was drawn around the entire enlarged cardiac silhouette.
- Since pericardial effusion is inferred rather than directly visualized, the bounding box follows the outer margin of the pericardial sac as seen on the X-ray.

**Avoided:**
- Annotating only part of the heart  
- Including adjacent normal mediastinal structures  

---

### 3.2 Pneumothorax

**Radiographic Indicators:**
- Thin, sharp white line representing the visceral pleural edge  
- Absence of lung markings beyond this line  

**Annotation Method:**
- The clinically significant feature—the **visceral pleural line**—was annotated.
- A **polygon** was used to trace the pleural edge from its visible start to end point and closed back onto itself.
- This approach was used instead of outlining the entire collapsed lung, which is largely featureless.

**Avoided:**
- Including normal lung tissue beyond the pleural line  
- Misidentifying skin folds or scapular edges as pleural lines  

---

### 3.3 Pleural Effusion

**Radiographic Indicators:**
- Basal white opacity  
- Upward-curving meniscus sign  
- Blunted costophrenic angle  
- Fluid layering along the diaphragm  

**Annotation Method:**
- The fluid collection was traced using polygon segmentation.
- Annotation typically started at the blunted lateral costophrenic angle.
- The meniscus curve (concave upward) was carefully followed.
- For large effusions, tracing extended medially along the mediastinum.
- Annotation remained below visible lung markings.

**Avoided:**
- Annotating the entire diaphragm when only the angle was involved  
- Combining pneumonia and effusion into a single annotation  

---

### 3.4 Bronchopneumonia

**Radiographic Indicators:**
- Multiple patchy, ill-defined opacities  
- Fuzzy borders  
- Frequent lower zone involvement  
- Possible air bronchograms  

**Annotation Method:**
- Each patch of abnormal opacity was annotated **separately**.
- Loose polygons were used to reflect the naturally hazy borders.
- No attempt was made to force sharp or anatomical boundaries.

**Avoided:**
- Connecting clearly separate patches  
- Over-precision in inherently indistinct infiltrates  
- Forcing lobar boundaries where none were visible  

---

### 3.5 Lobar Pneumonia

**Radiographic Indicators:**
- Dense consolidation occupying an entire anatomical lobe  
- Sharp borders along fissure lines (when visible)  
- Silhouette sign (loss of heart or diaphragm border)  

**Annotation Method:**
- A **single polygon** was used to cover the entire consolidated lobe.
- Fissure lines were followed when visible.
- Where fissures were obscured, the outer edge of dense opacity was used.
- Air bronchograms within the consolidation were included.

**Avoided:**
- Extending into adjacent unaffected lobes  
- Excluding regions obscured by silhouette sign  

---

## 4. Quality Control Process

Each annotation underwent a three-step review process:

### Consistency Check
- Verified polygons accurately followed opacity borders  
- Confirmed correct pathology labels  
- Ensured annotations did not overlap incorrectly  

### Clinical Accuracy Check
- Cross-checked findings against standard radiology criteria  
- Verified classic signs (meniscus sign, silhouette sign)  
- Reconfirmed pneumothorax pleural lines  

### Technical Validation
- Confirmed COCO JSON exports loaded without errors  
- Reviewed annotations using the Label Studio viewer  

---

## 5. Tools & Workflow

- **Annotation Software:** Label Studio  
- **Export Format:** COCO JSON (polygon segmentation + bounding boxes)  
- **Workflow:** Systematic image review prior to annotation  
- **Time Investment:** ~8–12 minutes per image  

---

## 6. Example Annotation Note

**Pleural Effusion Case Example:**

> “The left costophrenic angle is clearly blunted with a classic upward meniscus curve. A polygon was drawn following the fluid density, respecting the soft curvature of the meniscus and stopping medially at the diaphragm border.”

---

## Acknowledgments

I am grateful to **Yamah Princewill, B.Rad., Radiologist**, for providing radiology guidance and performing an independent review of selected annotations.  
His cross-checking supported clinical accuracy, particularly in anatomical localization and interpretation of radiographic signs.
