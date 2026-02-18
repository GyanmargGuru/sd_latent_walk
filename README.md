# Stable Diffusion Latent Walk with Artistic Models

This Google Colab notebook provides a comprehensive environment for generating dynamic latent walk videos using various artistic Stable Diffusion models. Explore the creative possibilities of AI-generated art by smoothly transitioning between different latent spaces, creating mesmerizing and seamless animated sequences.

## ✨ Features

- **Multiple Artistic Models**: Choose from a selection of popular Stable Diffusion models like DreamShaper, Deliberate, Dreamlike Diffusion, ReV Animated, and OpenJourney to achieve diverse artistic styles.
- **Latent Walk Generation**: Create smooth interpolations in the latent space, generating sequences of images that evolve from one concept to another.
- **Two Walk Types**: 
    - **Linear Noise Walk**: Interpolate directly between two distinct noise seeds, ideal for showcasing transitions between specific starting and ending points.
    - **Circular Noise Walk**: Generate seamless, looping animations by interpolating noise in a circular path, ensuring perfect video loops.
- **RIFE Frame Interpolation (Optional)**: Integrate Real-time Intermediate Flow Estimation (RIFE) to generate additional frames, resulting in ultra-smooth, high-frame-rate videos.
- **Customizable Parameters**: Control various aspects of the generation, including prompt, negative prompt, number of frames, FPS, image dimensions, guidance scale, and inference steps.
- **Preview Functionality**: Quickly preview a single frame of your generated art before committing to a full video render.
- **Prompt Resources**: Links to popular platforms for discovering Stable Diffusion prompts and artistic inspiration.

## 🚀 Getting Started

### 1. Open in Google Colab

Click the button below to open this notebook directly in Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GyanmargGuru/sa_latent_walk/blob/main/SD_Latent_walk_v1.ipynb) 

### 2. Choose Your Artistic Model

In the notebook, navigate to the **"STEP 0: Choose Your Artistic Model"** cell. Uncomment the `MODEL_ID` and `MODEL_NAME` variables for your desired model.

```python
# Option 1: DreamShaper - Best all-around artistic model
# MODEL_ID = "Lykon/DreamShaper"
# MODEL_NAME = "DreamShaper"

# Option 3: Dreamlike Diffusion - Surreal, dreamy art
MODEL_ID = "dreamlike-art/dreamlike-diffusion-1.0"
# MODEL_NAME = "Dreamlike"

# ... other options ...
```

### 3. Install Dependencies and Load Model

Run the initial cells to install necessary libraries and load the chosen Stable Diffusion model. This may take a few minutes for the first run.

### 4. Define Your Prompt

Update the `prompt` variable in the **"PROMPT"** cell with your creative text description. You can also adjust `seed1` and `seed2` for different starting points.

```python
prompt="Silhouettes of angelic beings, totem animals, broad rough strokes , energy misty, breathtaking, oil painting style, artistic, aesthetic modern art, hyper-realism, trending on artstation"
# ... other prompt-related code ...
```

### 5. Preview Your Image

Run the **"PREVIEW"** cell to generate and display a single image based on your current prompt and settings. This helps in fine-tuning your prompt before generating a full video.

### 6. Generate Latent Walk Videos

Choose between **Linear Walk** or **Circular Walk** examples. Modify parameters like `num_frames`, `fps`, `width`, `height`, and `num_inference_steps` to achieve your desired video output.

**Example: Linear Walk**

```python
frames2, video2 = generate_latent_walk_video(
    prompt=prompt,
    walk_type="linear_noise",
    seed_start=random.randint(1, 99),
    seed_end=random.randint(8000, 9999),
    num_frames=60,
    fps=10,
    width=960,
    height=480,
    num_inference_steps=15,
    output_path=outfile,
    reverse_loop=True
)
```

**Example: Circular Walk (Seamless Loop)**

```python
frames1, video1 = generate_latent_walk_video(
    prompt=prompt,
    walk_type="circular_noise",
    num_frames=20,
    fps=10,
    num_inference_steps=15,
    width=960,
    height=480,
    output_path=outfile
)
```

### 7. (Optional) RIFE 4X Frame Interpolation

To make your generated video even smoother, run the **"RIFE 4X FRAMES"** cell. This will use the RIFE model to interpolate additional frames, effectively quadrupling your video's frame rate.

```python
%cd /content/arXiv2020-RIFE
vidfile = "../" + outfile
!python3 inference_video.py --exp=2 --video={vidfile}
%cd /content/
```

## 💡 Tips for Prompts

- **Be Descriptive**: The more details you provide, the better the AI can understand your vision.
- **Use Keywords**: Include artistic styles (e.g., `oil painting`, `cyberpunk`), artists (e.g., `by Greg Rutkowski`), qualities (e.g., `highly detailed`, `8k`), and emotions.
- **Experiment with Negative Prompts**: Use negative prompts to specify what you *don't* want in your image (e.g., `blurry`, `low quality`).

## 📚 Resources for Prompts

| Site           | URL                                      | Best For                                  |
| -------------- | ---------------------------------------- | ----------------------------------------- |
| **PromptHero** | [prompthero.com](https://prompthero.com) | Curated artistic prompts with examples    |
| **Lexica.art** | [lexica.art](https://lexica.art)         | Search 10M+ generated images with prompts |
| **Civitai**    | [civitai.com](https://civitai.com)       | Model-specific prompts and workflows      |
| **OpenArt**    | [openart.ai](https://openart.ai)         | Prompt search + prompt book library       |
| **ArtHub.ai**  | [arthub.ai](https://arthub.ai)           | Community prompts with style tags         |


## 🤝 Contributing

Feel free to fork this repository, experiment with different models and techniques, and contribute your improvements!

## 📄 License

This project is open-sourced under the MIT License.
