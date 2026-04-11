# Proteina-Complexa: Colab Auto-Pilot Edition
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Geauga/Proteina-Complexa-coLab/blob/dev/coLab/Proteina_Complexa_coLab.ipynb)


> **⚠️ Acknowledgment & Disclaimer**
> This repository is a fork of [NVIDIA's Proteina-Complexa](https://github.com/NVIDIA-Digital-Bio/Proteina-Complexa). 
> All core algorithms, deep learning models, and the original architecture belong entirely to the NVIDIA Digital Bio team. 
> 
> **My Contribution:** I designed and integrated a specialized Google Colab workflow, including a decoupled UI dashboard, persistent caching, and an unattended "Auto-Pilot" screening shell. For deep technical details, core algorithmic theory, or local installation instructions, please refer to the [Original NVIDIA README](README_NVIDIA_Official.md) or visit their official repository.

---

## 💡 Architecture Overview
This notebook employs a decoupled **"Front-end UI / Back-end Engine"** architecture. Please read this quick start guide and configure all parameters exclusively within the **Section 0** dashboard. This centralized panel persists your configuration data to Google Drive, ensuring seamless execution even across kernel restarts.

## 💻 Hardware Requirements
* **Storage:** At least **20GB** of free space on Google Drive is recommended; **30GB+** is required if localizing program initialization data to accelerate startup times via caching.
* **GPU:** A minimum of an **L4 GPU** runtime is required. For longer protein chains with high VRAM usage, an A100 runtime is needed. *(Note: The included GFP tutorial can be completed using an L4 runtime with default settings).*

## 📦 Zero-Configuration Assets
Demonstration protein structures (`GFP_1_10.pdb` and `GFP_11.pdb`) are pre-integrated into the environment.
* **Custom Targets:** Upload your PDB files directly to the `Proteina-Complexa/targets/` directory on Google Drive, or use the integrated upload toggle in Section 0.
* **Configuration:** After uploading, ensure you update the `task_name` and `pdb_file_name` in the Section 0 dashboard accordingly.

---

## 🔄 Execution Workflows

### Phase I: Universal Initialization
1. **Read & Configure:** Review the guidelines and adjust all parameters (Auto-Pilot, Standard Generation, Geometric Scanning) in the **Section 0** UI dashboard. Execute the cell to register the variables persistently.
2. **Environment Initialization:** Execute **Section 1**.
   * *Note:* Initial compilation and asset synchronization take approximately 10–20 minutes. Enabling Google Drive persistent backup (~10GB) is highly recommended, allowing subsequent runs to skip this lengthy stage entirely.
3. **🛑 CRITICAL: Mandatory Kernel Restart** After completing Section 1, a Colab runtime restart is strictly required to apply core library upgrades (JAX/Flax/CUDA). Navigate to `Runtime -> Restart session` from the top menu, and then **run Section 1 again**. Failure to do so will cause the pipeline to crash. *(Re-running Section 0 is optional).*
4. **Target Pre-processing:** Expand and execute **Section 2** to parse and prepare your target structure.

### Phase II: Divergent Execution Pathways
Choose the module that fits your research needs:

* **Section 3: GFP Tutorial** The system automatically scans the surface of Split-GFP subunit 1 to identify the subunit 2 binding groove. It then calls the `Proteina_Complexa` evaluation module to generate the complex, providing baseline data for the natural ligand peptide alongside 3D structural models.
* **Section 4: High-Throughput Auto-Pilot** Continuously generates, evaluates, and logs candidates unattended until a predefined **success threshold** (e.g., ipSAE score) is met. By default, it screens for subunit 1 binding peptides; users can specify custom targets via Section 0.
* **Section 5: Batch Production** Continuously generates and evaluates candidates until a predefined **quantity** is reached. Defaults to subunit 1; customizable via Section 0.
* **Section 6: Targeted Surface Screening** Scans for hotspots with the strongest binding affinity on the target protein's surface and designs their corresponding peptides. Customizable via Section 0.
