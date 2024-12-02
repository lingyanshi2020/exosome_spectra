CANCER CLASSIFIER BASED ON RAMAN SPECTRA OF EXOSOMES
USING PCA-LDA
Workflow Overview

**1. PCA Dimensionality Reduction**
- It is an unsupervised machine learning algorithm that identifies a smaller set of features (principal components), which are linear combinations of the original features. 
These components capture the majority of the variance in the dataset.
Input: Processed Exosome Spectra File Path
       Intended Number of Principal Components
Output: Scatterplot of the spectra along 2 Principal Components
        Explained and Cumulative Variance Plot
        3D PCA plot 
        Loadings plot for n PCs
  
**2. PCA Feature Extraction**
- The weighted sum of loadings for each wavenumber is obtained by multiplying the absolute loading of each wavenumber by the explained 
variance of the corresponding PC and adding these values across all selected PCs.
- The top n% of wavenumbers, based on the weighted sum of loadings, are identified as the most relevant features for subsequent analyses.
Input: Percentage of wavenumbers to be extracted
Output: List of top n% of wavenumbers


**3. Spectral Similarity Analysis**
-  Perform Min-Max normalization first of exosome and lipid spectra.
-  For each lipid spectrum, mean squared error, cosine similarity, and cross-correlation coefficient are calculated with the exosome spectra 
only at the wavenumbers identified by PCA Feature Extraction.
-  Average similarity scores are calculated for each lipid spectrum across all exosome spectra.
Input: Exosome Spectra File Path
       Lipid Spectra File Path
Output: Ranked Similarity scores for each lipid subtype

**4. PCA-LDA for Cancer Type Classification**
- LDA is a supervised machine learning algorithm that optimizes class separation by finding the linear combination (Linear Discriminants or LDs) 
of PCA extracted features that maximizes between-class variance while minimizing within-class variance.
- Data split 50/10/40: train, validation, and test sets
- After training, the LDA model's performance is visualized on the validation set 
- Then, the model is tested on the test set. 
- For robustness and reliability of results, this process is iterated 15 times, with performance metrics averaged across the runs.
Input: Exosome File Path
       Exosome Labels
Output:Scatterplot of test set data
       Confusion Matrix of test set data
       Average Performance Metrics

  
**NOTES**
- Ensure that all exosome and lipid spectra have the same wavenumbers and data lengths
- Ensure that all exosome spectra are pre-processed with min-max normalization and baseline correction with Asymmetric Least Squares (ALS).




Code authors: Jorge Villazon and Nathaniel Dela Cruz






Shift + Enter to add a new line
