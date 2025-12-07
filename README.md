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
    ├── fullmodulev3.ipynb    # Advanced grid detection with clustering
    └── fullmodulev4.ipynb    # Batch processing pipeline (recommended for multiple images)
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

4. **Batch Processing Pipeline** (`fullmodulev4.ipynb`) ⭐ **Recommended**
   - Combines best techniques from previous versions
   - Processes multiple module images from a folder
   - Automatic dark border cropping
   - Hough line detection + morphological operations
   - Peak detection with DBSCAN clustering
   - Organized output: each module's cells saved in separate folders
   - Works perfectly for batch processing multiple images

## Setup

### Prerequisites

- Python 3.7 or higher
- Conda (recommended) or pip

### Environment Setup

#### Option 1: Using Conda (Recommended)

1. **Create a new conda environment:**
   ```bash
   conda create -n cleanenv python=3.9
   conda activate cleanenv
   ```

2. **Install dependencies:**
   ```bash
   conda install -c conda-forge opencv numpy matplotlib scikit-image scikit-learn scipy tqdm
   ```
   
   Or using pip within the conda environment:
   ```bash
   pip install opencv-python numpy matplotlib scikit-image scikit-learn scipy tqdm
   ```

3. **Install Jupyter kernel for the environment:**
   ```bash
   conda install ipykernel
   python -m ipykernel install --user --name cleanenv --display-name "Python (cleanenv)"
   ```

4. **Verify setup:**
   - Open Jupyter Notebook
   - Select the kernel: **Kernel → Change Kernel → Python (cleanenv)**

#### Option 2: Using pip and virtualenv

1. **Create a virtual environment:**
   ```bash
   python -m venv cleanenv
   # On Windows:
   cleanenv\Scripts\activate
   # On Linux/Mac:
   source cleanenv/bin/activate
   ```

2. **Install dependencies:**
   ```bash
   pip install opencv-python numpy matplotlib scikit-image scikit-learn scipy tqdm ipykernel
   ```

3. **Install Jupyter kernel:**
   ```bash
   python -m ipykernel install --user --name cleanenv --display-name "Python (cleanenv)"
   ```

## Requirements

The project uses the following Python libraries with recommended versions:

| Package | Version | Purpose |
|---------|---------|---------|
| `opencv-python` | ≥4.5.0 | Image processing and computer vision |
| `numpy` | ≥1.19.0 | Numerical operations |
| `matplotlib` | ≥3.3.0 | Visualization |
| `scikit-image` | ≥0.18.0 | Additional image processing utilities |
| `scikit-learn` | ≥0.24.0 | Clustering algorithms (DBSCAN) |
| `scipy` | ≥1.6.0 | Signal processing (peak detection) |
| `tqdm` | ≥4.60.0 | Progress bars for batch processing |
| `ipykernel` | ≥6.0.0 | Jupyter kernel support |

**Install all dependencies at once:**

```bash
pip install opencv-python>=4.5.0 numpy>=1.19.0 matplotlib>=3.3.0 scikit-image>=0.18.0 scikit-learn>=0.24.0 scipy>=1.6.0 tqdm>=4.60.0 ipykernel>=6.0.0
```

**Or using conda:**

```bash
conda install -c conda-forge opencv numpy matplotlib scikit-image scikit-learn scipy tqdm ipykernel
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

**Recommended: Batch Processing** (`fullmodulev4.ipynb`)

1. Open `fullModules/fullmodulev4.ipynb`
2. Update the module folder path:
   ```python
   module_folder = r"path/to/your/module/images"
   ```
3. Run all cells to process all images in the folder
4. Extracted cells will be saved in `extracted_cells/` with subfolders for each module

**Single Image Processing:**

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

- Extracted cells are saved as images (size varies based on notebook)
- **Batch processing** (`fullmodulev4.ipynb`): Cells organized in folders, one per module image
- Original image metadata is preserved in filenames
- Failed extractions are logged with appropriate error messages
- Progress information displayed during batch processing

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
