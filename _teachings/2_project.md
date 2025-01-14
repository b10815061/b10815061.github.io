---
layout: page
title: RAG @ CGU
description: We demonstrate the example usage of LangChain. Also in the labatory section, students are assigned to improve the embedding model.
img: assets/img/teachings/RAG/Overview.png
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
        {% include figure.liquid loading="eager" path="assets/img/teachings/RAG/TA.png" title="TAs" class="img-fluid rounded z-depth-1" class="img-fluid rounded z-depth-1"%}
    </div>
</div>
<div class="caption">
    This lab is conducted with my smartest collegue, Jason, during our time in Institute of Information Science, Academia Sinica. The target audience are doctors in the phd-level class at Chung Guan University.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/teachings/RAG/Overview.png" title="overview" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The overview of the RAG pipeline. When a user query gets in, model retrieves the most relevant document in the database. Then a LLM is employed to summarize the result and return the answer. In this lab, we will use LangChain as our external DB. Llama3, served with ollama, as our LLM.
</div>

LangChain is an open-source framework designed to develop applications powered by language models. The framework is structured in layers (left image): LangChain-Core provides the fundamental building blocks, LangChain-Community offers integration components, and LangChain proper includes chains, agents, and retrieval strategies. LangServe enables deployment, while LangSmith provides observability.
The right image illustrates the typical LangChain workflow through four key stages: LOAD (ingesting various document formats like PDFs, JSONs, and URLs), SPLIT (chunking documents into manageable segments), EMBED (converting text chunks into vector embeddings), and STORE (saving embeddings in vector stores for efficient retrieval). This pipeline enables applications to process, understand, and retrieve information from diverse data sources effectively.
For more details, visit: <a href="https://github.com/langchain-ai/langchain">LangChain GitHub Repository</a>

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/RAG/langchain.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/RAG/split.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


The embedding model plays crucial role when retrieving, an example of training the model is to leverage contrasive learning. Contrastive learning optimizes representations by minimizing the distance between similar pairs while maximizing it for dissimilar ones. The model implementation follows the approach presented in (<a href="https://openaccess.thecvf.com/content/CVPR2021/papers/Wang_Understanding_the_Behaviour_of_Contrastive_Loss_CVPR_2021_paper.pdf">Wang et al., 2021</a>). The loss function ℓᵢⱼ shown at the top computes the negative log ratio between the similarity of positive pairs exp(sim(zᵢ, zⱼ)/τ) and the sum of similarities with all other samples in the batch. The temperature parameter τ controls the concentration of the distribution - lower values (e.g., τ=0.07) lead to more concentrated clusters as shown in the bottom right visualization, while higher values (e.g., τ=0.2) result in more spread-out embeddings. The model maps inputs into a hypersphere where semantically similar items are pulled closer together while pushing dissimilar ones apart.
<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/RAG/Contrasitive.png" title="Contrastive" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/RAG/interactive1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/RAG/interactive2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An interactive demonstration of contrastive learning, where as positive examples move closer to the anchor point (blue), the loss decreases, while moving negative examples (red) away from the anchor reduces the loss. As the temperature parameter τ approaches zero, the loss becomes more sensitive to distances, creating sharper decision boundaries. It is worth noting that in high-dimensional spaces, the distance metric is not Euclidean but rather cosine similarity, making the angle between vectors more important than absolute distances.
</div>




