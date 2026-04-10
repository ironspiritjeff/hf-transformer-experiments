# hf-transformer-experiments
This repository tracks my implementation of transformer models using the Hugging Face ecosystem.


April 9th: Food Not Food Classifier incorrectly predicts 'not food' every time, with 97-99% probability.

April 10th: Changed Learning rate from 0.0001 to 0.00002, and set processing class to tokenizer in Trainer. Model now predicts fairly well whether a phrase is about food or not. 
* Weakness to address: After trying examples such as "After dinner we'll have dessert", which the model predicted as "not food", it seems that the model only correctly predicts whether the phrase is about food or not if a specific food is mentioned. 
