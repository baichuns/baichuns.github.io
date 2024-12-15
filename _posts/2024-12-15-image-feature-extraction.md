---
title: "Image edge and texture feature detection"
date: 2024-07-15 00:00:00 +0800
tags: [edge detection, canny, sato filter, phase congruence, phase symmetry]
---



In the field of image processing and computer vision, feature extraction is a crucial step that involves identifying and isolating various attributes or patterns within an image. Among the numerous features that can be extracted, edge and lineament features are particularly significant, especially in applications such as object detection, image segmentation, and geological analysis. Some methods are listed here,

- Edge Features: Edges represent significant changes in intensity or color in an image, marking the boundaries of objects. They are essential for understanding the structure and shape of objects within an image. Common methods for edge detection include:

- Sobel Operator: Utilizes convolution with Sobel kernels to compute the gradient magnitude and direction, highlighting edges.

- Canny Edge Detector: A multi-stage algorithm that includes noise reduction, gradient calculation, non-maximum suppression, and edge tracking by hysteresis, providing robust edge detection.

- Laplacian of Gaussian (LoG): Combines Gaussian smoothing with Laplacian filtering to detect edges by identifying regions of rapid intensity change.

- Sato Filter: A technique designed to enhance the detection of edges and textures in images, particularly useful in remote sensing applications. The Sato filter operates by applying a combination of directional filtering and statistical analysis to improve the visibility of features that may be obscured by noise or other artifacts.

Lineament features are linear features that can represent geological structures, roads, or other linear patterns in an image. Extracting lineament features often involves:

- Hough Transform: A technique that detects lines in an image by transforming points in the image space to a parameter space, allowing for the identification of straight lines.

- Directional Filtering: Applying filters that enhance specific orientations can help in detecting linear features by emphasizing their directionality.

- Morphological Operations: Techniques such as dilation and erosion can be used to enhance and extract line-like structures from binary images.


In this post, I compare the feature extraction results from Sato filter, Canny edge detection, phase congruency and symmetry. 

- Sato Filter: This technique is particularly effective in enhancing the detection of edges and textures in images, especially in remote sensing applications. The Sato filter employs a combination of directional filtering and statistical analysis, which allows it to improve the visibility of features that may be obscured by noise or other artifacts. Its strength lies in its ability to adapt to various orientations, making it suitable for detecting complex patterns in images.

- Canny Edge Detector: In contrast, the Canny edge detector is a multi-stage algorithm renowned for its robustness in edge detection. It involves several steps, including noise reduction, gradient calculation, non-maximum suppression, and edge tracking by hysteresis. This comprehensive approach ensures that the detected edges are thin and well-defined, making it highly effective for applications requiring precise edge localization.

- Phase Congruency: This concept is based on the idea that important features in an image, such as edges and corners, are characterized by a consistent phase relationship across different frequency components. The phase congruency method identifies points in an image where the phase of the Fourier transform is consistent, indicating the presence of significant features. This approach is advantageous because it is less sensitive to variations in illumination and contrast, making it robust for detecting features in challenging conditions.

- Phase Symmetry: Complementing phase congruency, phase symmetry focuses on the symmetry of the phase information in an image. It identifies regions where the phase of the frequency components exhibits a symmetrical pattern, which often corresponds to the presence of edges or other significant structures. Phase symmetry can be particularly useful for detecting features that are not easily captured by traditional edge detection methods, as it emphasizes the underlying structure rather than just intensity changes.



In summary, for the Sato filter and Canny edge detection serving the purpose of edge detection, the Sato filter excels in enhancing features in noisy environments, whereas the Canny edge detector is preferred for its accuracy and reliability in defining edges. The choice between the two methods ultimately depends on the specific requirements of the image processing task at hand.



More notes about sato filter, the size of the filter object in the Sato filter has a significant impact on the performance and results of edge and texture detection in images. Here is one key effect of filter object size:

Smaller Filter Sizes: These are more sensitive to fine details and can detect smaller features in an image. However, they may also be more susceptible to noise, leading to false detections.

Larger Filter Sizes: These can capture broader features and are generally more robust against noise. However, they may overlook finer details and lead to a loss of important information.


Here is an image example illustrating the results obtained from a few methods for extracting texture features.
![image example](img/img_2extract.png)





The Canny edge detector tends to detect more features than the Sato filter due to its multi-stage algorithm, which includes several steps designed to enhance edge detection. These steps—noise reduction, gradient calculation, non-maximum suppression, and edge tracking by hysteresis—ensure that the detected edges are thin and well-defined. This comprehensive approach allows the Canny edge detector to effectively identify and localize edges in an image, making it highly effective for applications requiring precise edge localization.

In contrast, the Sato filter is particularly effective in enhancing the detection of edges and textures in images, especially in noisy environments. However, its performance can be influenced by the amplitude of the features being detected. The Sato filter's ability to adapt to various orientations and enhance features relies on the filter size and the amplitude of the features. Smaller filter sizes may be more sensitive to fine details but can also be more susceptible to noise, while larger filter sizes may overlook finer details but are generally more robust against noise.

Thus, while amplitude does matter to the Sato filter in terms of its sensitivity and robustness, the Canny edge detector's methodology allows it to consistently detect a wider range of features regardless of amplitude variations.

The Sato filter is designed to enhance the detection of both ridge and valley features in images, making it effective for identifying a wider range of textures and structures. In contrast, the Canny edge detector primarily focuses on detecting edges, which are typically associated with significant changes in intensity or color, and may not effectively capture valley features in the same way as the Sato filter.

The misalignment of edges detected by the Sato filter and the Canny edge detector can be attributed to several factors related to their methodologies and the nature of the filters used. The Sato filter's reliance on phase information may also contribute to differences in edge detection. If the phase relationships in the image are not consistent, it could lead to variations in the detected edges compared to the Canny method, which focuses more on intensity gradients. The presence of noise or artifacts in the image can affect the performance of both detectors differently. The Canny edge detector is designed to handle noise through its multi-stage process, while the Sato filter's performance can be influenced by the amplitude of the features being detected, potentially leading to misalignment.

Phase congruency is designed to identify significant features such as edges and corners by looking for points where the phase of the Fourier transform is consistent. This allows it to capture a wider range of features that are critical for image analysis possiblly. Phase congruency is less sensitive to changes in illumination and contrast. This robustness enables it to identify more features that might be missed by other methods. In contrast, phase symmetry focuses on the symmetry of phase information, which may not capture as many features since it is more specific to symmetrical patterns. This specificity can limit its ability to detect a broader range of features compared to phase congruency.

![image example](img/img_2extract_b.png)
In this image, the colors represent different edge detection methods: blue indicates the Canny edge detector, red corresponds to the Sato filter, green represents phase congruency, and violet signifies phase symmetry. 

