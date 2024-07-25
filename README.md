# Tweet-Analyser (Sentiment Analysis from Tweets)
**Objective :** Implement a Support Vector Machine classifier (or SVM) that classifies tweets according to their sentiment, i.e. positive or negative. We will derive features from the text of the tweets to build and train the classifier on part of the dataset. We will then test the accuracy of your classifier on an unseen portion of the dataset.

**Simple data input and pre-processing:**
parse_data_line()
• The function “parse_data_line” extracts the label and text from a data line, which is a list of the contents of a row from the file.
• The second item of the list (index=1) is label and the third is the text (index=2)
pre_process():
• The function ‘pre_process’ takes a statement as an argument and splits it on whitespace resulting in a list of words from statement.
• We are normalising all the words to lower case and return the resultant list.

**Simple feature extraction:**
• The function ‘to_feature_vector’ takes tokens (list of words) as an input and returns a dictionary containing features as keys and weights as values.
• We’re using binary feature values in this; meaning that if a word is present, it will be assigned a value of 1 and the words not present will be defaulted to 0
• We also add the features seen to a global dictionary to be considered for analysis and improvements.

**Cross-validation on training data:**
• The function “cross_validate()” takes the dataset and number of folds as arguments
• We call it with training data and folds=10 to perform a 10-fold cross validation
• To perform a 10-fold cross validation, we need to divide the whole dataset into 10
sets of data and use 1 part as test data.
• To achieve this, we define fold_size which is 1/10th of the whole dataset and then use
it along with a pointer to define the start point of test data.
• We train the classifier on the remaining 9 parts of the dataset
• Then we classify the test data to predict its labels and compare it with the true values
• We calculate and store the precision, recall, f-score and accuracy of each iteration
• Then we calculate the mean of all these values and return them (cv_results)

**Error analysis:**
• Used the 1st fold of the training data for the error analysis
• To get test_data, we hardcoded the range from 0 to 2684, approximately 1/10th. We
use this number as the whole train_dataset has around 26832 records
• Then use the remaining portion as training data
• Then we called the already defined method to creation the confusion matrix heatmap
• We also save the false-positives and false-negatives to a file: “error_analysis.csv”
• Analysis:
o FP = 223 and FN = 181; they’re close together, and the results are not skewed heavily towards one. So, this doesn’t give us much information
o Uponinvestigatingtheerrorfile,noticedthatstop-wordsarealsobeingused as features, which is not informative
o Also, symbols at the beginning and end of a word cause confusion
o User tags and links are not useful and could be pre-processed
o Individualwordscansometimesleadtoerrors.e.g.“Idon’tlike”isnegative,
but can be classified as positive because of the word like. So, maybe unigrams is not the best approach.

**Optimising pre-processing and feature extraction:**

• Using the following table to record values for each optimisation made
• All values are mean values for 10-fold cross validation

| Optimisations Done |  Precision |    Recall   |   F-Score  | Accuracy|
| ------------------ |:----------:| -----------:|------------|:-------:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
| col 3 is      | right-aligned | $1600 
| col 2 is      | centered      |   $12 
| zebra stripes | are neat      |    $1 

***Optimisations Done                           Precision              Recall              F-Score                Accuracy***

Without optimisation                          0.7833                0.8074               0.7911                  0.8074
     
Pre-process Improvement
• Remove words starting with @ and http       0.7746                0.7987               0.7826                  0.7987                    
• Remove punctuations
• Remove stop words

Pre-process Improvement
• Add Lemmatizing to pre- processing          0.8268                0.8284                0.8273                 0.8284

Using TfidVectorizer for unigram and          0.8547                0.8562                0.8527                 0.8562
bigram both

Discarding negative stop words from           0.8707                0.8719                0.8691                 0.8719
stop-word removal as they’re portray 
strong negative emotions’

     
