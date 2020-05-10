EEG-Signals-Detection
===

Electroencephalogram (EEG) is a method used to measure the sudden electrical activity of the brain, this is because neurons in the brain produce electrical signals that are captured by the EEG. In this section, I will explain how to detect muscle artifact signals and ictal signals. The method I use in this chapter is the Support Vector Machine.

The steps are as follows:
1. Make sure you have EEG signals datasets.
2. EEG Signals Preprocesing
    - cut of signals
    - remove signals noise
3. EEG Signals Decomposition
    - Discrete Wavelet Transform (DWT)
4. Features Extraction
    - Mean
    - Max
    - Min
    - Entropy
    - Deviance
5. Classification
    - Support Vectore Machine

---

if you want to practice, you can download EEG datasets which upload by University of Bonn. link as follows: http://epileptologie-bonn.de/cms/front_content.php?idcat=193&lang=3

---
*Note : Python is The application that I use to solve this problem. So that make sure it is installed on your computer*
