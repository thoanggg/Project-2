# A Pixel-Based Approach for Aerial Image Segmentation of Sentinel-2 Imagery



This project implements and compares three machine learning approaches for land cover classification using Sentinel-2 satellite imagery, focusing on urban areas in central Hanoi, Vietnam.



## 🎯 Project Overview



The rapid urbanization of Hanoi poses significant challenges for land use management and urban planning. This study addresses these challenges by developing automated land cover classification systems that can:



- Monitor urban growth and land use changes

- Support intelligent land management systems

- Provide geospatial data for urban planning authorities

- Detect unauthorized land conversions



## 📊 Results Summary



| Model | Overall Accuracy | Best Use Case |

|-------|------------------|---------------|

| **1D CNN** | **95.26%** | Complex spectral patterns, mixed land covers |

| **Random Forest** | 91.75% | Fast processing, interpretable results |

| **SVM** | 89.84% | Small datasets, linear class boundaries |



## 🗺️ Study Area



- **Location**: Central Hanoi, Vietnam

- **Districts**: Tay Ho, Ba Dinh, Dong Da, Cau Giay, Hoan Kiem, Hai Ba Trung

- **Characteristics**: Dense urban core with mixed land use patterns



## 🏷️ Land Cover Classes



1. **Water** - Lakes, rivers (e.g., West Lake, To Lich River)

2. **Built Area** - High-density residential and commercial zones

3. **Vegetation** - Parks, tree-lined roads, green spaces

4. **Others** - Bare land, construction sites, parking lots



## 📡 Data Source



- **Satellite**: Sentinel-2 Level 2A

- **Acquisition Date**: February 18, 2020

- **Image ID**: L2A_T48QWJ_A024325_20200218T033333

- **Source**: Copernicus Open Access Hub



### Selected Spectral Bands



| Band | Wavelength (nm) | Resolution (m) | Purpose |

|------|-----------------|----------------|---------|

| Band 2 (Blue) | 490 | 10 | True color composite |

| Band 3 (Green) | 560 | 10 | True color composite |

| Band 4 (Red) | 665 | 10 | True color composite, NDVI |

| Band 8 (NIR) | 842 | 10 | Vegetation detection, NDVI |

| Band 11 (SWIR1) | 1610 | 20 | Built-up area detection |

| Band 12 (SWIR2) | 2190 | 20 | Moisture content, impervious surfaces |



**Additional Feature**: NDVI (Normalized Difference Vegetation Index)

```

NDVI = (B8 - B4) / (B8 + B4)

```



## 🛠️ Requirements



### Python Libraries

```

numpy

matplotlib

scikit-learn

gdal

rasterio

pandas

tensorflow

keras

```



### Software

- **QGIS** (for data preprocessing and ground truth creation)

- **Semi-Automatic Classification Plugin (SCP)** (for ROI digitization)

- **Python 3.x** (for model implementation)



## 🚀 Getting Started



### 1. Data Preparation

1. Download Sentinel-2 Level 2A imagery from Copernicus Open Access Hub

2. Extract and preprocess spectral bands in QGIS

3. Calculate NDVI using the raster calculator

4. Create training data using SCP plugin



### 2. Model Training



#### Support Vector Machine (SVM)

```python

from sklearn.svm import SVC

from sklearn.model_selection import GridSearchCV



# Parameter tuning

param_grid = {

&nbsp;   'C': [2**i for i in range(-2, 8)],

&nbsp;   'gamma': [2**i for i in range(-5, 5)]

}



svm = SVC(kernel='rbf')

svm_grid = GridSearchCV(svm, param_grid, cv=5)

```



#### Random Forest

```python

from sklearn.ensemble import RandomForestClassifier



# Parameter tuning

rf = RandomForestClassifier(

&nbsp;   n_estimators=[100, 200, 500],

&nbsp;   max_features=range(1, 11)

)

```



#### 1D CNN Architecture

```python

import tensorflow as tf

from tensorflow.keras import layers



model = tf.keras.Sequential([

&nbsp;   layers.Conv1D(64, 2, activation='relu', input_shape=(7, 1)),

&nbsp;   layers.BatchNormalization(),

&nbsp;   layers.Dropout(0.3),

&nbsp;   

&nbsp;   layers.Conv1D(32, 2, activation='relu'),

&nbsp;   layers.BatchNormalization(),

&nbsp;   layers.Dropout(0.3),

&nbsp;   

&nbsp;   layers.Conv1D(16, 2, activation='relu'),

&nbsp;   layers.BatchNormalization(),

&nbsp;   layers.Dropout(0.3),

&nbsp;   

&nbsp;   layers.Flatten(),

&nbsp;   layers.Dense(16, activation='relu'),

&nbsp;   layers.Dense(128, activation='relu'),

&nbsp;   layers.Dense(4, activation='softmax')  # 4 classes

])

```



### 3. Dataset Split

- **Total labeled pixels**: 18,681

- **Training set**: 14,944 pixels (80%)

- **Testing set**: 3,737 pixels (20%)



## 📈 Model Performance



### Class-wise F1-Scores



| Class | SVM | Random Forest | 1D CNN |

|-------|-----|---------------|---------|

| Water | 0.99 | 0.98 | **0.99** |

| Built Area | 0.94 | 0.95 | **0.98** |

| Vegetation | 0.59 | 0.63 | **0.77** |

| Others | 0.76 | 0.75 | **0.88** |



### Key Findings



1. **CNN Superior Performance**: The 1D CNN model achieved the highest accuracy (95.26%) by effectively learning spectral patterns

2. **Class Confusion**: Most errors occurred between vegetation and bare land/construction sites due to spectral similarity

3. **NDVI Importance**: Adding NDVI significantly improved vegetation vs. others classification

4. **Urban Complexity**: Traditional ML methods (SVM, RF) struggled with spectrally mixed urban land covers



## 🔄 Applications



### Urban Planning & Management

- Monitor urban growth patterns

- Manage infrastructure development

- Preserve green spaces

- Support sustainable city planning



### Environmental Monitoring

- Track vegetation cover changes

- Monitor water body variations

- Detect illegal land conversions

- Assess environmental degradation



### Smart City Development

- Integrate with GIS systems

- Enable data-driven governance

- Support decision-making tools

- Facilitate proactive land management



### Disaster Risk Management

- Flood risk assessment

- Emergency response planning

- Climate resilience strategies



## 🔮 Future Work



1. **Spatial Context Integration**: Implement 2D CNNs or hybrid spatial-spectral architectures

2. **Temporal Analysis**: Develop time-series models for land-use change detection

3. **Transfer Learning**: Adapt models for other Vietnamese cities

4. **Real-time Processing**: Implement automated monitoring systems

5. **Multi-sensor Fusion**: Combine Sentinel-2 with other satellite data



## 👥 Contributing



This project was developed as part of research at Hanoi University of Science and Technology. Contributions are welcome for:



- Model improvements

- Additional study areas

- Performance optimizations

- Documentation enhancements





## 📞 Contact



- **Student**: Vu Duc Thang (thang.vd225553@sis.hust.edu.vn)

- **Supervisor**: PhD Tran Nguyen Ngoc

- **Institution**: School of Information and Communications Technology, Hanoi University of Science and Technology



## 📚 References



Key references include works on Sentinel-2 classification, CNN architectures for remote sensing, and urban land cover mapping. See the full report for complete bibliography.



---



*This project demonstrates the effectiveness of deep learning approaches in urban remote sensing applications and provides a foundation for scalable land cover monitoring in Vietnam and beyond.*

