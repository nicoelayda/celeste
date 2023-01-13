---
layout: post
title: Virtual Anatomist
truncated_preview: true
excerpt_separator: <!--more-->
---

<div class="message">
  Some of our most complex work yet! This particular project is still in the development phase. Come back soon for more updates and a demo!
</div>

## The problem

Research at the intersection of MR applications and anatomy education has routinely demonstrated a role for new MR-based modalities in improving anatomy education, but most MR apps rely on custom illustrated projections of 3D-models into user and screen space. These virtual assets are subject to device-intrinsic or developer-based differences in display fidelity and specimen art quality. An intrinsic barrier is present in the development of digital 3D models, which are not trivial to create. Existing evidence also suggests that virtual models may produce inferior results for learning in some use-cases compared to existing physical models. Such evidence forms a case to instead place emphasis on improving the experience of using existing physical models.

## Our proposal

We are building a mixed-reality (MR) educational smartphone app intended to improve the experience of using physical 3D models in classrooms by identifying and labeling various anatomical features on models, built on a deep-learning based computer vision framework.

Point the camera at an existing anatomical model, and let the phone label key features on the model for you.

<!--more-->

## Sounds complicated. How on earth does it work?

First of all, this computer vision/artificial intelligence app will only work on models on which it is trained. In other words, you can't just point it at <em>anything.</em> The current implementation of the application is trained solely on skull-base anatomy, but may be extended to other anatomical areas of interest. 

This labeling is made possible by a hybrid depth-estimation and semantic segmentation-focused machine learning (ML) architecture. When you point the camera at an object, the app runs the image through a depth-estimator to create a depth map (or in the future, to use an existing LIDAR phone sensor, if present, to create a true depth map), and also runs the color image through a neural network to segment-map out what the anatomical object of interest is. The depth map and the segment maps are then parsed in a seperate network to label regions of interest.

<img src="{{site.baseurl}}/assets/img/Capture.png">

The primary barrier to making an app like this is often the generation of quality ground truth data. Image collections of anatomical specimens must ideally be taken under different conditions, with different augmentations applied to images to improve the ability of the application to robustly recognize and label different parts of a specimen. Manual collection and annotation of the hundreds or thousands of such images required for training is infeasible. 

However, we've created a novel workflow using procedurally generated images from a 3D-modelled skull (here, in the open-source computer graphics software Blender). With Python programming and Blender, we can produce arbitrarily large, photorealistic ground-truth training datasets with pixel-perfect semantic segmentation of anatomical features. 

We were also able to increase generalizability of the ML classifier (i.e. to not let it get distracted by random things in the background) by augmenting individual renders in Blender by randomizing the model's textures, lighting, background environments, specific skull topology via displacement mapping, the use of “distractor” objects in backgrounds, and by changing camera angles.

### What's the takeaway?

Essentially, we've demonstrated the feasibility of developing an anatomical landmark classifier from RGB-image data, trained on fully synthetic data. Future steps include formally characterizing the accuracy of segmentation on cadaveric specimens, and to train alternative models to incorporate true-depth data, to leverage depth-sensing capabilities that are available on select higher-end mobile devices.


-----
