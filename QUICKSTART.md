# Quick Start Guide

Get up and running with DPS in 5 minutes! 🚀

## ⚡ 30-Second Setup

### On Google Colab
```
1. Open: https://colab.research.google.com
2. Upload: DPS_for_General_Noisy_Inv_Problems_implementation.ipynb
3. Runtime → Change runtime type → GPU (T4)
4. Run all cells (top to bottom)
5. Check Google Drive for results!
```

## 📋 Prerequisites

- ✅ Google Account (for Colab)
- ✅ Google Drive with space for datasets
- ✅ Sample images (or use the provided FFHQ samples)

## 🎬 Step-by-Step

### Step 1: Mount Google Drive
```python
from google.colab import drive
drive.mount('/content/drive')
```

### Step 2: Run Initialization (Sections 1-5)
- GPU check ✅
- Install packages ✅
- Download model ✅
- Load libraries ✅
- Setup DPS ✅

**Time**: ~5 minutes

### Step 3: Load Images (Section 6)
```python
# Modify this line with your zip file path:
zip_file_path = '/content/drive/MyDrive/your_images.zip'
num_images_to_load = 3
```

**Expected**: Loads 3 random images from your dataset

### Step 4: Choose Your Task (Section 4)
Available tasks:
```python
# Option 1: Inpainting (recommended for first run)
task_config = {
    'conditioning': {'method': 'ps', 'params': {'scale': 0.5}},
    'measurement': {
        'operator': {'name': 'inpainting'},
        'mask_opt': {
            'mask_type': 'box',
            'mask_len_range': (96, 97),
            'image_size': 256,
            'margin': 32
        }
    }
}

# Option 2: Super-Resolution
task_config = {
    'conditioning': {'method': 'ps', 'params': {'scale': 1.0}},
    'measurement': {
        'operator': {
            'name': 'super_resolution',
            'scale_factor': 4
        }
    }
}

# Option 3: Gaussian Deblurring
task_config = {
    'conditioning': {'method': 'ps', 'params': {'scale': 0.3}},
    'measurement': {
        'operator': {
            'name': 'gaussian_blur',
            'kernel_size': 61,
            'intensity': 3.0
        }
    }
}
```

### Step 5: Run Inference (Sections 7-9)
```
Section 7: Create degraded measurements
Section 8: Run DPS Inference ⏳ (5-10 min per image)
Section 9: Visualize results
```

**Expected**: See before/after images

### Step 6: Calculate Metrics (Sections 10-16)
```
Section 10: PSNR metrics
Section 11-12: Install LPIPS/SSIM
Section 13: Comprehensive metrics
Section 14: Visualization
Section 15: Export to CSV
```

**Expected**: Detailed metrics and plots

### Step 7: Save & Download (Section 17-21)
```
Section 17: Save individual images
Section 20: Download to Google Drive
```

**Expected**: All results in `DPS_Results/` on Drive

## 📊 Understanding Results

### Visual Results
- **Left**: Original image
- **Middle**: Degraded (what model receives)
- **Right**: DPS Reconstruction

### Metrics Interpretation
| Metric | Good Value | Better if |
|--------|-----------|-----------|
| **PSNR** | > 30 dB | Higher ↑ |
| **SSIM** | > 0.85 | Higher ↑ |
| **LPIPS** | < 0.10 | Lower ↓ |
| **MSE** | < 0.01 | Lower ↓ |
| **MAE** | < 0.05 | Lower ↓ |

## 💡 Common Configurations

### Fast Inference (1-2 min per image)
```python
diffusion_config['steps'] = 250
diffusion_config['timestep_respacing'] = '250'
```

### High Quality (5-10 min per image)
```python
diffusion_config['steps'] = 1000
diffusion_config['timestep_respacing'] = '1000'
```

### Process Multiple Images
```python
num_images_to_load = 10  # Load 10 images instead of 3
```

### Change Noise Level
```python
'noise': {'name': 'gaussian', 'sigma': 0.1}  # Higher = more noise
```

## 🐛 Troubleshooting

