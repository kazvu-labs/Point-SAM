# Point SAM Setup 


### 1. **Create and Activate the Environment**
```bash
conda create -n pointsam python=3.10
conda activate pointsam
```

---

### 2. **Install PyTorch, TorchVision, and timm (with CUDA 12.8 support)**

Go to [PyTorch’s Get Started page](https://pytorch.org/get-started/locally/) and customize for:
- OS: Linux (or your OS)
- Package: pip or conda (prefer pip for compatibility with other steps)
- Language: Python
- CUDA: 12.8

The command is:
```bash
pip install torch==2.1.0+cu128 torchvision==0.16.0+cu128 --index-url https://download.pytorch.org/whl/cu128
pip install timm==0.9.0
```
- If you get a version error later, try `torch==2.1.0` and `torchvision==0.16.0` (these are tested versions for Point-SAM).

---

### 3. **Install Third Party Modules**

```bash
conda install gxx_linux-64=9.3.0
```

**torkit3d**:
```bash
git submodule update --init third_party/torkit3d
FORCE_CUDA=1 pip install third_party/torkit3d
```

**apex** (for CUDA extensions):
```bash
git submodule update --init third_party/apex
pip install -v --disable-pip-version-check --no-cache-dir --no-build-isolation \
  --config-settings "--build-option=--cpp_ext" --config-settings "--build-option=--cuda_ext" \
  third_party/apex
```
If you encounter issues, you might need to build `apex` manually to ensure CUDA 12.8 compatibility.

---

### 4. **(Optional) Install Backend for Demo**

```bash
pip install flask flask-cors
```

---

### 5. **Get or Download Pretrained Checkpoints**

- Download from [Hugging Face](https://huggingface.co/yuchen0187/Point-SAM/tree/main)

---

### 6. **Run Point-SAM Demo**

Example:
```bash
python demo/app.py --host localhost --port 5000 --pointcloud demo/static/models/scene.ply --checkpoint ./pretrained/model.safetensors
```

---

### **Additional Notes**
- If you run into library version or CUDA compatibility errors, check PyTorch release notes for updated support for CUDA 12.8.
- For training or evaluation, follow the script examples in the README.

Would you like terminal commands for a specific step, troubleshooting for CUDA 12.8, or a guide for mesh/point-cloud demo?
