# Point SAM Setup 


### 1. **Create and Activate the Environment**
```bash
python3.10 -m venv .venv
source .venv/bin/activate
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
pip install torch==2.3.0 torchvision==0.18.0 --index-url https://download.pytorch.org/whl/cu121
pip install timm==0.9.0
```
- If you get a version error later, try `torch==2.1.0` and `torchvision==0.16.0` (these are tested versions for Point-SAM).

---

### 3. **Install Third Party Modules**

**torkit3d**:
```bash
git submodule update --init third_party/torkit3d
FORCE_CUDA=1 pip install third_party/torkit3d
```

**apex** (for CUDA extensions):
```bash
git submodule update --init third_party/apex
FORCE_CUDA=1 pip install --no-build-isolation third_party/apex
```

---

### 4. **(Optional) Install Backend for Demo**

```bash
pip install flask flask-cors
```

---

### 5. **Get or Download Pretrained Checkpoints**

- Download from [Hugging Face](https://huggingface.co/yuchen0187/Point-SAM/tree/main)
```bash
wget https://huggingface.co/yuchen0187/Point-SAM/resolve/main/model.safetensors -O model.safetensors
```


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
