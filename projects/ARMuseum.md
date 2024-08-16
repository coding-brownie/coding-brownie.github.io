---
layout: post
title: 'AR Museum'
permalink: 'projects/ar-museum'
---

### ETH, Game Technology Center (2019-2021)
**Technology Stack:** *Unity, C#, Vuforia, OpenCV, Vue.js, Javascript, MongoDB, GridFS, Google BigData*

<div style="width:100%; aspect-ratio:16/9; float: none; clear: both; margin: 2px auto;">
  <embed
    src="https://www.youtube.com/embed/sa1C9v-zqLg?autohide=1&autoplay=0"
    wmode="transparent"
    type="video/mp4"
    width="100%" height="100%"
    allow="autoplay; encrypted-media; picture-in-picture"
    allowfullscreen
    title="Keyboard Cat"
  >
</div>
<p style="margin-top:0;">
<i style="font-size:0.8em;">Trailer of the exhibtion in Vienna of the Princely Collections (@GTC, 2021).</i>
</p>

How can museum visits be enhanced with modern technology - especially AR? That was the main question we were tasked to solve. The result is a platform that allows museum curators to author their own AR content through a web-based content management system (CMS). Said content is then presented to the museum visitors through an app running on their personal devices. 
The museum visitor facing app was developed with Unity, C# and Vuforia as AR image tracker. The curator facing website is implemented with Javascript, Vue.js and a MongoDB database.   
This AR museum platform is now part of an ETH Spinoff and marketed under the name [Viseum](https://aperionxr.com).

<img src="../assets/img/cms_en.jpg" width="80%" style="display: block; margin: 0 auto;">  
<p style="margin-top:0;">
    <i style="font-size:0.8em;">Overview of the AR Museum platform (@Aperion XR, 2024).</i>
</p>


### My Contributions
I was mainly involved in the creation of the UI and AR functionalities on the Unity app, but also contributed to the frontent (Vue.js) and backend (Javascript) of the CMS website.  

#### AR App
I created several **AR functionalities**, such as displaying videos on top of the art-pieces, or a slider interaction, allowing to see two different versions of the same painting. One additional notable AR functionality I implemented is a *face-swap* feature (OpenCV), allowing museum visitors to place their faces instead of pre-defined faces on some of the paintings in the museum and seeing the result in AR. Challenges were mainly the face-detection, re-coloring of the taken photograph to match the style of the painting and a simple UI to present the feature to the museum visitors. This was accomplished with OpenCV and overlaying the physical painting with an AR-based UI.  
Furthermore, I implemented a **wiki-style UI** for visitors to read the textual information the curators want to empart. The wiki also supports **videos** and **image galleries** to be displayed in the app. I also signed responsible for developing a visual floorplan with all paintings of the exhibition as authored in the CMS. 
All UI developments were done in close collaboration with the in-house digital artist who guided the design process.  

#### Web CMS
On the CMS-side I spent notable time to develop a **visualization framework of the user data** gathered by the AR app. This includes Google BigData queries, visualization of the SVG floorplan and adding additional SVG content to visualize and highlight paths users have taken through the exhibition space. Following this line of work, I was also responsible for creating an SVG-based **editor to place art pieces** on an SVG image of the floorplan of the exhibition. 
Furthermore I created various pages to **display and edit information stored in the database**, integrated the **file-upload system**, as well as the GridFS filesystem for the MongoDB database, and contributed greatly to the overall datastructures used in the database.  

#### Student Thesis Supervision
I supervised two Bachelor theses in this project. Both included existing neural networks to animate the paintings: One would create an [animated version of landscape paintings](https://gtc.inf.ethz.ch/research/student-projects/animated-paintings.html), by making clouds move and potentially change the time of day. The other one would use a short video of the user's face and use the facial expressions within to [animate a selected portrait painting](https://gtc.inf.ethz.ch/research/student-projects/facial-expression-transfer-ar.html). 

### Videos
<div style="width:100%; aspect-ratio:16/9; float: none; clear: both; margin: 2px auto;">
  <embed
    src="https://www.youtube.com/embed/3NR8IrEAsyI?autohide=1&autoplay=0"
    wmode="transparent"
    type="video/mp4"
    width="100%" height="100%"
    allow="autoplay; encrypted-media; picture-in-picture"
    allowfullscreen
    title="Keyboard Cat"
  >
</div>
<p style="margin-top:0;">
    <i style="font-size:0.8em;">Trailer of the "Parallelen" exhibition of the ETH Graphische Sammlung in Zurich (@GTC, 2020).</i>
</p>



### Links
- [Research Page (ETH)](https://gtc.inf.ethz.ch/research/augmented-and-virtual-reality-research/behind-the-art.html)
- [Viseum (Aperion XR)](https://aperionxr.com/)