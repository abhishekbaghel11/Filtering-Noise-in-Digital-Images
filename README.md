# Filtering-Noise-in-Digital-Images

Have you ever captured a photo using your camera and thought that "I had captured a perfect photo but why does it look so messy", then what you might have encountered is noise in the captured image. 
<br>
In the current world of digital imaging, one of the most challenging problems is the presence of noise. Whether you're capturing a photo with your smartphone or processing satellite imagery, noise can degrade image quality, making it difficult to extract meaningful information and visually unappealing. Noise is often regarded as the random variations in brightness or color, corrupting the details that truly matter. This noise can arise due to various reasons like camera lens, atmospheric conditions, different camera settings, long exposure, etc. Fortunately, we have many techniques in the image processing field to filter out this unwanted noise. One of the most common ways to remove noise is the use of filters. In this blog, we'll explore some of the most common methods for reducing additive noise, ensuring that our images are recovered without this unwanted noise.

## Introduction

We denote imaegs by two-dimensional functions of the form $f(x,y)$ where $x$ and $y$ represent the spatial coordinates and function value represents the intensity level (or the pixel value) at that point. Now, the image which has been degraded by noise can be formulated as follows: 
```math
g(x,y) = f(x,y)*h(x,y) + n(x,y)
```
where $g(x,y)$ is the degraded image, $f(x,y)$ is the original image (clear image free from degradation), $h(x,y)$ is the multiplicative noise and $n(x,y)$ is the additive noise.
<br> 
In this blog, we will consider that the image is degraded only by the additive noise (although, this is not the case in real world). So, the formulation becomes:
```math
g(x,y) = f(x,y) + n(x,y)
```
We try to obtain the true image from the degraded image using filters and the resulting image is an estimate of the true image which is denoted by $\hat{f}(x,y)$.

## Filters

### 1. Mean filters
Using the mean filter we try to remove the noise in the image by taking mean of the pixels present in the neighbouring region of the pixel on which we are operating. Mean filters tend to smooth local variations in an image. Mean filter tend to give to give good results when poisson noise is present in the image. The mean filters can be divided into different categories based on which type of mean is used:

- ### Arithmetic Mean Filter
When we take the arithmetic mean of the neighbouring pixels. It tends to smoothen the local variations in an image, and noise gets reduced as a result of blurring. The underlying operation is:
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
\hat{f}(x,y) = \frac{mn}{\sum_{(r,c) \in S_{xy}} \frac{1}{g(r,c)}} 
```


2. 
3. 
4. 


