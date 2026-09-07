# ComfyUI GUI Installer for Arch Linux

An interactive, GUI-driven installation and launcher setup script for **ComfyUI** on Arch Linux and Arch-based distributions (EndeavourOS, Manjaro, CachyOS).

Built specifically to resolve common Arch Linux friction points—including PEP-668 virtual environment restrictions, rolling Python release ABI mismatches, and native Fish shell virtualenv activation.

---

## Key Features

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

## Prerequisites

* **Operating System:** Arch Linux or any Arch-based distribution.
* **Permissions:** `sudo` privileges (required only if system packages like `zenity` are missing).
* **Hardware:** NVIDIA CUDA or AMD ROCm graphics card recommended.

---

## Quick Start

Run the following commands in your terminal to clone the repository and launch the GUI installer:

```fish
git clone https://github.com/queenoffiends/comfyui-arch-installer.git
cd comfyui-arch-installer
chmod +x install_comfyui.sh
./install_comfyui.sh
