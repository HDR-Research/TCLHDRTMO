# Taking a Closer Look at High Dynamic Range Tone Mapping in the Wild

> **[A Survey on High Dynamic Range Imaging and Tone Mapping Operators]**
>
> <sup>1</sup>Yan Lab, <sup>2</sup>JIANGXI UNIVERSITY OF FINANCE AND ECONOMICS

**⚡We will actively maintain this repository and incorporate new research as it emerges. If you have any questions, please contact [qiulinzeng0722@163.com]，[yuming03133@163.com]，[3198186694@qq.com]. Welcome to collaborate on academic research and writing papers together.**

## 📌 What is This Survey About?

<p align="center">
    <img src="TMO.png" width="100%" alt="Luminance Range and Human Vision">
</p>

<p align="center">
    <b>Figure 1: The Physical Basis of HDR.</b> <br>
    The real world exhibits a vast dynamic range of luminance, from starlight ($10^{-6} cd/m^2$) to sunlight ($10^{9} cd/m^2$). However, standard displays (CRT/LCD) cover a much narrower range. <b>Tone Mapping Operators (TMOs)</b> serve as the critical bridge, mimicking the human visual system's adaptive capabilities to compress this wide dynamic range into the visible gamut of display devices.
</p>

<br>

<p align="center">
    <img src="TMOpipline.png" width="100%" alt="HDR Imaging Pipeline">
</p>

<p align="center">
    <b>Figure 2: The Modern HDR Processing Pipeline.</b> <br>
    A comprehensive view of the image processing workflow:
    (1) <b>Acquisition</b>: Capturing raw data via Professional Cameras (RAW/Log) or Exposure Fusion.
    (2) <b>Processing</b>: Converting signals using transfer functions like <b>PQ (Perceptual Quantizer)</b> and <b>HLG (Hybrid Log-Gamma)</b>.
    (3) <b>LTM Core</b>: The central tone mapping stage, categorizing algorithms into Global, Local, and DNN-based methods to adapt content for both HDR (HDR10, Dolby Vision) and LDR displays.
</p>

<br>

High Dynamic Range (HDR) imaging is gaining increasing attention in both computer graphics and computational photography. Over the past few decades, significant efforts have been made to optimize the pipeline from capture to display. This paper presents a comprehensive review of the state-of-the-art methods, focusing on the evolution from traditional global operators to modern Deep Neural Network (DNN) approaches.

Finally, we discuss the limitations of current objective quality metrics (IQA) for tone-mapped images and explore promising future directions. Our key argument is that evaluation should be integrated into the design loop to better support the development of next-generation visual systems.

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

