---
layout: page
title: Coach Vision
description: The final version of our annotation site. I apply the feedbacks from both the domain expert and research needs.
img: assets/img/new_annotation_system/filter_page.png
importance: 3
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

After the first prototype and some negotiation with the domain expert. We set off to build the second version of our website with some key features essential for us or recommended by the skating coach.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/new_annotation_system/login.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/new_annotation_system/signup.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The login and signup page, utilized for multiple coach usage. This helps our system to scale up quickly.
</div>

The main filter page: we filtered the action type into cards to better visualize them.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/new_annotation_system/filter_page.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The main annotation page. During our experiments, several problems arise:

1. It is hard to tell the performed action and the rotate count by us, it would be more reasonable to let the domain experts determine the jump they are currently annotated on.
2. Since we are able to visualize the skeleton information, we are curious how precise our model is focusing on each keypoints. We add a new slot for the coaches to enter which part of the body the learners should focus on. This will greatly help us to check if our model is paying attention to the correct part of the body.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/new_annotation_system/annotation_page.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

A complete demonstration is shown, in the demo we have shown the following aspects:

1. The filter page
2. Collections of task in each actions
3. A fine-grained annotation process
4. Jump type / Rotate count selection
5. Body part selection
6. Drag function to quickly relocate the annotaion, if more than one annotation span at the exact timestamp, the later one will be pushed to the second line.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include project_video.liquid path="assets/img/new_annotation_system/new_sys_demo.mp4" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>