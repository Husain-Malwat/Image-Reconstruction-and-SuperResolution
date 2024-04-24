# Image Reconstruction and Super-Resolution

## a. Image Reconstruction 
This implementation utilizes Linear Regression in conjunction with Random Fourier Features (RFF) for image reconstruction. 

**Random Fourier Features (RFF):** RFF offers a means to approximate complex non-linear mappings by projecting input data into a higher-dimensional feature space via random Fourier basis functions. This transformation enables linear models to effectively capture intricate patterns present in the data.

**Linear Regression:** The Linear Regression model is then employed to learn the linear relationship between the high-dimensional RFF-transformed input coordinates and the corresponding pixel values in the image.

**Training and Evaluation:** Training involves optimizing the model parameters using Mean Squared Error (MSE) loss. Subsequently, the reconstructed image's fidelity is assessed using Root Mean Squared Error (RMSE) and Peak Signal-to-Noise Ratio (PSNR), providing quantitative comparisons against the ground truth.




## Metrics:

### 1. PSNR:

The PSNR is calculated using the following formula:

$\text{PSNR} = 10 \cdot \log_{10}\left(\frac{\text{MAX}^2}{\text{MSE}}\right)$

where:
<br>&nbsp; &nbsp; &nbsp; &nbsp; - **MAX:** The maximum possible pixel value of the image (e.g., 255 for an 8-bit image).
<br>&nbsp; &nbsp; &nbsp; &nbsp; - **MSE:** The Mean Squared Error between the original and reconstructed images.

- It is expressed in decibels (dB) and higher values are indicative of better image quality.
- A higher PSNR suggests that the reconstructed image is closer to the original, as the signal power (image content) is much greater than the noise power (differences between the images).

### 2. RMSE:

The Root Mean Squared Error (RMSE) is a metric used to quantify the average pixel-wise difference between the original and reconstructed images. It is calculated using the following formula:

$ \text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2} $

where:
- **$( \hat{y}_i $):** The predicted value.
- **$(y_i$):** The actual (ground truth) value.
- **$(n$):** The number of samples.

- RMSE provides an overall measure of the magnitude of differences between the original and predicted values.
- Lower RMSE values are generally desirable, indicating better agreement between the original and reconstructed images.
- RMSE is sensitive to outliers, meaning that large errors have a more significant impact on the overall metric.

In summary, RMSE is a useful metric for assessing the accuracy of a predictive model or reconstructed image, with lower values reflecting better performance.

## Random Missing data  

- For entirely masked image, i.e. all the pixel values are set to '0', RMSE value is equal to 0.6113, which serves as a reference point for comparison. 

- Lower RMSE values are better, and signify a closer resemblance to the original image. 

- Specifically, the calculated RMSE of 0.6113 can be considered indicative of the worst-case scenario for reconstruction error. Therefore, for a well-performing reconstruction algorithm, RMSE values should consistently fall below this threshold, and any deviations may suggest a degradation in image fidelity.


- As the mask percentage increases, you may observe an increase in RMSE. This is because a higher mask percentage corresponds to a greater portion of the image being hidden or set to zero. Consequently, the predicted values might deviate more from the ground truth, leading to higher RMSE values.

- Conversely, as the mask percentage increases, PSNR values may decrease. Higher mask percentages often introduce more noise or distortion in the reconstructed image, resulting in lower PSNR values. A lower PSNR indicates poorer image quality.

### General Observations:

- Lower mask percentages (e.g., 10-30%) may result in better reconstruction quality, as there is less information being masked.
- Moderate mask percentages (e.g., 40-60%) might show a balance between retaining image details and introducing some level of distortion.
- Higher mask percentages (e.g., 70-90%) often lead to more noticeable degradation in image quality, with increased errors in the reconstructed regions.

There are some deviations from general observation, from 10% to 20% and from 30% to 40%, the RMSE values increase sligtly instead of decreasing. If the pixels in the 10-20% and 30-40% ranges have specific patterns or features that make them more challenging for the algorithm, it could result in unexpected fluctuations in RMSE.