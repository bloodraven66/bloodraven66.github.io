---
layout: post
title:  "Generative adverserial networks: introduction"
date:   2021-07-10 13:03:29 +0530
categories: research
comments: true
---
Understanding the inital work in GANs - it's creation and modifications to get it working for image generation.

<!--more-->
Generative adverserial networks <b>(GANs)</b> are now known to be very good generative models, producing realistic samples in image, speech etc. It also has a lot of applications such as super resolution, style transfer etc.
In this post, I will start with the paper by Goodfellow et al. which introduced the learning framework in 2014. Later on, I'll cover few papers from the following years which extended the work towards stable training, realistic samples etc.

<b>Generative Adversarial Nets:</b><br>
This work [1] introduced the idea of GANs. The goal is to implicitly capture the data distribution in the network. With this, it wouldn't be possible to estimate the probability density function but it should be able to sample from a function such that the samples belong to the data distribution. This function is called the generator <b>G</b> and another function called the discriminator <b>D</b> is used in order to learn <b>G</b>.

The generator <b>G</b> samples from a noise distribution and produces a sample through a neural network - MLP, CNN etc. This is then fed to the discriminator <b>D</b> which classifies whether the sample is real or fake. The objective would be to train <b>G</b> to produce good samples while optimising <b>D</b> such that it will no longer be able to differentiate between real and fake samples. The challenge is to optimise this learning frmaework through a min mix learning strategy. The loss is shown below. <b>D</b> has the usual classification loss while <b>G</b> has the opposite in order to confuse <b>D</b>.

![ganpaper1_1 alt ><]({{ '/assets/images/ganpaper1_1.png'}}){:width="600px"}

It is trained by alternatively optimisng <b>G</b> and <b>k</b> steps of <b>D</b>. A modification is made in order to train <b>G</b> since it starts with poor samples. Instead of minimising the loss on <b>G</b>, the objective on <b>D</b> is maximised. This helps in stable training.

The authors obtain the theoritical optimal <b>D</b> to be
![ganpaper1_2 alt ><]({{ '/assets/images/ganpaper1_2.png'}}){:width="250px"}
With this, the loss can be written as
![ganpaper1_3 alt ><]({{ '/assets/images/ganpaper1_3.png'}}){:width="350px"}
where <b>JSD</b> is the jenson Shannon divergence, which is alsways greater than or equal to zero. Hence, the loss has a global minima of - log(4)

This work was just before other deep generative models such as VAE, flows and is a huge contribution to the field of probabilistic machine learning. This had its limitations - very blurry samples and a huge challenge to get it to work practically on real-world datasets. The following papers dwelve into tackling these problems.

<b>Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks:</b>

This work [2] introduces the DCGAN architecture. It is a fully convolutional network while replaces pooling with strided convolution to downsample. No linear layers are used in the end, required sizes are obtained only with convolution. In the generator, the samples noise is converted into a 4D tensor with fully connected layer. The authors also utilise batch normalisation also with relu activation, this helps dealing with training issues.

The results are demonstrated on three datasets- Large-scale Scene Understanding (LSUN), Imagenet-1k and Faces. Adam optimiser was used to train with learning rate of 0.0002 with β<sub>1</sub>=0.5 to obtain stability. The authors were able to obtain detailed samples from the models and also utilised the trained generator and discriminator for downstream tasks.

The authors use the trained discriminator with L2-SVM to classify on CIFAR-10 to demonstrate the value of the genrative model. Guided backpropagation was used on the model trained on LSUN to visualise some of the features learnt, which correlated with the fetaures present in the image. Promising samples were also obtained by interpolating on latent space by averaging mutliple latents.

This is good work towards training convolutional in a batchgenerative models. The authors also demonstrate the quality of learnt features by utilising them in other tasks.

<br>

<b>Improved Techniques for Training GANs:</b>

Training GANs is a min max game which can be considered as  a 2 player non cooperative Nash equilibrium. The authors reason that it is hard to optimise GANs since redusing the objective w.r.t <b>D</b> can increase it for <b>G</b> and vice versa. Due to this, gradient descent can enter a stable orbit and fail to converge. To overcome this, a set of techniques are introduced in this work.

Feature matching:

