---
title: "Masked autoencoder to reconstruct spatial image"
date: 2024-08-25 00:00:00 +0800
categories: MAE
tags: [autoencoder, MAE, spatial image]
---


Masked Autoencoders has been widely utilized across various domains, including the latest development of LLM. As it's sucess in respective fields, yielding meaningful insights from complex dataset. Would these autoencoders hold the potential to uncover complex relationships within spatial data, facilitating the extraction of valuable insights from diverse geospatial information. A trial in the blog has shown it might be used to filter out noisy spatial data, so to improve the focus to more significant features from the spatial map.

Masked Autoencoder is one of neural networks, which can address some particular challenges of complex data:

- Autoencoders emerged in the 1980s for unsupervised learning, focusing on reconstructing input data to learn efficient representations.

- Masked Autoencoder Development: This variant enhances traditional autoencoders by incorporating masking techniques, preventing access to future information during training, which is crucial for managing sequential data like text and time series.

- Masked Autoencoders are widely used in natural language processing, speech recognition, and anomaly detection. So far, it is still yet to demonstrate effective in spatial analysis, enabling the understanding of complex dependencies in datasets. This will require a comprehensive tests in the field.

- As for now they are integral to machine learning, driving progress in generative modeling, data compression, and feature learning.

Masked Autoencoder with Vision Transformer Model

When combined with a Vision Transformer (ViT) model, can we train a model for spatial data?. In general, the visual network design includes:

- Patch Embedding: Transforms input data through a convolutional projection.

- Blocks: Feature extraction using attention mechanisms and multi-layer perceptrons (MLPs).

- Spectral Attention: Manages spectral information through GSAttention and convolutional layers.

- Decoder: A linear transformation layer decodes data into a lower-dimensional space, followed by tailored decoder blocks for reconstruction.

To make the Masked Autoencoders one of potential methods for spatial feature extraction and uncovering complex relationships in geospatial information, we need to utilize the workflow for our own particular purpose.

In this post, I try to use the pre-trained model from meta to apply on a spatial image, to see how it works to reconstruct the image. This application will demonstrate the capabilities of Masked Autoencoders in spatial geoscience, in this case, abstract the data, so potentially to compress the data, or further improve for anaomaly detection.

The pre-trained model checkpoint can be found here,
[mae_visualize_vit_large](https://dl.fbaipublicfiles.com/mae/visualize/mae_visualize_vit_large.pth)

The following analysis, there are three distinct scenarios: one utilizing 25% masked patches, another employing 50% masked patches, and a third based on three iterations of 25% masked patches. 

If the results obtained from either the 50% masking or the iterative approach yield superior outcomes, it is imperative to consider the accuracy when applying for feature engineering.

Notably, when employing a 25% mask, the performance of the results derives abstract of the spatial distribution of the image. In contrast, the predictions derived from the 50% masked approach demonstrate enhanced detail and clarity. Similarly, the results from the three iterations of the 25% masked patches also exhibit improved performance metrics. This suggests that both the extent of masking and the iterative process will contribute in optimizing the efficacy of the model for feature extraction and overall image quality enhancement.


![MAE run on one image](img/mae1.png)


![MAE run 3 iterations](img/mae2.png)

