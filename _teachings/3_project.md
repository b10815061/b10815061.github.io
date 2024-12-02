---
layout: page
title: BERT @ NCGU
description: We demonstrate the example usage of LangChain. Also in the labatory section, students are assigned to improve the embedding model.
img: assets/img/teachings/BERT/Overview.png
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

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/teachings/BERT/TA.png" title="TAs" class="img-fluid rounded z-depth-1" class="img-fluid rounded z-depth-1"%}
    </div>
</div>
<div class="caption">
    This lab is conducted with Feiyueh, during our time in Institute of Information Science, Academia Sinica. The target audience are doctors in the phd-level class, Nation Chung Guan University.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/teachings/BERT/Overview.png" title="overview" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The overview of the BERT pipeline. When a user query gets in, model retrieves the most relevant document in the database. Then a LLM is employed to summarize the result and return the answer. In this lab, we will use LangChain as our external DB. Llama3, served with ollama, as our LLM.
</div>

A comparison of traditional word embeddings and BERT's contextualized embeddings. The left image illustrates basic word embeddings where each word has a fixed vector representation in a continuous space - similar words like 'dog', 'cat', and 'rabbit' cluster together, while semantically different words like 'tree' and 'flower' occupy different regions. The right image shows BERT's (<a href="https://arxiv.org/abs/1810.04805">Devlin et al., 2019</a>) more sophisticated encoding approach, where each token's representation is dynamically influenced by its context. The visualization demonstrates how BERT combines token embeddings (E_token), segment embeddings (E_A/E_B), and positional embeddings (E_0 to E_10) to create context-aware representations, enabling the model to understand the same word differently based on its usage in different contexts.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/BERT/Context.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/BERT/BertFormat.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>




