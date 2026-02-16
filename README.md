# Group_5_Image_Smoothing_Using_Mean_and_Gaussian-Filters

**Course:** DCIT407 - Image Processing  
**Group:** 5  

 ## 👥 Group Members
*

| No. | Student Name | Student ID |
| :--- | :--- | :--- |
| 1 | **Keren Kuma Lartey** | 11173490 |
| 2 | **Favour Ackonu** | 11014111 |
| 3 | **Ebenezer Ofori Acquah** | 11154989 |
| 4 | **EMMANUEL FRIMPONG KWAO** | 11353279 |
| 5 | **Osei Jephthah Afriyie** | 11354112 |
| 6 | **Kwesi Ahenkorah Gyamenah** | 11116940 |
| 7 | **Fenteng Kwame Michael** | 11210750 |
| 8 | **Richmond Manu Andoh** | 11254304 |
| 9 | **Bless Adeti** | 11015523 |

---

##  Abstract
This project investigates **Spatial Domain Filtering** techniques for image restoration, specifically focusing on **Image Smoothing** (low-pass filtering). We implement and analyze two fundamental linear shift-invariant (LSI) filters: the **Mean (Box) Filter** and the **Gaussian Filter**. The study evaluates their efficacy in mitigating Gaussian noise while assessing their impact on image fidelity, specifically edge preservation and artifact introduction.

---

## 1. Introduction
Image smoothing is a critical preprocessing step in computer vision systems. Its primary objective is to modify the signal of an image to reduce high-frequency noise and irrelevant detail, thereby enhancing the image for subsequent analysis such as edge detection or segmentation.

Smoothing is mathematically modeled as a **Convolution** operation. If $f(x,y)$ serves as the input image and $h(x,y)$ as the filter kernel, the smoothed image $g(x,y)$ is obtained by:
$$g(x,y) = f(x,y) * h(x,y)$$

This project contrasts the implementation and results of using a uniform kernel (Mean) versus a weighted kernel (Gaussian).

---

## 2. Theoretical Framework

### 2.1 The Mean Filter (Box Filter)
The Mean filter is the simplest form of linear smoothing. It functions by replacing each pixel's value with the arithmetic mean of the intensity values within a local neighborhood (kernel).

* **Kernel Structure:** It utilizes a "rectangular pulse" kernel where all coefficients are uniform. For a $3 \times 3$ kernel, the weight of each element is $1/9$.
* **Mechanism:**
    $$g(x,y) = \frac{1}{mn} \sum_{(s,t) \in S_{xy}} g(s,t)$$
    Where $S_{xy}$ is the set of coordinates in a rectangular sub-image window of size $m \times n$.
* **Limitations:** While computationally efficient, the Mean filter is not "smooth" in the frequency domain. It tends to produce "ringing" artifacts and severe blurring of edges because it assigns equal weight to pixels regardless of their spatial distance from the center.

### 2.2 The Gaussian Filter
The Gaussian filter is a sophisticated smoothing operator that represents the kernel weights as a 2D Gaussian distribution (a bell curve). Unlike the Mean filter, pixels closer to the center of the kernel contribute significantly more to the weighted average than those at the periphery.

* **Mathematical Definition:**
    The 2D Gaussian kernel is defined by:
    $$G(x,y) = \frac{1}{2\pi\sigma^2} e^{-\frac{x^2 + y^2}{2\sigma^2}}$$
    Here, $\sigma$ (sigma) represents the standard deviation. A higher $\sigma$ yields a wider bell curve, resulting in a greater degree of smoothing.

* **Key Properties:**
    1.  **Rotational Symmetry:** The Gaussian filter smooths equally in all directions, avoiding the directional bias often seen in box filters.
    2.  **Separability:** A significant computational advantage. The 2D Gaussian operation can be separated into two 1D convolutions (horizontal then vertical):
        $$G(x,y) = g(x) \times g(y)$$
        Where the 1D kernel is:
        $$g[x] \approx \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{x^2}{2\sigma^2}}$$
    3.  **Optimal Localization:** It minimizes the product of position and frequency uncertainties, ensuring no "ringing" artifacts are introduced.

---

## 3. Methodology & Implementation
The project is implemented in **Python** using the following scientific stack:

* **OpenCV (`cv2`):** For efficient image I/O and applying filter kernels.
* **NumPy:** For matrix operations and generating synthetic Gaussian noise.
* **Matplotlib:** For visualizing the spatial domain results and histograms.


---

## 4. Evaluation Metrics

To quantitatively and qualitatively compare the Mean and Gaussian filters, the following evaluation criteria are used:

### 4.1 Mean Squared Error (MSE)

The **Mean Squared Error (MSE)** measures the average squared difference between the original image and the filtered image:

$$
MSE = \frac{1}{MN} \sum_{x=1}^{M} \sum_{y=1}^{N} \left[ f(x,y) - g(x,y) \right]^2
$$

Where:
- $f(x,y)$ is the original image  
- $g(x,y)$ is the filtered image  
- $M \times N$ is the image size  

Lower MSE values indicate better noise reduction while preserving image fidelity.

### 4.2 Visual Analysis

In addition to numerical evaluation, visual inspection is performed to assess:

- Edge preservation  
- Degree of smoothing  
- Presence of artifacts (e.g., ringing or excessive blurring)  

Combining quantitative metrics with visual analysis provides a more comprehensive comparison of filter performance.

---

### Project Structure
```text
Group_5_Image_Smoothing/
├── Mean_Filter_Implementation/
│   ├── Mean_Filter_Custom_Images.ipynb   # Analysis of Box/Mean Filter
│   └── [Source Images]
├── project/
│   ├── gaussin_filtering.ipynb           # Analysis of Gaussian Filter & Noise Generation
│   └── images/
│       └── noisy.jpg
├── README.md                             # Documentation
