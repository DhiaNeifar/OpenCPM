# OpenCPM

OpenCPM is a framework that brings multiple research modules into a single environment.
Currently, it integrates OpenCDA (as a submodule). OpenCOOD and others are planned.

---

## 🚀 Installation

### 1) Prereqs (once)
- Install Conda (Anaconda/Miniconda)
- Install CARLA 0.9.14 locally

Recommended conda config:
    conda config --add channels conda-forge
    conda config --set channel_priority strict

### 2) Environment variables
Linux / macOS:
    export CARLA_HOME=/path/to/CARLA_ROOT
    export CARLA_VERSION=0.9.14

Windows (PowerShell):
    setx CARLA_HOME "C:\path\to\CARLA_ROOT"
    setx CARLA_VERSION "0.9.14"
(After setting on Windows, open a new shell.)

### 3) Clone the repo + submodules
    git clone https://github.com/DhiaNeifar/OpenCPM.git
    cd OpenCPM
    git submodule update --init --recursive

### 4) Create the Conda env (single env for everything)
    conda env create -f environment.yml
    conda activate opencpm
    
### 5) Install Torch and Yolov5
    conda install pytorch==1.8.0 torchvision==0.9.0 torchaudio==0.8.0 cudatoolkit=11.1 -c pytorch -c conda-forge

### 6) Install CARLA bindings for OpenCDA
Linux / macOS:
    cd OpenCDA
    bash setup.sh
    cd ..

Windows (PowerShell):
    cd OpenCDA
    .\setup.sh
    cd ..
(Use Git Bash or WSL if setup.sh doesn’t run in PowerShell.)

### 6) Verify
    python -c "import carla, opencda; print('CARLA + OpenCDA OK'); print('opencda:', opencda.__file__)"

---

## 🔗 Submodule: using your fork of OpenCDA (optional)

If you need to edit OpenCDA, fork it and point this repo to your fork.

Switch submodule URL to your fork (only once):
    git config -f .gitmodules submodule.OpenCDA.url https://github.com/DhiaNeifar/OpenCDA.git
    git submodule sync OpenCDA
    git submodule update --init --remote OpenCDA
    git add .gitmodules
    git commit -m "Use forked OpenCDA"
    git push

Typical update flow (when you change OpenCDA):
1) Commit & push inside OpenCDA (to your fork/branch or tag).
2) In parent repo, record the new submodule commit:
       git -C OpenCDA status
       git add OpenCDA
       git commit -m "Bump OpenCDA submodule (e.g., 0.2.0)"
       git push
(Submodules are pinned to a commit SHA. The parent won’t see your changes until you commit the updated pointer.)

---

## 🧪 Development
    pip install -e .[dev]
    pytest -q

---

## 🩹 Troubleshooting

Matplotlib/Pillow/NumPy typing error (Pillow → numpy.typing.NDArray):
    conda activate opencpm
    conda install -c conda-forge "numpy=1.24.*"
    conda install -c conda-forge --force-reinstall pillow matplotlib
    python -c "import numpy, PIL, matplotlib; print(numpy.__version__, PIL.__version__)"

CARLA import error:
- Re-check CARLA_HOME and CARLA_VERSION.
- Re-run OpenCDA/setup.sh.

---

## 📌 Notes
- One Conda env (opencpm) manages OpenCPM + submodules.
- Submodules may require extra assets (datasets, pretrained models).
- Windows users may prefer WSL for shell scripts.

---

## ✅ TODO
- (OpenCDA) Update Dockerfile CARLA version → 0.9.14 and test.
