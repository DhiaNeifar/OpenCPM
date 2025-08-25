# OpenCPM

OpenCPM is a framework that brings together multiple research modules into a single environment.  
Currently, the project integrates **OpenCDA** as the first submodule, with plans to add **OpenCOOD** and others.

---

## 🚀 Installation

### 1. Prerequisites
- [Conda](https://docs.conda.io/en/latest/) (Anaconda or Miniconda)  
- [CARLA Simulator](https://carla.org/) (version **0.9.14**) installed locally  

#### Linux / macOS
Set the following environment variables:
```bash
export CARLA_HOME=/path/to/CARLA_ROOT
export CARLA_VERSION=0.9.14
```

#### Windows (PowerShell)
```powershell
setx CARLA_HOME "C:\path\to\CARLA_ROOT"
setx CARLA_VERSION "0.9.14"
```
After setting environment variables on Windows, open a **new PowerShell/Anaconda Prompt** so they take effect.

---

### 2. Clone Repository
```bash
git clone https://github.com/DhiaNeifar/OpenCPM.git
cd OpenCPM
git submodule update --init --recursive
```

---

### 3. Create Conda Environment
We maintain a single environment for OpenCPM and all submodules:

#### Linux / macOS / Windows (Anaconda Prompt or PowerShell)
```bash
conda env create -f environment.yml
conda activate opencpm
```

---

### 4. Install Submodules
OpenCPM automatically installs its submodules (e.g., OpenCDA) into the same environment via `environment.yml`.  

You can verify installation with:
```bash
pip show OpenCDA
python -c "import opencda; print('OpenCDA imported from:', opencda.__file__)"
```

---

### 5. CARLA Setup for OpenCDA
After setting `CARLA_HOME` and `CARLA_VERSION`, install CARLA into the `opencpm` environment:

#### Linux / macOS
```bash
cd OpenCDA
bash setup.sh
cd ..
```

#### Windows (PowerShell)
```powershell
cd OpenCDA
.\setup.sh
cd ..
```
> ⚠️ Note: On Windows, you may need **Git Bash** or **WSL** to run `setup.sh`.  
> Alternatively, copy the steps from `setup.sh` and run them manually in PowerShell.

If successful, a `cache/` folder will be created in `OpenCDA` and the script will print **“Successful Setup!”**.  

To double-check CARLA was installed:
```bash
python -c "import carla; print('CARLA imported successfully')"
```

---

### 6. Verify Installation
```bash
conda activate opencpm
python -c "import carla, opencda; print('CARLA + OpenCDA setup complete!')"
```

---

## 🛠 Development

For contributors, install with development dependencies:
```bash
pip install -e .[dev]
```

This enables tools like **pytest**, **black**, and **mypy**.

---

## 📌 Notes
- OpenCPM original author: Dhia Neifar
- OpenCPM is under active development.  
- More submodules (e.g., OpenCOOD, a third module) will be integrated in future versions.  
- Each submodule may have additional setup steps (datasets, pretrained models, etc.).  
- On **Windows**, some submodules may require WSL or Git Bash for compatibility with shell scripts.  
