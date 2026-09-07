```markdown
# ComfyUI GUI Installer for Arch Linux

An interactive, GUI-driven installation and launcher setup script for **ComfyUI** on Arch Linux and Arch-based distributions (EndeavourOS, Manjaro, CachyOS).

Built specifically to resolve common Arch Linux friction points—including PEP-668 virtual environment restrictions, rolling Python release ABI mismatches, and native Fish shell virtualenv activation.

---

## 🌟 Key Features

* **GUI-Driven Setup:** Interactive Zenity dialogs for directory selection, GPU hardware targeting, and real-time installation progress.
* **Arch & PEP-668 Compliant:** Automatically provisions an isolated Python virtual environment (`venv`) to keep system packages clean.
* **Python 3.12 Auto-Fallback:** Prefers `python3.12` when available to prevent PyTorch wheel ABI incompatibilities caused by Arch's rolling Python updates.
* **Multi-GPU Target Support:** Automatically configures PyTorch index URLs for:
  * **NVIDIA GPUs** (CUDA)
  * **AMD GPUs** (ROCm 6.1)
  * **CPU-only mode**
* **Native Fish Shell Launcher:** Generates a dedicated `run_comfyui.fish` script (`activate.fish`), allowing Fish users to launch ComfyUI without broken environment variables.
* **Automated Prerequisite Resolution:** Detects missing system tools (`zenity`, `git`, `python`) and prompts for installation via `pacman`.

---

## 📋 Prerequisites

* **Operating System:** Arch Linux or any Arch-based distribution.
* **Permissions:** `sudo` privileges (required only if system packages like `zenity` are missing).
* **Hardware:** NVIDIA CUDA or AMD ROCm graphics card recommended.

---

## 🚀 Quick Start

Run the following commands in your terminal to clone the repository and launch the GUI installer:

### Fish Shell
```fish
git clone [https://github.com/queenoffiends/comfyui-arch-installer.git](https://github.com/queenoffiends/comfyui-arch-installer.git)
cd comfyui-arch-installer
chmod +x install_comfyui.sh
./install_comfyui.sh

```

### Bash / Zsh

```bash
git clone [https://github.com/queenoffiends/comfyui-arch-installer.git](https://github.com/queenoffiends/comfyui-arch-installer.git)
cd comfyui-arch-installer
chmod +x install_comfyui.sh
./install_comfyui.sh

```

---

## 🖥️ Usage

### Launching ComfyUI

After installation completes, navigate to your installation folder and execute the generated launch script:

**Fish Shell:**

```fish
cd /path/to/ComfyUI
./run_comfyui.fish

```

**Bash / Zsh:**

```bash
cd /path/to/ComfyUI
source venv/bin/activate
python main.py

```

### Quick Launcher Abbreviation (Fish)

To launch ComfyUI from anywhere in your Fish terminal without navigating directories, set up an abbreviation:

```fish
abbr -a comfyui "/path/to/ComfyUI/run_comfyui.fish"

```

Then simply run `comfyui` from any terminal session.

---

## 🛠️ Troubleshooting & Logs

If an error occurs during installation, check the installation log created at:

```bash
/tmp/comfyui_install.log

```

### Common Arch Linux Edge Cases

#### 1. NVIDIA GTX 10-Series GPUs (Pascal / Compute Capability 6.1)

Default PyTorch builds targeting CUDA 13.0+ drop support for older GPUs (e.g., GTX 1070 / 1080). If you receive an `sm_61` compute capability error, force-reinstall PyTorch with CUDA 12.1 inside your virtual environment:

```fish
source venv/bin/activate.fish
pip install --upgrade --force-reinstall torch torchvision torchaudio --index-url [https://download.pytorch.org/whl/cu121](https://download.pytorch.org/whl/cu121)

```

#### 2. `Fatal Python error: Illegal instruction` (`kornia-rs`)

If ComfyUI crashes on startup during module import on older CPUs, compile `kornia-rs` locally from source:

```fish
sudo pacman -S --needed rust
pip install --force-reinstall --no-binary kornia-rs kornia-rs

```

---

