# High Dynamic Range Imaging & Tone Mapping: A Survey

> **[A Survey on High Dynamic Range Imaging and Tone Mapping Operators](https://arxiv.org/your-paper-link)**
>
> *<sup>1</sup>Your Lab/University Name, <sup>2</sup>Co-author Affiliation*

**⚡We will actively maintain this repository and incorporate new research as it emerges. If you have any questions, please contact [your_email@domain.com]. Welcome to collaborate on academic research and writing papers together.**

## 📌 What is This Project About?

<p align="center">
    <img src="TMOpipline.png" width="100%" alt="HDR and Tone Mapping Pipeline">
</p>

High Dynamic Range (HDR) imaging is essential for capturing and reproducing the vast range of luminosity found in real-world scenes. As display technologies and capture devices evolve, the pipeline from **Real Scenes** to final **Display Variations** has become increasingly complex.

This repository (and associated survey) aims to provide a comprehensive roadmap of the HDR imaging pipeline, with a specific focus on:

1.  **Source Acquisition:** Processing pipelines for RAW/Log data and Multi-exposure Fusion techniques.
2.  **Image Processing Pipeline:** The transformation from linear light to perceptual quantizers (PQ/HLG) and standard formats.
3.  **Tone Mapping Operators (TMOs):** A deep dive into the "LTM Core," covering the critical transition from HDR to LDR displays. We categorize methods into:
    * 📈 **Global TMOs**
    * 🖼️ **Local TMOs**
    * 🧠 **Deep Neural Network (DNN) TMOs**
4.  **Display Adaptation:** Strategies for HDR-to-HDR (e.g., HDR10, Dolby Vision) and HDR-to-LDR rendering.

Our key goal is to organize the state-of-the-art methods in tone mapping and value the evaluation of visual quality in the HDR domain.

## HDR 数据集汇总

| Dataset | Years | Scene | Encode | Resolution | Public availability |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Narwaria** | | 10 | Linear | 1080×1920 | [Link](https://www.repository.cam.ac.uk/items/c2d00e29-07b5-4b67-bcfc-80893b17fa53) |
| **Korshunov** | | 20 | Linear | 1080×944 | [Link](https://www.repository.cam.ac.uk/items/c2d00e29-07b5-4b67-bcfc-80893b17fa53) |
| **Funt** | | 112 | ffmpeg-linear | 1421×2141 | [Link](https://www.cs.sfu.ca/~colour/data/funt_hdr/) |
| **HDRC** | | 80 | ffmpeg-linear | 1080×1920 | [Link](https://github.com/Yliu724/HDRC) |
| **MIT fiveK** | | 5000 | PQ | 3000×4000 | [Link](https://data.csail.mit.edu/graphics/fivek/) |
| **HDR-Eye** | | 46 | Linear | 512×512 | [Link](https://www.epfl.ch/labs/mmspg/downloads/hdr-eye/) |
| **HDR-gallery** | | 8 | ffmpeg-linear | 1536×2048 | [Link](https://pfstools.sourceforge.net/hdr_gallery.html) |
| **HDRQAD** | | 235 | ffmpeg-linear | 1080×944 | - |
| **HDRT** | | 10000 | Linear | 5120×3840 | [Link](https://huggingface.co/datasets/jingchao-peng/HDRTDataset) |
| **SJTU-HDR** | | 16 | PQ | 2160×3840 | [Link](https://medialab.sjtu.edu.cn/files/SJTU%20HDR%20Video%20Sequences/demo_images/) |
