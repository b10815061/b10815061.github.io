---
layout: page
title: twVLM demo
description: We conduct continual pretraining on ViT + twllm (70B) to create the first vlm that speaks traditional chinese.
img: assets/img/twVLM/llama-in-tw.jpeg
importance: 3
category: demo
---

<style>
.zoom-overlay {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80%;
  height: 80%;
  background: rgba(0, 0, 0, 0);
  z-index: 1000;
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease, visibility 0.3s;
  pointer-events: none;
}

.zoom-overlay img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  transform: scale(0.9);
  transition: transform 0.3s ease;
}

.zoom-container:hover + .zoom-overlay,
.zoom-overlay:hover {
  opacity: 1;
  visibility: visible;
}

.zoom-container:hover + .zoom-overlay img,
.zoom-overlay:hover img {
  transform: scale(1);
}
</style>

<!-- Add this right before your closing body tag -->
<script>
document.addEventListener('DOMContentLoaded', function() {
  function setupZoomImages() {
    const images = document.querySelectorAll('.img-fluid:not(.zoom-ready)');
    
    images.forEach(img => {
      // Mark image as processed
      img.classList.add('zoom-ready');
      
      // Create wrapper structure
      const wrapper = document.createElement('div');
      wrapper.style.position = 'relative';
      
      // Create container
      const container = document.createElement('div');
      container.className = 'zoom-container';
      
      // Create overlay
      const overlay = document.createElement('div');
      overlay.className = 'zoom-overlay';
      const zoomImg = document.createElement('img');
      zoomImg.src = img.src;
      overlay.appendChild(zoomImg);
      
      // Setup DOM structure
      const originalParent = img.parentNode;
      originalParent.insertBefore(wrapper, img);
      container.appendChild(img);
      wrapper.appendChild(container);
      wrapper.appendChild(overlay);
    });
  }

  // Setup initial images
  setupZoomImages();

  // Setup mutation observer for dynamically added images
  const observer = new MutationObserver(function(mutations) {
    mutations.forEach(function(mutation) {
      if (mutation.addedNodes.length) {
        setupZoomImages();
      }
    });
  });

  observer.observe(document.body, {
    childList: true,
    subtree: true
  });
});
</script>


This is an ongoing project. During development, we utilize a combination of VisionTransformer, MLP, and Taiwan Llama for our model architecture. Our current findings demonstrate that the model maintains instruction-following capabilities even without explicit prompt training. We attribute this behavior to Taiwan Llama's inherent instruction-aligned nature from its pre-training.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/twVLM/bubble-tea.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The model exhibits reasoning skills. In the prompt we asked: Where is the bubble tea originate from? The model responded with "Taiwan"
</div>


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/twVLM/waterloo.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/twVLM/notre-dame.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Question: Where is this place? Answer: "University of Waterloo locates at Waterloo, Province of Ontario, Canada".
    Right: Question: What is this? Answer: Notre Dame de Paris.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/twVLM/cmu.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Question: Where is this place? Answer: "Carnegie Mellon University is a private research university located in Pittsburgh, Pennsylvania, USA.".
</div>
