# 🎨 Inpainting with DPS - Complete Guide

## Problem Fixed

You encountered this error when trying inpainting:
```
ValueError: Require mask
```

**Root Cause**: Inpainting requires a **mask** to specify which regions to fill, but the notebook wasn't generating or passing it.

## ✅ Solution Applied

I've updated **two cells** in the notebook:

### 1. Cell 18 (Create Degraded Measurement)
Now automatically:
- Detects when task is inpainting
- Generates a mask using the config parameters
- Passes mask to the forward operator
- Displays both mask and masked image

### 2. Cell 20 (Run Inference)
Now automatically:
- Passes the mask to the conditioning function for inpainting
- Ensures mask is used during the diffusion process

## 🎯 How to Use Inpainting

### Step 1: Configure for Inpainting

In **Cell 12 (Section 4)**, set:

```python
task_config = {
    'conditioning': {
        'method': 'ps',
        'params': {'scale': 0.5}  # 0.3-0.5 recommended for inpainting
    },
    'measurement': {
        'operator': {'name': 'inpainting'},
        'noise': {
            'name': 'gaussian',
            'sigma': 0.0  # Usually 0.0 for inpainting
        },
        'mask_opt': {
            'mask_type': 'box',           # Type of mask
            'mask_len_range': (128, 129), # Size of box to inpaint
            'image_size': 256,
            'margin': (16, 16)            # Margin from edges
        }
    }
}
```

### Step 2: Run All Cells

Just run from **Section 5** onwards. The notebook now handles everything automatically!

## 🎭 Mask Types Available

### 1. Box Mask (Center Region)
```python
'mask_opt': {
    'mask_type': 'box',
    'mask_len_range': (128, 129),  # Size of box: min=128, max=129
    'image_size': 256,
    'margin': (16, 16)  # Margin from edges (height, width)
}
```
- **Use case**: Fill center portion of image
- **mask_len_range**: `(128, 129)` → 128×128 box
- **mask_len_range**: `(64, 65)` → 64×64 box
- **mask_len_range**: `(192, 193)` → 192×192 box
- **margin**: Distance from edges where box center can be placed

### 2. Random Mask
```python
'mask_opt': {
    'mask_type': 'random',
    'mask_prob_range': (0.3, 0.7),  # 30-70% of pixels masked
    'image_size': 256
}
```
- **Use case**: Random scattered missing regions
- **mask_prob_range**: `(0.3, 0.7)` → 30-70% pixels removed
- Good for restoring images with random damage

### 3. Extreme Mask (Inverse Box)
```python
'mask_opt': {
    'mask_type': 'extreme',
    'mask_len_range': (128, 129),
    'image_size': 256,
    'margin': (16, 16)
}
```
- **Use case**: Keep only center region, remove surroundings
- Opposite of 'box' type

## 📊 Mask Visualization

After running **Cell 18**, you'll see:
```
Mask                          Masked Image
┌────────────┐               ┌────────────┐
│ ████████████│               │            │
│ ██        ██│               │  CONTENT   │
│ ██  [    ]]██│    →          │            │
│ ██        ██│               │  VISIBLE   │
│ ████████████│               │            │
└────────────┘               └────────────┘
White = Keep                 Black region = to inpaint
Black = Inpaint              
```

## 🎨 Example Configurations

### Small Center Region Inpainting (64×64)
```python
task_config = {
    'conditioning': {'method': 'ps', 'params': {'scale': 0.5}},
    'measurement': {
        'operator': {'name': 'inpainting'},
        'noise': {'name': 'gaussian', 'sigma': 0.0},
        'mask_opt': {
            'mask_type': 'box',
            'mask_len_range': (64, 65),  # Small 64×64 box
            'image_size': 256,
            'margin': (16, 16)
        }
    }
}
```

### Medium Center Region Inpainting (128×128)
```python
task_config = {
    'conditioning': {'method': 'ps', 'params': {'scale': 0.5}},
    'measurement': {
        'operator': {'name': 'inpainting'},
        'noise': {'name': 'gaussian', 'sigma': 0.0},
        'mask_opt': {
            'mask_type': 'box',
            'mask_len_range': (128, 129),  # Medium 128×128 box
            'image_size': 256,
            'margin': (16, 16)
        }
    }
}
```

