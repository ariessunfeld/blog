---
layout: post
title: "Normalizing Scalebars in ChemCam Remote Micro Images"
date: 2025-10-02 11:52:00
categories: tech-tips
tags: [technology, ChemCam, project, scalebar, normalization]
---

I was working on an image classification paper in May 2024 when I ran into a time-consuming and repetitive task: normalizing scalebars in images to produce publication-ready figures. Specifically, I was working with ChemCam remote micro images (RMIs) from the Mars *Curiosity* rover. These images get produced with a fixed-pixel-length scalebar, and the image metadata is then used to add a label to this scalebar, typically in mm. For example, an image might have a label indicating that the scalebar distance represents 7.7 mm. Because images are taken at diffeent angles and from different standoff distances, it's common to see a wide spread of values in the labels, and it's *uncommon* to see nice, round numbers. For this reason, scientists working with ChemCam RMIs or similar image data often take a little extra time to create new, more standard scalebars with their images.

For example, a mentor of mine taught me to normalize scalebars to 1 cm. He showed me how to use the screenshot tool to count pixels, and then use Photoshop to produce a longer or shorter scalebar, replacing the previous one. I agree that a length-standardized scalebar, rather than a pixel-standardized scalebar, is more useful and intuitive for people looking at the images and trying to get a sense of scale. But producing these improved scalebars manually, by counting pixels and photoshopping little rectangles, is too time-consuming and error-prone for my liking. 

So I wrote some code, [available here on GitHub](https://github.com/ariessunfeld/RMI-scalebar-normalization), that uses OCR to extract scalebar labels, calculates the new sizes, and then edits the image to apply the new scalebar and normalized label. Goodbye "7.7 mm", hello "1 cm"! I made a little video explaining the process and how the code works; feel free to [check it out on YouTube](https://youtu.be/DQXveOq5Peo?si=JbgU1AKOa2vFXqbz). This code also helps with stitching together images into rows, handling variable aspect ratios gracefully.

A quick note about the code: As of time of writing, it's not generalized whatsoever; it's written for this very specific purpose and even hard-codes some local filepaths. But, the basic idea could easily be applied to other use cases with some small modifications, so I figure it could still be helpful to some!