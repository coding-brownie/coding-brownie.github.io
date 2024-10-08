---
layout: post
title: 'Mesh Approximation of 3D Paintings (Bachelor Thesis)'
permalink: 'projects/bachelor-thesis'
---

<h2>ETH, Disney Research Zurich</h2>

<div class="project-page-tech-stack">
  <b>Technology Stack:</b> <i>C++, Qt</i>
</div>
<!-- <div class="project-page-icon-bar">
  <div class="icon-container float-left">
    <img src="../assets/img/c++.png" alt="C++">
  </div>
  <div class="icon-container float-left">
    <img src="../assets/img/qt.png" alt="QT">
  </div>
  <!-- Need to clear float, such that parent elements gets height of contained content. -->
  <!-- <div style="clear:both;"></div>
</div> -->


<h3 class="intro-text">
  My Bachelor thesis was about creating approximations of 3D paintings created by an in-house tool called <a href="https://zurich.disneyresearch.com/OverCoat/">OverCoat</a>. The reason behind this thesis topic was to be able to render such 3D paintings in real-time and to be able to rig and animate them for video games. 
</h3>

<img src="../assets/img/eleCubeComparison.jpg" width="100%">  
<p style="margin-top:0;" class="caption">
    <i>Comparison between the original 3D painting (top) and the 3D mesh approximation (bottom).</i>
</p>

In order to create approximations of the Overcoat 3D paintings, I developed a tool with Qt and C++, that takes a 3D mesh (usually the one used as the base of the 3D painting) and create a layered mesh (like an onion) of it. Each layer is the same mesh, but scaled by a certain factor along the vertex normals. The goal of the approach is to calculate the texture for each layer in such a way that the resulting textured layer mesh looks as close as possible as the 3D painting from any direction. Thus, the second input for the algorithm is a set of RGBA images (samples) of the original 3D painting, taken from various directions.

<img src="../assets/img/kimonoSampling.jpg" width="60%" style="display: block; margin: 0 auto;">  
<p class="center-horizontal caption" style="margin-top:10px; width:60%;">
    <i>Visualization of the equation generated for the texture of the 5-layer mesh K<sub>5</sub> by a single pixel of sample (S<sub>j</sub>) of the 3D painting.</i>
</p>

Now, each sample is essentially projected from the correct direction onto the layered mesh to determine, which texture pixels are responsible for rendering that color of the sample (see image above). This is done by turning each sampled color into an alpha-blending equation including all the pixels of all the layers involved in rendering that color. The unknowns of the equation are the pixel values of the resulting textures. To solve this **overdetermined system of equations**, we employ a L-BFGS solver. Due to the large number of unknowns (in the range of millions), this process usually takes several minutes. 

<img src="../assets/img/KimonoCreatorGUI.jpg" width="80%" style="display: block; margin: 0 auto;">  
<p class="center-horizontal caption" style="margin-top:10px; width:80%;">
    <i>The UI to create the 3D mesh approximation.</i>
</p>

This approach manages to render such paintings in real-time albeit with a degradation in visual fidelity depending on the size of brush used to draw the 3D painting.
