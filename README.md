# 🎨 AI Image Processing Studio

A comprehensive image processing application powered by **U²-Net** deep learning architecture and classical computer vision algorithms. This project provides an interactive Streamlit interface for various image transformation tasks.

## 📋 Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Technical Details](#technical-details)
- [Extending the Application](#extending-the-application)
- [References](#references)

## ✨ Features

### Current Processing Tasks

1. **Picture to Sketch** 🎨
   - Converts photographs into artistic pencil sketches
   - Uses U²-Net deep learning model
   - Preserves fine details and edges
   - Real-time processing

2. **Edge Detection** 📐
   - Applies Canny edge detection algorithm
   - Detects sharp intensity changes
   - Clean, precise edge extraction

3. **Cartoon Effect** 🎭
   - Transforms photos into cartoon-style images
   - Combines edge detection with bilateral filtering
   - Maintains color while simplifying details

4. **Background Removal** 🖼️
   - Segments foreground from background
   - Outputs transparent PNG
   - Uses U²-Net for accurate segmentation

5. **Custom Prompt** 🔧
   - Extensible placeholder for future AI models
   - Ready for integration with Vision Language Models
   - Support for custom processing instructions

## 🏗️ Architecture

### U²-Net Architecture Overview

```
Input (RGB Image)
      ↓
┌─────────────────────┐
│   ENCODER STAGES    │
│                     │
│  Stage 1: RSU-7     │ ─┐
│  Stage 2: RSU-6     │  │
│  Stage 3: RSU-5     │  │ Skip
│  Stage 4: RSU-4     │  │ Connections
│  Stage 5: RSU-4F    │  │
│  Stage 6: RSU-4F    │ ─┘
│     (Bottleneck)    │
└─────────────────────┘
      ↓
┌─────────────────────┐
│   DECODER STAGES    │
│                     │
│  Stage 5d: RSU-4F   │
│  Stage 4d: RSU-4    │
│  Stage 3d: RSU-5    │
│  Stage 2d: RSU-6    │
│  Stage 1d: RSU-7    │
└─────────────────────┘
      ↓
┌─────────────────────┐
│  SIDE OUTPUTS &     │
│  FUSION LAYER       │
└─────────────────────┘
      ↓
Output (Sketch/Mask)
```

### RSU Block (Residual U-block)

Each RSU block is a mini U-Net structure with:
- Encoder path with max pooling
- Decoder path with upsampling
- Skip connections at each level
- Residual connection from input to output

**Key Innovations:**
- Two-level nested U-structure
- Multi-scale feature extraction
- Efficient parameter usage
- Deep supervision with side outputs

## 🚀 Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager
- (Optional) CUDA-capable GPU for faster processing

### Step 1: Clone or Download

```bash
git clone <repository-url>
cd ai-image-processing-studio
```

Or download the project files directly.

### Step 2: Create Virtual Environment (Recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate on Windows
venv\Scripts\activate

# Activate on macOS/Linux
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Download Pre-trained Weights (Optional)

For the Picture to Sketch feature, you can download pre-trained U²-Net weights:

1. Create a directory:
```bash
mkdir -p pretrained_u2net
```

2. Download weights from [U²-Net GitHub](https://github.com/xuebinqin/U-2-Net)
3. Place `u2net.pth` in the `pretrained_u2net/` folder

**Note:** The application will work without pre-trained weights, but the Picture to Sketch feature will produce random results until you load proper weights.

## 📱 Usage

### Running the Streamlit App

```bash
streamlit run app.py
```

The application will open in your default web browser at `http://localhost:8501`

### Using the Application

1. **Upload Image**
   - Click "Browse files" in the sidebar
   - Select an image (JPG, PNG, BMP)
   - Image info will be displayed

2. **Select Task**
   - Choose from the dropdown menu:
     - Picture to Sketch
     - Edge Detection
     - Cartoon Effect
     - Background Removal
     - Custom Prompt

3. **Configure Options**
   - Adjust output size (256-1024 pixels)
   - For custom prompt, enter instructions

4. **Process**
   - Click "🚀 Process Image"
   - Wait for processing to complete
   - View results side-by-side with original

5. **Download**
   - Click "💾 Download Processed Image"
   - Save result to local machine

### Using the Jupyter Notebook

```bash
jupyter notebook U2NET_Image_Processing.ipynb
```

The notebook includes:
- Detailed architecture explanations
- Network diagrams
- Step-by-step implementation
- Visualization examples
- Educational content

## 📁 Project Structure

```
ai-image-processing-studio/
├── app.py                          # Streamlit application
├── U2NET_Image_Processing.ipynb    # Educational notebook
├── requirements.txt                # Python dependencies
├── README.md                       # This file
├── pretrained_u2net/              # Pre-trained model weights
│   └── u2net.pth
├── images/                        # Sample images
│   ├── test_photos/              # Test dataset
│   └── my_photos/                # custom images
└── results/                       # Output directory
    └── my_sketches/              # Generated sketches
```

## 🔬 Technical Details

### U²-Net Specifications

- **Total Parameters:** ~44 million
- **Input Size:** 512×512 RGB
- **Output Size:** 512×512 grayscale
- **Architecture Depth:** 6 stages
- **Memory:** ~2GB GPU RAM / ~4GB CPU RAM

### Processing Pipeline

#### Picture to Sketch

1. **Preprocessing**
   - Resize to 512×512
   - Normalize using ImageNet statistics
   - Convert to tensor (C×H×W format)

2. **Inference**
   - Forward pass through U²-Net
   - Multi-scale feature extraction
   - Deep supervision with 6 side outputs
   - Fusion layer combines all predictions

3. **Post-processing**
   - Invert prediction (1 - output) for sketch effect
   - Normalize to [0, 1] range
   - Convert to PIL Image
   - Resize to desired output size

#### Edge Detection

- Grayscale conversion
- Gaussian smoothing (noise reduction)
- Gradient calculation (Sobel operators)
- Non-maximum suppression
- Hysteresis thresholding (100, 200)

#### Cartoon Effect

- Adaptive thresholding for edges
- Bilateral filtering (9px kernel)
- Edge and color combination
- Maintains color while simplifying details

### Performance

| Task | CPU Time | GPU Time | Memory |
|------|----------|----------|--------|
| Picture to Sketch | 2-3s | 0.3-0.5s | 4GB |
| Edge Detection | 0.1s | N/A | <1GB |
| Cartoon Effect | 0.2s | N/A | <1GB |
| Background Removal | 2-3s | 0.3-0.5s | 4GB |

## 🔧 Extending the Application

### Adding New Processing Tasks

1. **Define Processing Function**

```python
def my_custom_processing(image):
    """Custom processing logic."""
    # Process the image
    result = image.copy()
    # Apply transformations
    return result
```

2. **Add to Task Options**

```python
task_options = {
    "New Task": "Description of what it does",
    # ... existing tasks
}
```

3. **Add Processing Logic**

```python
elif selected_task == "New Task":
    result_image = my_custom_processing(image)
```

### Integrating Vision Language Models

The Custom Prompt feature is designed for easy integration with VLMs:

```python
# Example: CLIP, BLIP, or other VLM integration
def process_with_vlm(image, prompt):
    """Process image based on text prompt using VLM."""
    # Load VLM model
    model = load_vlm_model()
    
    # Process with prompt
    result = model.process(image, prompt)
    
    return result
```

### Adding Anime Style Transfer

```python
def apply_anime_style(image):
    """Convert image to anime style."""
    # Use anime GAN or similar model
    from anime_gan import AnimeGAN
    
    model = AnimeGAN()
    result = model.transform(image)
    
    return result
```

## 📚 References

### Papers

- **U²-Net**: Qin, X., Zhang, Z., Huang, C., Dehghan, M., Zaiane, O., & Jagersand, M. (2020). U²-Net: Going deeper with nested U-structure for salient object detection. *Pattern Recognition*, 106, 107404.
  - [Paper Link](https://arxiv.org/abs/2005.09007)

### Code Repositories

- **Original U²-Net Implementation**: [GitHub](https://github.com/xuebinqin/U-2-Net)
- **PyTorch**: [pytorch.org](https://pytorch.org/)
- **Streamlit**: [streamlit.io](https://streamlit.io/)

### Datasets

- **DUTS**: Salient object detection training dataset
- **ImageNet**: Pre-training normalization statistics

## 🤝 Contributing

Contributions are welcome! Areas for improvement:

1. **Model Enhancements**
   - Add more pre-trained models
   - Implement model ensemble
   - Fine-tuning capabilities

2. **UI/UX**
   - Batch processing
   - Progress bars for long operations
   - Image comparison slider

3. **Features**
   - Video processing
   - Real-time webcam processing
   - Style transfer models
   - Anime conversion
   - Super-resolution

4. **Performance**
   - GPU acceleration
   - Model quantization
   - Batch inference optimization

## 📄 License

This project uses the U²-Net architecture which is released under Apache License 2.0.

## 🙏 Acknowledgments

- Xuebin Qin et al. for the U²-Net architecture
- PyTorch team for the deep learning framework
- Streamlit team for the web app framework
- OpenCV contributors for computer vision algorithms

## 📧 Contact

For questions, issues, or suggestions, please open an issue on the repository or contact the maintainers.

---

**Happy Image Processing! 🎨✨**
