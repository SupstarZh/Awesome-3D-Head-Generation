# awesome-3D-Object-Generation

---

last update: 2023/9/30
## 1. 3D 数据表征：
### 1. Voxel-based representation
  Voxel-based适合表示任意形状的实体模型，但数据量庞大并且曲面不够精细光滑，且细节程度受体素分辨率限制，较难表示平滑曲面，对硬件要求高。通常与其他如网格、隐式函数等结合使用。
#### 2. Point Cloud-based representation
  点云直观反应物体表面，保留了最原始的3D采样数据。但需要进行进一步的处理来生成网格或提取信息。缺点：点分布不均匀，密集区域点过多，无法直观表示拓扑结构。
#### 3. SDF-based representation
  可以精确无缝的表示物体的表面轮廓，对物体内部结构建模较为方便。缺点在于生成表面时运算量大，表示拓扑结构较为复杂，难以直接应用现有数据等等。
#### 4. NeRF-based representation
  NeRF是从图像中学习生成精细的3D形状，并且只需要存储网络参数，数据量小。但缺点在于，NeRF需要大量图像进行训练，计算量巨大，对训练数据需求高，容易过拟合，并且很难表示静止的准确几何结构，无法显式编辑模型。
## 2. 通用物体生成
### 2.1 Unconditional 3D Generation：
    - 3D Shape Generation and Completion through Point-Voxel Diffusion
  提出PVD，3D生成模型，通过PVCNN来预测每个step中，每个点的位移
    - Diffusion probabilistic models for 3d point cloud generation
    提出DPM，3D生成模型，使用Normalization Flow模型编码Shape，训练条件概率模型，与上文差异在于DPM使用PointNet来预测噪声的均值
    - Score-Based Point Cloud Denoising
    与DPM同一作者，通过将Score-based方法应用于3D点云上，指导每一次迭代的梯度方向
    - 3DQD: Generalized Deep 3D Shape Prior via Part-Discretized Diffusion Process
    - Diffusion-Based Signed Distance Fields for 3D Shape Generation
    提出SDF-Diffusion模型，基于voxel-shaped SDF representation，包含diffusion-based SDF generation model用来生成低分辨率3D模型，一个diffusion-based SDF superresolution model，将低分辨率模型变成高分辨率模型
    - Diffusion-SDF: Text-to-Shape via Voxelized Diffusion
    提出DIffusion-SDF模型，首先训练一个Auto-Encoder用于学习体素化TSDF的patch-independent的正态分布表示。然后提出了体素化扩散框架与UinU-Net降噪器来生成形状表示
    - Fast Point Cloud Generation with Straight Flows
    将recfiled flow应用到点云生成模型中，通过学习，采样，再学习，蒸馏四步，建立一个一步采样的点云生成模型
    - MeshDiffusion: Score-based Generative 3D Mesh Modeling
    第一篇使用diffusion模型做基于meshes的无条件3D生成
    - 
    - 
      
### 2.2 Text to 3D：
    - DreamField: Zero-Shot Text-Guided Object Generation with Dream Fields
  使用CLIP监督引导NeRF渲染的图像与文本描述尽可能接近
    - DreamFusion: Text-to-3D using 2D Diffusion
    使用Diffusion代替CLIP，提出了SDS损失，用于从2D文生图模型中采样3D模型
    - Optimized-based methods (NeRF)
    - Learning-based methods 
    Image 
    
    - 
### 2.3 3D Reconstruction
  - 基于NeRF：
    - Make-It-3D: High-Fidelity 3D Creation from A Single Image with Diffusion Prior
    提出
    - Magic123: One Image to High-Quality 3D Object Generation Using Both 2D and 3D Diffusion Priors
    提出了Magic123，一个重建+超分的两阶段模型。使用2D和3D先验来实现单图重建功能。2D先验有利于控制模型生成的丰富度，3D先验有利于控制形状细节。相比于Zero123的重建过程，引入了2D的监督
    - $PC^2$: Projection-Conditioned Point Cloud Diffusion for Single-Image 3D Reconstruction
    使用生成模型做单图重建，在每个steps中，将图像特征投射到点云上，再将这一步生成的点云投射到图像上，做监督。之后提出了两个过滤器来提升性能，分别对应于有监督信号的情况和没有监督信号的情况。
    - CCD-3DR: Consistent Conditioning in Diffusion for Single-Image 3D Reconstruction
    提出Centered denoising Diffusion Probabilistic Model(CDPM)，用于解决PC2中扩散过程中，点云模型中心偏移导致的图像-3D模型特征不对齐问题，
    - Zero-1-to-3: Zero-shot One Image to 3D Object
    提出Zero-123模型，输入一张图像，使用latent-diffusion生成新视角的图像，可以使用产生的新视角图像输入NeRF中渲染出3D模型
    - One-2-3-45: Any Single Image to 3D Mesh in 45 Seconds without Per-Shape Optimization
### 2.4 3D Editing



