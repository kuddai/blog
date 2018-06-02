---
layout: post
title: Unsupervised skip connections
---

[Ladder nets](https://arxiv.org/abs/1507.02672) (aka [Unets](https://arxiv.org/abs/1505.04597)) are currently achieving state-of-the art results on image to image translation, for example [see here](https://phillipi.github.io/pix2pix/).

This network architecture achieves such great results because the skip connetions allow higher frequency information, such as edges and gradients, to be easily communicated between the encoder and decoder. This is useful for image to image translation as typically we are translating between 'styles' (low frequency content such as palette, textures), while the high frequency content maps to the 'content' (see [style transfer](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf)).

TODO image of unet

## An autoencoder with skips

Given this architectures power for image processing, it would be nice to use in unsupervised setting as well. However, naive implementation of an autoencoder with these skip connections is just cheating...

TODO show example of pathology. Deeper layers dont need to learn anything...

__Q__ How can we force the network to use the deeper layers?

### Filter the frequency content

What if we enforced constrains on the skip connections to ensure the earlier skip connections can not communicate low freqency information? Lets construct a high and low pass filter and ...

$$
\begin{align}
z_{low} &= \text{avg_pool}(x)\\
z_{high} &= x - z_{low}\\
\end{align}
$$

TODO examples of the high/low freq content. (could make a live version?!)

<div id="filter-net-example">
  // todo need to organise these. preferablly in the shape of a ladder net...
  <img height="224" width="224" id="cat" src="https://lh3.ggpht.com/IrU3-A_BtS3alAiaLMzIeDQrNUiPy7poxngSaD8drq9gEr5W3vbD6HZaqEaE69-pDqE=w300"/>
  <img height="224" width="224" id="cat_low"/>
  <img height="224" width="224" id="cat_high"/>
</div>

<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.11.2"></script>
<script type="text/javascript">
  function low_pass_filter(img){
    pool = tf.layers.averagePooling2d({"poolSize": [2,2],
                                       "strides": [2,2],
                                       "padding": "same",
                                       "dataFormat": "channelsLast"});
    return pool.apply(img.reshape([1,224,224,3]));
  }

  const catElement = document.getElementById('cat');
  const img = tf.fromPixels(catElement).toFloat();

  low = low_pass_filter(img);
  high = img - low;

  const lowElement = document.getElementById('cat_low');
  // set lowElement pixels with low
</script>

### Structured latent space

structure on the hidden space. Where earlier skips carry high frequency content and later skips would carry low frequency content.
(allowing you to have distinct priors on each one?)

TODO image of hidden space decomposition.

### Wavelet decomposition

Relationship to a wavelet decomposition...


## Results

TODO ... need to get around to this... wont be extensive...

***

The idea was Paul Matthews', I just wrote it down.
