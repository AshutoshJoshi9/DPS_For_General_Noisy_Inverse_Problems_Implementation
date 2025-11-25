# Repository Structure Guide

This document explains the organization of the DPS Implementation repository.

## 📁 Directory Layout

```
DPS_FOR_GENERAL_NOISY_INVERSE_PROBLEMS/
├── README.md                              # Main documentation (start here!)
├── LICENSE                                # MIT License
├── .gitignore                             # Git ignore rules
├── CONTRIBUTING.md                        # Contribution guidelines
├── requirements.txt                       # Python dependencies
│
├── DPS_for_General_Noisy_Inv_Problems_implementation.ipynb
│   └── Main notebook with full implementation
│       Sections: 1-21 (Setup to Results)
│
├── METRICS_GUIDE.md                       # Detailed metrics explanation
├── DATASET_LOADING_CHANGES.md             # Data loading documentation
├── INPAINTING_GUIDE.md                    # Inpainting task guide
│
├── diffusion-posterior-sampling/          # Original DPS repository
│   ├── guided_diffusion/                  # Core DPS implementation
│   ├── util/                              # Utility functions
│   ├── configs/                           # Configuration files
│   └── models/                            # Model weights storage
│
├── results/                               # (Generated) Output images
│   ├── image_001_original.png
│   ├── image_001_degraded.png
│   ├── image_001_reconstructed.png
│   └── image_001_comparison.png
│
├── dps_comprehensive_metrics.csv          # (Generated) Metrics table
├── dps_all_results.png                    # (Generated) All results
├── metrics_comparison.png                 # (Generated) Metrics plots
│
└── FFHQ_256_(images_only)/                # (Optional) Sample images
    └── ffhq256/
        ├── 00000.png
        ├── 00001.png
        └── ...
```

## 📄 File Descriptions

### Core Files

#### `README.md`
**Most Important!** Start here for:
- Overview of the project
- Quick start guide
- Installation instructions
- Feature highlights
- Results and metrics
- References and citations

#### `DPS_for_General_Noisy_Inv_Problems_implementation.ipynb`
Main Jupyter notebook containing:
- 21 sections of implementation
- Complete DPS pipeline
- Metric calculations
- Google Drive integration
- Results visualization

**How to use:**
1. Upload to Google Colab
2. Run sections sequentially (1 → 21)
3. Modify task_config in Section 4 for different tasks
4. Results saved to Google Drive automatically

### Documentation Files

#### `METRICS_GUIDE.md`
Complete guide to all 5 metrics:
- PSNR (Peak Signal-to-Noise Ratio)
- SSIM (Structural Similarity Index)
- LPIPS (Learned Perceptual Image Patch Similarity)
- MSE (Mean Squared Error)
- MAE (Mean Absolute Error)

Use when:
- Interpreting metric values
- Understanding metric ranges
- Deciding which metric to use
- Comparing with other papers

#### `DATASET_LOADING_CHANGES.md`
Explanation of batch image loading:
- How to load images from Google Drive zip files
- Random vs sequential selection
- Handling different image formats
- Error handling and troubleshooting

#### `INPAINTING_GUIDE.md`
Detailed guide for inpainting tasks:
- Box mask generation
- Random mask generation
- Parameter tuning
- Visual examples

#### `CONTRIBUTING.md`
Guidelines for contributing:
- How to report bugs
- How to suggest features
- Code style guidelines
- Pull request process

### Configuration Files

#### `.gitignore`
Specifies files to exclude from version control:
- Large data files (*.zip, *.pt)
- Generated outputs (results/, *.csv)
- Python cache files (__pycache__)
- Virtual environments (venv/)
- IDE settings (.vscode/, .idea/)

#### `requirements.txt`
Python package dependencies:
- PyTorch and torchvision
- Image processing libraries
- Visualization tools
- Metrics libraries (LPIPS, scikit-image)

### License

#### `LICENSE`
MIT License for the project:
- Permits commercial use
- Requires attribution
- Comes with no warranty
- Full text included

### Source Code

