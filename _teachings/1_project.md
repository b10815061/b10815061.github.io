---
layout: page
title: Llama3 Laboratory @ MediaTek
description: In this lab, we explaind the essential design choices used by llama3, including RMSNorm, Rotrary Embedding, SwiGLU, Group Query, and KV cache.
img: assets/img/teachings/llama3/rotarary.png
importance: 1
category: work
related_publications: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/teachings/llama3/TAs.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    This lab is conducted with my smartest collegue, Jason, during our time in Institute of Information Science, Academia Sinica. The target audience are engineers from MediaTek. One of the world's leading semiconductor solution company.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/teachings/llama3/architechture.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    The overall architechture of llama3, each block is stacked by a RMS Norm, a GQA + KV cache, and a SwiGLU as an activation function.
</div>


Basically, the norm method is selected to be RMSNorm mainly becuase [Some research] shows that RMS Norm has the pretty equal ability to achieve other norms, with lower computation thus speed up the inference speed.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/teachings/llama3/RMSNorm.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


Compared to standard position embedding, which is categorized into "absolute embedding", rotarary proposed by [Some Research] is more flexible. First of all, a relative embedding in nature helps the model to learn an arbitrary position of embedding. The computation is somewhat easy, we first compute the rotation of each embedding dimension, then we take the inner product of the word embedding and the positional embedding.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/llama3/rotarary.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A 2D visualization of rotarary embedding, we did not scale the original embedding to better preserve the embedding length. The left shows the original embedding, the middle is the rotary positional embedding. The rotary mechanism ensure that no matter which exact position of the 2 words in the sequence are, they remain the same distance to each other. (While in the standard positional embeddings, [????]). The right is taking the inner product of the word and positional embedding. Note: This visualization only shows the first 2 dimensions of all embeddings. An interactable is provided in the colab.
</div>

KV Cache section, need implementation.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/teachings/llama3/KVCache.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


