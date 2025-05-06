# Prototype: Photo/Text to 3D Model Generator (STL/OBJ)

This prototype generates a simple 3D model (`.obj` format) from either:

- A **photo** of a single object (e.g., `chair.jpg`)
- A **text prompt** (e.g., `"a small toy car"`)

It leverages [OpenAI's Point-E](https://github.com/openai/point-e) to convert these inputs into colored point clouds and export them as `.obj` files.

---

## 🚀 How to Run

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
