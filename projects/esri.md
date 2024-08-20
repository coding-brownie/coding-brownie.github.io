---
layout: post
title: 'Interactive Storytelling with ArcGIS'
permalink: 'projects/esri'
---

<h2>Esri R&D, Zurich (2017)</h2>

<div class="project-page-tech-stack">
    <b>Technology Stack:</b> <i>Javascript, Ract, Redux</i>
</div>
<!-- 
<div class="project-page-icon-bar">
  <div class="icon-container float-left">
    <img src="../assets/img/javascript.png" alt="Javascript">
  </div>
  <div class="icon-container float-left">
    <img src="../assets/img/react.png" alt="React">
  </div>
  <div class="icon-container float-left">
    <img src="../assets/img/redux.png" alt="Redux">
  </div>
  <!-- Need to clear float, such that parent elements gets height of contained content. -->
  <!-- <div style="clear:both;"></div>
</div> -->

<h3 class="intro-text">
    Bring interactive PowerPoint presentations to Esri's ArcGIS framework. That was essentially the task for my 6-month internship. Under the lead of my supervisor, I created a React/Redux-based web-application to create and visualize dynamic presentations with the ArcGIS API. Here is a rough overview of it.
</h3>

<div>
    <video src="../assets/videos/esri.mp4" controls></video> 
    <p class="caption" style="margin-top:5px;">
        <i>Example presentation of the relocation of a USPS office in the Redlands.</i>
    </p>
</div>

There are two modes to this web-application: 1) authoring mode and 2) presentation mode.
<p>
During <b>authoring mode</b>, the author can set a keyframe for the current camera location of ArcGIS. Additionally, for each keyframe, the user can select the time-of-day, which ArcGIS layers should be active and if there should be custom HTML elements visible at certain locations. Such a chain of keyframes becomes a presentation and should be compared to slides in PowerPoint. Furthermore, keyframes can have more than one follow-up keyframe, allowing for interactive branching in the visual "story". In such a case, the author can either select a default follow-up branch, which would trigger after some timeout, or leave it to the presenter to select which story branch to take next during presentation mode. Each story is saved as a JSON file.
</p>
<p>
During <b>presentation mode</b>, a story is loaded and the algorithm interpolates between the set keyframes to get a smooth camera movement, as well as smooth blending between the 3D and HTML elements that should be active in the current/next keyframe. The presenter can pause the presentation at any time and change the point of view, or jump to a different part of the presentation through the timeline on the bottom. 
</p>

The UI is handled by React, which reflects any changes done in the Redux store. Similarly, changes done to the ArcGIS API by the story or the user, such as camera movements, time-of-day changes, addition/removal of 3D objects, etc, are also persisted in the Redux store.

<img src="../assets/img/esri_overview.png" width="100%" class="center-horizontal">  
<p class="caption" style="margin-top:0;">
    <i>Overview of the implemented application.</i>
</p>

<div>
    <video src="../assets/videos/esri-ui.mp4" controls></video> 
    <p class="caption" style="margin-top:5px;">
        <i>Demonstration of the 3D HTML elements.</i>
    </p>
</div>


### Links
- [ArcGIS](https://www.arcgis.com/)