# 🚀 Quick Start Guide

Get up and running with AI Image Processing Studio in 5 minutes!

## ⚡ Installation (2 minutes)

### Option 1: Quick Setup (Recommended)

```bash
# 1. Navigate to project directory
cd ai-image-processing-studio

# 2. Run setup script
python setup.py

# 3. Install dependencies
pip install -r requirements.txt
```

### Option 2: Manual Setup

```bash
# 1. Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 2. Install packages
pip install -r requirements.txt

# 3. Create directories
mkdir -p images/test_photos images/my_photos results pretrained_u2net
```

## 🎯 First Run (1 minute)

### Launch the App

```bash
streamlit run app.py
```

The app will open at `http://localhost:8501`

### Or Use the Notebook

```bash
jupyter notebook U2NET_Image_Processing.ipynb
```

## 📸 Process Your First Image (2 minutes)

### Step 1: Upload

1. Click **"Browse files"** in the sidebar
2. Select any image (JPG, PNG, BMP)
3. See image info displayed

### Step 2: Choose Task

Select from dropdown:
- **Picture to Sketch** - Best for portraits
- **Edge Detection** - Extract clean edges
- **Cartoon Effect** - Fun artistic effect
- **Background Removal** - Remove background

### Step 3: Process

1. Click **"🚀 Process Image"**
2. Wait a few seconds
3. View side-by-side comparison
4. Download result!

## 🎨 Sample Workflows

### Create a Pencil Sketch

```
1. Upload a portrait photo
2. Select "Picture to Sketch"
3. Set output size to 512
4. Process
5. Download sketch
```

### Remove Background

```
1. Upload a product photo
2. Select "Background Removal"
3. Process
4. Download transparent PNG
```

### Batch Process (Using Notebook)

```python
# In Jupyter notebook
1. Add images to images/my_photos/
2. Run all cells
3. Find results in results/my_sketches/
```

## 🔧 Troubleshooting

### "Model weights not found"

**Solution:** The app works without weights, but for best results:

1. Visit https://github.com/xuebinqin/U-2-Net
2. Download `u2net.pth`
3. Place in `pretrained_u2net/` folder

### "Module not found" Error

**Solution:**
```bash
pip install -r requirements.txt
```

### Slow Processing

**Solutions:**
- Use smaller output size (256 instead of 1024)
- If you have GPU, ensure PyTorch CUDA is installed
- Close other applications

### Image Won't Upload

**Check:**
- File format (JPG, PNG, BMP only)
- File size (< 10MB by default)
- File isn't corrupted

## 📚 Next Steps

### Learn the Architecture

Open the Jupyter notebook for:
- Detailed architecture diagrams
- Line-by-line code explanations
- Neural network theory
- Custom processing examples

### Customize Settings

Edit `config.py` to change:
- Output sizes
- Processing parameters
- UI colors and text
- Enable/disable features

### Add Your Own Tasks

See `README.md` section "Extending the Application" for:
- Adding new processing functions
- Integrating other AI models
- Custom UI components

## 💡 Tips & Tricks

### Best Results for Sketches
- Use high-contrast images
- Portrait photos work best
- Ensure good lighting
- Avoid blurry images

### Performance Tips
- Use GPU if available
- Process at 512x512 for speed
- Close unnecessary browser tabs
- Use batch processing for multiple images

### Advanced Usage

**Custom Processing:**
```python
# In app.py, add your function
def my_filter(image):
    # Your code here
    return processed_image
```

**Adjust Parameters:**
```python
# In config.py
PROCESSING_CONFIG = {
    'canny_threshold1': 50,  # Lower = more edges
    'canny_threshold2': 150,
}
```

## 🎓 Learning Resources

### Understanding U²-Net
- Read the notebook's architecture section
- Original paper: [arXiv:2005.09007](https://arxiv.org/abs/2005.09007)
- GitHub: https://github.com/xuebinqin/U-2-Net

### Image Processing
- OpenCV tutorials
- Streamlit documentation
- PyTorch tutorials

## ❓ FAQ

**Q: Do I need a GPU?**
A: No, CPU works fine but GPU is faster (3s → 0.5s)

**Q: Can I process videos?**
A: Not yet, but it's on the roadmap!

**Q: How do I add more AI models?**
A: See README.md "Extending the Application" section

**Q: Is my data secure?**
A: Yes, everything runs locally on your machine

**Q: Can I use this commercially?**
A: Check the license file and U²-Net's Apache 2.0 license

## 🆘 Getting Help

1. Check this guide
2. Read README.md
3. Explore the Jupyter notebook
4. Open an issue on GitHub
5. Check the original U²-Net repo

##  You're Ready!

Start processing images and have fun exploring different effects!

**Happy Processing! 🎨✨**

---

*Last updated: 2024*
*For detailed documentation, see README.md*
