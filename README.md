# Mice Run Thermography Dataset

This repository contains thermographic images and metadata recorded from 11 **C57BL/6J** mice (120 days old) during **incremental treadmill running tests** without electrical stimulus.  
The data were collected at the **Laboratory of Applied Sports Physiology** (State University of Campinas — *Unicamp*), following ethical approval protocol **CEUA 4940-1/2018**.

---

## 📂 Dataset Structure

```
MICE-RUN-THERMOGRAPHY-DATASET/
│
├── dataset/               # Thermographic images (JPG)
│   ├── ...                # 31,818 frames divided by intensity and split
│
├── metadata.csv           # Mapping between file, mouse_id, intensity class, and split
├── LICENSE                # CC BY 4.0 License
└── .gitignore
```

### **Metadata fields**

| Column | Description |
|---------|-------------|
| `filename` | Image file name (e.g., `00a8e415889.jpg`) |
| `mice_id` | Identifier of the subject (1–11) |
| `class` | Exercise intensity domain (`Low`, `Moderate`, `Heavy`, `Severe`) |
| `split` | Data partition (`train`, `test`) |

---

## 🧪 Experimental Setup

- **Species:** *Mus musculus* (C57BL/6J, 120 days old)  
- **Camera:** FLIR One Pro (7.5–13 µm spectral range, 640×512 px)  
- **Position:** 28 cm above the treadmill  
- **Treadmill stall dimensions:** 9.1 cm width × 8 cm height × 18 cm length  
- **Recording rate:** 30 Hz  
- **Location:** Laboratory of Applied Sports Physiology — Unicamp  
- **Ethics approval:** CEUA 4940-1/2018  

Each video was captured during an incremental running session where animals exercised until exhaustion.  
The dataset aims to support **classification and modeling of physiological transitions** between intensity domains through thermographic imagery.

---

## 🏃 Exercise Intensity Domains

| Stage | Label | Duration | Speed (m/min) | Description |
|--------|--------|-----------|---------------|--------------|
| 1️⃣ | **Low** | 0–3 min | 6 m/min | Warm-up intensity |
| 2️⃣ | **Moderate** | 3–6 min | Below MLSS | Submaximal steady-state |
| 3️⃣ | **Heavy** | 6–9 min | MLSS | Near maximal |
| 4️⃣ | **Severe** | 9–12 min | > MLSS (+20%) | Maximal intensity |

Each session was individually adjusted to maintain proper progression across intensities.  
Mice 7 and 11 achieved the highest final speeds (29.0 and 32.8 m/min, respectively).

---

## 📊 Dataset Statistics

| Class | Complete | Train | Validation | Test |
|--------|-----------|--------|-------------|--------|
| Low | 12,141 | 8,742 | 971 | 2,428 |
| Moderate | 11,436 | 8,234 | 915 | 2,287 |
| Heavy | 6,850 | 4,932 | 548 | 1,370 |
| Severe | 1,391 | 1,002 | 111 | 278 |
| **Total** | **31,818** | **22,910** | **2,545** | **6,363** |

> The dataset shows a natural imbalance, with more samples in lower intensity domains.

---

## ⚙️ Usage Example

```python
import pandas as pd
import cv2
import matplotlib.pyplot as plt

# Load metadata
df = pd.read_csv("metadata.csv")

# Read one sample image
img_path = f"dataset/{df.iloc[0]['filename']}"
img = cv2.imread(img_path)

# Display
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title(f"{df.iloc[0]['class']} (Mouse {df.iloc[0]['mouse_id']})")
plt.show()
```

---

## 🧩 Applications

This dataset can be used for:
- Thermal image classification and segmentation  
- Exercise physiology modeling  
- Domain transition detection  
- Data augmentation and cross-species learning  

---

## 📜 License

This dataset is distributed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.  
You are free to share and adapt the material, provided appropriate credit is given.  
Full text: [https://creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/)

---

## Citation

If you use this dataset, please cite:

> Bernini, P., Gobatto, F.B.M., Gobatto, C.A., Angelis, A.F., & Dias, U. (2025).  
> *Classification of Physical Exercise Intensity Domains in Thermographic Images of Mice Using Convolutional Neural Networks.*  
> Scientific Reports (Nature Portfolio).  
> School of Technology and School of Applied Sciences, University of Campinas (UNICAMP), Brazil.


---

## Acknowledgments

- Laboratory of Applied Sports Physiology — Unicamp  
- School of Technology (FT) — University of Campinas  
- CEUA Protocol 4940-1/2018  
- Support from graduate program in Technology (FT/Unicamp)