### Large Center Region Inpainting (192×192)
```python
task_config = {
    'conditioning': {'method': 'ps+', 'params': {'scale': 0.7, 'num_sampling': 5}},
    'measurement': {
        'operator': {'name': 'inpainting'},
        'noise': {'name': 'gaussian', 'sigma': 0.0},
        'mask_opt': {
            'mask_type': 'box',
            'mask_len_range': (192, 193),  # Large 192×192 box
            'image_size': 256,
            'margin': (16, 16)
        }
    }
}
```

### Random Scattered Inpainting
```python
task_config = {
    'conditioning': {'method': 'ps+', 'params': {'scale': 0.5, 'num_sampling': 5}},
    'measurement': {
        'operator': {'name': 'inpainting'},
        'noise': {'name': 'gaussian', 'sigma': 0.0},
        'mask_opt': {
            'mask_type': 'random',
            'mask_prob_range': (0.3, 0.7),  # 30-70% pixels masked
            'image_size': 256
        }
    }
}
```

## ⚙️ Hyperparameter Tuning for Inpainting

### Guidance Scale
| Scale | Effect | When to Use |
|-------|--------|-------------|
| 0.3   | Gentle, smooth | Small regions, natural textures |
| 0.5   | **Recommended** | Most cases |
| 0.7   | Strong, sharp details | Large regions, complex structures |

### Method
- **`ps`**: Fast, standard
- **`ps+`**: **Recommended** - More robust for complex inpainting

### Expected Quality
- **Small regions (64×64)**: Excellent, nearly perfect
- **Medium regions (128×128)**: Very good
- **Large regions (192×192)**: Good, may have some blending artifacts

## 🔄 Workflow

1. **Set configuration** (Cell 12)
2. **Load model** (Cell 14)
3. **Load image** (Cell 16)
4. **Generate mask** (Cell 18) - **Automatic now!**
5. **Run inference** (Cell 20) - Mask passed automatically
6. **View results** (Cell 22)

## 🎯 Tips for Best Results

1. **Start with scale=0.5** and adjust based on results
2. **Use ps+ method** for difficult cases (especially large regions)
3. **Keep sigma=0.0** for inpainting (no additional noise)
4. **Reduce steps to 250** for faster testing
5. **mask_len_range parameter**: 
   - `(64, 65)` → Small 64×64 region (easy, fast)
   - `(128, 129)` → Medium 128×128 region (balanced)
   - `(192, 193)` → Large 192×192 region (challenging, needs ps+ and higher scale)

## 📸 What You'll See

### Before (Cell 18 Output):
- **Left**: Mask (white=keep, black=fill)
- **Right**: Masked image (what DPS receives)

### After (Cell 22 Output):
- **Left**: Original image
- **Center**: Masked image
- **Right**: DPS inpainted result

## 🐛 Troubleshooting

### "TypeError: cannot unpack non-iterable NoneType"?
This means `mask_len_range` is missing for 'box' type mask. **Fixed in latest version!**
- Verify you're using updated Cell 18
- For 'box' type: must have `mask_len_range: (128, 129)`
- For 'random' type: must have `mask_prob_range: (0.3, 0.7)`

### Still getting "Require mask" error?
- Make sure you're running **Cell 18** (not skipping it)
- Verify `task_config['measurement']['operator']['name'] == 'inpainting'`
- Check that `mask_opt` is defined in config

### Poor inpainting quality?
- **Increase scale** to 0.7 or 0.8
- **Use ps+ method** with `num_sampling=5`
- **Reduce region size**: use `(64, 65)` instead of `(128, 129)`
- **Increase steps**: use 500 or 1000 instead of 250

### Artifacts at boundaries?
- **Decrease scale** to 0.3
- **Add slight noise**: `sigma=0.01`
- **Use ps+ method** for smoother blending

## 💡 Advanced: Custom Masks

To use your own mask:

```python
# After Cell 18, before Cell 20:
import torch

# Create custom mask (1=keep, 0=inpaint)
custom_mask = torch.ones(1, 1, 256, 256).to(device)
custom_mask[:, :, 50:200, 50:200] = 0  # Inpaint this region

# Override the generated mask
globals()['inpainting_mask'] = custom_mask

# Now run Cell 20 (inference)
```

---

**The notebook is now fully configured for inpainting!** Just set the config in Cell 12 and run. ✨

