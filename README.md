# Text Classification with Hugging Face Transformers

This notebook demonstrates an end-to-end workflow for text classification using the Hugging Face Transformers library. The goal is to classify text as either 'food' or 'not food' based on image captions.

## Table of Contents
- [Setup and Dependencies](#setup-and-dependencies)
- [Data Loading and Preprocessing](#data-loading-and-preprocessing)
- [Model Training](#model-training)
- [Evaluation and Prediction](#evaluation-and-prediction)
- [Gradio Demo](#gradio-demo)
- [Hugging Face Space Deployment](#hugging-face-space-deployment)

## Setup and Dependencies
To run this notebook, you will need a GPU. The following libraries are installed:
- `datasets`
- `evaluate`
- `accelerate`
- `gradio`
- `torch`
- `transformers`
- `pandas`

Your Hugging Face token should be set up in Colab secrets under the name `HF_TOKEN` for pushing models to the Hugging Face Hub.

## Data Loading and Preprocessing
The dataset used is `mrdbourke/learn_hf_food_not_food_image_captions` from the Hugging Face Hub. It contains text captions labeled as 'food' or 'not_food'.

Steps include:
- Loading the dataset using `load_dataset`.
- Inspecting random samples and label distribution.
- Creating `id2label` and `label2id` mappings.
- Mapping text labels to numerical labels.
- Splitting the dataset into training and testing sets.
- Tokenizing the text data using `AutoTokenizer` (specifically, `distilbert-base-uncased`).

## Model Training

**Model Architecture**: A `DistilBERT` model (`distilbert-base-uncased`) fine-tuned for sequence classification (`AutoModelForSequenceClassification`).

**Training Process**:
- Setting up `TrainingArguments` for hyperparameters such as learning rate, batch size, number of epochs, and evaluation strategy.
- Using the `Trainer` API for training, evaluation, and saving the model.
- Monitoring training and evaluation loss curves.

## Evaluation and Prediction

- The model is evaluated using accuracy as a metric.
- Predictions are made on the test set, and probabilities are calculated.
- Analysis of prediction probabilities and identification of challenging examples.

## Gradio Demo
A local Gradio interface is built to interactively test the trained model. This demo allows users to input text and get predictions on whether it's 'food' or 'not food'.

## Hugging Face Space Deployment
The notebook demonstrates how to deploy the Gradio demo to a public Hugging Face Space. This involves creating `app.py`, `requirements.txt`, and `README.md` files for the Space, and programmatically uploading them to the Hugging Face Hub.

### Live Demo
You can interact with the deployed Gradio app here:

<iframe
	src="https://ironspiritjeff-food-not-food-text-classifier-demo.hf.space"
	frameborder="0"
	width="850"
	height="450"
></iframe>

**Hugging Face Space**: [https://huggingface.co/spaces/ironspiritjeff/food_not_food_text_classifier_demo](https://huggingface.co/spaces/ironspiritjeff/food_not_food_text_classifier_demo)

## Source Code
- This Notebook's Source Code: [https://github.com/ironspiritjeff/hf-transformer-experiments/blob/main/HuggingFace_TextClassificationTutorial.ipynb](https://github.com/ironspiritjeff/hf-transformer-experiments/blob/main/HuggingFace_TextClassificationTutorial.ipynb)





April 10th: Changed Learning rate from 0.0001 to 0.00002, and set processing class to tokenizer in Trainer. Model now predicts fairly well whether a phrase is about food or not. 
* Weakness to address: After trying examples such as "After dinner we'll have dessert", which the model predicted as "not food", it seems that the model sometimes predicts wrong when a specific food isn't mentioned.
* However, the phrase "After the main course we'll have dessert" is correctly predicted, so it doesn't always rely on the mentioning of a specific food.
* The model would benefit from further training on these kinds of phrases which don't specify a particular food but are still food related.


April 9th: Food Not Food Classifier incorrectly predicts 'not food' every time, with 97-99% probability.
