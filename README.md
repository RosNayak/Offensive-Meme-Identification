## Abstract
*Nowadays memes have become a way in which people express their ideas on social media. These memes can convey various views including offensive ones. Memes can be intended for a personal attack, homophobic abuse, racial abuse, attack on minority etc. The memes are implicit and multi-modal in nature. Here we analyze the meme by categorizing them as offensive or not offensive and this becomes a binary classification problem. We propose a novel offensive meme classification using the transformer-based image encoder, BiLSTM for text with mean pooling as text encoder and a Feed-Forward Network as a classification head. The SwinT + BiLSTM has performed better when compared to the ViT + BiLSTM across all the dimensions. The performance of the models has improved significantly when the contextual embeddings from DistilBert replace the custom embeddings. We have achieved the highest recall of 0.631 by combining outputs of four models using the soft voting technique*

## Dataset
<p align="center">
<img width="336" alt="Screenshot 2023-10-23 at 2 12 01 PM" src="https://github.com/RosNayak/Offensive-Meme-Identification/assets/45042726/3f127812-f085-453d-a3db-a660a3455da5">
</p>
We use the Multimodal Meme Dataset (MultiOFF) for Identifying Offensive Content in Image and Text. Each type of data file has three columns. The name of the image with the file extension is given in the first column. In the second column meme text is in English and finally, the third column is for annotation (“offensive” or “non-offensive”). The data is quite imbalanced with more
offensive data than non-offensive. The data is divided intotraining data constituting 60%, testing data constituting 20% and the remaining 20% is validation data

## Methodology

### Data Preprocessing
<p align="center">
<img width="466" alt="Screenshot 2023-10-23 at 2 02 02 PM" src="https://github.com/RosNayak/Offensive-Meme-Identification/assets/45042726/60c7dddc-5b54-4bd3-83ac-20137f626f95">
</p>
The dataset being used for the purpose of the analysis is a multi-modal dataset consisting of image and text pairs. The images had text embedded on them as they do not help in extracting the features from the image. Data augmentation techniques like Flip and Blur were applied to the image while training. We first converted the meme captions to lowercase, decontracted the words (eg. don't -> do not), removed special characters, and then converted the words to their base form using the lemmatization technique.

### Word embeddings
Computers cannot process data in the form of text. Hence words have to be represented in the form of numbers. In natural language processing, word embeddings are representations of the words as a vector of numbers. We have tried out two ways of embedding the words. In the first method, our model learns the embeddings during the training process. The embedding layer in PyTorch randomly initializes the embeddings of a word and then updates them during backpropagation. As these embeddings are learned during the training process, they are called task-specific embeddings. In
a second way, we have used DistilBert. DistilBert has an upper hand over some of the other models including Glove and Word2Vec because there is fixed representation in Word2Vec and Glove for each word, independent of the word’s context, whereas in DistilBert, word embeddings are produced that are context-dependent and they are informed by other words which are present around them. The type of embeddings used will be denoted by the "Embeddings" column in the results table later.

### Soft Voting
<p align="center">
<img width="297" alt="Screenshot 2023-10-23 at 2 05 23 PM" src="https://github.com/RosNayak/Offensive-Meme-Identification/assets/45042726/1507dd44-ce3f-4d24-8ca9-04cc64c66b4c">
</p>
Since we have trained multiple models, ensembling them to predict the final output will generally work better. Hence, we have used soft voting as the ensembling technique. In this technique, we take the average of the probabilities of each class obtained from multiple models to decide on the final prediction. A class is then considered to be the predicted class if it has the highest average probability. This is better when compared with the hard voting method because it considers the confidence level of each model. In Fig. 4 thepredicted probabilities from the four models are passed on to the soft voting layer to make the final decision.

### Model Architecture
<p align="center">
<img  src="https://user-images.githubusercontent.com/46472021/158046394-ba1a62c4-728e-49d9-a761-857da483a3a7.png" width="600" height ="600" />
 </p> 
 
## Results
 
 <p align="center">
<img  src="https://user-images.githubusercontent.com/46472021/158046446-4731c81b-3ccc-4ca7-bd50-67111b4fa0e6.png" width="850" height ="300" />
 </p> 
 
<p align="center">
<img  src="https://user-images.githubusercontent.com/46472021/158046482-e662f247-741f-43ed-9d62-9df3927262c0.png" width="850" height ="300" />
 </p> 
 

![image](https://user-images.githubusercontent.com/46472021/158046713-fa399068-f57f-4721-8c15-03b7c4ed78fc.png)

## References
* Shardul Suryawanshi, Bharathi Raja Chakravarthi, Mihael Arcan, and Paul Buitelaar, “Multimodal meme dataset (MultiOFF) for identifying offensive content in image and text,” European Language Resources Association (ELRA), May, 2020, pp. 32-41
