# hf-transformer-experiments
This repository tracks my implementation of transformer models using the Hugging Face ecosystem.


April 9th: Food Not Food Classifier incorrectly predicts 'not food' every time, with 97-99% probability.

April 10th: Changed Learning rate from 0.0001 to 0.00002, and set processing class to tokenizer in Trainer. Model now predicts fairly well whether a phrase is about food or not. 
* Weakness to address: After trying examples such as "After dinner we'll have dessert", which the model predicted as "not food", it seems that the model sometimes predicts wrong when a specific food isn't mentioned.
* However, the phrase "After the main course we'll have dessert" is correctly predicted, so it doesn't always rely on the mentioning of a specific food.
* The model would benefit from further training on these kinds of phrases which don't specify a particular food but are still food related.
