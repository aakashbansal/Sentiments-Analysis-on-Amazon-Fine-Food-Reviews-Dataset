# Sentiments-Analysis-on-Amazon-Fine-Food-Reviews-Dataset
This project contains the code for Sentiments Analysis applied on the Amazon Fine Food Reviews Dataset. After the training phase, the model can classify any Food review into a **positive** or a **negative review**.

## Dataset

[Amazon Fine Food Reviews](https://www.kaggle.com/snap/amazon-fine-food-reviews) dataset is used. The dataset contains 568,454 food reviews Amazon users left up to October 2012.

## Preprocessing

All NLP models require text preprocessing. In this model also, a lot of preprocessing is applied on the text.
<br>

First all of the text is converted into **lowercase**. Then all **HTML tags** are removed. 
<br>

After that all **special characters** are removed and only letters of English Alphabet **(a-z)**, digits **(0-9)** and full stop **(.)** are kept.
<br>

All **stop words( the, and, of etc.)** are also removed from the text.
<br>

The words are then **Lemmatized** (i.e. to convert the word into its base or dictionary form. e.g. studying to study). 
<br>

When the dataset was pictorially represented, it was discovered that **more than 70%** of the dataset contains **less than 60 words**. So, 60 was set as an upper limit for a review to be considered in the training data ie. all reviews with length greater than 60 words were rejected by the model.
<br>

Then the dataset was split into **TRAIN-VALIDATION-TEST** in the ratio of **60:20:20**.
<br>

Then the dataset was **Tokenized** i.e. words were converted to corresponding indices. The reviews with length less than 60 were **padded with zeroes** so as to have a consistent length of 60 for all reviews.

## Models 

**Four models** were used for training :

1. **Custom Embedding Model** : In this model, the Custom Word Embeddings Layer is used as the first layer in the model i.e. **no pre-trained embeddings were used**. Instead, the model learnt the word embeddings for the first layer on its own.

  Training Accuracy - **99.14%**<br>
  Validation Accuracy - **94.86%**<br>
  Test Accuracy - **94.92%**

2. **Word2Vec Model** : In this model, the Word Embeddings were first learnt using the **Gensim Word2Vec model**. After the embeddings were learnt, they were given as **fixed untrainable input** to the model as the first layer.

  Training Accuracy - **93.21%**<br>
  Validation Accuracy - **93.72%**<br>
  Test Accuracy - **93.89%**

3. **Averaging Model** : In this model, **pre-trained 100-dimensional [GloVe Embeddings](https://nlp.stanford.edu/projects/glove/)** (i.e. glove.6B.100d) were used. For each word in the review, the corresponding GloVe word embedding was extracted which was then **averaged out** for the whole review. The final averaged embedding was then used as an input to the model. This model did not take into account the **relative positioning of words** as they were just being averaged out.

  Training Accuracy - **90.27%**<br>
  Validation Accuracy - **89.42%**<br>
  Test Accuracy - **89.38%**

4. **GloVe Model** : This model is exactly similiar to the **2nd** model except for the difference that **fixed pre-trained untrainable 100-dimensional [GloVe Embeddings](https://nlp.stanford.edu/projects/glove/)** (i.e. glove.6B.100d) were used instead of **Word2Vec embeddings**.

  Training Accuracy - **92.92%**<br>
  Validation Accuracy - **93.38%**<br>
  Test Accuracy - **93.13%**
  
The **First** and **Second Model** are implemented in **sentiments_analysis_amazon_fine_food_reviews_custom_embedding_and_word2vec.ipynb** file.

The **Third** and **Fourth Model** are implemented in **sentiments_analysis_amazon_fine_food_reviews_glove_embedding.ipynb** file.

## Model Performances

The first model i.e. **Custom Embeddings Model** clearly outperfomed all other models and stood first with the Test Set Accuracy of **94.92%**. 
<br>

**Word2Vec Model** has second best Test Set accuracy of **93.89%** and **GloVe Embeddings Model** stood third with **93.13%** accuracy.
<br>

The **Averaging Model** has worst Test accuracy out of all the models i.e. **89.38%** which was fairly intuitive as the model was pretty basic in the sense that it was not considering the relative positioning of words in the reviews.
