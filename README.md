App link: https://vae-digit-generator.onrender.com/
<br>
🧠 Conditional VAE Digit Generator (MNIST)

This project implements a Conditional Variational Autoencoder (CVAE) for generating handwritten digits from the MNIST dataset and deploys the decoder model as a web application using Streamlit on Render.

The application allows users to:

Select a digit class (0–9)

Control latent variables 
𝑧
1
z
1
	​

 and 
𝑧
2
z
2
	​


Generate diverse handwritten digit samples conditioned on the selected class

📌 Project Overview

Model type: Conditional Variational Autoencoder (CVAE)

Dataset: MNIST

Latent space dimension: 2

Deployment: Streamlit + Render

Inference-only deployment: Decoder model (no training at runtime)

This project demonstrates end-to-end ML deployment, from model training and serialization to cloud deployment and interactive inference.

📁 Repository Structure
FML_Auto_VAE/
├── app.py                         # Streamlit application (entry point)
├── requirements.txt               # Python dependencies
├── cvae_mnist_decoder.keras/      # Saved decoder model (Keras v3 format)
│   ├── config.json
│   ├── metadata.json
│   └── model.weights.h5
├── VAEMODEL.ipynb                 # Training notebook (reference)
├── VAEMNSITModel.ipynb            # Training experiments
├── VAEFinalMNSIT.ipynb            # Model development
└── VAEfacefinal.ipynb             # Additional experiments


Note:
.ipynb files are kept for reference. Render ignores them during deployment.

🧠 Model Explanation
Conditional Variational Autoencoder (CVAE)

A CVAE models the conditional distribution:

𝑝
(
𝑥
∣
𝑧
,
𝑦
)
p(x∣z,y)

Where:

𝑥
x → generated image

𝑧
=
(
𝑧
1
,
𝑧
2
)
z=(z
1
	​

,z
2
	​

) → latent variables

𝑦
y → class label (digit 0–9)

The decoder learns to generate digit images given:

a latent vector 
𝑧
z (controls style/variation)

a class label 
𝑦
y (controls digit identity)

🎛 Latent Space (
𝑧
1
z
1
	​

, 
𝑧
2
z
2
	​

)

𝑧
1
z
1
	​

 and 
𝑧
2
z
2
	​

 are continuous latent variables

They represent degrees of variation along learned abstract features

Changing them smoothly alters the style of the generated digit while keeping the digit class fixed

This demonstrates:

Latent space continuity

Disentangled representation (class vs style)

🚀 Deployment Pipeline (End-to-End)

This section is intentionally detailed so you can reproduce deployment later without confusion.

Step 1: Save the Decoder Model (Training Phase)

From the training notebook:

decoder.save('/content/drive/MyDrive/cvae_mnist_decoder.keras')


This saves the decoder in Keras v3 format, which includes:

Model architecture

Weights

Metadata

Step 2: Download the Model from Google Drive

Download the folder:

cvae_mnist_decoder.keras/


Do not modify or rename any internal files.

Step 3: Create the Streamlit App (app.py)

The Streamlit app:

Loads the decoder using tf.keras.models.load_model

Accepts digit and latent variables as user input

Calls the decoder as a multi-input model:

decoder.predict([z, label])

Step 4: Define Dependencies (requirements.txt)
streamlit
tensorflow
numpy


These are sufficient for inference and deployment.

Step 5: Push Files to GitHub

Ensure the repository contains:

app.py

requirements.txt

cvae_mnist_decoder.keras/

Step 6: Deploy on Render
Render Configuration

Service type: Web Service

Runtime: Python 3

Build Command

pip install -r requirements.txt


Start Command

streamlit run app.py --server.port $PORT --server.address 0.0.0.0


Render will:

Clone the repository

Install dependencies

Load the model

Start the Streamlit server

Step 7: Access the Live Application

Once deployment is complete, Render provides a public URL.

Example:

https://vae-digit-generator.onrender.com
