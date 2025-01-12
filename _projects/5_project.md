---
layout: page
title: Sport Tech Demos
description: A collection of so far demonstrations of our SportTech project
img: assets/img/sporttech_logo.jpeg
importance: 1
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

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
    {% include instagram.liquid 
    path="https://www.instagram.com/reel/DCiSAebyMTx/?utm_source=ig_web_copy_link"
    max-width="600px"
    aspect_ratio="100%"
    class="featured-post"
    caption="Final term demonstration. This demonstration serves as our final report to the National Science and Technology Council, showcasing our system (instruction generation)'s capabilities. The presentation was shared by my advisor, Dr. Ku."
    hide_caption=true
    %}
    </div>
</div> 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include youtube.liquid path="https://www.youtube.com/watch?v=m7LDiiOyHjQ&ab_channel=SuYu-An%28Tommy%29" %}
    </div>
</div>
<div class="caption">This educational video demonstrates the methodology to convert videos to meaningful representation and compare concept differences between learner and reference performances. As part of this group project, I develop the visualization to detail how we enables comparison of two videos. (1:06 - 1:50)</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include youtube.liquid path="https://youtu.be/bhH3Bjbk6Rk" %}
    </div>
</div>
<div class="caption">Our system demonstration video. This demonstration was created for the <a href="https://www.futuretech.org.tw/futuretech/index.php">2024 Futex</a> competition.</div>





