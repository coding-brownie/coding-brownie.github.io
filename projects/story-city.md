---
layout: post
title: 'City-wide Interactive AR Storytelling'
permalink: 'projects/story-city'
---

<h2>Disney Research Zurich (2018)</h2>

**Technology Stack:** *Unity3D, C#, Vuforia*
<div class="project-page-icon-bar">
  <div class="icon-container float-left">
    <img src="../assets/img/unity.png" alt="Unity">
  </div>
  <div class="icon-container float-left">
    <img src="../assets/img/csharp.png" alt="C#">
  </div>
  <div class="icon-container float-left" style="width:48px;">
    <img src="../assets/img/vuforia.png" alt="Vuforia">
  </div>
</div>

<h3 class="intro-text">
    As a follow-up to my <a href="master-thesis">Master thesis</a>, we extended the interactive storytelling framework iCANVAS to be able to tell interactive stories through AR within a real city environment. This project was a use-case scenario for the FLAME EU project (Horizon 2020).
</h3>
<h2>Scenario</h2>
<p>
    The user enters the city, connects to the network, opens the app and can choose from a variety of stories that can be experienced in this region. Such stories could be used as a means of city tour guide, educational purposes or simply for entertainment. By augmenting the world with 3D objects, even historic scenes could be brougght back to life in front of the user’s eyes. Life-size virtual 3D stages including virtual actors are anchored at pre-defined lcoations in the city and visualized in AR. The developed prototype is intended for the Millennium Square in Bristol, UK. Due to its rich history in naval discovery and pirates, the story is set in the late 18th century and revolves around oversea trading and pirates.
</p>
<h2>Challenges</h2>
<h3>Story</h3>
<p>
    One major challenge was the architecture and authoring of a longer story. Especially finding a suitable state representation to accommodate the various user interactions without exponentially authoring more content was difficult and required some artistic freedom. 
</p>
<h3>Augmented Reality within a City</h3>
<p>
    Due to the limited AR capabilities of mobile devices at the time, the correct placement and orientation of AR stages was rather tricky. Anchoring was done through a combination of AR image target (for the orientation and location) and the AR plane tracking to properly place the stage on the physical floor.
</p>
<h3>Asset Delivery</h3>
<p>
    Since this project was a use-case scenario prototype for the FLAME project (Horizon 2020), the content of the AR stages should be donwloaded as asset bundles from nearby servers and instantiated at runtime. This also reqquired some logic to decide which stage assets need to be places at which location in the city. For this, each connected device would send its progress in the story to a server, which can then decide which assets need to be placed on which database server in order to serve users in a timely and memory efficient fashion.
</p>
<div>
    <img src="../assets/img/drz-flameStoryCityNetwork.jpg" width="80%" class="center-horizontal">
    <p class="center-horizontal caption" style="margin-top:2px; width:80%;">
        <i>Schema of the network for the prototype, including the Story Compute Server and Repository nodes to download assets from.</i>
    </p>
</div>