---
layout: post
title: 'XR Surgeryy Simulator'
permalink: 'projects/tha-simulator'
---

<h2>University Clinic Balgrist, ROCS (2025-2026)</h2>

<div class="project-page-tech-stack">
  <b>Technology Stack:</b> <i>Unity, C#, ROS2, Python, Hololens 2</i>
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
  Enabling thorough training and hands-on education for resident surgeons is a prevalent topic in medical research. The <a href="vhttps://www.surgicalproficiency.ch/project">PROFICIENCY</a> project, funded by Innosuisse, brought together research institutes and hospitals from all around Switzerland to work on the future of orthopedic education and tackle some of the most pressing issues. The aim of the sub-project that I have been working on is to develop an XR simulator that allows resident surgeons to practice with the real tools at any time, in a low-risk, low-cost environment, while being given automated, and instantaneous feedback. To this end, we used the Microsoft Hololens 2 to spatially display relevant information for each stage of the surgery, while tracking the surgical tools and sawbones in real time, to give feedback to the user. 
</h3>
<p>
  The developed simulator consists of two main logical parts: 1) the Hololens 2 app, to visualize real-time information and offering the main user interface to the user, 2) a server, running several ROS2 nodes that offer real-time tracking data, and perform compute-intensive tasks such as volume renderings for the Hololens. 
</p>
<img src="../assets/img/tha-cover.jpg" width="100%" class="center-horizontal">
<p>
  This simulator was a collaboration between the <a href="https://rocs.balgrist.ch/de/">ROCS Team at University Clinic Balgrist</a>, and the <a href="https://www.zhaw.ch/en/engineering/institutes-centres/ids">Institut for Data Science at the Zurich University of Applied Sciences (ZHAW)</a>. At the time I took over this work in April 2025, there was already a working prototype. Over the coming 1.5 years, I integrated cutting-edge research results from PhDs into the project, and polished the experience into a workable prototype.
</p>

<h2>UI</h2>

<h2>World Space Registration</h2>
In order to allow spatially correct overlays based on external tracking data, the Hololens2 requires to be calibrated relative to the same global frame. For this, the pose <textt>p_e</textt> of the Hololens is captured by the external tracking system, tagged with a timestamp, and then sent to the Hololens. The Hololens app tracks a series of its own device poses <texttt>p_u</texttt>, which are expressed in Unity world coordinates, and also tagged with a timestamp. By comparing <texttt>p_u</texttt> and <texttt>p_u</texttt> of roughly the same timestamp, we can calculate the coordinate transform for the current session. 
Since <texttt>p_e</texttt> however only represents the pose of the marker array attached to the Hololens 2, an additional one-time calibration had to be done to calculate the coordinate transform from marker array to the PV camera of the Hololens2, from where <texttt>p_u</texttt> are derived from at runtime. This one-time calibration is done with a special checkerboard that features a fiducial marker array, such that it can not only be tracked by the Hololens' PV camera (the checkerboard corners), but also the Atracsys camera. From a series of timestamped  poses of the checkerboard and the Hololens (as measured by Atracsys) and the timestamped checkerboard corners (as tracked by the PV camera), the desired transform between Hololens marker and PV camera can be deducted. To account for the deviation of timestamps between the two devices, we calculate several coordinate transforms, each with a different timestamp offset applied while matching the pose series by timestamp. The final chosen offset (and transform) is the one with the most inliers. A pose observation is considered to be an inlier when backprojecting the checkerboard corners (as measured by atracsys) via atracsys device pose, estimated transform and PV camera projection, leads to a backprojection error below a certain threshold. This RANSAC approach is also applied to calculating the transform for each timestamp offset, making the final result robust. 

<h2>Tool Tracking</h2>
During this project we experimented with two different tracking methodologies:

<h3>Marker-based</h3>
With 300Hz and submillimeter precision, the Atracsys Fusiontrack 500 is one of the few tracking devices that have made it into the OR to support surgeons during complicated surgeries, where precision is paramount. It uses infrared light to track highly reflective fiducials inside the working environment in front of the camera. Poses are calculated based on the pre-defined marker geometry (a unique arrangement of 4 or more fiducials) for each object to track. Therefore, we attach unique marker arrays to each tool and sawbone to establish their pose. While precision and latency leaves nothing to be desired, the marker arrays themselves are a bit cumbersome to use and are subject to loss of tracking if one of the fiducials is accidentaly repositioned, or when parts of the marker array gets visually covered during usage. 

<h3>Marker-less</h3>

<h2>Ultra Sound Registration</h2>
So far, we assumed that resident surgeons would practice on sawbones, whose shapes are known at compile time, such that we can set cutting planes and reaming targets inside the Unity editor. However, one addition to the simulator that we decided to add is the registration of a speciment body. We have the CT scan of the specimen but we can't track the bone as we did before since its neither visible nor can we attach a fiducial marker array precisely enough to track the bone under the skin. 

<h2>Links</h2>
- <a href="https://www.surgicalproficiency.ch/project">PROFICIENCY Project Page</a>
- <a href="https://www.sciencedirect.com/science/article/pii/S0010482524016214">Scientific Paper: A novel augmented reality-based simulator for enhancing orthopedic surgical training</a>