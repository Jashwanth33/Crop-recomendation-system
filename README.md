# Crop Recommendation System

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.0+-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://tensorflow.org)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-0.24+-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

> Machine learning-based crop recommendation system analyzing soil nutrients to suggest optimal crops.

## ML Pipeline

`mermaid
flowchart TD
    A[Raw Data] --> B[Data Collection]
    B --> C[Data Preprocessing]
    C --> D[Feature Engineering]
    D --> E[Model Training]
    E --> F[Model Evaluation]
    F --> G[Model Deployment]
    G --> H[Prediction API]
    H --> I[User Interface]
    
    C --> C1[Missing Values]
    C --> C2[Normalization]
    C --> C3[Encoding]
    
    D --> D1[Feature Selection]
    D --> D2[Dimensionality Reduction]
    
    E --> E1[Train/Test Split]
    E --> E2[Cross Validation]
    E --> E3[Hyperparameter Tuning]
    
    F --> F1[Accuracy]
    F --> F2[Precision]
    F --> F3[Recall]
    F --> F4[F1-Score]
`

## System Architecture

`mermaid
graph TB
    subgraph "User Interface"
        Web[Web App]
        Mobile[Mobile App]
        CLI[CLI Tool]
    end

    subgraph "API Layer"
        Flask[Flask API]
        Validator[Input Validator]
    end

    subgraph "ML Engine"
        Preprocessor[Data Preprocessor]
        Model[ML Model]
        Predictor[Prediction Engine]
    end

    subgraph "Data Layer"
        CSV[(CSV Data)]
        ModelDB[(Model Storage)]
    end

    Web --> Flask
    Mobile --> Flask
    CLI --> Flask
    Flask --> Validator
    Validator --> Preprocessor
    Preprocessor --> Model
    Model --> Predictor
    Predictor --> Flask
    Flask --> CSV
    Model --> ModelDB
`

## Crop Prediction Flow

`mermaid
flowchart TD
    Start([User Input]) --> Input{Input Parameters}
    
    Input --> N[Nitrogen N]
    Input --> P[Phosphorus P]
    Input --> K[Potassium K]
    Input --> Temp[Temperature]
    Input --> Humidity[Humidity]
    Input --> pH[pH Level]
    Input --> Rainfall[Rainfall]
    
    N --> Process[Data Processing]
    P --> Process
    K --> Process
    Temp --> Process
    Humidity --> Process
    pH --> Process
    Rainfall --> Process
    
    Process --> Normalize[Normalization]
    Normalize --> Features[Feature Extraction]
    Features --> Model[ML Model Prediction]
    
    Model --> Result{Prediction}
    Result --> Rice[Rice]
    Result --> Wheat[Wheat]
    Result --> Cotton[Cotton]
    Result --> Sugarcane[Sugarcane]
    Result --> Other[Other Crops]
    
    Rice --> Confidence[Confidence Score]
    Wheat --> Confidence
    Cotton --> Confidence
    Sugarcane --> Confidence
    Other --> Confidence
    
    Confidence --> Output([Recommended Crop])
`

## Project Structure

`
Crop-recomendation-system/
│
├── data/
│   ├── raw/
│   │   └── crop_data.csv            # Raw dataset
│   ├── processed/
│   │   └── cleaned_data.csv         # Preprocessed data
│   └── README.md
│
├── notebooks/
│   ├── 01_data_exploration.ipynb    # EDA notebook
│   ├── 02_data_preprocessing.ipynb  # Data cleaning
│   ├── 03_model_training.ipynb      # Model training
│   ├── 04_model_evaluation.ipynb    # Model evaluation
│   └── 05_deployment.ipynb          # Deployment prep
│
├── src/
│   ├── __init__.py
│   ├── data/
│   │   ├── __init__.py
│   │   ├── data_loader.py           # Data loading
│   │   ├── preprocessor.py          # Data preprocessing
│   │   └── feature_engine.py        # Feature engineering
│   │
│   ├── models/
│   │   ├── __init__.py
│   │   ├── trainer.py               # Model training
│   │   ├── predictor.py             # Prediction engine
│   │   ├── evaluator.py             # Model evaluation
│   │   └── saved/                   # Saved models
│   │       ├── random_forest.pkl
│   │       ├── xgboost.pkl
│   │       └── neural_network.h5
│   │
│   ├── api/
│   │   ├── __init__.py
│   │   ├── app.py                   # Flask app
│   │   ├── routes.py                # API routes
│   │   └── validators.py            # Input validation
│   │
│   └── utils/
│       ├── __init__.py
│       ├── logger.py                # Logging
│       └── helpers.py               # Utility functions
│
├── models/
│   ├── random_forest/
│   ├── xgboost/
│   ├── svm/
│   └── neural_network/
│
├── tests/
│   ├── test_data.py
│   ├── test_models.py
│   └── test_api.py
│
├── api/
│   ├── app.py                       # Main API application
│   └── requirements.txt
│
├── web/
│   ├── templates/
│   │   ├── index.html
│   │   └── result.html
│   └── static/
│       ├── css/
│       └── js/
│
├── configs/
│   ├── model_config.yaml
│   └── api_config.yaml
│
├── requirements.txt
├── setup.py
├── Dockerfile
└── README.md
`

## Models Used

| Model | Accuracy | Description |
|-------|----------|-------------|
| Random Forest | 95% | Ensemble learning method |
| XGBoost | 96% | Gradient boosting |
| SVM | 92% | Support Vector Machine |
| Neural Network | 94% | Deep learning |
| Logistic Regression | 89% | Baseline model |

## Soil Parameters

| Parameter | Description | Unit |
|-----------|-------------|------|
| N | Nitrogen content | kg/ha |
| P | Phosphorus content | kg/ha |
| K | Potassium content | kg/ha |
| temperature | Temperature | Celsius |
| humidity | Relative humidity | % |
| pH | Soil pH level | 0-14 |
| rainfall | Rainfall | mm |

## Installation

`ash
git clone https://github.com/Jashwanth33/Crop-recomendation-system.git
cd Crop-recomendation-system

pip install -r requirements.txt

# Run Jupyter notebooks
jupyter notebook notebooks/

# Run API
python src/api/app.py
`

## API Usage

`python
import requests

# Predict crop
response = requests.post("http://localhost:5000/predict", json={
    "nitrogen": 90,
    "phosphorus": 42,
    "potassium": 43,
    "temperature": 21,
    "humidity": 82,
    "phH": 6.5,
    "rainfall": 200
})

print(response.json())
# {"crop": "rice", "confidence": 0.95}
`

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT License

## Author

**Jashwanth** - [GitHub](https://github.com/Jashwanth33)