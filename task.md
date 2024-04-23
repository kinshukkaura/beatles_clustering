# The Beatles
The Beatles are regarded as the most influential band of all time. 

With over 279 text files obtained from the media company, removing duplicates and files with missing information, we have **213** unique lyrics. 

Answers to questions that will give us more insight into the data:- 

1. How many songs feature the song name in the song lyric?  \
**142**   
    Each file name has the song name in lower case with whitespaces and punctuations replaced by '-'. We transform the lyric in the same format and check whether the file name exists in the transformed lyrics. \
    We utilize the string library to get replace punctuations.

2. How many of the songs feature at least one pair of lines that rhyme? \
**143**  
    To check whether a pair of lines rhyme, we extract the last word of each sentence of the lyric by again removing punctuation and splitting the lyric.
    We utilize the library **pronouncing** that provides, for a given word, a list of words that rhyme with it phonetically.  
    Finally we check if consecutive pairs of lines have rhyming last words or not.

## Clustering
### Data Preprocessing
* Remove stopwords using an expansive list coded with specific observations.
* Tokenize the lyrics and remove any non-alphabet characters.
* Use a lemmatizer for each word and combine the lyrics.
### Literature Review
To cluster text, we often need numerical or vector representation of the text for classification or clustering.
Traditionally, count Vectorizers and then TFIDF vectorizers are utilized. They would measure the count of a specific word in a document(single lyric) relative to the total count of the word in all documents(all lyrics). These methods have the drawback of understanding linguistic information about the words such as the real meaning of the words, similarity with other words etc. Since the task involves clustering based on themes of songs, it is important that words like 'adore' and 'love' are represented similarly.

Hence, we utilize the embeddings from SentenceTransformers, which is a Python framework for state-of-the-art sentence, text and image embeddings.\
Word embeddings give us a way to use an efficient, dense representation in which similar words have a similar encoding. Instead of specifying the values for the embedding manually, they are trainable parameters (weights learned by the model during training).We utilize an all-round model tuned for many use cases with over 1 billion parameters.

To achieve this unsupervised task of clustering, we utilize two different approaches, **Hierarchical clustering** and **K-Means clustering**. While we could also consider the same models used for embedding, these models typically require much larger datasets and lack flexibility. And with a small dataset of just 215 data points, it seems more prudent to use traditional approaches.
#### Hierarchical clustering

Hierarchical clustering is an alternative approach which does not require that we commit to a particular choice of K. Another advantage is hierarchical clustering results in an ttractive tree-based representation of the observations called a dendrogram.\
Here, we use bottom up or agglomerative clustering. This is the most common type of hierarchical clustering and refers to the fact that a dendrogram is build starting from the leaves and combing clusters up to the trunk.
The algorithm can be summarized as
1. Start with each point in its own cluster.
2. Identify the closest two clusters and merge them.
3. Repeat Step 2.
4. Stop when all points are in a single cluster.

![Alt text](image.png)
The height of fusing (on vertical axis) indicates how different the two observations (or groups of observations) are. Considering a threshold of 2.0, we can cut the tree into **4** clusters.

![Clusters after PCA](image-1.png)

![Alt text](image-2.png)

#### K-means clustering
In K-means clustering, we aim to partition the observation into a pre-specified number of clusters based on a distance metric.
We want to partition the observations into
K clusters such that the total within-cluster variation, summed over all K clusters, is as small as possible.

**Algorithm**
1. Randomly assign a number, from 1 to K, to each of the observations. These
serve as initial cluster assignments for the observations.
1. Iterate until the cluster assignments stop changing: \
a) For each of the K clusters, compute the cluster centroid. The k-th cluster centroid is the average of the observations currently in the k-th cluster. \
b) Assign each observation to the cluster whose centroid is closet (where closest is defined using Euclidean distance).

![Word Cloud with k-means clusters](image-3.png)
Elbow method
![Alt text](image-5.png)



![Alt text](image-4.png)

Silhouette Score = **(b-a)/max(a,b)** where \
a = average intra-cluster distance, i.e the average distance between each point within a cluster.\
b = average inter-cluster distance i.e the average distance between all clusters.

### Prediction of new lyrics (K-means)


'0': sailing metal machine exploring deep blue marine current journey diving exploring conquer deep blue sea discover mystery underwater history gliding light shining bright mile venturing night watching school creature sea metal living carefree diving exploring conquer deep blue sea discover mystery underwater history endless journey  return shore remember ocean.

'2': time alive sound twinkling light air snow fall spirit felt wonderful time year laughter ringing ear season season peace time share home caroler sing song voice wing child excitement glee dream tree wonderful time year laughter ringing ear season season peace time share spread kindness love wonderful time year laughter ringing ear season season peace time share embrace open heart smile.

'1': filled pain search ease strain journey step love light heart peace day love conquer fear love gentle touch love healing return tenfold love grow light heart peace day love conquer fear love spread kindness love light heart peace day love conquer fear love embrace open heart smile love.

'2': filled chaos strife search lead life love conquer fear peace spread peace plant seed filled harmony glee live peace mountain valley sing peace build close peace plant seed filled harmony glee live peace spread land sea peace set spirit free peace plant seed filled harmony glee live peace peace brighter day filled peace.

'3': morning light feel free sun shining walking hand road dream step living scene walking sky blue breeze blowing feel flying true walking living life field laugh play flower feel perfect day dance rhythm heart beat feel walking sky blue breeze blowing feel flying true walking living life smile feel dream true moment brand walking sky blue breeze blowing feel flying true walking living life night fall star shine bright walking endless.