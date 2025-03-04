Heart Disease Risk Assessment App

This repository contains a Streamlit app that predicts the risk of heart disease based on 13 health metrics. The app uses a trained machine learning model to make predictions and provides a user-friendly interface for inputting health metrics and viewing predicted risk levels.

Features

User-friendly interface for inputting 13 health metrics
Predicts risk of heart disease based on trained machine learning model
Displays predicted risk level as "High" or "Low"
Easy to use and understand, even for those without a medical background
Technical Details

Built using Streamlit and Python
Uses joblib to load trained machine learning model
NumPy is used for numerical computations
Model was trained on a dataset of heart disease patients (not included in this repository)
How to Use

Clone this repository to your local machine
Install required dependencies using pip install -r requirements.txt
Run the app using streamlit run app.py
Open a web browser and navigate to http://localhost:8501
Enter your health metrics and click the "Predict" button to see your predicted risk of heart disease

import streamlit as st
import joblib
import numpy as np

# Load the trained model
model = joblib.load('heart_disease_model.pkl')

# Define the Streamlit app
st.title("Heart Disease Risk Assessment")

st.write("""
### Enter your health metrics to predict the risk of heart disease:
""")

# Define input fields
age = st.number_input("Age", min_value=0, max_value=120, value=30)
sex = st.selectbox("Sex", [0, 1], format_func=lambda x: 'Male' if x == 1 else 'Female')
cp = st.number_input("Chest Pain Type (0-3)", min_value=0, max_value=3, value=0)
trestbps = st.number_input("Resting Blood Pressure", min_value=0, max_value=200, value=120)
chol = st.number_input("Serum Cholestoral in mg/dl", min_value=0, max_value=600, value=200)
fbs = st.selectbox("Fasting Blood Sugar > 120 mg/dl", [0, 1], format_func=lambda x: 'True' if x == 1 else 'False')
restecg = st.number_input("Resting Electrocardiographic Results (0-2)", min_value=0, max_value=2, value=0)
thalach = st.number_input("Maximum Heart Rate Achieved", min_value=0, max_value=220, value=150)
exang = st.selectbox("Exercise Induced Angina", [0, 1], format_func=lambda x: 'Yes' if x == 1 else 'No')
oldpeak = st.number_input("ST Depression Induced by Exercise", min_value=0.0, max_value=10.0, value=1.0)
slope = st.number_input("Slope of the Peak Exercise ST Segment (0-2)", min_value=0, max_value=2, value=0)
ca = st.number_input("Number of Major Vessels (0-3)", min_value=0, max_value=3, value=0)
thal = st.number_input("Thal (1-3)", min_value=1, max_value=3, value=1)

# When the user clicks the "Predict" button
if st.button("Predict"):
    input_data = np.array([[age, sex, cp, trestbps, chol, fbs, restecg, thalach, exang, oldpeak, slope, ca, thal]])
    prediction = model.predict(input_data)
    risk = 'High' if prediction[0] == 1 else 'Low'
    
    st.write(f"### Predicted Risk of Heart Disease: {risk}")

# Run the app with: streamlit run app.py
