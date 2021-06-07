# Record-Linkage



This project aims at linking the firm names recorded in the case files to their names in the registered companies dataset. It’s a simple string matching problem where techniques like fuzzy matching can be used directly on the complete dataset but which will take a lot of computation and memory resources.


# Extraction:

Using the Beautiful soup package, the case details are extracted from each HTML file. The details mainly include the petitioner and respondent’s name, which will help us figure out whether it’s a company. A list of words helps us in deciding whether a name is a company name or not. 


# Preprocessing:

Text Hero package is used to preprocess the data and make it refined before clustering.
The functions I have used to clean the data are:
Remove whitespaces and punctuations
Remove stopwords
Removing diacritics

A different approach is taken by removing those words from the company names which are common to all companies and don’t reveal a lot of information about the company. 

# Modeling:


Approach 1:

sparse_dot_topn provides a fast way to performing a sparse matrix multiplication followed by top-n multiplication result selection.
Comparing very large feature vectors and picking the best matches, in practice often results in performing a sparse matrix multiplication followed by selecting the top-n multiplication results. In this package, we implement a customized Cython function for this purpose. When comparing our Cythonic approach to doing the same use with SciPy and NumPy functions, our approach improves the speed by about 40% and reduces memory consumption. The matches are found by comparing the Levensteihn distances between each of these names.



Approach 2:

I will be applying  Kmeans clustering on the two datasets and find similarities between them based on that cluster’s top words. Each cluster will find the best match with a cluster from the other dataset, once this is done the fuzzy matching can be done between the two clusters using Levenshtein distance. This method will lessen the computations significantly.



