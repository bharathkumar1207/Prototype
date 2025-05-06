# Prototype: Photo/Text to 3D Model Generator (STL/OBJ)

This prototype generates a simple 3D model (`.obj` format) from either:

- A **photo** of a single object (e.g., `chair.jpg`)
- A **text prompt** (e.g., `"a small toy car"`)

It leverages [OpenAI's Point-E](https://github.com/openai/point-e) to convert these inputs into colored point clouds and export them as `.obj` files.

## Thought Process
The goal was to design a prototype that can convert a single image or short text prompt into a 3D model in .obj format using open-source AI models. To do this, I chose OpenAI's Point-E, which is well-suited for generating 3D point clouds conditioned on either text or image input.

### Approach Breakdown:
#### Model Setup:
I used two versions of Point-E:
- base40M for image-to-3D generation
- base40M-textvec for text-to-3D generation
Each uses an upsampler model to improve point cloud resolution from 1024 to 4096 points.

#### Modular Code Design:
I refactored the code into separate functions:
- image_to_3d(): Converts an image to a point cloud.
- text_to_3d(): Converts text prompts into a 3D point cloud.
- plot_pointcloud(): Uses Plotly for interactive 3D visualization.
- save_pointcloud_to_obj(): Exports the point cloud to .obj format.

#### Visualization:
- I chose Plotly for interactive 3D plotting, supporting both Jupyter and browser rendering.
- Exporting: The .obj exporter includes RGB color values for better visualization in external tools like Blender or MeshLab.
- Ease of Use: Everything is wrapped in a simple script that allows users to run either pipeline with minimal input (just a file path or text prompt).

---

## How to Run

### 1. Clone and Set Up the Environment

```bash
git clone https://github.com/openai/point-e
cd point-e
pip install -e .
```

### 2. Then install additional dependencies:
```bash
pip install -r requirements.txt
```
Ensure you are using a Python environment with GPU support (CUDA) if available, as 3D generation is computationally intensive.
### 3. Run the Script
Import and use the functions provided in the jupyternotebook
```bash
from point_e_3dgen import image_to_3d, text_to_3d, plot_pointcloud, save_pointcloud_to_obj

# Generate from image
pc = image_to_3d("chair.jpg")
plot_pointcloud(pc)
save_pointcloud_to_obj(pc, "chair_model.obj")

# Generate from text
pc = text_to_3d("a small toy car")
plot_pointcloud(pc)
save_pointcloud_to_obj(pc, "toy_car.obj")
```
### 4. Outputs
- A visualized 3D point cloud (shown in your browser or Jupyter)
- A downloadable .obj file
### 5.  Libraries Used
- OpenAI Point-E
- torch
- Pillow
- tqdm
- plotly
### Output Format
.obj file compatible with:
- Blender
- MeshLab
- 3D Slicer software
- Rendered interactive 3D point cloud using Plotly
### License
This prototype uses the OpenAI Point-E license and is intended for educational and research purposes only.
