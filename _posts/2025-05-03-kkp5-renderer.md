---
layout: post
title: "Renderer for Kaiko Project 5"
author: Jan Enders
---

In my three years at KAIKO, I worked on "Project 5", a top-down action adventure from a beloved THQNordic IP that sadly did not make it to release.
The game was built entirely on in-house technology, and the main part of my work was building the render in a small two-person team together with Senior Programmer Florian Eisele.

Being such a small team, I got to work on many different parts of the renderer, which was a great learning experience.

<div class="image-grid">
	<img src="/images/KKP5_Level01.png" alt="Game Screenshot 1">
	
	<img src="/images/KKP5_Level02.png" alt="Game Screenshot 2">	
</div>

The renderer features that I worked on include:

- Forward plus rendering architecture with compute shader-based light culling
- Implementating our own set of PBR shaders based on a metalness/roughness workflow
- Image-based lighting with environment maps for specular and irradiance maps for diffuse
- A number of special-purpose shaders like water, foliage, refractives, ghosts etc.
- Specular Anti-aliasing
- Decals
- Height Fog
- Terrain shader with heightmap-based blending between materials and soft intersections with other geometry
- A variety of Post FX, including Atmospheric Scattering, Depth of Field, Color Grading and Automatic Exposure
- Implementing a custom Tonemapper with an adjustable curve
- Prototype Implementation of Light Propagation Volumes

<div class="video-row vid-2" >
	<figure>
		<video autoplay muted loop playsinline preload="metadata">
			<source src="/images/KKP5_pbrshader.mp4?v=4" type="video/mp4">
			Could not load the video		
		</video >
		<figcaption>PBR shader</figcaption>
	</figure>
	<figure>
		<video autoplay muted loop playsinline preload="metadata">
			<source src="/images/KKP5_foliageshader.mp4?v=4" type="video/mp4">
			Could not load the video		
		</video >
		<figcaption>Foliage shader</figcaption>
	</figure>
</div >

<div class="video-row vid-2" >
	<figure>
		<video autoplay muted loop playsinline preload="metadata">
			<source src="/images/KKP5_terrain.mp4?v=4" type="video/mp4">
			Could not load the video		
		</video >
		<figcaption>Terrain shader</figcaption>
	</figure>	
	<figure>
		<video autoplay muted loop playsinline preload="metadata">
			<source src="/images/KKP5_ghost_dissolve.mp4?v=4" type="video/mp4">
			Could not load the video		
		</video >
		<figcaption>Dissolving ghost shader</figcaption>
	</figure>
</div >

<div class="video-row" >
	<figure>
		<video autoplay muted loop playsinline preload="metadata">
			<source src="/images/KKP5_depth_of_field.mp4?v=4" type="video/mp4">
			Could not load the video		
		</video >
		<figcaption>Depth of field</figcaption>
	</figure>
</div>

I also implemented some tool functionality to integrate with our renderer, such as:

- Filtering HDR cubemaps into irradiance maps
- Automatic merging of material textures based on semantic flags
- Integrating newer block compression formats (BC 4 - 7) into our texture conversion pipeline

Our codebase includes a platform abstraction layer, which I also contributed to by implementing support for compute shaders, ReadWriteBuffers, and ReadWriteTextures.
In terms of APIs/Backends, I mostly interacted with Vulkan for PC and the NVN Library for Nintendo Switch.

