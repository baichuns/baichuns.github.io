---
title: "Similarity Mapping with Limited Positive Samples"
date: 2024-09-20 00:00:00 +0800
categories: similarity_mapping
published: True
tags: [similarity, mapping, positive samples]
---


Positive-Unlabeled Learning (PUL) can be though of as one of similarity mapping method, and is designed to address situations where a dataset includes only a small number of labeled positive samples, with the rest remaining unlabeled. The foundation of PUL can be traced back to seminal works such as Elkan and Noto's study in 2008, Mordelet and Vert's bagging-based method in 2013, and Hsieh, Niu, and Sugiyama's classification approach for positive-unlabeled and biased negative data.

Undoubtedly, PUL falls within the category of supervised learning and has garnered significant attention in machine learning research in recent years. This interest is largely driven by the prevalence of datasets dominated by unlabeled data, such as those encountered in malware detection and disease identification through medical imaging.

Here is a method for more stable estimation of unlabeled positivity and an integrated workflow to enhance classification confidence. This approach involves an iterative learning process, where a new classifier is trained using labeled data while continuously re-sampling the unlabeled samples.


Classification from positive and unlabeled (PU) data is a variation of standard classification, where the training dataset includes both positive and unlabeled examples. The key assumption is that each unlabeled example could belong to either the positive or negative class. For a detailed review of various PU learning methods, refer to J. Kristen's work from 2019. The figure below highlights how PU learning differs from standard classification.

![PUL J.Kristen](gif/pul1.png)

There are two main types of Positive-Unlabeled (PU) learning: inductive and transductive PU learning (M. Fantine and V. Jean-Philippe, 2010). Inductive PU learning focuses on building a model that can predict outcomes for new incoming data. In contrast, transductive PU learning is designed to identify positive instances within unlabeled samples. For example, in mineral exploration (as illustrated in Figure 1), transductive PU learning uses regional spatial data and known positive samples to identify potential deposits in unlabeled regions. This disclosure is specifically designed to address transductive PU problems.  

A key theoretical foundation of PU learning is that the ratio of the conditional distributions of positive and unlabeled examples monotonically increases with the ratio of positive to negative examples (Elkan and Noto, 2008; Scott and Blanchard, 2009). In practice, this principle is applied by training a standard classifier to distinguish between positive and unlabeled examples, while compensating for the presence of hidden positives within the unlabeled data. This often involves prioritizing false-negative errors over false positives.  

Figure 2 illustrates this process. It depicts the probabilities of positive and unlabeled data, where their overlap represents the likelihood of hidden positives among the unlabeled examples. Using these probabilities, a standard model is trained to classify positive and unlabeled data, as shown by the black dashed line. To adjust for hidden positives, the model is refined to include both positive and unlabeled data, represented by the yellow dashed line.  

While various classification methods, such as Random Forest and XGBoost, can theoretically be applied to PU learning, some algorithms are better suited for this task. In this disclosure, Support Vector Machine (SVM) has been the primary algorithm used for addressing PU learning challenges.


![PUL standard classifier](gif/pul2.png)


# Example

Here, I demonstrate the application of this algorithm to synthetic data using toy datasets from scikit-learn. These datasets are used to compare the performance of different clustering algorithms.

![toy datasets](gif/pul3.png)


![result 1](gif/pul4.png)

The first column shows results from the standard classifier, the second column from Mordelet & Vert’s bagging classifier, the third column from Elkan & Noto’s PUL classifier, and the last column presents the transductive PUL classifier from this disclosure.

![result 2](gif/pul5.png)

The accuracy of four algorithms (standard, bagging Elkan & Noto, and transductive PU) is shown here by hiding varying sizes of positive samples. The results are presented for the following datasets: (a) circle dataset, (b) moons dataset, and (c) blobs dataset.

![result 3](gif/pul6.png)