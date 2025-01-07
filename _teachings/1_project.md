---
layout: page
title: Llama3 Laboratory @ MediaTek
description: In this lab, we explaind the essential design choices used by llama3, including RMSNorm, Rotrary Embedding, and KV cache.
img: assets/img/teachings/llama3/rotarary.png
importance: 1
category: work
related_publications: false
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
        {% include figure.liquid loading="eager" path="assets/img/teachings/llama3/TAs.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    This lab is conducted with my smartest collegue, Jason, during our time in Institute of Information Science, Academia Sinica. The target audience are engineers from MediaTek, one of the world's leading semiconductor solution company.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/teachings/llama3/architechture.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    The overall architechture of llama3, each block is stacked by a RMS Norm, a GQA + KV cache, and a SwiGLU as an activation function.
</div>


RMSNorm was selected as the normalization method due to its computational efficiency while maintaining normalization effectiveness, as originally demonstrated by <a href="https://arxiv.org/abs/1910.07467">Zhang and Sennrich (2019)</a>. The advantages of RMSNorm are twofold: it reduces computational complexity by eliminating the mean statistics and centering operation present in LayerNorm, while maintaining comparable model performance. This efficiency-to-performance ratio has led to its adoption in several prominent language models including <a href="https://arxiv.org/abs/2112.11446">Gopher (Rae et al., 2021)</a>, <a href="https://arxiv.org/abs/2302.13971">LLaMA (Touvron et al., 2023)</a>, and <a href="https://arxiv.org/abs/2307.09288">LLaMA 2 (Touvron et al., 2023)</a>.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/teachings/llama3/RMSNorm.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


Compared to standard positional embedding (categorized as 'absolute embedding'), <a href="https://arxiv.org/abs/2104.09864"> rotary position embedding (Su et al., 2021</a>) offers greater flexibility. The key advantage of rotary embedding lies in its relative nature, which enables the model to learn position-dependent representations without being constrained to fixed absolute positions. The computation process involves two main steps: first, calculating the rotation for each embedding dimension, then computing the inner product between the rotated word embeddings and positional embeddings. This is visualized across three plots: the leftmost shows the original word embeddings, the middle displays the rotary embedding base vectors, and the rightmost demonstrates the final rotated embeddings. The transformation preserves the relative relationships between tokens while allowing for more flexible position modeling.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/llama3/rotarary.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A 2D visualization of rotarary embedding, we did not scale the original embedding to better preserve the embedding length. The left shows the original embedding, the middle is the rotary positional embedding. The rotary mechanism ensure that no matter which exact position of the 2 words in the sequence are, they remain the same distance to each other. (While in the standard positional embeddings, [????]). The right is taking the inner product of the word and positional embedding. Note: This visualization only shows the first 2 dimensions of all embeddings. An interactable is provided in the colab.
</div>

The KV (Key-Value) Cache implementation optimizes transformer inference by storing and reusing previously computed key and value tensors. When generating tokens sequentially, instead of recomputing attention for the entire sequence, the implementation caches past key-value pairs and only computes attention for the new token (<a href="https://arxiv.org/abs/2107.14500">Dao et al., 2022</a>). This significantly reduces computational overhead, especially for long sequences. As shown in the diagram, the top half illustrates standard attention without caching (computing full Q×K^T for all tokens), while the bottom half demonstrates cached attention (computing Q×K^T only for the new token by reusing stored keys). The implementation includes a KVCache dataclass for managing the cache state and a CachedAttention module that leverages this cache during inference.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/llama3/KVCache.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


