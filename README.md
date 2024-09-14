# Filtering-Noise-in-Digital-Images

Have you ever captured a photo using your camera and thought that "I had captured a perfect photo but why does it look so messy", then what you might have encountered is noise in the captured image. 
<br>
<br>
In the current world of digital imaging, one of the most challenging problems is the presence of noise. Whether you're capturing a photo with your smartphone or processing satellite imagery, noise can degrade image quality, making it difficult to extract meaningful information and visually unappealing. Noise is often regarded as the random variations in brightness or color, corrupting the details that truly matter. This noise can arise due to various reasons like camera lens, atmospheric conditions, different camera settings, long exposure, etc. Fortunately, we have many techniques in the image processing field to filter out this unwanted noise. One of the most common ways to remove noise is the use of filters. In this blog, we'll explore some of the most common methods for reducing additive noise, ensuring that our images are recovered without this unwanted noise.

## Introduction

We denote imaegs by two-dimensional functions of the form $f(x,y)$ where $x$ and $y$ represent the spatial coordinates and function value represents the intensity level (or the pixel value) at that point. Now, the image which has been degraded by noise can be formulated as follows: 
```math
g(x,y) = f(x,y)*h(x,y) + n(x,y)
```
where 
 - $g(x,y)$ is the degraded image
 - $f(x,y)$ is the original image (clear image free from degradation)
 - $h(x,y)$ is the multiplicative noise
 - $n(x,y)$ is the additive noise.

<br> 
In this blog, we will consider that the image is degraded only by the additive noise (although, this is not the case in real world). So, the formulation becomes:

```math
g(x,y) = f(x,y) + n(x,y)
```
<br>
We try to obtain the true image from the degraded image using filters and the resulting image is an estimate of the true image which is denoted by $\hat{f}(x,y)$.

## Filters

### 1. Mean filters
Using the mean filter we try to remove the noise in the image by taking mean of the pixels present in the neighbouring region of the pixel on which we are operating. Mean filters tend to smooth local variations in an image. Mean filter tend to give to give good results when poisson noise is present in the image. The mean filters can be divided into different categories based on which type of mean is used:

- ### Arithmetic Mean Filter
When we take the arithmetic mean of the neighbouring pixels. It tends to smoothen the local variations in an image, and noise gets reduced as a result of blurring.
```math
\hat{f}(x,y) = \frac{1}{mn} \sum_{(r,c) \in S_{xy}} g(r,c) 
```
where $r$ and $c$ are the row and column coordinates of the pixels contained in the neighbouring region $S_{xy}$ and the filter being m*n in shape.

- ### Geometric mean filter
When we take the geometric mean of the neighbouring pixels. It also achieves smoothing comparable to an arithmetic mean filter, but it tends to loss less image while doing the smoothening.
```math
\hat{f}(x,y) = \left(\prod_{(r,c) \in S_{xy}} g(r,c) \right)^{\frac{1}{mn}}
```
- ### Harmonic mean filter
When we take the harmonic mean of the neighbouring pixels. It works well for the salt noise and also gaussian noise, but fails for pepper noise. 
```math
\hat{f}(x,y) = mn \left(\sum_{(r,c) \in S_{xy}} \frac{1}{g(r,c)}\right)^{-1}
```
### 2. Median filter
When we take the median of the neighbouring pixels. It is the most common order-statistic (value is chosen based on ranking or order) spatial filter. It is particularly effective for salt-and-pepper noise with considerably less blurring than the mean filters.
```math
\hat{f}(x,y) = \underset{(r,c) \in S_{xy}}{\text{median}}\{g(r,c)\} 
```

### 3. Max filter
When we take the maximum pixel value in the neighbouring pixels. It is useful for finding the brightest points in an image or for brightening dark regions adjacent to bright areas and it also removes pepper noise.
```math
\hat{f}(x,y) = \underset{(r,c) \in S_{xy}}{\text{max}}\{g(r,c)\} 
```

### 4. Min filter
When we take the minimum pixel value in the neighbouring pixels. It is useful for finding the darkest points in an image or for darkening the bright regions adjacent to dark areas and it also removes salt noise.
```math
\hat{f}(x,y) = \underset{(r,c) \in S_{xy}}{\text{min}}\{g(r,c)\} 
```

### 5. Midpoint filter
When we take the average of the maximum and the minimum pixel values in the neighbouring pixels. It works best for randomly distributed noise like Gaussian noise.
```math
\hat{f}(x,y) = \frac{1}{2} \left[ \underset{(r,c) \in S_{xy}}{\text{max}}\{g(r,c)\}  + \underset{(r,c) \in S_{xy}}{\text{min}}\{g(r,c)\} \right]
```
### 6. Alpha-Trimmed Mean filter 
When we remove $\frac{d}{2}$ smallest and $\frac{d}{2}$ largest elements (according to intensity values) of $g(r,c)$ in the neighbourhood of $S_{xy}$, we represent the remaining pixels by $g_R(r,c)$. When the value of $d$ is $0$, the filter is the same as arithmetic mean filter and when the value of $d$ is $mn - 1$, then the filter acts as the median filter. The alpha-trimmed mean filter is useful for situations involving combination of noises such as salt-and-pepper and Gaussian filter.
```math
\hat{f}(x,y) = \frac{1}{mn-d} \sum_{(r,c) \in S_{xy}} g_R(r,c) 
```

### 7. Adaptive filter
This filter takes into regard how the image characteristics change from region to region and then applies the filter operation based on the characteristics of this region. The characteristics of a region can be defined by statistical measures like mean, variance, etc. 
```math
\hat{f}(x,y) = g(x,y) - \frac{\sigma_n^2}{\sigma_{S_{xy}}^2}\left[g(x,y) - \bar{z}\right]
```
where 
- $\sigma_n^2$ is the variance of the noise corrupting the true image $f(x,y)$
- $\sigma_{S_{xy}}^2$ is the local variance of the neighbouring pixels
- $\bar{z}$ is the local mean of the neighbouring pixels.

## Conclusion
In conclusion, dealing with additive noise is a crucial step in enhancing image quality, whether we're working with everyday photos or complex scientific imaging techniques using satellite images. By applying the above discussed spatial filter techniques such as mean filters, median filters, adaptive filters, and more advanced algorithms, it's possible to significantly reduce additive noise and recover those details that comprise the true image. However, the impact of noise in the digital image doesn't stop at additive forms. 
<br>
Multiplicative noise, which scales with the intensity of the image, presents its own challenges, especially in fields like medical imaging, remote sensing, satellite imagery, etc. The multiplicative noise is relatively difficult to remove and requires even more computational power for the calculations. While this blog focuses on the topic of additive noise, the same principles of filtering and restoration can be extended to handle multiplicative noise, often requiring more sophisticated approaches such as inverse filters, weiner filters, etc. Taking care of both the additive and the multiplicative noise will help to make your images more clear and extract more information from them and help to create more data for your particular task. 
