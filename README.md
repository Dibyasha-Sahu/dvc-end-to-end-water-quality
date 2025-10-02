# Predicting Water Portability with a DVC Pipeline

![Python Version](https://img.shields.io/badge/python-3.9+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-complete-green.svg)


This repository contains an end-to-end MLOps project demonstrating how to build a reproducible machine learning pipeline using *DVC (Data Version Control)*. The project focuses on a real-world classification problem: predicting the portability of water based on its quality metrics.

The core idea is to move from a single script/notebook to a modular, production-ready structure where each step of the ML lifecycle is a separate, version-controlled stage.

---

## 🎯 Problem Statement

The goal is to build a machine learning model to predict whether a water sample is potable (safe for human consumption) or not. This project emphasizes the MLOps process, creating an automated and reproducible pipeline that tracks changes in data, code, and models, ensuring consistency and reliability.

---

## ⚙ MLOps Pipeline with DVC

This project uses DVC to orchestrate the entire machine learning workflow. DVC defines a *Directed Acyclic Graph (DAG)* where each node is a stage in our pipeline. This setup ensures that when we re-run the pipeline, only the stages affected by a change (in code or data) are executed.

The pipeline is structured into four distinct stages:

1.  **Data Collection (data_collection.py):**
    * Loads the raw water quality dataset.
    * Performs a train-test split (e.g., 80-20 split).
    * Saves the split datasets (train.csv, test.csv) into a data/raw/ directory.

2.  **Data Preprocessing (data_prep.py):**
    * Loads the raw training and testing data.
    * Handles missing values by filling them with the median of each respective column.
    * Saves the cleaned datasets (train_processed.csv, test_processed.csv) into a data/processed/ directory.

3.  **Model Training (model_building.py):**
    * Loads the preprocessed training data.
    * Trains a *Random Forest Classifier* on the features.
    * Serializes and saves the trained model as model.pkl using the pickle library.

4.  **Model Evaluation (model_eval.py):**
    * Loads the saved model and the processed test data.
    * Makes predictions on the test set.
    * Calculates key classification metrics: *Accuracy, Precision, Recall, and F1-Score*.
    * Saves these metrics to a JSON file (metrics.json) for easy tracking.


---

## 🛠 Tech Stack

* *Language:* Python
* *Libraries:* Pandas, NumPy, Scikit-learn
* *MLOps Framework:* *DVC (Data Version Control)* for pipeline automation and data versioning.
* *Model Serialization:* Pickle
* *Code Editor:* Visual Studio Code

---

## 📂 Project Structure

The repository follows a modular structure to separate concerns and improve maintainability.


## 🚀 How to Reproduce the Project

To run this pipeline on your local machine, ensure you have Python, Git, and DVC installed.

1.  *Clone the repository:*
    bash
    git clone <your-repository-url>
    cd <repository-name>
    

2.  *Initialize Git and DVC:*
    bash
    git init
    dvc init
    

3.  *Install dependencies:*
    bash
    pip install -r requirements.txt
    

4.  *Run the entire pipeline:*
    bash
    dvc repro
    
    This single command tells DVC to execute all stages defined in dvc.yaml in the correct order, from data collection to model evaluation.

---

## 📊 Visualizing Results

DVC provides commands to easily inspect the outcomes of your pipeline.

* *Visualize the pipeline structure:*
    bash
    dvc dag
    

* *Show the latest model metrics:*
    bash
    dvc metrics show
    
    This command will display the contents of metrics.json in a clean, tabular format.

---

This project utilizes a modern MLOps stack for development and deployment:

* *Model Training & Experimentation*: scikit-learn, pandas, numpy
* *Data & Pipeline Versioning*: dvc 
* *Web Framework for API*: fastapi 
* *Asynchronous Server*: uvicorn 
* *Environment Management*: python-dotenv 

## Project Architecture

The project follows a standard MLOps workflow:

1.  *Data Ingestion*: Data is loaded and preprocessed.
2.  *Model Training*: A scikit-learn model is trained on the preprocessed data.
3.  *Model Serialization*: The trained model is saved as an artifact.
4.  *DVC Pipeline*: DVC is used to version control the dataset and model, ensuring reproducibility.
5.  *FastAPI Application*: An API is built to load the saved model and serve predictions via HTTP endpoints.
6.  *Server*: The FastAPI application is run using a Uvicorn server.

## 🔮 Future Enhancements

* *CI/CD Integration:* Use GitHub Actions to automatically run the dvc repro command on every push to ensure the pipeline is always working.
* *Cloud Deployment:* Deploy the final API to a cloud service for public access.
