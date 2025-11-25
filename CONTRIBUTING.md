# Contributing to DPS Implementation

Thank you for your interest in contributing! This document provides guidelines and instructions for contributing.

## 📋 Ways to Contribute

### 1. Report Bugs
- **Use GitHub Issues**: Create a detailed issue describing the bug
- **Include**: Python version, environment (Colab/Local), error message, steps to reproduce
- **Title Format**: `[BUG] Brief description`

### 2. Suggest Improvements
- **Use GitHub Discussions**: Discuss new features or improvements
- **Provide Context**: Explain why this improvement would be useful
- **Title Format**: `[SUGGESTION] Brief description`

### 3. Submit Code Changes
- **Fork the Repository**: Create your own fork
- **Create a Branch**: `git checkout -b feature/your-feature-name`
- **Make Changes**: Keep changes focused and well-documented
- **Commit**: Write clear commit messages
- **Push**: Push to your fork
- **Pull Request**: Submit PR with detailed description

### 4. Improve Documentation
- **Fix Typos**: Correct any documentation errors
- **Add Examples**: Include usage examples for new features
- **Clarify Sections**: Improve unclear explanations
- **Add Guides**: Create new documentation as needed

### 5. Share Results
- **Results**: Share your DPS results with the community
- **Format**: Include metrics, task type, and model configuration
- **Discussion**: Describe any interesting findings

## 🔧 Development Setup

### Prerequisites
```bash
git clone https://github.com/YOUR_USERNAME/DPS_FOR_GENERAL_NOISY_INVERSE_PROBLEMS
cd DPS_FOR_GENERAL_NOISY_INVERSE_PROBLEMS
```

### Create Development Environment
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
pip install jupyter black flake8  # Development tools
```

### Run Tests
```bash
# Currently no automated tests - manual testing recommended
# Test on sample images before submitting PR
```

## 📝 Commit Guidelines

### Commit Message Format
```
[TYPE] Brief description (50 chars max)

Detailed explanation if needed (wrap at 72 chars)

Fixes: #123
Related: #456
```

### Types
- `[FEATURE]` - New feature
- `[FIX]` - Bug fix
- `[DOCS]` - Documentation
- `[REFACTOR]` - Code refactoring
- `[PERF]` - Performance improvement
- `[TEST]` - Test additions

### Example
```
[FEATURE] Add SSIM metric calculation

Implement SSIM metric using scikit-image
Includes proper color channel handling
Tests included for RGB and grayscale images

Fixes: #42
```

## 🎯 Code Style

### Python Style Guide
- Follow PEP 8
- Use type hints where appropriate
- Write descriptive variable names
- Add docstrings to functions

### Example Function
```python
def calculate_metric(img1: torch.Tensor, img2: torch.Tensor) -> float:
    """
    Calculate metric between two images.
    
    Args:
        img1: First image tensor of shape (1, 3, H, W)
        img2: Second image tensor of shape (1, 3, H, W)
        
    Returns:
        Metric value as float
        
    Raises:
        ValueError: If image shapes don't match
    """
    if img1.shape != img2.shape:
        raise ValueError(f"Shape mismatch: {img1.shape} vs {img2.shape}")
    
    # Implementation
    return result
```

## 📦 Pull Request Process

### Before Submitting
1. ✅ Test your changes locally
2. ✅ Update documentation
3. ✅ Add comments to complex code
4. ✅ Run code formatter: `black .`
5. ✅ Check style: `flake8 .`

### PR Description Template
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Tested on Colab
- [ ] Tested locally on GPU
- [ ] Tested on CPU

## Related Issues
Fixes #123
Related to #456

## Checklist
- [ ] Code follows style guidelines
- [ ] Documentation is updated
- [ ] Commit messages are clear
- [ ] No new warnings introduced
```

## 🧪 Testing Guidelines

### Test Cases
- **New Features**: Test with various image sizes and types
- **Metrics**: Verify metric calculations against known values
- **Edge Cases**: Handle boundary conditions (single image, very small images, etc.)
- **Performance**: Check computational efficiency

### Test Checklist
- [ ] Runs on Google Colab (T4 GPU)
- [ ] Runs on local GPU (if available)
- [ ] Handles edge cases gracefully
- [ ] Produces correct output format
- [ ] Performance is acceptable

## 📚 Documentation Guidelines

### Code Comments
```python
# Good - explains WHY
# Use bilinear interpolation to match original DPS paper
degraded_upsampled = F.interpolate(...)

# Bad - explains WHAT (obvious from code)
# Interpolate the image
degraded_upsampled = F.interpolate(...)
```

### Docstring Format
```python
"""
One-line description.

Longer description explaining what this does, why it's needed,
and any important details.

Args:
    param1: Description
    param2: Description
    
Returns:
    Description of return value
    
Raises:
    ExceptionType: When this exception is raised
    
Example:
    >>> result = function(param1, param2)
    >>> print(result)
"""
```

### README Updates
- Update table of contents if you add sections
- Ensure links are correct
- Test code examples before committing
- Update version number if applicable

## 🚀 Release Process

### Version Numbering (Semantic Versioning)
- `MAJOR.MINOR.PATCH`
- Example: `2.0.1`

### Release Checklist
1. Update version in README
2. Update CHANGELOG
3. Tag commit: `git tag v2.0.1`
4. Create GitHub Release with notes

## ⚖️ Code of Conduct

- **Be Respectful**: Treat all contributors with respect
- **Be Inclusive**: Welcome contributions from everyone
- **Be Constructive**: Provide helpful feedback
- **Be Patient**: Remember everyone is volunteering

## 📞 Questions?

- **GitHub Issues**: For bugs and technical questions
- **GitHub Discussions**: For general questions and ideas
- **Email**: [Contact information if applicable]

## 🎉 Recognition

Contributors will be:
- Added to CONTRIBUTORS.md
- Mentioned in release notes
- Credited in README

Thank you for contributing! 🙌