#### `diffusion-posterior-sampling/`
Original DPS repository:
```
├── guided_diffusion/
│   ├── condition_methods.py    # Posterior sampling conditioning
│   ├── measurements.py          # Measurement operators
│   ├── gaussian_diffusion.py    # Diffusion process
│   ├── unet.py                  # U-Net architecture
│   └── ...
├── util/
│   ├── img_utils.py             # Image utilities
│   ├── logger.py                # Logging utilities
│   └── ...
├── configs/                     # Configuration files for different tasks
├── scripts/                     # Utility scripts
└── models/                      # Model storage
```

**Cloned from**: https://github.com/DPS2022/diffusion-posterior-sampling

### Generated Files (After Running)

#### `results/`
Output images from inference:
- `image_001_original.png` - Original ground truth
- `image_001_degraded.png` - Degraded measurement
- `image_001_reconstructed.png` - DPS reconstruction
- `image_001_comparison.png` - Side-by-side comparison

#### `dps_comprehensive_metrics.csv`
Metrics export in CSV format:
- Per-image metrics
- Average metrics row
- All 5 metrics (PSNR, SSIM, LPIPS, MSE, MAE)
- Input/Output/Improvement columns

#### `dps_all_results.png`
Combined visualization showing:
- All processed images
- Original → Degraded → Reconstructed
- Suitable for presentations and papers

#### `metrics_comparison.png`
6-plot dashboard showing:
- PSNR comparison
- SSIM comparison
- LPIPS comparison
- MSE comparison
- MAE comparison
- Average improvements bar chart

### Optional Sample Data

#### `FFHQ_256_(images_only)/`
Optional sample dataset:
- 256×256 RGB face images
- From CelebA-HQ dataset
- Used for testing and examples

## 🔄 Workflow

### Typical Usage Flow

```
1. Clone repository
2. Read README.md
3. Run notebook in Colab
4. Modify configuration in Section 4
5. Run Sections 5-20 sequentially
6. Download results from Google Drive
7. (Optional) Commit improvements back
```

### For Development

```
1. Fork repository
2. Create feature branch
3. Make changes (code + docs)
4. Test locally/on Colab
5. Submit pull request
6. Address review comments
7. Merge to main
```

## 📊 Size Guidelines

### What to Commit to Git
✅ `README.md` - Documentation  
✅ `.gitignore` - Configuration  
✅ `requirements.txt` - Dependencies  
✅ `LICENSE` - License  
✅ `*.md` - Documentation files  
✅ `DPS_for_General_Noisy_Inv_Problems_implementation.ipynb` - Main notebook  
✅ `CONTRIBUTING.md` - Guidelines  
✅ Sample images (if small)  

### What NOT to Commit
❌ `*.pt` - Model weights (too large)  
❌ `*.zip` - Dataset archives (too large)  
❌ `results/` - Generated outputs  
❌ `*.csv` - Generated metrics  
❌ `__pycache__/` - Python cache  
❌ `.venv/` - Virtual environment  
❌ `diffusion-posterior-sampling/` - Submodule (clone separately)  

## 🎯 Quick Navigation

| I want to... | Read this file |
|:------------|:-------------:|
| Get started | `README.md` |
| Understand metrics | `METRICS_GUIDE.md` |
| Learn about inpainting | `INPAINTING_GUIDE.md` |
| Load custom data | `DATASET_LOADING_CHANGES.md` |
| Contribute code | `CONTRIBUTING.md` |
| See dependencies | `requirements.txt` |
| Run the code | `DPS_for_General_Noisy_Inv_Problems_implementation.ipynb` |

## 📝 Creating New Files

When adding new files, follow this naming convention:
- Markdown docs: `UPPERCASE_WITH_UNDERSCORES.md`
- Python files: `lowercase_with_underscores.py`
- Config files: `config_name.yaml` or `config_name.json`

## 🔗 Important Links

- **Original Paper**: https://arxiv.org/abs/2209.06604
- **Original Repo**: https://github.com/DPS2022/diffusion-posterior-sampling
- **LPIPS Library**: https://github.com/richzhang/PerceptualSimilarity
- **Guided Diffusion**: https://github.com/openai/guided-diffusion

---

**Last Updated**: November 2025  
**Version**: 2.0
