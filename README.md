# Human Activity Classification Using Sensor Data

## 1. Project Overview

This project implements a machine learning system to classify human physical activities using wearable sensor data from the PAMAP2 Physical Activity Monitoring dataset.

The project compares six machine learning models using two feature configurations: a full feature set containing sensor measurements from multiple body locations and a limited feature set containing hand sensor measurements and heart rate.

The objective is to evaluate model performance and understand how the choice of sensor features affects human activity classification.

## 2. Objectives

- Explore and understand the PAMAP2 dataset.
- Preprocess sensor data and handle missing values.
- Construct full and limited feature configurations.
- Train and evaluate six machine learning models.
- Compare accuracy, precision, recall, and F1-score.
- Visualize model performance using comparison plots and confusion matrices.

## 3. Dataset

**Dataset:** PAMAP2 Physical Activity Monitoring

The dataset contains wearable sensor measurements collected during physical activities. The project uses the nine protocol files, `subject101.dat` through `subject109.dat`.

The original dataset is not included in this repository. Download it from the official UCI Machine Learning Repository:

https://archive.ics.uci.edu/dataset/231/pamap2+physical+activity+monitoring

After downloading and extracting the dataset, arrange the files as follows:

```text
data/
├── PAMAP2/
│   ├── Optional/
│   └── Protocol/
│       ├── subject101.dat
│       ├── subject102.dat
│       ├── ...
│       └── subject109.dat
└── processed/
```

The notebooks use relative paths to access the dataset. Run them from the project structure shown above.

## 4. Project Structure

```text
Human-Activity-Classification/
├── .gitignore
├── README.md
├── requirements.txt
├── data/
│   ├── PAMAP2/
│   └── processed/
├── notebooks/
│   ├── 01_dataset_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   └── 03_model_training.ipynb
├── results/
│   ├── confusion_matrices/
│   ├── model_accuracy_comparison.png
│   ├── model_f1_comparison.png
│   ├── model_performance.csv
│   └── precision_recall_comparison.png
├── report/
└── src/
```

Generated result filenames may vary slightly depending on the final saved files.

## 5. Technologies Used

- Python
- Jupyter Notebook
- NumPy
- pandas
- scikit-learn
- Matplotlib
- PyArrow

## 6. Installation and Setup

### Prerequisites

- Python installed on your system
- Git
- Visual Studio Code or Jupyter Notebook
- The PAMAP2 dataset downloaded and arranged as described above

### Create a virtual environment

From the project root directory, run:

```powershell
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install the project dependencies:

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Register the environment as a Jupyter kernel:

```powershell
python -m ipykernel install --user --name pamap2-activity --display-name "Python (PAMAP2 Activity)"
```

Open the project in VS Code and select the `Python (PAMAP2 Activity)` kernel for the notebooks.

## 7. Execution Steps

Run the notebooks in the following order:

1. **`01_dataset_exploration.ipynb`** — inspect the dataset files, load sample data, and examine the dataset structure.
2. **`02_preprocessing.ipynb`** — combine subject data, handle missing values, prepare the feature configurations, and save processed datasets.
3. **`03_model_training.ipynb`** — train the models, evaluate their predictions, compare performance metrics, and generate visualizations.

Execute the cells sequentially. The dataset must be available at the expected relative path before running the notebooks.

## 8. Machine Learning Models

The project evaluates the following six classifiers:

1. Logistic Regression
2. Support Vector Machine (RBF kernel)
3. Decision Tree
4. AdaBoost
5. Random Forest
6. Multi-Layer Perceptron Neural Network

### Feature configurations

- **Full features:** 52 features, including measurements from the hand, chest, and ankle sensors and heart rate.
- **Limited features:** 18 features, using hand sensor measurements and heart rate.

The main dataset split uses 85% of the data for training and 15% for testing, with random state 42 and stratification. The SVM experiment uses a separate sampled training and testing subset because of its computational requirements.

## 9. Results

The following accuracies were obtained from the current notebook results.

| Model | Full Features | Limited Features |
|---|---:|---:|
| Logistic Regression | 85.70% | 66.72% |
| RBF SVM | 96.44% | 88.82% |
| Decision Tree | 98.31% | 97.61% |
| AdaBoost | 88.40% | 75.02% |
| Random Forest | 99.22% | 96.81% |
| MLP Neural Network | 94.92% | 83.59% |

Random Forest achieved the highest reported accuracy with the full feature configuration, at 99.22%. Decision Tree achieved the highest reported accuracy with the limited feature configuration, at 97.61%.

The project also evaluates precision, recall, and F1-score and generates confusion matrices to help examine classification performance.

**Evaluation note:** The SVM results use a separate sampled test subset, so its accuracy should not be treated as a strictly like-for-like comparison with models evaluated on the full held-out test set.

## 10. Results and Output Files

The `results/` directory contains the model performance summary, comparison plots, and confusion matrices generated by the training notebook.

These artifacts provide a convenient way to inspect the results without rerunning model training.

## 11. Limitations

- The project uses a specific wearable-sensor dataset, and results may differ on other datasets or devices.
- The main evaluation uses a row-wise train-test split rather than a subject-independent split. Therefore, the results do not establish performance on entirely unseen individuals.
- The SVM uses a sampled training and test subset due to computational requirements.
- Performance depends on preprocessing choices, feature selection, and the distribution of activities in the dataset.

## 12. Conclusion

This project demonstrates the application of supervised machine learning to human activity classification using wearable sensor data. The comparison between full and limited feature configurations illustrates the effect of sensor selection on classification performance.

Random Forest performed best in the reported full-feature experiment, while Decision Tree achieved the highest reported accuracy with the limited feature set.

The notebooks, evaluation metrics, and visualizations provide a reproducible workflow for exploring, preprocessing, training, and evaluating human activity classification models.