TITLE: APPAREL RECOMMENDER SYSTEM
A women apparel recommendation system based on Amazon datasets that recommends similar items based on Text and Image Features in this project.

BUSINESS OBJECTIVE:
“Judging by Amazon’s success, the recommendation system works. The company reported a 29% sales increase to $12.83 billion during its second fiscal quarter, up from $9.9 billion during 
the same time last year. A lot of that growth arguably has to do with the way Amazon has integrated recommendations into nearly every part of the purchasing process…”

PROBLEM STATEMENT:
Given a json file for extracting the 180k apparel(women's tops) images from amazon.com we need to recommend the similar apparel based on a specific product query and number of apparels to be recommended at a time. 
Each of those images will be recommended based on following fields:

1. asin  ( Amazon standard identification number)

2. brand ( brand to which the product belongs to )

3. color ( Color information of apparel, it can contain many colors as   a value ex: red and black stripes ) 

4. product_type_name (type of the apperal, ex: SHIRT/TSHIRT )

5. medium_image_url  ( url of the image )

6. title (title of the product.)

7. formatted_price (price of the product)

APPROACH:
We have two approaches here,

1.Content based recommendation: As its name suggests, we do content based recommendation, means its based on tittle text,Description text, images.

2.Collobarative filtering based recommendation: This recommendations are done based on the behaviour of the user.
   But, Amazon doesnt provide users data, so we are not going to do collobarative filtering. Instead we use content based.
   
  PLAN OF ATTACK:
  
  1.DATASETS AND INPUTS
https://www.kaggle.com/ajaysh/women-apparel-recommendation-engine-amazoncom#tops_fashion.json

    You can download the feature vectors from given link
   16k_data_cnn_features.npy: https://drive.google.com/open?id=0BwNkduBnePt2c1BkNzRDQ1dOVFk 
   bottleneck_features_cnn.npy : https://drive.google.com/open?id=0BwNkduBnePt2ODRxWHhUVzIyWDA
   
2.SOFTWARE REQUIREMENTS:
ANACONDA:https://www.anaconda.com/download/#linux
TENSOR FLOW:https://www.tensorflow.org/
PLOTLY:https://plot.ly/
PIL:https://pillow.readthedocs.io/en/5.2.x/

3. DATA ACQUISITION:
We can use Amazon's Product Advertising API, and get the required data. We took womens tops as the dataset . It consists of 183000 datapoints, having 19 features each.
Index(['asin', 'author', 'availability', 'availability_type', 'brand', 'color',
       'editorial_reivew', 'editorial_review', 'formatted_price',
       'large_image_url', 'manufacturer', 'medium_image_url', 'model',
       'product_type_name', 'publisher', 'reviews', 'sku', 'small_image_url',
       'title'],
      dtype='object')
      
But we use only 6 features for this project.
->asin ( Amazon standard identification number)
->brand ( brand to which the product belongs to )
->color ( Color information of apparel, it can contain many colors as a value ex: red and black stripes )
->product_type_name (type of the apperal, ex: SHIRT/TSHIRT )
->medium_image_url ( url of the image )
->title (title of the product.)
->formatted_price (price of the product)

4.DATA CLEANING:
->Basic Stats of every feature
->Removed missing datapoints 
->Removed all the datapoints that have null value in feature columns formatted_price and color.
->Keeping only  feature named medium_image_url this is url for our apparel image of medium size. (Uisng Python Imaging Library (PIL) got all those images and saved them.)
->Remove near duplicate items.The feature title, there are many similar duplicate texts only varying in colors or sizes in its title.So, we remove these duplicates, by comparing words in the title, we also remove title that contains less than 5 words.
    After removing all these duplicates we have our dataset around 16000 datapoints.

5.TEXT PROCESSING:
->stopwords removal
-> spaces
->alpha numeric characters removal 
->lowering the aplhabet cases

6.TEXT BASED PRODUCT RECOMMENDATION:
 Feature title was used to recommend apparels. In the next part used images for recommendation, we also combine both title and images for recommendation. 
 The main concept in this text based is we convert title text into vectors and find closest vectors to it using equilidean distance. 
 The more closer the both vectors the most similar it is. so to convert text into vectors, we use
 
 1.Bag of words model

 2.tf-idf model

 3.idf model

 4.word2vec model

 5.idf weighted word2vec model

 6.weighted similarity using brand and color

 7.visual features based using convolution neural networks

SUMMARY
->Used Text , color , brand and Images as features to recommend similar product to user
->Tried different weights to see the how features are recommended to user based on weights

Steps by steps
->Loading and reading data from json file
->Some insight of data how the features are , number of datapoints , number of features
->Pre-processing on text
->Trying different featurization
->Recommending similar based product using bag of words , Tf-idf, idf, w2v,avg-w2v
->Using visual features to recommend products to user.
->Tried combinnation of text , color, brand and image to recommend similar based produc to user.

_END_



