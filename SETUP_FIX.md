# 🛠️ Conda Environment Setup Fix for MIT Deep Learning (Apple Silicon / M-series)

This guide provides the necessary steps to resolve common dependency conflicts and ensure stability for MIT Deep Learning labs on Apple Silicon (M1/M2/M3).

---

## ❗ Core Issues Resolved
1. **ModuleNotFoundError: No module named `cv2`**  
   Caused by missing OpenCV dependency.
2. **Jupyter Kernel Death/Crash**  
   Caused by incompatible (Intel x86) versions of TensorFlow on Apple Silicon.

---

## ✅ Fix Steps

### **Step 1: Activate the Environment**
Ensure you are working within the correct Conda environment for the labs (`mitdl`):

```bash
conda activate mitdl
```

---

### **Step 2: Install OpenCV (`cv2`)**
The `mitdeeplearning` package (specifically `lob2.py`) relies on OpenCV. Use the stable `conda-forge` channel:

```bash
conda install -c conda-forge opencv
```

---

### **Step 3: Install Apple-Optimized TensorFlow (Crucial for Stability)**
Remove incompatible generic TensorFlow versions and install dedicated Apple Silicon builds.

#### 1. Remove Incompatible Packages:
```bash
pip uninstall tensorflow keras tensorflow-macos tensorflow-metal -y
conda remove tensorflow keras -y
```

#### 2. Install Optimized Packages:
```bash
# Provides the core framework for macOS
pip install tensorflow-macos

# Enables Metal Performance Shaders (GPU acceleration)
pip install tensorflow-metal
```

---

### **Step 4: Update Core Jupyter Packages (Optional, for VS Code stability)**
Ensure kernel interface packages are up-to-date:

```bash
conda install ipykernel jupyterlab
```

---

### **Step 5: Final Verification**
1. Fully restart **Visual Studio Code**.
2. Open your notebook and ensure the `mitdl` kernel is selected.
3. Run the following cell to confirm the environment is healthy:

```python
import sys
import mitdeeplearning as mdl
print(f"Python Executable: {sys.executable}")
print("mitdeeplearning package loaded successfully!")
```

---

## ✅ Quick Save Instructions:
1. Copy this entire text block.
2. Open a new file in VS Code or any text editor.
3. Paste the content.
4. Save the file as:  
   **`SETUP_FIX.md`**

---

You’re all set! This should fix the environment issues for MIT Deep Learning labs on Apple Silicon.
