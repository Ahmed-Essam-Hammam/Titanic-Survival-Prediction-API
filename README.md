# Titanic Survival Prediction API

The **Titanic Survival Prediction API** is a FastAPI-based service that predicts the survival probability of Titanic passengers using a trained neural network model. This project leverages machine learning to analyze passenger data and provide predictions on whether a passenger would have survived the Titanic disaster.

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Project Structure](#project-structure)
3. [Setup Instructions](#setup-instructions)
4. [Usage](#usage)
5. [API Endpoints](#api-endpoints)
6. [Example Request](#example-request)
7. [Model Development](#model-development)
8. [License](#license)

---

## Project Overview

This project aims to predict the survival probability of Titanic passengers based on features such as age, gender, class, fare, and family size. The model is built using TensorFlow and Keras, and the API is deployed using FastAPI. The model was trained on the Titanic dataset, which includes passenger information and survival outcomes.

Key features of the project:
- **Neural Network Model**: A deep learning model with multiple layers and dropout regularization to prevent overfitting.
- **Data Preprocessing**: Includes handling missing values, scaling numerical features, and encoding categorical variables.
- **API Deployment**: A FastAPI service that exposes endpoints for health checks and survival predictions.
- **Hyperparameter Tuning**: Utilizes Keras Tuner for optimizing model hyperparameters.

---

## Project Structure

The project is organized as follows:
```
C:.
│ .env.example
│ .gitignore
│ main.py
│ README.md
│ requirements.txt
├───src
│ │ config.py
│ │ inference.py
│ │ __init__.py
│ ├───artifacts
│ │ best_model.keras
│ │ preprocessor.joblib
│ ├───models
│ │ │ schemas.py
│ │ │ __init__.py
│ ├───notebooks
│ │ Titanic_G4.ipynb
```

- **`main.py`**: The FastAPI application entry point.
- **`src/`**: Contains the core logic for configuration, inference, and model schemas.
- **`artifacts/`**: Stores the trained model (`best_model.keras`) and preprocessing pipeline (`preprocessor.joblib`).
- **`notebooks/`**: Includes the Jupyter notebook (`Titanic_G4.ipynb`) used for exploratory data analysis (EDA), model training, and evaluation.

---

## Setup Instructions

To set up the project locally, follow these steps:

1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```
2. **Create a Virtual Environment**:
   ```bash
   python -m venv venv
   ```
3. **Activate the Virtual Environment**:
   - On Windows:
     ```bash
     venv\Scripts\activate
     ```
   - On Unix/MacOS:
     ```bash
     source venv/bin/activate
     ```
4. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
5. **Set Up Environment Variables**:
   Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```
   Fill in the required values in the `.env` file.

---

## Usage

To start the FastAPI server, run the following command:
```bash
uvicorn main:app --host 0.0.0.0 --port 8080 --reload
```
The API will be available at [http://localhost:8080](http://localhost:8080).

---

## API Endpoints

### 1. Health Check
- **Endpoint**: `GET /`
- **Description**: Checks if the API is running.
- **Response**:
  ```json
  {
    "app_name": "Titanic Survival Prediction API",
    "version": "1.0.0",
    "status": "up & running"
  }
  ```

### 2. Survival Prediction
- **Endpoint**: `POST /classify`
- **Description**: Predicts the survival probability for a list of passengers.
- **Request Body**: A list of passenger data (see example below).
- **Response**:
  ```json
  {
    "predictions": [
      {
        "passenger_id": 1,
        "survival_probability": 0.85,
        "survival_status": "Survived"
      },
      {
        "passenger_id": 2,
        "survival_probability": 0.23,
        "survival_status": "Not Survived"
      }
    ]
  }
  ```

---

## Example Request

Here is an example request body for the `/classify` endpoint:
```json
[
    {
        "passenger_id": 1,
        "age": 22.0,
        "fare": 7.25,
        "sex": "male",
        "embarked": "S",
        "parch": 0,
        "sibsp": 1,
        "pclass": 3
    },
    {
        "passenger_id": 2,
        "age": 29.0,
        "fare": 15.50,
        "sex": "female",
        "embarked": "C",
        "parch": 1,
        "sibsp": 0,
        "pclass": 2
    }
]
```

---

## Model Development

The model development process is documented in the Jupyter notebook (`Titanic_G4.ipynb`). Key steps include:

1. **Data Loading and Preprocessing**:
   - Load the Titanic dataset.
   - Handle missing values using median imputation for numerical features and mode imputation for categorical features.
   - Scale numerical features using `StandardScaler`.
   - Encode categorical features using `OneHotEncoder`.
2. **Feature Engineering**:
   - Create new features such as `family_size` and `is_alone`.
3. **Model Training**:
   - Build a neural network with multiple dense layers, dropout regularization, and L2 regularization.
   - Train the model using the Adam optimizer and binary cross-entropy loss.
4. **Hyperparameter Tuning**:
   - Use Keras Tuner to optimize the number of units, dropout rates, and other hyperparameters.
5. **Model Evaluation**:
   - Evaluate the model on the test set using accuracy and loss metrics.
   - Visualize training and validation loss/accuracy over epochs.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.
