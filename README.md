# 🌾 **Emmet County Crop-Type-Prediction-using-Machine-Learning** 🛰️


## 🔍 **Project Overview**  
This repository contains a **land cover classification project** for **Emmet County, Michigan**, using **two distinct approaches**:  
1. **Random Forest Classification** (Machine Learning)  
2. **Probability-Based Transition Model**  

The project leverages **historical satellite imagery** from **2008–2021** to predict **2021 land cover**, with a focus on **corn and soybean rotations**.  

## 🗂 **Data & Assumptions**  
- **Input Data:** TIFF raster images from **2008–2021** (30m resolution, EPSG:32615).  
- **Metadata:** `crop_metadata.json` maps crop codes to names, with a focus on **corn (1)** and **soybean (5)**.  
- **Labels:** 2021 pixel classes serve as ground truth, with **2020 held out for validation**.  
- **Class Reclassification:** All land covers outside corn/soybean collapsed into an **"Other"** category.  
- **Sampling Strategy:** Spatially balanced **10x10 grid sampling**, selecting **10% of pixels** evenly across the county.  
- **Feature Engineering:** Temporal land cover values from the **past 14 years**.

## 🧠 **Methods**  
### **Method 1: Random Forest Classifier**  
1. **Data Preparation**  
   - Extracted pixel values from **2008–2020**.  
   - Split dataset into **train (50%), validation (20%), test (30%)**.  

2. **Model Training & Optimization**  
   - Grid search to optimize **max_depth** and **class_weight** to handle class imbalance.  
   - Feature selection based on **historical importance**.  

3. **Evaluation & Prediction**  
   - Best model selected via **Precision-Recall AUC (PR-AUC)**.  
   - Applied trained model to classify **every pixel for 2021 land cover**.  

### **Method 2: Probability-Based Transition Model**  
1. **Transition Probabilities Computation**  
   - Grouped land cover values over past **7 years**.  
   - Calculated **historical transition probabilities** for **2021 predictions**.  

2. **Validation & Selection of Best History Length**  
   - Tested multiple **history lengths (3, 5, 7 years)**.  
   - Selected **best-performing sequence** based on **PR-AUC analysis**.  

3. **Final Prediction & Evaluation**  
   - Applied **maximum probability classification rule**.  
   - Compared **accuracy, precision, recall, and PR-AUC** with Random Forest.  

## 📈 **Results**  
### 🌳 **Random Forest Model (RF_65)**  
- **Validation PR-AUC:** **1.000** (best performing model).  
- **Test Accuracy:** **99.64%**  
- **Class-wise performance:**  
  - **Corn:** Precision **99.55%**, Recall **99.71%**  
  - **Soybean:** Precision **99.57%**, Recall **99.54%**  
  - **Other:** Precision **99.85%**, Recall **99.67%**  
- **Feature Importance:** 2015, 2017, 2018 were most influential.  

### 📊 **Probability-Based Model (7-Year History)**  
- **Validation PR-AUC:** **Stabilized at 7 years**.  
- **Test Accuracy:** **91.99%**  
- **Class-wise performance:**  
  - **Corn:** Precision **88.49%**, Recall **92.7%**  
  - **Soybean:** Precision **90.62%**, Recall **88.3%**  
  - **Other:** Precision **98.76%**, Recall **94.79%**  

### 🚧 **Challenges & Future Refinements**
### 🛠️ Challenges Faced
- ⚠️ Resolution Mismatch: The 2007 dataset (56m) was dropped for consistency
- ⚠️ Class Simplification: Non-corn/soy crops grouped into "Other"
- ⚠️ Temporal Gaps: Annual snapshots limit finer-scale transitions
- ⚠️ Stationarity Assumption: Model assumes historical transition rules remain unchanged
### 🔥 Future Improvements
- 🚀 Hybrid Model: Mixing Random Forest learning with probability-based classification for efficiency & accuracy
- 🗺️ Spatial Analysis: Introducing geospatial trends to refine predictions
- 📊 Dynamic Transition Modeling: Moving toward adaptive transition probabilities rather than fixed history window


## **How to Use This Repository**  
1. **Clone the Repository**  
   ```bash
   git clone https://github.com/your-username/emmet-landcover.git
   cd emmet-landcover
   ```
2. **Install Dependencies**  
 
3. **Run Random Forest Model**  
 
4. **Run Probability-Based Model**  

5. **Analyze Results**  
   - Outputs are saved as classified **TIFFs and evaluation reports**.  

## 👥 **Contributors**  
- **Calvin Samwel Swai** – Remote Sensing & Machine Learning Scientist Candidate  


🌟 Thank you for checking out this project! 🌍
Feel free to open issues, contribute, or reach out if you have feedback. 

