 # 🌲 Forest Cover Type Prediction
### Machine Learning Internship Project | Multi-Class Classification

## 📌 Project Overview
This project aims to predict the forest cover type (the predominant kind of tree) for 30 x 30 meter cells based on cartographic variables. The dataset used is the **UCI Forest Cover Type**, containing over 581,000 observations from the Roosevelt National Forest in northern Colorado.

## 📊 Dataset Features
The model utilizes **54 initial attributes** to classify 7 forest types:
* **Quantitative Features:** Elevation, Aspect, Slope, Horizontal/Vertical Distance to Hydrology, Roadways, and Fire Points.
* **Categorical Features (One-Hot Encoded):** 4 Wilderness Areas and 40 Soil Types.
* **Target Variable:** `Cover_Type` (Classes 1 through 7).

## 🛠️ Data Preprocessing & Engineering
To optimize model performance and efficiency, the following steps were implemented:

1.  **Label Refinement:** Adjusted target labels from `[1-7]` to `[0-6]` for compatibility with standard loss functions.
2.  **Memory Optimization:** Downcast binary features to `int8` and continuous features to `float32`, reducing RAM footprint by over **70%**.
3.  **Feature Engineering:** Created `Distance_To_Hydrology_Euclidean` using the Pythagorean theorem:
    $$Distance = \sqrt{\text{Horizontal\_Hydrology}^2 + \text{Vertical\_Hydrology}^2}$$
4.  **Zero-Variance Check:** Verified all features contained useful information; no constant columns were found.



## 🤖 Modeling Strategy: Random Forest
I chose the **Random Forest Classifier** for its robustness against outliers and its ability to handle high-dimensional tabular data without requiring intensive feature scaling.

### Iteration 1: Baseline Model
* **Overall Accuracy:** 89.14%
* **Analysis:** High accuracy, but low **Recall (0.39)** for Class 4 (minority class). The model was heavily biased toward majority classes.

### Iteration 2: Balanced Model
* **Modification:** Implemented `class_weight='balanced'`.
* **Overall Accuracy:** 90.10%
* **Analysis:** Massive improvement in fairness. **Class 4 Recall jumped from 0.39 to 0.93**, and the **Macro F1-Score increased from 0.84 to 0.86**.

## 📈 Final Model Results (Balanced)
| Metric | Score |
| :--- | :--- |
| **Overall Accuracy** | 90.10% |
| **Macro Avg Recall** | 92.00% |
| **Macro Avg F1-Score** | 86.00% |

## 💡 Key Takeaway
By addressing class imbalance through weighted penalties, the model became significantly more reliable at identifying rare forest types (Classes 4 and 5) without sacrificing—and actually slightly improving—overall accuracy.