### "Out of Memory" Error
```python
# Solution 1: Process fewer images
num_images_to_load = 1

# Solution 2: Use fewer steps
diffusion_config['steps'] = 250

# Solution 3: Restart and clear memory
from google.colab import runtime
runtime.unassign()
```

### "File not found" Error
```python
# Check your zip file path
# Use Google Drive file browser to get correct path
# Format: /content/drive/MyDrive/filename.zip
```

### GPU Not Available
```python
# In Colab: Runtime → Change runtime type → GPU
import torch
print(torch.cuda.is_available())  # Should print True
```

### Model Download Fails
```python
# Manual download option
# Put ffhq_10m.pt in Google Drive: MyDrive/ffhq_10m.pt
# Update path in Section 4
```

## 📈 Next Steps

After first run:

1. **Try Different Tasks**
   - Modify task_config in Section 4
   - Re-run Sections 5-20

2. **Use Your Own Data**
   - Create zip file with your images
   - Upload to Google Drive
   - Update zip_file_path in Section 6

3. **Fine-tune Parameters**
   - Adjust scale factor (smaller = smoother, faster)
   - Change number of diffusion steps
   - Modify noise levels

4. **Analyze Results**
   - Download CSV metrics
   - Plot improvements
   - Compare with baseline methods

5. **Save to GitHub**
   - Download results from Drive
   - Add to GitHub repository
   - Update README with results

## 📚 More Information

- 📖 **Full Guide**: See `README.md`
- 📊 **Metrics Explained**: See `METRICS_GUIDE.md`
- 🎨 **Inpainting Tips**: See `INPAINTING_GUIDE.md`
- 🤝 **Contribute**: See `CONTRIBUTING.md`
- 📁 **Structure**: See `REPOSITORY_STRUCTURE.md`

## ⏱️ Time Estimates

| Component | Time |
|-----------|------|
| Setup & Download | 5-10 min |
| Load Images | 2-3 min |
| Create Measurements | 1 min |
| Inference (1 image, 1000 steps) | 8-10 min |
| Inference (1 image, 250 steps) | 2-3 min |
| Metrics Calculation | 2-5 min |
| **Total (first run)** | **20-30 min** |

## 🎯 Success Checklist

- [ ] Google Colab notebook uploaded
- [ ] GPU enabled in runtime
- [ ] Google Drive mounted
- [ ] Images loaded successfully
- [ ] Task configuration set
- [ ] Inference ran without errors
- [ ] Results visualized
- [ ] Metrics calculated
- [ ] Results downloaded to Drive
- [ ] Ready for GitHub!

## 🎓 Learning Path

### Beginner
1. Run default inpainting task
2. Observe results
3. Check metrics interpretation
4. Done! 🎉

### Intermediate
1. Try super-resolution task
2. Adjust diffusion steps (250 vs 1000)
3. Compare metrics across tasks
4. Experiment with different images

### Advanced
1. Create custom operators
2. Fine-tune conditioning parameters
3. Analyze metric improvements
4. Submit results to community

## 🚀 Production Use

For production inference:

```python
# Use 250 steps for speed
diffusion_config['steps'] = 250

# Batch process multiple images
num_images_to_load = 100

# Export metrics for analysis
# Results automatically saved to CSV
```

## 📞 Need Help?

1. **Check Troubleshooting section** (above)
2. **Review README.md** for detailed docs
3. **Check Google Colab console** for error messages
4. **Try clearing Colab memory** and restarting
5. **Open GitHub issue** if stuck

## ✨ Quick Tips

💡 **Pro Tips:**
- Always enable GPU in Colab (Runtime → Change runtime type)
- Use 250 steps for testing, 1000 for final results
- Save images with descriptive names for easy tracking
- Export metrics CSV for comparison with papers
- Keep notebook cells organized for reproducibility

---

**Ready to go?** → Open Colab and start the notebook! 🚀

**Questions?** → Check README.md or open a GitHub issue

**First time?** → This should take ~30 minutes total. Enjoy! 😊
