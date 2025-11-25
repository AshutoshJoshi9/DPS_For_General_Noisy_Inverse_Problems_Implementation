# Dataset Loading Changes - Summary

## 🎯 Overview
Modified the notebook to load **3 images from a Google Drive zip file** instead of a single hardcoded image path.

---

## 📝 Changes Made

### 1. **New Cell: Mount Google Drive (Section 3.5)**
- Added cell to mount Google Drive in Colab
- Provides instructions for users
- Gracefully handles non-Colab environments

### 2. **Modified Cell: Load and Prepare Test Image (Section 6)**
**Previous behavior:**
- Loaded single image from hardcoded path: `/content/69951.png`

**New behavior:**
- Loads images from a **zip file** on Google Drive
- Extracts zip to `/tmp/extracted_dataset`
- Searches for all image files (`.png`, `.jpg`, `.jpeg`, `.bmp`, `.tiff`)
- Randomly selects **3 images** (configurable via `num_images_to_load`)
- Stores all images in `test_images` list with metadata
- Displays all selected images in a grid

**Configuration variables:**
```python
zip_file_path = '/content/drive/MyDrive/dataset.zip'  # Change this
num_images_to_load = 3  # Adjust as needed
```

### 3. **Modified Cell: Create Degraded Measurement (Section 7)**
**Changes:**
- Now processes **all images** in `test_images` list
- Stores measurements in `measurements` list (one per image)
- Each measurement contains:
  - `original`: Original image tensor
  - `degraded`: Degraded measurement
  - `mask`: Inpainting mask (if applicable)
  - `name`: Image filename
- Displays all degraded images in a grid

### 4. **Modified Cell: Run DPS Inference (Section 8)**
**Changes:**
- Loops through all measurements
- Processes each image sequentially
- Shows progress for each image
- Stores results in `reconstructed_images` list
- Each result contains:
  - `reconstructed`: DPS output
  - `original`: Ground truth
  - `degraded`: Input measurement
  - `name`: Image filename
  - `time`: Processing time
- Displays summary statistics (total time, average time per image)

### 5. **Modified Cell: Visualize Results (Section 9)**
**Changes:**
- Creates a grid showing all images side-by-side
- Each row shows: Original | Degraded | Reconstructed
- Saves combined visualization as `dps_all_results.png`

### 6. **Modified Cell: Calculate Quality Metrics (Section 10)**
**Changes:**
- Calculates PSNR for **all images**
- Shows per-image metrics with quality ratings
- Computes **summary statistics**:
  - Average Input PSNR
  - Average Output PSNR
  - Average Improvement
- Provides interpretation for average performance

### 7. **Modified Cell: Save Results (Section 11)**
**Changes:**
- Saves results for **all images** with numbered filenames
- For each image (e.g., image 001):
  - `results/image_001_original.png`
  - `results/image_001_degraded.png`
  - `results/image_001_reconstructed.png`
  - `results/image_001_comparison.png` (3-panel comparison)

---

## 🚀 Usage Instructions

### Step 1: Prepare Your Dataset
1. Collect your images in a folder
2. Create a **zip file** of the folder
3. Upload to Google Drive

### Step 2: Update Configuration
In **Section 6** (Load and Prepare Test Image), modify:
```python
zip_file_path = '/content/drive/MyDrive/YOUR_DATASET.zip'  # Update this
num_images_to_load = 3  # Change if you want more/fewer images
```

### Step 3: Run the Notebook
1. Run all cells in order
2. The notebook will:
   - Extract the zip file
   - Select 3 random images
   - Process each through DPS
   - Display results and metrics
   - Save all outputs

---

## 📊 Output Structure

After running, you'll have:
```
results/
├── image_001_original.png
├── image_001_degraded.png
├── image_001_reconstructed.png
├── image_001_comparison.png
├── image_002_original.png
├── image_002_degraded.png
├── image_002_reconstructed.png
├── image_002_comparison.png
├── image_003_original.png
├── image_003_degraded.png
├── image_003_reconstructed.png
└── image_003_comparison.png

dps_all_results.png  (combined grid of all results)
```

---

## 💡 Key Features

✅ **Automatic extraction** - Handles zip files seamlessly
✅ **Flexible selection** - Randomly selects N images from dataset
✅ **Batch processing** - Processes all images with progress tracking
✅ **Comprehensive metrics** - Per-image and average statistics
✅ **Organized output** - Numbered files for easy identification
✅ **Error handling** - Clear error messages for missing files

---

## 🔧 Customization Options

### Change number of images:
```python
num_images_to_load = 5  # Process 5 images instead of 3
```

### Use specific images (instead of random):
Replace line in Section 6:
```python
# Random selection (current):
selected_images = random.sample(image_files, num_images_to_load)

# First N images (sequential):
selected_images = image_files[:num_images_to_load]

# Specific indices:
selected_images = [image_files[0], image_files[5], image_files[10]]
```

### Different image formats:
Modify in Section 6:
```python
image_extensions = ['.png', '.jpg', '.jpeg', '.bmp', '.tiff', '.webp']
```

---

## 🐛 Troubleshooting

**Error: "Zip file not found"**
- Ensure Google Drive is mounted (Section 3.5)
- Check the `zip_file_path` is correct
- Verify file exists in Google Drive

**Error: "No images found in the zip file"**
- Check zip file contains images with supported extensions
- Ensure images are not in deeply nested folders

**Warning: "Only X images available"**
- Zip contains fewer images than `num_images_to_load`
- Reduce `num_images_to_load` or add more images to zip

---

## 📌 Notes

- Processing time scales linearly with number of images
- Each image takes ~5-10 minutes on T4 GPU (1000 diffusion steps)
- 3 images ≈ 15-30 minutes total
- Consider reducing `diffusion_config['steps']` for faster testing

---

## ✨ Benefits of This Approach

1. **Reproducibility** - Dataset stored in one zip file
2. **Scalability** - Easy to test on multiple images
3. **Organization** - Automatic file naming and saving
4. **Statistics** - Understand average model performance
5. **Flexibility** - Quick configuration changes

---

**Last Updated:** November 13, 2025