A new objective is introduced to stop <b>G</b> from overfitting on <b>D</b>. <b>G</b> is trained to match expected value of a layer in <b>D</b>. This is performed to allow <b>G</b> features to match real data statistics. A mean squared error loss is used between the 2 set of features.

Minibatch discrimination:

This is used to overcome mode collapse in GANs. To alleviate this, closeness between the samples in a batch are modelled, This is performed by a lieanr projection of a feature space where exponential of L1 loss between rows across each samples are computed and summed up per sample. This is concatenated with the features for the next layer. The idea behind this is to allow each sample to know how different it is from other samples in a batch to enforce sample diversity.

Historical averaging:
The cost function is modified to perform mean squarederror over the current paramters and average of older paramters. This is inspired by algorithms used to find equilibria in games.

One-sided label smoothing:

Instead of using 0/1 labels, smoothened value of 0.9 is used for one class. This is an old technique and been in use again recently, can be seen as injecting noise into training.

Virtual batch normalization:

Instead of making batch normalisation depended on the statistics of each batch, statistics of a fixed batch is used.

Inception score:
The authors introduce a new metric to score generative models. Inception CNN model is used to obtain conditional label distribution. This is assumed to have low entropy for good samples. To encourage diverse samples, marginal is expected to have high entropy. The score is then defined as exponential of the KL divergence between the conditional and marginal.

Semi-supervised learning:
The authors propose a semi-supervised framwok with GANs. With <b>k</b> classes in a supervised dataset, fake samples are considered an extra class and discriminator is followed by softmax over the <b>k+1</b> classes. The objective is divided into supervised an unsupervised loss. For the supervised loss, the disciminator is supposed to predict among of the first <b>k</b> classes. For the unsupervised loss, the generator samples should predict the <b>k+1<sup>th</sup></b> class while the real data should not predict it.

The authors perform semi-supervised learning on MNIST, CIFAR, SVHN and generative modelling on these datasets along with ImageNet. This paper introduces a lot of techniques to train and a metric to evaluate the sample quality.  
<br>

<b>Wasserstein Generative Adversarial Networks:</b>

This paper [4] has a great introduction, do give it a read! The reasoning in this paper revolves around choosing the objective to measure the distance between real data distribution and model distribution.

The authors consider distance metrics such as Total Variation (TV), Kullback-Leibler (KL) divergence, Jensen-Shannon (JS) divergence, Earth-Mover (EM) distance. Kl divergence is assymetric and infinte at some points.  JS divergence uses a mixture of the two distributions and is symmetrical. EM distance can be regarded as the amount of 'mass' to be transported to match the distributions.

When parameters are 0, JS, KL, reverse KL and TV do no converge. Only EM distance can be used to learn probablity distribution with gradient descent, over a low dimensional manifold. This is because other objective functions wouldn't be continuous in the region.   
![wgan1 alt ><]({{ '/assets/images/wgan1.png'}}){:width="450px"}
Here, supremum is over all 1-Lipschitz functions. The authors tried various ways to enforce it to be a Lipschitz function practically and ended up using gradient clipping for its simplicity. The loss function then becomes

![wgan2 alt ><]({{ '/assets/images/wgan2.png'}}){:width="550px"}

This is followed by gradient clipping. The model is trained by first sampling <b>m</b> samples from real and noise, and discriminator is optimised by the loss shown above. This is followed by sampling <b>m</b> noise samples and optimising generator by the second term in the loss function.

With this learning framework, it is possible to train the discrminator til optimality since the loss is continuous and differentiable. The authors find correlation between loer error and improved sample quality. This isn't the case with JS divergence loss. The authors find the mode collapse problem to be resolved with the use of EM distance as a loss function.


<b>Towards Principled Methods for Training Generative Adversarial Networks</b>

I was intending to cover this paper [5] as well though it is a theoritical work (with empirical results) with a lot of equations so it is easier to follow it by actually read the paper.

The papers covered here mainly represent the early days of GANs. In recent years, GANs are extremly good at producing realistic samples. It is also made to work well on different domains such as speech synthesis and has a lot of applications such as super resolution. In upcoming posts, I will cover topics such as SOTA architectures and different applications.

<b>References:</b><br>
1. https://arxiv.org/abs/1406.2661
2. https://arxiv.org/abs/1511.06434
3. https://arxiv.org/abs/1606.03498
4. https://arxiv.org/abs/1701.07875
5. https://arxiv.org/abs/1701.04862
