---
layout: post
title: 'Markerless Tool Tracking'
permalink: 'projects/markerless-tracking'
---

<h2>University Clinic Balgrist, ROCS (2025-2026)</h2>

<div class="project-page-tech-stack">
  <b>Technology Stack:</b> <i>ROS2, Python, Pytorch</i>
</div>
<!-- <div class="project-page-icon-bar">
  <div class="icon-container float-left">
    <img src="../assets/img/unity.png" alt="Unity">
  </div>
  <div class="icon-container float-left">
    <img src="../assets/img/csharp.png" alt="C#">
  </div>
  <div class="icon-container float-left">
    <img src="../assets/img/python.png" alt="Python">
  </div>
  <div class="icon-container float-left">
    <img src="../assets/img/ros2.png" alt="Google TTS">
  </div>
  <!-- Need to clear float, such that parent elements gets height of contained content. -->
  <!-- <div style="clear:both;"></div>
</div> -->

<h3 class="intro-text">  
Digital tool tracking enables surgeons to rely on computer based methods to localize tools in relation to relevant anatomical structures during high-precision surgeries. These tracking methods rely on optical markers  attached to the tools, causing substantial overhead for setup, high costs for special tracking cameras, and occasional loss-of tracking when markers are occluded in the busy OR. Thus methods that purely rely on rgb camera input for tool tracking would be greatly beneficial to simplify tracking. Furthermore, a multiview setup would not only be cheaper, but improve the problems caused by occlusion. In this project, I took openly published code for multiview rgb-based object tracking and turned it into a real-time pose tracking pipeline. While, the original algorithm takes 1+ second for a pose prediction, my optimized version does this in 90ms.
</h3>
<p>
  At the core of this pose prediction pipeline is a SurfEmb (surface embedding) models. SurfEmb models need to be trained for a specific rigid object. When given an input rgb image, it turns it into an image, where each pixel describes the estimated object surface at this pixel as a k-dimensional vector. Additionally, it also creates a mask estimating for each pixel how confident it is that this pixel belongs to the object's surface. In parallel, a MLP encoder is trained, which allows to assign a k-dimensional vector to any surface sample of the object's 3D model. To estimate the pose, the surface embeddings of the 3D model and query image can be used to find their 2D-3D relationships and calculate a pose from that. 
</p>
<img src="../assets/img/markerless-tracking-cover.jpg" width="100%" class="center-horizontal">
<p class="caption" style="margin-top:0;">
  <i>(@Balgrist, 2026)</i>
</p>

<h2>Object Detection</h2>
The original episurfemb codebase worked with BOP Datasets, which contain the gt pose and thus also the exact crop of where the object is located in the full-size image. For a real-time pipeline without any gt data, we first have to find the object in each received image, before being able to apply the episurfemb algorithm. For this, we can employ a YOLO or RF-DETR object detection model. They deliver bounding boxes for every detected object that they were trained on. Of course, the default models were never trained for specific surgical tools, so we have to train our own models.

<h2>Data Generation</h2>
In order to train the SurfEmb and YOLO models, we require a large amount of rgb data of the tool, associated ground truth pose, and bounding boxes. While capturing real data is possible (using the mentioned marker-based tracking system), it is inherently difficult to setup and calibrate with RGB cameras. Furthermore, to capture a diverse enough dataset, the marker-based tracking environment would need to be setup in various locations and calibrated. Thus, generating real data with vastly different backgrounds and lighting conditions is only feasible with a lot of manhours. The easier solution is to generate synthetic data - it not only allows to generate images of the tool in various poses and backgrounds, it also delivers the pixel perfect pose and object mask without any camera calibrations. The only downside is that synthetically rendered images are not representing real data captured by the target rgb cameras. On one hand this includes image noise and distortion, but also a realistic looking representation of the tool and background. For objects with simple surfaces, this is feasible with standard shaders, but for objects with semi-transparent surface parts, this becomes much more involved. Luckily, surgical tools usually have a simple surface and are thus simple to render.

We developed a Blender based renderer to quickly generate images of the tool in various locations (HDRI backgrounds), while being occluded by random objects. Those occluder objects are instantiated and then drawn towards the surgical tool by placing a gravitational field at its location. Furthermore, we simulate motion blur to also get samples of surgical tools that are moved during exposure time. This setup allows us to render roughly 1 realistic looking image per second. 

<h2>ROS2 Interface</h2>
Receiving, bundling, decoding, rectification

<h2>Optimizations</h2>
Subsampling, cuda, compile

<h2>Links</h2>
- <a href="https://github.com/rasmushaugaard/episurfemb">EpiSurfEmb</a>
