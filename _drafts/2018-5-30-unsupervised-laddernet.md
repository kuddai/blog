---
layout: post
title: Unsupervised skip connections
---

[Ladder nets](https://arxiv.org/abs/1507.02672) (aka [Unets](https://arxiv.org/abs/1505.04597)) are currently achieving state-of-the art results on image to image translation, for example [see here](https://phillipi.github.io/pix2pix/).

This network architecture achieves such great results because the skip connetions allow higher frequency information, such as edges and gradients, to be easily communicated between the encoder and decoder. This is useful for image to image translation as typically we are translating between 'styles' (low frequency content such as palette, textures), while the high frequency content maps to the 'content' (see [style transfer](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf)).

<!-- TODO image of unet -->

## An autoencoder with skips

Given this architectures power for image processing, it would be nice to use in unsupervised setting as well. However, naive implementation of an autoencoder with these skip connections is just cheating... The skip connections allow information to be skipped straight to the output, making reconstruction rather easy.

<!-- TODO show example of pathology. Deeper layers dont need to learn anything... -->

$\textbf{Q:}$ How can we force the network to use the deeper layers? How can we constrain the capacity of the skip connections?

### Filter the frequency content

What if we enforced constrains on the skip connections to ensure the earlier skip connections can not communicate low freqency information? Lets construct a high and low pass filter and ...

$$
\begin{align}
z_{low} &= \text{avg_pool}(x)\\
z_{high} &= x - z_{low}\\
\end{align}
$$


<div id="filter-net-example">
  <!-- todo need to organise these. preferablly in the shape of a ladder net... -->
  <img height="224" width="224" id="img" src="../images/starry-night.jpg"/>
</div>

<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.11.2"></script>
<script type="text/javascript">
  function draw(image, div, name) {
    const canvas = document.createElement('canvas');
    canvas.className = name;

    const [width, height] = [224, 224];
    canvas.width = width;
    canvas.height = height;
    const ctx = canvas.getContext('2d');
    const imageData = new ImageData(width, height);
    const data = image.dataSync();

    for (let i = 0; i < height * width; ++i) {
      const j = i * 4;
      const k = i * 3;
      imageData.data[j + 0] = data[k + 0] * 255;
      imageData.data[j + 1] = data[k + 1] * 255;
      imageData.data[j + 2] = data[k + 2] * 255;
      imageData.data[j + 3] = 255;
    }
    imageData.data = data;
    ctx.putImageData(imageData, 0, 0);

    div.appendChild(canvas);
  }

  function low_pass_filter(img){
    pool = tf.layers.averagePooling2d({"poolSize": [2,2],
                                       "strides": [2,2],
                                       "padding": "same",
                                       "dataFormat": "channelsLast"});
    low = pool.apply(img.reshape([1,224,224,3]));
    return tf.image.resizeBilinear(low, [224, 224]);
  }

  function main(){
    const div = document.getElementById('filter-net-example');

    const imgElement = document.getElementById('img');
    const img = tf.fromPixels(imgElement).toFloat();
    // sometimes this fails to load. need to make it async?

    const low = low_pass_filter(img);
    const high = tf.sub(img, low);

    draw(high, div, 'high');
    draw(low, div, 'low');
    // why isnt low rendering? it must be define as it is used to make high...
  }
</script>
<script>main();</script>


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
