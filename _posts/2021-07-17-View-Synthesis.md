---
layout: post
title:  "Neural View Synthesis"
date:   2021-07-17 13:03:29 +0530
categories: research
comments: true
---
How can one stitch together different views of a scene into a video with neural networks?  Neural View Synthesis!
<!--more-->

In this post, I will go through some of the recent work in the field of view synthesis with neural networks. The work mainly revolves around learning view representation based on the information of how images are captured - accessed as radiance fields and generating new images with techniques such as ray tracing. So it is mostly based on graphics features and representated using machine learning.


<b>NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis:</b><br>
This work [1] brought a lot of attention into this research area and a lot of work has been done to imrpove it since then. The method proposed by the authors can be considered as optimisation of a computer graphics problem - volume rendering using neural networks. Radiance emitted at different angles at different points act as a 5D input: <b>x</b>, <b>y</b>, <b>z</b> coordinates along with directions, <b>φ</b> & <b>θ</b>. This is mapped to a single volume density <b>σ</b> along with view-dependent RGB colour <b>c</b>.

The mapping is learnt by first using the coordinates to learn the density using an MLP with ReLU. This also outputs a feature vector, which is concatenated with the directions and passed through another MLP to obtain the colour. With this formulation, the volume density is only dependent on the cartesian dimensions while the color is learnt with location and direction.  

Using the oncepts of volume rendering in graphics, colour is rendered. <b>σ</b> is interpreted as differential probability of a ray terminating at a article in a location. The expected colour is given by,
![nerf1_1 alt ><]({{ '/assets/images/nerf1_1.png'}}){:width="800px"}
Here, <b>T</b> denotes the accumulated transmittance - the probability the ray travels from <b>t<sub>n</sub></b> to <b>t</b> without hitting other particles. The integral is approximated by partitioning the space of <b>t</b> into N uniform bins and sampling on value from each bin - known as stratified sampling. Thus, the approximation can be written as,
![nerf1_2 alt ><]({{ '/assets/images/nerf1_2.png'}}){:width="650px"}

The authors find that the the rendered images lack finer details as shown in the figure below. Due to this, additional techniques such as positional encoding and view dependence are added.
![nerf1_3 alt ><]({{ '/assets/images/nerf1_3.png'}}){:width="800px"}

The authors reason that MLPs are biased towards learning low frequency functions and use an idea from another work where high frequency information is inserted before passing the input through the neural network. To achieve this, sinusoidals are applied with different frequencies for each coordiante values.

![nerf1_4 alt ><]({{ '/assets/images/nerf1_4.png'}}){:width="700px"}

The authors also add another trick - hierarchical volume sampling. The idea is that randomly sampling points for the intergal is inefficient. To achieve results, a coarse version is produced which is based on stratified sampling. After this, finer version is obtained by a biased sampling procedure. This is acheieved by sampling from pdf obtained by weighting the composited colour in differentbins, in each ray from the coarse version.  

The model is optimised by the mean square error between the predicted and ground truth pixels, for both coarse and fine versions. Batch size of 4096 rays are used with 64 bins at coarse version and 128 samples in the fine version. It took 1-2 days for it to converge on 1 V100 GPU for a single scene.

The authors manage to outperform all the baselines and obtain very realstic samples. The method is based on replicating how images are acquired by cameras and the neural networks mainly act as feature transformation between individual points of illumination to overall volume density + colour. To achieve this, camera parameters are necessary since the model needs to be trained for every scene that has to be generated.  

<b>NeRF in the wild: Neural radiance fields for unconstrained photo collections:</b><br>
In this work [2], the authors extend NeRF to unstructured photo collection. NeRF-W learns the volume density as before but with NeRF, all the images had some fixed requirements - no change in illumination & background objects. The authors train NeRF-W on dataset of internet images where the previous constraints do not hold.

In order to adapt NeRF to different illumination & post processing conditions, the authors utilise Generative Latent Optimisation (GLO), with which an embedding is assosiated with every image. With this, the seoncd MLP in NeRF will be dependent on the embedding as well. The full architecture is shown below.

![nerf2_20 alt ><]({{ '/assets/images/nerf2_20.png'}}){:width="500px"}


The transient objects are modelled with another MLP which predicts both colour and density, with density made to vary between scenes (since the background objects can move/change). Additional changes are made by emitting a field of uncertainity where each pixel colour is modelled as an isotropic normal distribution. This is followed by the approximation of the integral as before.

Similar to NeRF, NeRF-W is trained for 2 days. The authors evaluate on a held out set to test it's extrapolation capability. The authors are also able to control the generation with the embeddings space. They show finer details compared to NeRF. They note that generation can be blurry due to wrong camera calibration.

<b>Free view synthesis:</b>

This work [3] does a significant improvement by not relying on structured image input and generate unseen scenes from a model trained on a dataset. A point cloud representation is obtained from the input images by performing structure-from-motion (SfM). This also estimates the intrinsic properties of the cameras. The authors also obtain depth maps from images using multi-view stereo (MVS) and create 3D point cloud of the view. The source images and mapped to a view with 3D point cloud based proxy geometry.

<b>K</b> source images are chosen which maximise the overlap with the target view from the proxy geometry. Output image is extracted by blending the information from the target view. Towards this, images are encoded with U-Net. These features create the target view which is processed by a GRU. The architetcure is shown below,
![nerf3_1 alt ><]({{ '/assets/images/nerf3_1.png'}}){:width="700px"}

New image is obtained by combining per pixel confidence of all image features. The network is optimised by samples a source image to perform L1 loss along with perceptual loss on outputs of the U-Net layers.

The authors compare the results on unseen view generation with works such as NeRF and obtain a lot of improvement. The number of images can differ since it acts as the sequence length on the GRU. This work completely learns with neural network and uses ground truth 3D point cloud representation to learn it as intermediary features.  

<b>pixelNeRF: Neural radiance fields from one or few images:</b>

In this work [4], the authors introduce a NeRF framework to generate views with very few images and no test time fine-tuning. The architecture introduced aims to overcome a limitaion of NeRF - independance between images. The images are encoded into a pixel grid with a CNN. A NeRF network learns the volume density and colour. The learning framework is shown below,

![nerf4_1 alt ><]({{ '/assets/images/nerf4_1.png'}}){:width="800px"}

For an input, a volume <b>W</b> is obtained. For a query direction, for a point on the ray, it is projected on image plane and features <b>W</b> is extracted by bilinear interpolation. These features are input to NeRF. In case of multi view, individual view features are collected and aggredgated with average pooling to obatin the volume denity and colour from NeRF.

Some of these papers are briefly covered because the details mostly deal with compute graphics. Essentially, most of the works covered here utilises NeRF to compute density and colour and then construct images from it. The main difference lies in how the input space is transformed. It should also be noted that most of the work in this field needs camera parametrs for training and inference, so here is a high barrier to use it in practice. It is cool work nonetheless!   




<b>References:</b><br>
1. https://arxiv.org/abs/2003.08934
2. https://arxiv.org/abs/2008.02268
3. https://arxiv.org/abs/2008.05511
4. https://arxiv.org/abs/2012.02190
