---
layout: post
title: "Particles in Kaiko Project 5"
author: Jan Enders
---

In my three years at KAIKO, I worked on "Project 5", a top-down action adventure from a beloved THQNordic IP that sadly did not make it to release.
We built the game entirely on in-house technology, and besides working on the [renderer](/kkp5-renderer), another of my tasks was designing and implementing our own particle runtime and editor.

## Particle runtime

The particle runtime is entirely GPU-based and strongly inspired by the system that Housemarque have built and used for their games (probably most prominently in Returnal).

In our system, particle effects are split up into layers, with freely programmable behavior and shading for each layer.
Both the behavior and shading are authored as HLSL snippets, which get converted by a custom preprocessor into compute and fragment shaders, respectively.
The system does not differentiate between emitters and particles, freely letting particles spawn other particles from any layer within the same effect.

Additionally, the system allows for one-sided parenting relations between particles of the same layer (each particle may have a single parent whose data it can access, but does not know anything about its children).
This enabled straightforward implementations of particle ribbons, but could also be used for some more "creative" particle effects like this *wacky waving inflatable arm flailing tube man* that I built to internally demo the tech:

<div class="video-row" >
	<figure>
		<video autoplay muted loop playsinline preload="metadata">
			<source src="/images/KKP5_tubeman.mp4?v=4" type="video/mp4">
			Could not load the video		
		</video >
		<figcaption>Implementing a little air pressure simulation in particles was a fun exercise</figcaption>
	</figure>
</div >

For rendering, particles can output a variety of geometry, from billboards and ribbons to instances of mesh assets and even individual triangles for fully procedural geometry.
All geometry gets appended to GPU buffers and rendered via indirect draw.

A variety of particle effects built with our system can be seen in the [portfolio of our amazing VFX artist Alex Anokhina](https://www.artstation.com/artwork/3EQxoD).

## The editor

Apart from the runtime, I also worked on the particle editor, internally named "Stabilizer". Like all of our tools at Kaiko, it is a standalone application built on Qt.

While most of the actual editing happens in a text editor panel, Stabilizer also contains a preview window using our in-engine renderer, playback controls including a timeline, hot-reloading shaders, UI for assigning textures and more.

Probably the most technologically interesting feature to implement was what we termed "Tweakables". 
These are variables that automatically generate little UI widgets to edit their values in real time, passing them into the the simulation through a constant buffer.
They are then freely usable in the snippets code and were used to quickly iterate on particle behaviors as well as customize behaviors that were used across multiple different particle effects.

<div class="image-grid">
	<figure >
		<img src="/images/KKP5_stabilizer.png" alt="Particle editor screenhot">
		<figcaption>Stabilizer's User Interface in all its glory</figcaption>
	</figure>
</div>

Working on the particle runtime and editor was a great learning experience, as it was my biggest (mostly) solo task in my time at Kaiko. 
Designing a fully GPU-based runtime architecture was fascinating and took some iteration to get right.
Work on the editor also gave me the chance to learn a lot about Qt as a framework, creating tools and designing for usability in general.
