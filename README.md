# American Sniper Tweets Topic Extraction

This project extract top trending topics from a corpus of tweets related to American Sniper movie.

All the code is in notebooks directory. The main program is in ipython notebook. I chose ipython notebook because development is much faster with it. But i will also package the code as pure python program soon.

##How to run the program - 
You will need ipython, ipython-notebooks as dependencies to run this program. And you may also need some other libraries as well. Please refer the code and install them with "pip install <package-name>"

Then you can just walk through the notebook running each snippet.

##Description
1. First raw tweets are loaded from "as.txt"
2. Then these tweets are cleaned and tokenized into words. Cleaning the data involves - 
   a. Removing stopwords
   b. Removing punctuations
   c. removing non ascii characters such as smileys.
   d. removing words with less than two character such as "i", "am"
3. Next, the hashtags are extracted from tweets and converted into words. If the hashtag is in camel case or separated by "_" then we just extract words by regex and splitting. Otherwise we use Viterbi Algorithm to decide the best split for the hashtag. The baseline corpus used to decide the split is in "big.txt". The first task completes here.
4. Then term-document matrix is formed using TF-IDF as values to understand importance of each keyword to a tweet. NLTK bigram extractor is used to extract bigrams along with word.
5. Total importance of word in a set of tweets is considered as sum of TF-IDF values of that word.
6. Then the matrix is sorted according to total TF-IDF to identify top phrases.
7. Upon observation of results from last step, a slight improvement is achieved by clubbing some words and phrases together boosing their values. For ex, "Oscar 2015", "Oscar", "2015" are clubbed together.
8. In the end, top results are displayed.

##Improvements
Some words are synonyms in final list and they all should be clubbed together. But finding synonyms for each word in a corpus is expensive. The only option i found is Wordnet in NLTK but it also give erraneous results due to multiple meanings of same word. Further things are complicated, since synonyms of phrase is not possible to compute by just lookup. 

If the desired output is flexible and actual topics are to be derived, then a topic is an idea which is a distribution over words. In this direction, we can use Topic Modelling to derive topics in unsupervised manner. An illustration is shown with Non-Negative Matrix Factorization in last part. This approach indeed gives better results. 
