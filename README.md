# Aspect Based Sentiment Analysis
A project for CS 583 uic that performs aspect based sentiment analysis 

The problem: An aspect is basically a feature of an entity. For eg. battery-life is an aspect of an entity called iPhone.   
The task is to predict the semantic polarity w.r.t aspect of an entity in a given sentence/user review.  
We assume that the sentence/review in question and the aspect is given to us. Our task is to predict the semantic label w.r.t aspect.   

My approach: 
The text was converted into 2 sets of features: 
1.	glove embeddings of all the words in the review
2.  distance embeddings of each word in the review   
The glove embeddings were computed based on the pretrained glove embeddings [2] on Twitter dataset.   
The distance embeddings were computed by passing the relative distance of each word in a 10-word window around the aspect into a keras embedding layer.    
The relative distances were calculated as shown in the following figure:   
![alt text](https://raw.githubusercontent.com/kashyap9395/Aspect_Based_Sentiment_Analysis/master/dist_img.png)  
Fig. from Soufian Jebbara et. al. [1]  
Here ‘stays fresh’ is the aspect.

Each glove embedding (of 50 dimensions) of a word in the 10-word window and the distance embedding (of 50 dimensions) of the same word were added to form a sort-of combined embedding for that word.   
Thus, now we had ten 50-dimensional vectors corresponding to 10 words in the 10-word window for each review. The size of the matrix came out to be (number of reviews, 10, 50)  
This matrix was then passed to a Recurrent Neural Network model consisting of a GRU layer of 100 units, a Maxout Dense layer of 100 units and another Maxout Dense layer of 3 units – each corresponding to the class +1, 0, -1. The activation function for the last layer was softmax. [1]  
This approach gave us an accuracy of 89% on Data 1 and 91% on Data2.    

References: 
[1] Soufian Jebbara and Philipp Cimiano, Aspect-Based Relational Sentiment Analysis Using a Stacked Neural Network Architecture  
[2] Jeffrey Pennington, Richard Socher, and Christopher D. Manning. 2014. GloVe: Global Vectors for Word Representation.

