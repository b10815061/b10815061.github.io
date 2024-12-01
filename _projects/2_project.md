---
layout: page
title: NLP Annotation Tools
description: Our prototype to an instruction-annotating system
img: assets/img/old_annotation_system/mainPage.png
importance: 2
category: work
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

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/old_annotation_system/mainPage.png" title="mainPage" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The main page of the annotation system. At the top left user can filter the videos by performed action and the uploader. At the bot right annotators can see the current annotation progress.
</div>



<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/old_annotation_system/annotation1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/old_annotation_system/annotation2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    In the annotation page, the annotator selects the target interval by dragging the yellow bar (visible in the right figure). And type in instructions to guide the learner, alternatively, annotators are welcome to record audio by clicking the red button at the top left to start recording. The speaking will then be processed into text using Whisper. 
</div>