## Traditional & Optimization-based
### Algorithm & Modeling
1.	<mark>WardHistAdj</mark> "A Visibility Matching Tone Reproduction Operator for High Dynamic Range Scenes". Larson G W, Rushmeier H, Piatko C. IEEE TVCG 1997. [[Paper]( https://ieeexplore.ieee.org/document/646233)]
2.	<mark>Ashikhmin</mark> "A Tone Mapping Algorithm for High Contrast Images". Ashikhmin M. EGWR 2002. [[Paper]( https://dl.acm.org/doi/10.5555/581896.581916)]
3.	<mark>Reinhard</mark> "Photographic Tone Reproduction for Digital Images". Reinhard E, Stark M, Shirley P, et al.. SIGGRAPH 2002. [[Paper]( https://dl.acm.org/doi/10.1145/566654.566575)]
4.	<mark>Drago</mark> "Adaptive Logarithmic Mapping For Displaying High Contrast Scenes". Drago F, Myszkowski K, Annen T, et al.. Eurographics 2003. [[Paper]( https://resources.mpi-inf.mpg.de/tmo/logmap/logmap.pdf)]
5.	<mark>ReinhardDevlin</mark> "Dynamic Range Reduction Inspired by Photoreceptor Physiology". Reinhard E, Devlin K. IEEE TVCG 2005. [[Paper]( https://cs.ucf.edu/~ceh/Publications/Papers/Rendering/IEEETVCG04ReinhardDevlin.pdf)]
6.	<mark>Lischinski</mark> "iCAM06: A refined image appearance model for HDR image rendering". Kuang J, Johnson G M, Fairchild M D. JVCIR 2007. [[Paper]( https://dl.acm.org/doi/10.1016/j.jvcir.2007.06.003)]
7.	<mark>KimKautzConsistent</mark> "Consistent Tone Reproduction". Kim M H, Kautz J. IASTED CGIM 2008. [[Paper]( https://vclab.kaist.ac.kr/cgim2008/MHKim_JKautz_CGIM2008s.pdf)]
8.	<mark>Raman</mark> "Bilateral Filter Based Compositing for Variable Exposure Photography". Raman S, Chaudhuri S. Eurographics 2009. [[Paper]( http://andrewd.ces.clemson.edu/courses/cpsc482/papers/RC09_bilateralFilterCompositing.pdf)]
9.	<mark>Windowed</mark> "Globally Optimized Linear Windowed Tone-Mapping". Shan Q, Jia J, Brown M S. IEEE TVCG 2010. [[Paper]( https://grail.cs.washington.edu/projects/sq_tonemapping/tonemapping_tvcg.pdf)]
10.	<mark>Optimized</mark> "Optimizing a Tone Curve for Backward-Compatible High Dynamic Range Image and Video Compression". Mai Z, Mansour H, Mantiuk R, et al.. IEEE TIP 2011. [[Paper]( https://www.cl.cam.ac.uk/~rkm38/pdfs/mai11otc.pdf)]
11.	<mark>Gradient-Domain</mark> "Gradient-Domain Image Reconstruction Framework with Intensity-Range and Base-Structure Constraints". Shibata T, Tanaka M, Okutomi M. CVPR 2016. [[Paper]( https://openaccess.thecvf.com/content_cvpr_2016/papers/Shibata_Gradient-Domain_Image_Reconstruction_CVPR_2016_paper.pdf)]
12.	<mark>Krawczyk</mark> "Perceptual Lightness Modeling for High-Dynamic-Range Imaging". Abebe M A, Pouli T, Larabi M C, et al.. ACM TAP 2017. [[Paper]( https://dl.acm.org/doi/epdf/10.1145/3086577)]
13.	<mark>Hybrid-l1-l0</mark> "A Hybrid l1-l0 Layer Decomposition Model for Tone Mapping". Liang Z, Xu J, Zhang D, et al.. CVPR 2018. [[Paper]( https://openaccess.thecvf.com/content_cvpr_2018/papers/Liang_A_Hybrid_l1-l0_CVPR_2018_paper.pdf)]
14.	<mark>Multi-Scale-Hist</mark> "Tone Mapping Based on Multi-scale Histogram Synthesis". Yang J, Liu Z, Shahnovich U, et al.. arXiv 2021. [[Paper]( https://arxiv.org/abs/2102.00408)]
15.	<mark>Perceptually Adaptive</mark> "Perceptually Adaptive Real-Time Tone Mapping". Tariq T, Matsuda N, Penner E, et al.. SIGGRAPH Asia 2023. [[Paper]( https://dl.acm.org/doi/abs/10.1145/3610548.3618222)]

## Deep Learning-based
### Generative & Representation Learning
1.	<mark>DeepTMO</mark> "Deep Tone Mapping Operator for High Dynamic Range Images". Rana A, Singh P, Valenzise G, et al.. IEEE Access 2019. [[Paper]( https://arxiv.org/abs/1908.04197)]
2.	<mark>TMNet </mark> "Deep tone mapping network in HSV color space". Zhang N, Wang C, Zhao Y, et al.. IEEE Access 2019. [[Paper]( https://ieeexplore.ieee.org/abstract/document/8965992)]
3.	<mark>TMO-Net</mark> "TMO-Net: A Parameter-Free Tone Mapping Operator Using Generative Adversarial Network". Panetta K, Kezebou L, Oludare V, et al.. IEEE Access 2021. [[Paper]( https://ieeexplore.ieee.org/document/9371686)]
4.	<mark>Deep Laplacian</mark> "Perceptually Optimized Deep High-Dynamic-Range Image Tone Mapping". Le C, Yan J, Fang Y, et al.. arXiv 2021. [[Paper]( https://arxiv.org/abs/2109.00180)]
5.	<mark>Deep Reformulated Laplacian</mark> "Deep Reformulated Laplacian Tone Mapping". Yang J, Liu Z, Lin M, et al.. arXiv 2021. [[Paper]( https://arxiv.org/abs/2102.00348)]
6.	<mark>Unpaired-TMO</mark> "Unpaired Learning for High Dynamic Range Image Tone Mapping". Vinker Y, Huberman-Spiegelglas I, Fattal R. ICCV 2021. [[Paper]( https://openaccess.thecvf.com/content/ICCV2021/papers/Vinker_Unpaired_Learning_for_High_Dynamic_Range_Image_Tone_Mapping_ICCV_2021_paper.pdf)]
7.	<mark>PS-TMO</mark> "A Perceptually Optimized and Self-Calibrated Tone Mapping Operator". Cao P, Le C, Fang Y, et al.. IEEE TMM 2023. [[Paper]( https://ieeexplore.ieee.org/document/10982125)]
8.	<mark>IVTMNet</mark> "Unsupervised HDR Image and Video Tone Mapping via Contrastive Learning". Cao C, Yue H, Liu X, et al.. arXiv 2023. [[Paper]( https://arxiv.org/abs/2303.07327)]
9.	<mark>TMO-GAN</mark> "A Generative Adversarial Network Based Tone Mapping Operator for 4K HDR Images". Zhang J, Wang Y, Tohidypour H, et al.. ICNC 2023. [[Paper]( https://ieeexplore.ieee.org/document/10074176)]
10.	<mark>G-SemTMO</mark> "G-SemTMO: Tone Mapping with a Trainable Semantic Graph". Goswami A, Bernard E, Hauser W, et al.. arXiv 2024. [[Paper]( https://arxiv.org/abs/2208.14113)]
11.	<mark>DPRNet</mark> "Learning Differential Pyramid Representation for Tone Mapping". Yang Q, Zhang F, Li Y, et al.. AAAI 2024. [[Paper]( https://arxiv.org/abs/2412.01463)]
