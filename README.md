# Computer Vision and Image Processing Assignment

This repository contains implementation of various fundamental image processing techniques using OpenCV and NumPy.

## Tasks Implemented

1. **Loading and Displaying Images**
   - Loading images using OpenCV
   - Converting between color spaces (BGR to RGB)

2. **Intensity Level Reduction**
   - Reducing the number of intensity levels in grayscale images
   - Implemented for various levels: 128, 64, 16, 8, 2
   - Demonstrates the effect of quantization on image appearance

3. **Spatial Averaging**
   - Implementation of averaging filters with different neighborhood sizes
   - Kernel sizes: 3×3, 10×10, 20×20
   - Shows the blurring effect of larger kernels

4. **Image Rotation**
   - Rotating images by specific angles (45° and 90°)
   - Includes proper handling of image boundaries during rotation

5. **Block Averaging for Resolution Reduction**
   - Reducing spatial resolution using block averaging
   - Block sizes: 3×3, 5×5, 7×7
   - Demonstrates pixelation effect at larger block sizes

## Requirements

- Python 3.x
- OpenCV (cv2)
- NumPy
- Matplotlib

## Usage

Run the Jupyter Notebook `4251_Image_Processing_Assignment_01.ipynb` to see all the implementations and their visual results.

## Note on Intensity Level Reduction

If the 2-level intensity reduction doesn't display properly, it's due to the implementation logic. The recommended fix is to use a direct thresholding approach for the binary (2-level) case:

```python
def intensity_levels(image, levels):
    if not (levels > 0 and (levels & (levels-1) == 0)):
        raise ValueError("Number of levels must be a positive power of 2")
    
    # Special handling for 2-level case
    if levels == 2:
        threshold = 128
        return np.where(image >= threshold, 255, 0)
    
    # Original implementation for other levels
    factor = 256 // levels
    return (image // factor) * factor
```

This will ensure proper visualization of the binary image case.