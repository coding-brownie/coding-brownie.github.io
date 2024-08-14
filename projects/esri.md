---
layout: post
title: 'Interactive Storytelling with ArcGIS'
permalink: 'projects/esri'
---

### Esri R&D, Zurich (2017)
**Technology Stack:** *Javascript, Ract, Redux*

<video src="../assets/videos/esri.mp4" controls></video> 

Bring interactive PowerPoint presentations to Esri's ArcGIS framework. That was essentially the task for my 6-month internship. Under the lead of my supervisor, I created a React/Redux based application to create and visualize dynamic presentations with the ArcGIS API. 
The UI for the presentation mode is handled by React, which reflects any changes done in the Redux store. Similarly, certain changes in the Redux store would invoke function calls on the ArcGIS API to perform visual changes, such as camera movements, time-of-day changes, addition/removal of 3D objects, etc.

In edit mode, the user can set a keyframe for the current camera location of ArcGIS. A chain of such keyframes is then  interpolated between during presentation mode to get a smooth camera movement. Additionally, for each keyframe, the user can select the time-of-day and which ArcGIS layers should be active. If any of these change from one keyframe to the next, the presentation script will fade in/out these changes. Furthermore, certain keyframes can have more than one follow-up frame, allowing for interactive branching in the visual "story". 
Presentations can be saved in JSON format.

<img src="../assets/img/esri_overview.png" width="100%" style="text-align:center;">  
<p style="margin-top:0;">
<i style="font-size:0.8em;">Overview of the implemented application.</i>
</p>


### Links
- [ArcGIS](https://www.arcgis.com/)