# Solar Cell Extraction

A computer vision project for extracting individual solar cells from solar module images. This repository contains preprocessing pipelines and extraction algorithms developed for research at IIT Mandi.

## Overview

This project provides tools and pipelines to automatically extract individual solar cells from images of solar modules. The extraction process involves image preprocessing, grid detection, and perspective transformation to isolate and normalize individual cells for further analysis.

## Project Structure

```
SolarCellExtraction/
├── cellExtract/              # Individual cell extraction from cropped module images
│   ├── preprocessing1.ipynb  # Initial preprocessing experiments
│   ├── preprocessing2.ipynb  # Advanced preprocessing with morphological operations
│   ├── preprocessing3.ipynb  # Alternative extraction method using contour detection
│   └── cell_extract_pipeline.ipynb  # Complete pipeline for batch processing
│
└── fullModules/              # Full module processing and cell extraction
    ├── fullmodulev1.ipynb    # Hough line detection approach
    ├── fullmodulev2.ipynb    # Morphological operations with peak detection
    └── fullmodulev3.ipynb    # Advanced grid detection with clustering
```

## Features

### Cell Extraction Pipeline (`cellExtract/`)

The cell extraction pipeline processes images of solar modules to extract individual cells:

1. **Image Preprocessing**
   - Median filtering for noise reduction
   - CLAHE (Contrast Limited Adaptive Histogram Equalization) for contrast enhancement
   - Adaptive thresholding for binary conversion

2. **Grid Detection**
   - Morphological operations to detect vertical and horizontal grid lines
   - Intersection point detection
   - Convex hull computation for corner detection

3. **Cell Extraction**
   - Perspective transformation to normalize cell orientation
   - Output: 256×256 pixel normalized cell images

### Full Module Processing (`fullModules/`)

Processes complete solar module images with various approaches:

1. **Hough Line Detection** (`fullmodulev1.ipynb`)
   - Canny edge detection
   - Hough line transform for grid detection
   - Automatic dark border cropping

2. **Morphological Operations** (`fullmodulev2.ipynb`)
   - Morphological opening for line extraction
   - Peak detection using projection profiles
   - DBSCAN clustering for line merging

3. **Advanced Grid Detection** (`fullmodulev3.ipynb`)
   - Combined morphological and Hough-based approaches
   - Automatic cell extraction from detected grid

## Requirements

The project uses the following Python libraries:

- `opencv-python` (cv2) - Image processing and computer vision
- `numpy` - Numerical operations
- `matplotlib` - Visualization
- `scikit-image` - Additional image processing utilities
- `scikit-learn` - Clustering algorithms (DBSCAN)
- `scipy` - Signal processing (peak detection)
- `tqdm` - Progress bars for batch processing

Install dependencies:

```bash
pip install opencv-python numpy matplotlib scikit-image scikit-learn scipy tqdm
```

## Usage

### Individual Cell Extraction

For processing cropped module images:

1. Open `cellExtract/cell_extract_pipeline.ipynb`
2. Update the input and output directory paths:
   ```python
   input_dir = "path/to/your/dataset"
   output_dir = "path/to/output/directory"
   ```
3. Run all cells to process the entire dataset

### Full Module Processing

For processing complete solar module images:

1. Choose the appropriate notebook based on your module characteristics:
   - `fullmodulev1.ipynb` - Best for modules with clear grid lines
   - `fullmodulev2.ipynb` - Best for modules with varying lighting
   - `fullmodulev3.ipynb` - Most robust approach with clustering

2. Update the image path in the notebook
3. Run cells sequentially to extract all cells from the module

## Methodology

### Preprocessing Steps

1. **Noise Reduction**: Median filtering (3×3 kernel) to reduce salt-and-pepper noise
2. **Contrast Enhancement**: CLAHE with clip limit 2.0 and tile grid size 8×8
3. **Thresholding**: Adaptive thresholding using mean or Gaussian method
4. **Grid Detection**: Morphological opening with rectangular kernels to extract grid lines
5. **Corner Detection**: Convex hull or intersection-based corner detection
6. **Perspective Transformation**: Warp perspective to normalize cell orientation

### Grid Detection Techniques

- **Morphological Operations**: Using structuring elements to detect vertical and horizontal lines
- **Hough Transform**: Line detection from edge maps
- **Peak Detection**: Projection profiles to find grid line positions
- **Clustering**: DBSCAN to merge nearby detected lines

## Output

- Extracted cells are saved as 256×256 pixel images
- Original image metadata is preserved in filenames
- Failed extractions are logged with appropriate error messages

## Notes

- Some images may fail extraction if grid lines are not clearly visible
- Parameters may need adjustment based on image quality and module characteristics
- The pipeline handles common image formats: `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tif`, `.tiff`

## Research Context

This project is part of research work at IIT Mandi focused on solar cell analysis and quality assessment. The extracted cells can be used for:
- Defect detection
- Performance analysis
- Quality grading
- Automated inspection systems

## License

This project is for research purposes at IIT Mandi.

## Contact

For questions or contributions, please contact the research team at IIT Mandi.
