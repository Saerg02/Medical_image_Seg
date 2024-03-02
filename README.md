# Tissue_image_Seg

Approach:
1.	Data Preprocessing:
To handle the data during the training, the original images were chopped into smaller images with size (256,256,3), as well as the labels, resulting in a dataset with a larger volume compared to the original data.
For normalization, the values in the image arrays were divided by 255.0 and transformed as float16 to reduce volume.
The label was transformed into a single-channel image since they have the same values.
The entire image data array was divided into 4 parts to avoid exceeding memory limitations.
20% of the original data was split to create a validation dataset.

2.	Model and Metrics:
A U-Net model with 30 billion parameters was used to train on this dataset sufficiently.
The output layer generated an image with size (256, 256, 1).
Loss function: 'binary_crossentropy'
Metrics: 'accuracy'

3.	Training:
The entire training process was performed in four iterations, with each iteration using one part of the data. This approach was necessary to handle the large array of training data effectively.
Findings:
1.	Data Volume: The chopping operation significantly increased the data volume compared to the original data.
2.	Model Performance: The prediction performance may not meet expectations, even though the accuracy during training was relatively high. This could be attributed to the small proportion of '1' labels in the data, causing class imbalance.
3.	Probability Thresholding: Some predictions have very low probabilities, which cannot be effectively plotted with a threshold of 0.5. However, these low probabilities can still provide meaningful information. Adjusting the probability threshold (e.g., setting it to 0.01) can lead to better visualization of the predictions.
